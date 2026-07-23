# Pine Script Indicators — Gold Trading Systems

15+ Pine Script v6 indicators for XAUUSD / gold futures (GC, MGC), built and iterated across
two years of live chart work. ICT/SMC market-microstructure concepts: order blocks, fair-value
gaps, liquidity pools and sweeps, market-structure shifts (BOS/CHoCH), premium/discount
positioning, multi-timeframe bias, and session killzones.

## Layout

### `quantum-flow/` — the evolution (v18 → v25)
The Quantum Flow line: a full SMC decision engine that grew version by version — bias engines,
zone-reaction scoring, confluence ladders, discipline gates, live win-rate tracking.
Included deliberately **with its flaws**: v19 reached 417 inputs and became a lesson in
over-engineering (see the audit in the companion research repo). v18.1 contains targeted fixes:
chart-relative bias timeframes, conservative intrabar trade resolution, corrected RSI regime labels.

### `systems/` — lean, honestly-measured systems
Small single-thesis indicators with a shared honesty layer:
- **`ob_react_v1.pine`** — order-block reaction system built from a 25-day, 315-trade zone study
  (order blocks held 75–87% vs FVGs 44–64%; broken-zone "breaker" re-entries lost money and are
  deliberately excluded). First-touch entries, dead-zone flagging, volatility go-windows.
- **`mtf_cascade_honest_pnl.pine`** — lower→higher timeframe confirmation cascade (1m→3m→5m→15m).
- **`asian_range_break_honest_pnl.pine`** — Asian-range/London-breakout test harness. Verdict from
  its own dashboard: trend beta, not edge — kept as a documented negative result.

Every system reports: cost-inclusive net P&L, stop-first resolution on ambiguous bars,
long/short split, buy-and-hold benchmark, and an explicit **two-sided (STRUCTURE) vs beta verdict**.
A strategy only counts if it is profitable long AND short in the same regime.

## Design principles
1. Conservative measurement beats flattering measurement.
2. An edge must beat buy-and-hold and work both directions — otherwise it's market drift.
3. Fewer inputs beat more inputs (v19's 417 inputs proved the point the hard way).

*Built with an AI-augmented workflow (LLM-driven chart automation via Chrome DevTools Protocol).*
