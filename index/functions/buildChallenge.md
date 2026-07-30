[**Tikka SDK v0.1.0**](../../README.md)

***

[Tikka SDK](../../modules.md) / [index](../README.md) / buildChallenge

# Function: buildChallenge()

> **buildChallenge**(`options`): `string`

Defined in: [auth/sep10.ts:136](https://github.com/wendypetersondev/tikka/blob/135e7048a6be51e7c3ee7bb769ffde8f8784171d/sdk/src/auth/sep10.ts#L136)

Build a SEP-10 challenge transaction.

## Parameters

### options

[`BuildChallengeOptions`](../interfaces/BuildChallengeOptions.md)

BuildChallengeOptions

## Returns

`string`

XDR string for the signed challenge transaction

## Example

```ts
const challengeXdr = buildChallenge({
  serverSecret: process.env.SEP10_SERVER_SECRET,
  clientAccount: clientPublicKey,
  anchorDomain: 'example.com',
  webAuthDomain: 'auth.example.com',
  timeout: 300,
  networkPassphrase: Networks.TESTNET,
});
```
