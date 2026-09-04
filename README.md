# Observer Radar

Live stock×meme radar for **Robinhood Chain (4663)** — launches, anchor complexes,
leadership flips and RPC latency edge.

**Built output only.** This repo holds the compiled page; the system that generates it lives
in a separate repository.

## How it runs with no backend

Every upstream it needs — all five public Robinhood RPCs, both WebSocket endpoints, and the
anchor-map API — serves `Access-Control-Allow-Origin: *`, including the RPCs on POST. So the
page opens its own WebSocket subscriptions to the Uniswap v4 PoolManager and reads the chain
directly. **Your tab is the process.** There is no server, no API key, and nothing is
collected.

- Launch detection is **push, sub-second** — not polling.
- Both WebSocket providers are subscribed at once and events deduplicated, because provider
  chain heads drift by up to ~64 blocks (≈4.5s). Whichever delivers first wins.
- Velocity baselines build while the tab is open, so the acceleration panel stays empty for
  the first ~4 minutes. That is deliberate: something newly discovered has no baseline and
  would otherwise read as infinitely fast.

State is per-tab and resets on reload.

Market data, not advice.
