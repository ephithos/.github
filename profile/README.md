# AlphaBoundary

> **Microstructure-native. Statistically validated. Online-adaptive.**
>
> *The institutional-grade quantitative research workstation built exclusively for systematic crypto perpetual trading.*

---

## What is AlphaBoundary?

AlphaBoundary is a desktop-first quantitative research platform for systematic crypto traders, prop firm quants, and independent researchers. It provides a complete institutional research workflow — from raw market data to statistically validated deployment, and beyond into live adaptive monitoring — without requiring you to write a single line of code.

Most trading tools confuse backtesting with edge discovery. They let you tweak parameters until the equity curve looks attractive, which guarantees overfitting and rarely survives live markets. AlphaBoundary was built to solve this specific problem by enforcing a strict separation between *discovery* (calibration) and *validation* (backtesting), using the same statistical rigour found in professional quant desks.

---

## The Closed-Loop Alpha Lifecycle

We treat a trading strategy as a living hypothesis, not a static file. The platform orchestrates a continuous, gated pipeline across six distinct phases:

1. **Discovery (Calibration)** — Bayesian (TPE) or Random Search explores the parameter space across walk-forward windows. This is where the system searches for parameters that generalise out-of-sample, rather than merely fitting historical noise.

2. **Statistical Validation** — Before any parameter reaches production, it passes through an institutional-grade gatekeeper: Deflated Sharpe Ratio (DSR), Probabilistic Sharpe Ratio (PSR), and Combinatorial Purged Cross-Validation (CPCV) to compute the Probability of Backtest Overfitting (PBO). If PBO exceeds 50 %, the platform locks the Deploy button and explains why.

3. **Backtesting (The Judge)** — The backtest is a sacred, deterministic replay of tick-level data with bit-identical live parity. It does not search; it only judges the final calibrated configuration against real market microstructure, fees, and funding.

4. **Guarded Execution** — Once deployed, the strategy runs with comprehensive risk guardrails: max notional, order-rate limits, stale-data blocks, and trailing drawdown locks.

5. **Live Monitoring & Drift Detection** — A static strategy is a dying strategy. Signal Monitoring tracks rolling Information Coefficients (IC) per alpha group and market regime, using CUSUM charts and first/second-half decay to detect erosion of edge in real time.

6. **Online Adaptation (φ-Overlay)** — When drift is detected, the system applies a dynamic multiplier (φ) per group and regime, bounded between 0.8 and 1.2. This operates in Shadow Mode first, then gates the correction to live execution — adjusting signal weights based on current market behaviour without destroying the core strategy logic.

---

## Why Crypto-Native?

Most generic quant platforms (including QuantConnect) were designed for equities, indices, and forex, with crypto added as an afterthought. They rely on OHLC or QuoteBar data, which obscures the microstructure that drives short-term alpha in perpetual futures.

AlphaBoundary is built exclusively for crypto perpetual futures and understands:

- **Tick-level L5–L20 Order Book Depth** — We replay the actual depth ladder, not just top-of-book. The edge in crypto lives in the microstructure; we capture it directly.
- **Funding Rate Dynamics** — 8‑hour settlements are modelled as a real cost drag, not an afterthought.
- **Liquidation Cascades** — Detected in real time via VPIN and order-flow imbalance, filtering toxic flow before it affects your entries.
- **HMM Regime Detection** — Five crypto-specific regimes (trend_up, trend_down, range, vol_expansion, stress), defined by the unique volatility clustering of crypto markets.
- **24/7 Market Structure** — No opening or closing bells; the engine runs continuously with low‑latency, event‑driven architecture.

Generic models fail in crypto. Crypto‑native models survive.

---

## Comparison at a Glance

| **Aspect** | **AlphaBoundary** | **Generic Quant Platforms (e.g., QuantConnect)** | **Retail Bots** |
| :--- | :--- | :--- | :--- |
| **Data Fidelity** | Tick + L5–L20 Depth. Full microstructure replay. | OHLC / QuoteBar. No L2 depth. | Candlestick OHLC. |
| **Crypto‑Native** | Yes. Funding, liquidations, 24/7, HMM regimes. | No. Equities/Forex first; crypto is an afterthought. | No. Grid/DCA agnostic to asset class. |
| **Edge Discovery** | Bayesian (TPE) / Random. Walk‑forward calibration. | User‑coded scripts. Requires manual programming. | Manual tweaking. |
| **Overfitting Detection** | Built‑in DSR, PSR, CPCV/PBO. Blocks deploy if PBO > 50 %. | Requires custom implementation. | None. |
| **Compute Architecture** | Local C# Agent. Zero cloud fees, unlimited runs. | Cloud Pay‑per‑hour ($0.15–$0.30/h). | Lightweight cloud. |
| **Parallelism Control** | **User‑configurable CPU cores** (e.g., 6/8 cores). Balance performance and system responsiveness. | Fixed cloud instance cores. Upgrading costs more. | Fixed / low parallelism. |
| **Execution Persistence** | **Headless background daemon.** Strategy runs even when UI is closed. Re‑open to see real‑time PnL. | Depends on cloud agent; UI closure may interrupt live view. | Often tied to the open app/tab. |
| **Live Parity** | Bit‑identical. Tick/L5 matches live executor. | Good, but limited. OHLC vs tick divergence remains. | Poor. |
| **Online Adaptation** | Dynamic φ‑Overlay. Corrects signal weights in live. | Static. Requires manual re‑calibration. | Static. |
| **Quant Copilot** | LLM + RAG. Actionable diagnostics. | Raw logs + Community forums. | Generic support. |

