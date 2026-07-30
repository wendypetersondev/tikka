[**Tikka SDK v0.1.0**](../../README.md)

***

[Tikka SDK](../../modules.md) / [index](../README.md) / parseSorobanContractErrorCode

# Function: parseSorobanContractErrorCode()

> **parseSorobanContractErrorCode**(`raw`): `number` \| `undefined`

Defined in: [utils/errors.ts:252](https://github.com/wendypetersondev/tikka/blob/135e7048a6be51e7c3ee7bb769ffde8f8784171d/sdk/src/utils/errors.ts#L252)

Extracts a numeric Soroban contract error code from a raw error string.
Recognizes the common formats surfaced by the Stellar RPC / SDK:
  - "Error(Contract, #35)"
  - "ScError::Contract(4)"
  - "contract error code 5"

## Parameters

### raw

`string` \| `null` \| `undefined`

## Returns

`number` \| `undefined`

the parsed code, or `undefined` if no recognizable pattern is found.
