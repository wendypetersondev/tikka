[**Tikka SDK v0.1.0**](../../README.md)

***

[Tikka SDK](../../modules.md) / [index](../README.md) / WinningEntry

# Interface: WinningEntry

Defined in: [modules/user/user.types.ts:125](https://github.com/wendypetersondev/tikka/blob/135e7048a6be51e7c3ee7bb769ffde8f8784171d/sdk/src/modules/user/user.types.ts#L125)

A claimable prize entry returned by UserService.getWinnings.

## Properties

### claimed

> **claimed**: `boolean`

Defined in: [modules/user/user.types.ts:133](https://github.com/wendypetersondev/tikka/blob/135e7048a6be51e7c3ee7bb769ffde8f8784171d/sdk/src/modules/user/user.types.ts#L133)

Whether this prize has already been claimed on-chain.

***

### prizeAmount

> **prizeAmount**: `string`

Defined in: [modules/user/user.types.ts:129](https://github.com/wendypetersondev/tikka/blob/135e7048a6be51e7c3ee7bb769ffde8f8784171d/sdk/src/modules/user/user.types.ts#L129)

Prize amount as a string (e.g. "500").

***

### prizeAsset

> **prizeAsset**: `string`

Defined in: [modules/user/user.types.ts:131](https://github.com/wendypetersondev/tikka/blob/135e7048a6be51e7c3ee7bb769ffde8f8784171d/sdk/src/modules/user/user.types.ts#L131)

Asset symbol for the prize (e.g. "XLM").

***

### raffleId

> **raffleId**: `number`

Defined in: [modules/user/user.types.ts:127](https://github.com/wendypetersondev/tikka/blob/135e7048a6be51e7c3ee7bb769ffde8f8784171d/sdk/src/modules/user/user.types.ts#L127)

The raffle ID this prize belongs to.
