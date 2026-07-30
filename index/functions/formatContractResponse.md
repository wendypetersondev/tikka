[**Tikka SDK v0.1.0**](../../README.md)

***

[Tikka SDK](../../modules.md) / [index](../README.md) / formatContractResponse

# Function: formatContractResponse()

> **formatContractResponse**(`value`, `decimals?`): `string`

Defined in: [utils/formatting.ts:178](https://github.com/wendypetersondev/tikka/blob/135e7048a6be51e7c3ee7bb769ffde8f8784171d/sdk/src/utils/formatting.ts#L178)

Formats a raw balance or ticket count for display.

Only accepts string values or **safe integers** — JS float numbers are
rejected because they may already be precision-corrupted before BigNumber
can process them (e.g. `0.1 + 0.2 === 0.30000000000000004`).

## Parameters

### value

`string` \| `number`

Raw value from the contract (string, or safe integer number).

### decimals?

`number` = `7`

Number of decimal places to show (default 7 for XLM).

## Returns

`string`
