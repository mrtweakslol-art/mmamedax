# MEMEDAX — AI-Powered Solana Memecoin Intelligence & Auto Signals Platform

MEMEDAX is a high-frequency Solana blockchain intelligence, deterministic quantitative analysis, NVIDIA GLM AI trade evaluation, and autonomous signal detection platform.

Designed using the **Terminal Intelligence** aesthetic (Bloomberg-grade financial clarity meets cyberpunk telemetry), MEMEDAX continuously digests on-chain Solana tokens, calculates multi-factor quantitative scores, cross-verifies on-chain security risks via RugCheck, renders real-time 5m OHLCV candlestick charts via GeckoTerminal and DEX Screener, runs NVIDIA GLM 5.3 Flash qualitative evaluations, and autonomously publishes actionable trading setups with entry zones, invalidation stop-loss levels, and triple profit targets.

---

## 1. System Architecture

```
[ Telegram Call Ingestion ] (Supabase Table Discovery)
                   │
                   ▼
┌────────────────────────────────────────────────────────┐
│             MEMEDAX Intelligence Engine                │
├────────────────────────────────────────────────────────┤
│ 1. Multi-Pool Discovery (DEX Screener & GeckoTerminal) │
│ 2. Real-Time Telemetry & Solana RPC Health             │
│ 3. On-Chain Risk & RugCheck Audit                      │
│ 4. Deterministic Indicators (EMA 9/21/50, RSI, ATR)   │
│ 5. 7-Factor Weighted MEMEDAX Score (0-100)             │
│ 6. Hard Risk Gates (Freeze Authority, Top 10 Holder)   │
│ 7. NVIDIA GLM 5.3 Flash AI Trade Interpretation        │
└────────────────────────────────────────────────────────┘
                   │
         ┌─────────┴─────────┐
         ▼                   ▼
[ MEMEDAX Tokens Feed ]   [ MEMEDAX Auto Signals ]
 (Telegram Call Pipeline)  (Autonomous Pair Discovery)
         │                   │
         └─────────┬─────────┘
                   ▼
[ Forward Outcome Tracking & Telegram Broadcaster ]
```

---

## 2. Environment Variables & Secrets

Configure these in the AI Studio UI (**Settings > Secrets**) or `.env`:

| Variable | Description | Status |
| :--- | :--- | :--- |
| `NVIDIA_API_KEY` | NVIDIA API key for pair analysis with `z-ai/glm-5.3-flash`. | **Active & Live** |
| `SUPABASE_URL` | Supabase project URL hosting the existing Telegram calls table. | *Configurable* |
| `SUPABASE_ANON_KEY` | Public anon key for querying calls. | *Configurable* |
| `SUPABASE_SERVICE_ROLE_KEY` | Service role key for server-side persistence. | *Configurable* |
| `SOLANA_RPC_URL` | Custom RPC endpoint (defaults to `https://api.mainnet-beta.solana.com`). | **Active (Public)** |
| `TELEGRAM_BOT_TOKEN` | Bot token to broadcast signals to Telegram channels. | *Optional* |
| `TELEGRAM_CHAT_ID` | Telegram target channel or group ID. | *Optional* |

---

## 3. Live Integrated APIs

- **DEX Screener API**: Real-time pool resolution, 5m/1h/24h price changes, volume, liquidity, buy/sell ratios. (Free public API, zero key needed).
- **GeckoTerminal API**: 5-minute OHLCV candlestick data and pool metadata. (Free public API, zero key needed).
- **RugCheck API**: Mint authority check, freeze authority check, LP lock percentage, top 10 holders concentration. (Free public API, zero key needed).
- **Solana JSON-RPC**: `getHealth` latency monitoring and account verification.
- **NVIDIA NIM (`z-ai/glm-5.3-flash`)**: Server-side qualitative analysis, evidence weighting, confidence scoring, and trade reasoning. If `NVIDIA_API_KEY` is unavailable or the API request fails, the app uses deterministic analysis.

