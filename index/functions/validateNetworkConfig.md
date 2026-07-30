[**Tikka SDK v0.1.0**](../../README.md)

***

[Tikka SDK](../../modules.md) / [index](../README.md) / validateNetworkConfig

# Function: validateNetworkConfig()

> **validateNetworkConfig**(`config`): [`NetworkConfig`](../interfaces/NetworkConfig.md)

Defined in: [network/network.config.ts:109](https://github.com/wendypetersondev/tikka/blob/135e7048a6be51e7c3ee7bb769ffde8f8784171d/sdk/src/network/network.config.ts#L109)

Validate a fully-resolved network config (issue #1096).

Runs at construction rather than at first request. A malformed RPC URL
previously surfaced as a fetch failure on the first call — far from the line
that actually caused it, and indistinguishable from the endpoint being down.

Every failure names the offending field, so the message points at the fix.

## Parameters

### config

[`NetworkConfig`](../interfaces/NetworkConfig.md)

## Returns

[`NetworkConfig`](../interfaces/NetworkConfig.md)

## Throws
