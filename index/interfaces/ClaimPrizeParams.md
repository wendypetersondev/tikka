[**Tikka SDK v0.1.0**](../../README.md)

***

[Tikka SDK](../../modules.md) / [index](../README.md) / ClaimPrizeParams

# Interface: ClaimPrizeParams

Defined in: [modules/ticket/ticket.types.ts:91](https://github.com/wendypetersondev/tikka/blob/135e7048a6be51e7c3ee7bb769ffde8f8784171d/sdk/src/modules/ticket/ticket.types.ts#L91)

Parameters for claiming a finalized raffle prize.

## Properties

### memo?

> `optional` **memo?**: [`TxMemo`](../type-aliases/TxMemo.md)

Defined in: [modules/ticket/ticket.types.ts:95](https://github.com/wendypetersondev/tikka/blob/135e7048a6be51e7c3ee7bb769ffde8f8784171d/sdk/src/modules/ticket/ticket.types.ts#L95)

Optional transaction memo for tracking or external integrations.

***

### raffleId

> **raffleId**: `number`

Defined in: [modules/ticket/ticket.types.ts:93](https://github.com/wendypetersondev/tikka/blob/135e7048a6be51e7c3ee7bb769ffde8f8784171d/sdk/src/modules/ticket/ticket.types.ts#L93)

Raffle ID (must be positive integer)
