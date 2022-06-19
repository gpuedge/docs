---
id: farming
title: Farming
sidebar_label: 🚜 Farming
---

 - Download the latest `farm` release at https://github.com/gpuedge/farm/releases
 - Run it by doing `./farm`
 - Check your node identity is available `https://wallet.gpux.ai/api/node/list`

#### Envvars

FARMER `Your private key that will settle transactions (default: same as identity)`  
ADDRESSES `HTTP-DNS/IPv4/IPv6 addresses that your node is reachable from (default: "") (example: "https://node0.gpux.ai/,http://node0.gpux.ai/")`  

:::caution
Currently this is the quickest way to pass key so we use it. TPMs dont support ED25519 keys, signer enclave is complex, alternative solution will take some time.
:::

:::success
If you are behind a Router the easiest way to make your
farm accessible from the outside is to setup Cloudflare Argo Tunnel
https://www.cloudflare.com/products/tunnel/ (its totally free)
:::

Running with envvars
```bash
ADDRESSES="https://node0.gpux.ai/,https://*.node0.gpux.ai/,http://142.132.248.55/" FARMER=QgTw6C9C7USdmtxhRMhnyjG9iVg96rwbgKViT2oYpTa ./farm
```