---

## Total Cost of Ownership (TCO)

To genuinely discover and maintain a non‑overfitted edge, a serious trader traditionally pays for three independent pillars. AlphaBoundary consolidates them into a single subscription.

| **Cost Center** | **Traditional Setup (Market Rate)** | **AlphaBoundary** |
| :--- | :--- | :--- |
| **Institutional Data** (Tick / L2 / Depth) | $200 – $500 / month | **Included** |
| **Cloud Compute** (Calibration / MC / CPCV) | $50 – $150 / month | **Included** (Local Agent) |
| **Quant Developer Time** (Coding DSR/PBO/EVT/Overlay) | $2,000 – $5,000 / month (in senior hours) | **Included** (Automated) |
| **Monthly Total** | **$250 – $800+** | **$99** |
| **Annual Cost** | **$3,000 – $9,600+** | **$1,188** |

**Economic Resilience** — Because compute is local and data sync is incremental (only downloading missing partitions, e.g., 0 bytes downloaded for 725 checked files), heavy usage by power users does **not** increase our server costs. We can afford unlimited calibrations at a fixed price.

---

## Core Research Modules (At a Glance)

- **Data Layer** — Real‑time tick ingestion, L5–L20 depth synchronisation, local encrypted storage (Parquet + DuckDB), and **incremental sync** (only downloads deltas). No cloud data fees.
- **Alpha Research** — 88+ features across 8 groups (trend, momentum, mean reversion, volatility, microstructure, derivatives, cross‑asset, composite) with regime‑aware scoring and HMM state detection.
- **Calibration** — Bayesian (TPE), Random, and Multi‑Period search with walk‑forward validation and parameter robustness analysis.
- **Statistical Validation** — DSR, PSR, CPCV/PBO, Monte Carlo (block, i.i.d., shuffle), EVT (Extreme Value Theory), Stress Testing (cost sweeps, adverse regimes, jitter), and cross‑regime validation.
- **Execution Engine** — Event‑driven, bit‑identical live parity, maker/taker modes, and comprehensive risk guardrails (max notional, order‑rate limits, stale‑data blocks, trailing drawdown locks). **Headless background execution** ensures strategies continue trading even when the UI is closed. Re‑open the dashboard to see equity, PnL, open positions, and margin in real time.
- **User‑Configurable Parallelism** — Through the Settings panel, users can cap the number of CPU cores allocated for backtesting, IC, and calibration (e.g., 6 out of 8 cores). This balances computational throughput against system responsiveness, offering flexibility for laptops (low core count) to high‑end workstations (unleashing full power) without incurring extra cloud costs.
- **Live Monitoring & Adaptation** — Rolling IC per group/regime, CUSUM drift charts, and a dynamic φ‑overlay (Shadow → Gated → Live correction) that learns from market behaviour without rewriting the strategy.
- **Quant Copilot** — A multi‑layer LLM assistant (RAG + detection + open‑ended LLM) that explains metrics, diagnoses failures, and recommends actionable parameter adjustments.

---

## Design Principles

- **Local‑First** — Your data, your compute. No dependency on external cloud billing.
- **Statistical Honesty** — We block deployment if the edge is not statistically proven (PBO > 50 %).
- **Reproducible Research** — Every calibration, backtest, and overlay state is persisted and auditable.
- **Crypto‑Native** — Built exclusively for perpetual futures, not adapted from equities.
- **Explain Every Decision** — The Quant Copilot ensures you never stare at a raw number without context.
- **Zero‑Code Research** — Institutional‑grade quant research, accessible without writing Python or C#.
- **Resilient by Design** — The execution engine runs as a background daemon; the UI is a viewer. A closed laptop or crashed front‑end does not interrupt your live strategy.
- **User‑Controlled Compute** — You choose how much of your CPU to dedicate to heavy jobs, preserving your machine's responsiveness while maximising throughput.

---

## Technology Stack

- **C#** — High‑performance local execution agent (struct/value types, low GC, headless capable).
- **Node.js / React / TypeScript** — Backend orchestration and modern desktop UI (viewer for the headless agent).
- **DuckDB + Parquet** — Columnar storage for massive tick/L2 historical datasets with incremental sync.
- **MongoDB** — Operational state and job orchestration.
- **LLM (RAG)** — Quant Copilot for contextual assistance.

---

## Current Status

- 🚧 Active Development
- ✅ Tick‑level L5 Depth replay validated.
- ✅ Calibration (Bayesian/TPE) + DSR/PBO validation live.
- ✅ Signal Monitoring + Overlay Control (Shadow/Gated) production‑ready.
- ✅ Local C# Agent fully integrated.
- ✅ Headless background execution & user‑configurable CPU parallelism active.
- 📅 Commercial release planned — Freemium / Professional / Enterprise tiers available.

---

## The One‑Sentence Takeaway

> *"We do not sell you a backtest or a bot. We sell a statistical feedback system: you design the hypothesis, we validate it rigorously with PBO/DSR, we execute it faithfully with bit‑identical parity (even when the UI is closed), and we correct it dynamically via an online φ‑overlay as the market evolves — without requiring you to write a single line of code to adapt it."*

AlphaBoundary is built for traders who understand that edge is rare, fragile, and non‑stationary. It is the infrastructure of a quant desk, packaged for the independent professional. No data fees. No compute bills. No coding. Just statistical truth.

---

## License

Available under **Freemium**, **Professional**, and **Enterprise** tiers.
