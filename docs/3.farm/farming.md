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

:::caution
Currently this is the quickest way to pass key so we use it. TPMs dont support ED25519 keys, alternative solution will take some time.
:::

Running with envvars
```bash
FARMER=QgTw6C9C7USdmtxhRMhnyjG9iVg96rwbgKViT2oYpTa ./farm
```