---

## 4. Supabase Table Discovery & Telegram Ingestion

MEMEDAX automatically scans your Supabase database for any of the standard Telegram call tables:
- `telegram_calls`
- `token_calls`
- `calls`
- `signals`
- `token_alerts`
- `telegram_messages`

It reads:
- `token_name` / `name`
- `ticker` / `symbol`
- `mint_address` / `contract_address` / `ca`
- `original_message` / `text`
- `source_channel`
- `reported_price` & `reported_mcap`
- `created_at` timestamp

When Supabase has no Telegram calls to display, the feed falls back to live Solana token discovery from DEX Screener. Discovered pairs include their available market data and token images; no placeholder or fabricated assets are inserted.

---

## 5. Scoring Engine & Deterministic Rules

The 7-factor scoring engine calculates a 0–100 score:
1. **Token Safety & Risk (25 pts)**: LP burned/locked status, mint authority revoked.
2. **Price Structure & Trend (20 pts)**: EMA 9 > EMA 21, support test, breakout detection.
3. **Volume & Momentum (15 pts)**: Volume acceleration factor, buy dominance %.
4. **Liquidity & Execution (15 pts)**: Executable depth, slippage for $100, $500, and $2,500 orders.
5. **Holder Analysis (10 pts)**: Top 10 wallet concentration < 30%.
6. **Entry Quality & Risk/Reward (10 pts)**: Retest distance to support, stop distance.
7. **Market Context (5 pts)**: Solana network health and trend.

### Hard Risk Gates:
- Active Freeze Authority $\rightarrow$ Instant **REJECTED** verdict.
- Unrevoked Mint Authority + Top 10 holders > 65% $\rightarrow$ Instant **REJECTED** verdict.
- Pool Liquidity < $5,000 $\rightarrow$ Instant **REJECTED** verdict.

---

## 6. How to Test the Complete End-to-End Workflow

1. **Tokens Feed**:
   - Open the **Tokens** tab to view live calls.
   - Filter by `All (142)`, `New (38)`, `Analyzing (12)`, `Watchlist (9)`, `Qualified (7)`, or `Risk Flags (3)`.
   - Sort by `Age`, `Vol`, `MEMEDAX`, or `5m Gain`.
   - Use search or paste a Solana CA.

2. **Triggering AI & Market Analysis**:
   - Click on any discovered or ingested token card.
   - The detailed telemetry modal opens:
     - View the interactive SVG 5m candlestick chart with EMA 9/21 lines, RSI 14, and volume bars.
     - Inspect the RugCheck security audit matrix.
     - Review the 7-factor score breakdown with reasons and deductions.
     - Read the NVIDIA GLM 5.3 Flash interpretation with supporting vs conflicting evidence.
     - Click **"RE-ANALYZE"** to trigger an on-demand server-side NVIDIA AI analysis pass.

3. **MEMEDAX Auto Signals**:
   - Switch to the **Auto Signals** tab in the navigation bar.
   - Inspect the top scanner metrics (Pairs monitored, Candidates analyzed, Qualified setups, Scanner status).
   - Filter by `Best Setups`, `Early Momentum`, `Breakouts`, `Pullbacks`, or `High Volume`.
   - Review each opportunity's Entry Zone, Stop-Loss / Invalidation level, Target 1, 2, and 3, and Risk/Reward ratio.
   - Click **"Telegram"** to dispatch the signal alert (or test ping via the Config modal).
   - Click **"SCAN SOLANA NOW"** to force an autonomous discovery pass across Solana pairs.

4. **Outcome Tracking**:
   - Switch to **Outcomes / Stats** tab.
   - Inspect documented win rates, average trade return, profit factor, max drawdown, and target hit distribution.

5. **Config & Settings**:
   - Click the **Config** icon to adjust score weights, risk thresholds, inspect Supabase connection status, or test Telegram alerts.
