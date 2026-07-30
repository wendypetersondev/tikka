[**Tikka SDK v0.1.0**](../../README.md)

***

[Tikka SDK](../../modules.md) / [index](../README.md) / RaffleStateError

# Class: RaffleStateError

Defined in: [modules/raffle/raffle.types.ts:114](https://github.com/wendypetersondev/tikka/blob/135e7048a6be51e7c3ee7bb769ffde8f8784171d/sdk/src/modules/raffle/raffle.types.ts#L114)

Thrown when an operation is attempted in an invalid state.
E.g. calling `triggerDraw` on an already-finalized raffle.

## Extends

- `Error`

## Constructors

### Constructor

> **new RaffleStateError**(`raffleId`, `currentStatus`, `attempted`): `RaffleStateError`

Defined in: [modules/raffle/raffle.types.ts:115](https://github.com/wendypetersondev/tikka/blob/135e7048a6be51e7c3ee7bb769ffde8f8784171d/sdk/src/modules/raffle/raffle.types.ts#L115)

#### Parameters

##### raffleId

`number`

##### currentStatus

[`RaffleStatus`](../enumerations/RaffleStatus.md)

##### attempted

[`RaffleTransition`](../type-aliases/RaffleTransition.md)

#### Returns

`RaffleStateError`

#### Overrides

`Error.constructor`

## Properties

### attempted

> `readonly` **attempted**: [`RaffleTransition`](../type-aliases/RaffleTransition.md)

Defined in: [modules/raffle/raffle.types.ts:118](https://github.com/wendypetersondev/tikka/blob/135e7048a6be51e7c3ee7bb769ffde8f8784171d/sdk/src/modules/raffle/raffle.types.ts#L118)

***

### currentStatus

> `readonly` **currentStatus**: [`RaffleStatus`](../enumerations/RaffleStatus.md)

Defined in: [modules/raffle/raffle.types.ts:117](https://github.com/wendypetersondev/tikka/blob/135e7048a6be51e7c3ee7bb769ffde8f8784171d/sdk/src/modules/raffle/raffle.types.ts#L117)

***

### raffleId

> `readonly` **raffleId**: `number`

Defined in: [modules/raffle/raffle.types.ts:116](https://github.com/wendypetersondev/tikka/blob/135e7048a6be51e7c3ee7bb769ffde8f8784171d/sdk/src/modules/raffle/raffle.types.ts#L116)
