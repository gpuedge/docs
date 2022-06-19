---
id: wallet_api
title: Wallet API
sidebar_label: ⭐ Wallet API
---
API is still not finalized. Currently inspect element on a Web GUI for a node to see how it works.

Balances use 8 decimal places.

---

## Balance
```bash
curl https://wallet.gpux.ai/api/wallet/balance \
  -d '{"public_key":"FtKHw6C9C7USdmtxhRMhnyjG9iVg96rwbgKViT1xFgDa"}'

# {"credit":15014619178,"earned":0}
```

## Node List

Provides a simple way to check online nodes until DHT/NodeDiscovery is coded

```bash
curl https://wallet.gpux.ai/api/node/list

# {"error":"ok","nodes":[{"binary_sha256":"4a75e05f292babf17145c50993eb9a095556a19fd8a32638704e6d8ade6929c1","cost":{"cpu":314580,"disk":6900,"gpu":{},"ram":69420},"cpu_arch":"x86_64","farmer":"8eNQHcncG31ttdNZzZ31MtiUyEWXZ8WcYHvAHGRmrbav","identity":"8eNQHcncG31ttdNZzZ31MtiUyEWXZ8WcYHvAHGRmrbav","resources":{"cpu_avail":32,"cpu_total":32,"gpu_avail":[],"gpu_total":[],"ram_avail":128,"ram_total":128},"timestamp":1655238689,"version":"0.0.10"}]}
```