---
id: blender
title: Blender
---

Lets walk through https://github.com/gpuedge/examples/tree/main/blender

```javascript
//Source URL or GPUX sha1
const source_url = "https://whereis.com/my.blend" || "gpux://${sha1}"

//use OCIO2 colors
const ocio2 = true;

//build args to pass to bootstrap.sh
var args = [
  width ? `resolution_x:${width}` : null,
  height ? `resolution_y:${height}` : null,
  samples ? `samples:${samples}` : null,
  frame_start ? `frame_start:${frame_start}` : null,
  frame_end ? `frame_end:${frame_end}` : null,
  frame_step ? `frame_step:${frame_step}` : null,
  animation ? `animation:true` : null,
]
.filter(v=> v)
.join(",")

//build start_cmd (we can put this into the Dockerfile later)
var start_cmd = [
  `wget -q https://raw.githubusercontent.com/gpuedge/examples/main/blender/bootstrap.sh && chmod +x bootstrap.sh`,
  ocio2 ? `wget https://github.com/sobotka/filmic-blender/archive/master.zip && apt-get -y install unzip && unzip master.zip && export OCIO=/filmic-blender-master/config.ocio` : null,
  `./bootstrap.sh "${source_url}" GPUX ${args}`.trim()
]
.filter(v=> v)
.join(" && ")

//Lets use all available resources. Blender scales well
var response = await fetch(`http://somenode.com/caps`)
var {cpu_avail, ram_avail, gpu_avail, info} = await response.json()

var job = {
  type: "docker",
  meta: {subtype: "blender"},
  path: "docker.io/nytimes/blender:3.1-gpu-ubuntu18.04",
  start_cmd: start_cmd,
  cpu: cpu_avail,
  cpu_price: info.cpu_price,
  ram: ram_avail,
  ram_price: info.ram_price,
  disk: 30,
  gpu: gpu_avail,
}
```

