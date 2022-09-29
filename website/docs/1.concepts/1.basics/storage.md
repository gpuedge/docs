---
id: storage
title: Storage
---

GPUX has its own storage system refered to as the `gpux://` protocol.  
  
GPUX mounts `/gpux_usr/` folder to persist storage between reruns on the same node. Also `/gpux_job/` is
mounted to persist storage for the current job only.  
  
Each container you run on GPUX has access to the native storage protocol via `/gpux_api` unix tcp domain socket to 
make it easy to get data into and out of the container.

## Capabilities {#storage-caps}

- Store files or folders
- Persistent storage between reruns
- Node local only

---

## Future Features {#storage-future}

- Distributed, Node global, different nodes can fetch from different nodes
- Mountable

