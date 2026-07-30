[**Tikka SDK v0.1.0**](../../README.md)

***

[Tikka SDK](../../modules.md) / [index](../README.md) / BuyBatchParams

# Interface: BuyBatchParams

Defined in: [modules/ticket/ticket.types.ts:134](https://github.com/wendypetersondev/tikka/blob/135e7048a6be51e7c3ee7bb769ffde8f8784171d/sdk/src/modules/ticket/ticket.types.ts#L134)

Parameters for batch ticket purchases across multiple raffles.
Supports up to 100 purchases per batch.

## Properties

### memo?

> `optional` **memo?**: [`TxMemo`](../type-aliases/TxMemo.md)

Defined in: [modules/ticket/ticket.types.ts:141](https://github.com/wendypetersondev/tikka/blob/135e7048a6be51e7c3ee7bb769ffde8f8784171d/sdk/src/modules/ticket/ticket.types.ts#L141)

Optional transaction memo for tracking or external integrations.
Supports text (≤28 bytes), numeric id, or 32-byte hash.

***

### purchases

> **purchases**: [`BatchTicketPurchase`](BatchTicketPurchase.md)[]

Defined in: [modules/ticket/ticket.types.ts:136](https://github.com/wendypetersondev/tikka/blob/135e7048a6be51e7c3ee7bb769ffde8f8784171d/sdk/src/modules/ticket/ticket.types.ts#L136)

Array of purchases (1-100 items)
