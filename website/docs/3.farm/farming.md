---
id: farming
title: Farming
sidebar_label: 🚜 Farming
---

 - Download the latest `farm` release at https://github.com/gpuedge/farm/releases
 - Run it by doing `./farm`
 - Check your node identity is available `https://wallet.gpux.ai/api/node/list`

#### Envvars

FARMER `Your public key that will receive settled funds (default: same as identity)`  
ADDRESSES `HTTP-DNS/IPv4/IPv6 addresses that your node is reachable from (default: "") (example: "https://node0.gpux.ai,http://node0.gpux.ai")`  
`Using a * wildcard in address indicates the node supports wildcard port forwarding http://*.node0.gpux.ai`

:::success
If you are behind a Router the easiest way to make your
farm accessible from the outside is to setup Cloudflare (Zero Trust) Tunnel
https://www.cloudflare.com/products/tunnel/ (its totally free)
:::

Running with envvars
```bash
ADDRESSES="https://node0.gpux.ai,https://*.node0.gpux.ai,http://142.132.248.55" FARMER=QgTw6C9C7USdmtxhRMhnyjG9iVg96rwbgKViT2oYpTa ./farm
```
