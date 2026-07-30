[**Tikka SDK v0.1.0**](../../README.md)

***

[Tikka SDK](../../modules.md) / [index](../README.md) / resolveNetworkConfig

# Function: resolveNetworkConfig()

> **resolveNetworkConfig**(`networkOrConfig`): [`NetworkConfig`](../interfaces/NetworkConfig.md)

Defined in: [network/network.config.ts:173](https://github.com/wendypetersondev/tikka/blob/135e7048a6be51e7c3ee7bb769ffde8f8784171d/sdk/src/network/network.config.ts#L173)

Resolves a NetworkConfig by name, or accepts a custom override.

The result is validated before it is returned (issue #1096), so an invalid
config fails here rather than on the first request.

## Parameters

### networkOrConfig

[`NetworkConfig`](../interfaces/NetworkConfig.md) \| [`TikkaNetwork`](../type-aliases/TikkaNetwork.md) \| `Partial`\<[`NetworkConfig`](../interfaces/NetworkConfig.md)\> & `object`

## Returns

[`NetworkConfig`](../interfaces/NetworkConfig.md)

## Throws
