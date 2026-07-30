[**Tikka SDK v0.1.0**](../../README.md)

***

[Tikka SDK](../../modules.md) / [index](../README.md) / FeeQuoteConfidence

# Type Alias: FeeQuoteConfidence

> **FeeQuoteConfidence** = `"high"` \| `"medium"` \| `"low"`

Defined in: [fee-estimator/fee-estimator.types.ts:18](https://github.com/wendypetersondev/tikka/blob/135e7048a6be51e7c3ee7bb769ffde8f8784171d/sdk/src/fee-estimator/fee-estimator.types.ts#L18)

Confidence level of the fee estimate.
- `high`   — live simulation succeeded; safe to present to the user
- `medium` — simulation data is stale (past `staleAfterMs`) but usable
- `low`    — fallback estimate; actual fee may differ significantly
