---
id: software
title: How to Setup Software 
sidebar_label: 🔡 Software
---

Officially Ubuntu 22.04 is supported.  
WSL2 is semi supported.  
Other distros your on your own but it should be straight forward.  
BTRFS is nice due to zstd disk compression to save space.  

#### Path of least pain
Download jammy server live and install it.  
(https://releases.ubuntu.com/22.04/ubuntu-22.04-live-server-amd64.iso)  
  
Install podman + allow rootless quota
```bash
apt-get install ca-certificates podman

#allow rootless podman CPU quota
mkdir -p /etc/systemd/system/user@.service.d/
cat <<EOT >> /etc/systemd/system/user@.service.d/delegate.conf
[Service]
Delegate=memory pids io cpu cpuset
EOT
```

Install the NVIDIA driver + cuda + nvidia-container-runtime if you have NVIDIA Gpus.
```bash
#latest NVIDIA driver currently upstream
apt-get install -y --no-install-recommends nvidia-driver-510

#latest cuda currently available
wget https://developer.download.nvidia.com/compute/cuda/11.6.2/local_installers/cuda_11.6.2_510.47.03_linux.run
sh cuda_11.6.2_510.47.03_linux.run --silent --toolkit --no-drm --no-man-page
rm cuda_11.6.2_510.47.03_linux.run
echo "PATH=\"\$PATH:/usr/local/cuda-11.6/bin\"" > /etc/environment && \
echo "CUDA_HOME=\"/usr/local/cuda-11.6\"" >> /etc/environment && \
echo "CUDA_PATH=\"/usr/local/cuda-11.6\"" >> /etc/environment

#install nvidia-container-runtime + setup OCI hook
curl -s -L https://nvidia.github.io/nvidia-docker/gpgkey | apt-key add -
curl -s -L https://nvidia.github.io/nvidia-container-runtime/gpgkey | apt-key add -
mkdir -p /etc/apt/sources.list.d/
cat <<EOT >> /etc/apt/sources.list.d/nvidia-container-runtime.list
deb https://nvidia.github.io/libnvidia-container/experimental/ubuntu18.04/\\\$(ARCH) /
deb https://nvidia.github.io/nvidia-container-runtime/experimental/ubuntu18.04/\\\$(ARCH) /
deb https://nvidia.github.io/nvidia-docker/ubuntu18.04/\\\$(ARCH) /
EOT
apt-get update
apt-get install -y nvidia-container-runtime
mkdir -p /usr/share/containers/oci/hooks.d
cat <<EOT >> /usr/share/containers/oci/hooks.d/oci-nvidia-hook.json
{
    "version": "1.0.0",
    "hook": {
        "path": "/usr/bin/nvidia-container-toolkit",
        "args": ["nvidia-container-toolkit", "prestart"],
        "env": [
            "PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin"
        ]
    },
    "when": {
        "always": true,
        "commands": [".*"]
    },
    "stages": ["prestart"]
}
EOT
#TODO: remove this once cgroupsV2 support is stable (likely the next major release)
sed -i 's/^#no-cgroups = false/no-cgroups = true/;' /etc/nvidia-container-runtime/config.toml
```

#### (Path of pain) Provision Disk

:::warning
Make sure you dont format your main disk
:::

Reference https://github.com/gpuedge/farm_image

```bash
export DRIVE="sda"
export HOSTNAME="node1"
BLOCKSIZE=$(cat /sys/block/$DRIVE/queue/physical_block_size)
IOSIZE=$(cat /sys/block/$DRIVE/queue/optimal_io_size)
ALIGN=$(cat /sys/block/$DRIVE/alignment_offset)
SECTOR=$(($IOSIZE/$BLOCKSIZE))
FIRSTSECTOR=$(($ALIGN+$IOSIZE)/BLOCKSIZE)
SIZEBOOT=$((1024*1024*1024) / IOSIZE) * SECTOR)

#Align diskspace to sectors
parted -s /dev/$DRIVE mklabel gpt
parted -s -a optimal /dev/$DRIVE mkpart primary $FIRSTSECTORs $FIRSTSECTOR+$SIZEBOOTs
parted -s -a optimal /dev/$DRIVE mkpart primary $FIRSTSECTORs $FIRSTSECTOR+$SIZEBOOTs
parted -s -a optimal /dev/$DRIVE mkpart primary $FIRSTSECTOR+$SECTOR+$SIZEBOOTs 100%
parted -s /dev/$DRIVE set 1 esp on
parted -s /dev/$DRIVE set 1 boot on

#make disk bootable by UEFI by placing fat32 parition first
mkfs.vfat /dev/$DRIVE1
#make second partion BTRFS
mkfs.btrfs -f -R free-space-tree /dev/$DRIVE2
```

Lets mount the partitions now and copy the jammy base daily.
```bash
wget https://cdimage.ubuntu.com/ubuntu-base/jammy/daily/current/jammy-base-amd64.tar.gz
mount -o discard=async,space_cache=v2,compress-force=zstd:2,ssd,noatime /dev/$DRIVE2 /mnt
tar --same-owner -xf jammy-base-amd64.tar.gz -C /mnt
mkdir /mnt/boot/efi
mount -o umask=0077 /dev/$DRIVE1 /mnt/boot/efi
```
:::note
By mounting the disk initially with zstd compression forced we will save space off the initial tar extraction of the base system.
:::

Lets update our fstab now.
```bash
UUID1=$(blkid -s UUID -o value /dev/$DRIVE1)
UUID2=$(blkid -s UUID -o value /dev/$DRIVE2)
cat <<EOT > /mnt/etc/fstab
proc /proc proc defaults 0 0
UUID=\$(UUID2) / btrfs defaults,discard=async,space_cache=v2,compress-force=zstd:2,ssd,noatime 0 0
UUID=\$(UUID1) /boot/efi vfat umask=0077 0 0
EOT
```

Locales
```bash
cat <<EOT > /mnt/etc/default/locale
LC_CTYPE="en_US.UTF-8"
LC_ALL="en_US.UTF-8"
LANG="en_US.UTF-8"
LANGUAGE="en_US.UTF-8"
EOT
```

Hostname and hosts
```bash
echo $HOSTNAME > /mnt/etc/hostname
cat <<EOT > /mnt/etc/hosts
127.0.0.1 localhost
127.0.0.1 \$(HOSTNAME)
EOT
```

#### Provision packages
