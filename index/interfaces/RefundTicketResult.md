[**Tikka SDK v0.1.0**](../../README.md)

***

[Tikka SDK](../../modules.md) / [index](../README.md) / RefundTicketResult

# Interface: RefundTicketResult

Defined in: [modules/ticket/ticket.types.ts:79](https://github.com/wendypetersondev/tikka/blob/135e7048a6be51e7c3ee7bb769ffde8f8784171d/sdk/src/modules/ticket/ticket.types.ts#L79)

Result of a ticket refund.
Provides transaction confirmation.

## Properties

### feePaid

> **feePaid**: `string`

Defined in: [modules/ticket/ticket.types.ts:85](https://github.com/wendypetersondev/tikka/blob/135e7048a6be51e7c3ee7bb769ffde8f8784171d/sdk/src/modules/ticket/ticket.types.ts#L85)

Transaction fee paid in stroops

***

### ledger

> **ledger**: `number`

Defined in: [modules/ticket/ticket.types.ts:83](https://github.com/wendypetersondev/tikka/blob/135e7048a6be51e7c3ee7bb769ffde8f8784171d/sdk/src/modules/ticket/ticket.types.ts#L83)

Ledger number where transaction was confirmed

***

### transactionHash

> **transactionHash**: `string`

Defined in: [modules/ticket/ticket.types.ts:81](https://github.com/wendypetersondev/tikka/blob/135e7048a6be51e7c3ee7bb769ffde8f8784171d/sdk/src/modules/ticket/ticket.types.ts#L81)

Transaction hash for confirmation
