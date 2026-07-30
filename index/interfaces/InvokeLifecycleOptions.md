[**Tikka SDK v0.1.0**](../../README.md)

***

[Tikka SDK](../../modules.md) / [index](../README.md) / InvokeLifecycleOptions

# Interface: InvokeLifecycleOptions

Defined in: [contract/lifecycle.ts:100](https://github.com/wendypetersondev/tikka/blob/135e7048a6be51e7c3ee7bb769ffde8f8784171d/sdk/src/contract/lifecycle.ts#L100)

Combined options for a full invoke (simulate + sign + submit + poll).

## Properties

### fee?

> `optional` **fee?**: `string`

Defined in: [contract/lifecycle.ts:104](https://github.com/wendypetersondev/tikka/blob/135e7048a6be51e7c3ee7bb769ffde8f8784171d/sdk/src/contract/lifecycle.ts#L104)

Override the transaction base fee (in stroops). Default: BASE_FEE.

***

### memo?

> `optional` **memo?**: [`TxMemo`](../type-aliases/TxMemo.md)

Defined in: [contract/lifecycle.ts:108](https://github.com/wendypetersondev/tikka/blob/135e7048a6be51e7c3ee7bb769ffde8f8784171d/sdk/src/contract/lifecycle.ts#L108)

Optional memo attached to the transaction envelope.

***

### poll?

> `optional` **poll?**: [`PollConfig`](PollConfig.md)

Defined in: [contract/lifecycle.ts:106](https://github.com/wendypetersondev/tikka/blob/135e7048a6be51e7c3ee7bb769ffde8f8784171d/sdk/src/contract/lifecycle.ts#L106)

Polling configuration.

***

### sourcePublicKey?

> `optional` **sourcePublicKey?**: `string`

Defined in: [contract/lifecycle.ts:102](https://github.com/wendypetersondev/tikka/blob/135e7048a6be51e7c3ee7bb769ffde8f8784171d/sdk/src/contract/lifecycle.ts#L102)

Override the source public key (defaults to wallet.getPublicKey()).
