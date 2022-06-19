---
id: monitoring
title: Monitoring
sidebar_label: 🧩 Monitoring
---

### Run Farm as a service

```bash
#add a regular user /w homedir (no sudo)
useradd -m -s /bin/bash user

#Add user to linger
touch /var/lib/systemd/linger/user

#create the service
cat <<EOT > /etc/systemd/system/farm.service
[Unit]
Description=Farm
After=network.target local-fs.target multi-user.target nvidia-persistenced.service

[Service]
ExecStartPre=/bin/sleep 8
Type=forking
LimitNOFILE=1048576
KillMode=control-group
User=user
ExecStart=/usr/bin/screen -UdmS farm bash -c "./farm"
WorkingDirectory=/home/user/
Restart=always
RestartSec=3

[Install]
WantedBy=default.target
EOT

#enable and run the service
systemctl enable farm
systemctl start farm
````