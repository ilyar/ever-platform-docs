---
description: Evercloud API changelog
---

# Evercloud

## February 16, 2023

### New

* Remove "UNSTABLE" marks from `blockchain` API

## January 18, 2023

### New

* [TON (The Open Network) mainnet endpoint](../graphql-api/networks.md) added

## December 22, 2022

### New

* [query Cost API](../evercloud-api-add-ons/query-cost.md) added&#x20;
* [Price API](../evercloud-api-add-ons/price.md) added&#x20;

## December 15, 2022

### New

* [Flex API ](../evercloud-api-add-ons/flex-api.md)is added to Evercloud

## October 26, 2022

### New

* increase `Q_REQUESTS_MAX_SIZE` default to 64kb (now it is possible to send external inbound messages of size > 16kb, up to 64kb)

## September 15, 2022

### New

* `capabilities_flags` companion field to p8 config parameter `capabilities`

### Fixed

* `in: []` (empty list) filter now leads to an empty query result as expected
* `notIn: []` (empty list) filter now is ignored as expected

## August 29, 2022

### New

* Add new option `--query-max-timeout-arg` or `Q_QUERY_MAX_TIMEOUT_ARG`.\
  This adds upper boundary for `timeout` parameter in collection API queries.\
  Default is 24 hours.

## August 15, 2022

### New

* [FT (Fungible token) API](../evercloud-api-add-ons/ft-fungible-token-api.md) is added to Evercloud

## June 06, 2022

### New

* master config `p30`, `p40`, `p42` fields types
* `prev_code_hash` account field
*   `allow_latest_inconsistent_data` option in paginated `blockchain` queries:

    > By default there is a delay of realtime data (several seconds) to ensure impossibility of data inserts before the latest accessible cursor. Now it became possible to disable this guarantee and thus - to reduce delay of realtime data by setting this flag to true.
* two config options for reading external subscriptions health messages from Redis channel
  * `subscriptions-health-redis-channel`
  * `subscriptions-health-timeout`

### Fixed

* `blockchain.master_seq_no_range` behavior for edge cases (when boundaries are close to first and/or latests blocks) E.g. for `time_start=time_end=now` this function used to return `end<start` but now it returns `end=null`, because a masterblock for end doesn't exist yet.
* `max_shard_gen_utime_string` and `min_shard_gen_utime_string` in `BlockMaster`

### Improved

* faster and more reliable ArangoDB query for `blockchain.master_seq_no_range.end`

### Removed

See the [migration guide](https://docs.everos.dev/evernode-platform/reference/breaking-changes/migration-guides#migrate\_stats-1)

Queries:

* `blockchain.workchain_blocks`. Use `blockchain{ blocks }` instead.
* `blockchain.workchain_transactions`. Use `blockchain{ transactions }` instead.
* `blockchain.account_transactions`. Use `blockchain{ account{ transactions } }` instead.
* `explainQueryAccounts`
* `explainQueryTransactions`
* `explainQueryMessages`
* `explainQueryBlocks`
* `explainQueryBlockSignatures`
* `explainQueryZerostates`
* `getAccountsCount`
* `getTransactionsCount`
* `getAccountsTotalBalance`
* `QueryExplanation` and `SlowReason` types

## May 25, 2022

### New

* Deleted accounts added to API (even old ones)
* `Subscription.remReceipts` subscription.

## May 17, 2022

### Improved

* Subscriptions improved: no more websocket reconnections on stable network, no missed data during short websocket reconnections caused by network problems&#x20;

## March 16, 2022

### New

* Add new functions to `blockchain` root api:
  * `account`, allows:
    * to fetch account info (e.g. boc) via `info` field
    * to fetch transaction info via `transactions` (similar to now deprecated `blockchain.account_transactions`)
  * `blocks` (is similar to now deprecated `workchain_blocks`)
  * `transactions` (is similar to now deprecated `workchain_transactions`)
* Support for `null` in scalar filter. e.g. `filter: { last_paid: null }`. Means missing filter.

### Deprecated

* `blockchain { workchain_blocks }`. Use `blockchain{ blocks }` instead.
* `blockchain { workchain_transactions}`. Use `blockchain{ transactions }` instead.
* `blockchain { account_transactions }`. Use `blockchain{ account{ transactions } }` instead.

### Breaking

* In `blockchain.key_blocks` rename `seq_no` argument to `master_seq_no_range`.

## Feb 26, 2022

### New

* `account.init_code_hash` – account 's initial code hash (when it was deployed). All new accounts will have this field after such capability is enabled in the network.&#x20;
* Support `X-Evernode-Expected-Account-Boc-Version` http header. `1` (default) means "return old boc version" , `2` – "return new boc version" (with `init_code_hash` field).

## Feb 21, 2022

### Deprecated

* `when` argument in all joined fields (for example, transaction.in\_message's `when` argument)
* the following root queries:
  * `explainQueryAccounts`
  * `explainQueryTransactions`
  * `explainQueryMessages`
  * `explainQueryBlocks`
  * `explainQueryBlockSignatures`
  * `explainQueryZerostates`
  * `getAccountsCount`
  * `getTransactionsCount`
  * `getAccountsTotalBalance`
* `QueryExplanation` type

[Migration guide](../breaking-changes/migration-guides.md)

[Deprecation schedule](../breaking-changes/deprecation-schedule.md)

## Feb 1, 2022

### New features

``[`Statistics`](https://docs.everos.dev/ever-sdk/samples/graphql-samples/statistics) API

