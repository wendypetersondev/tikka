[**Tikka SDK v0.1.0**](../../README.md)

***

[Tikka SDK](../../modules.md) / [index](../README.md) / TxMemo

# Type Alias: TxMemo

> **TxMemo** = \{ `type`: `"text"`; `value`: `string`; \} \| \{ `type`: `"id"`; `value`: `string`; \} \| \{ `type`: `"hash"`; `value`: `Buffer`; \}

Defined in: [contract/lifecycle.ts:45](https://github.com/wendypetersondev/tikka/blob/135e7048a6be51e7c3ee7bb769ffde8f8784171d/sdk/src/contract/lifecycle.ts#L45)

Transaction memo — attach tracking data or external references.
Mirrors the three Stellar memo types the protocol supports.
