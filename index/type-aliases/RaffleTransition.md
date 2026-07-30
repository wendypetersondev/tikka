[**Tikka SDK v0.1.0**](../../README.md)

***

[Tikka SDK](../../modules.md) / [index](../README.md) / RaffleTransition

# Type Alias: RaffleTransition

> **RaffleTransition** = `"open→drawing"` \| `"drawing→finalized"` \| `"open→cancelled"`

Defined in: [modules/raffle/raffle.types.ts:105](https://github.com/wendypetersondev/tikka/blob/135e7048a6be51e7c3ee7bb769ffde8f8784171d/sdk/src/modules/raffle/raffle.types.ts#L105)

Valid state transitions in the raffle contract state machine:

 Open ──► Drawing  (trigger_draw)
 Drawing ──► Finalized (receive_randomness → internal finalization)
 Open ──► Cancelled (cancel_raffle)

Any other transition is rejected by the contract and surfaced as
`RaffleStateError`.
