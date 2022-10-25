---
description: Endpoint info
---

# Info API

Info query is used to get API version, as well as health parameters of the API, such as latency of blocks, messages and transactions

![](<../../.gitbook/assets/image (31).png>)

```graphql
query{
  info{
    version # API version
    time # server time
    blocksLatency
    messagesLatency
    transactionsLatency
    latency
    chainOrderBoundary # data consistency timestamp
    rempEnabled # true if REMP is enabled
  }
}
```
