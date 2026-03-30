# YNOT.NOW — Insurance AI Signal Intelligence for Context Hub

[![Weekly Update](https://img.shields.io/badge/update-every%20Monday-blue)](https://ynot-now.vercel.app)
[![Signals](https://img.shields.io/badge/output-27%2B%20findings%2Fweek-green)](https://ynot-now.vercel.app/api/context-hub)
[![License](https://img.shields.io/badge/license-MIT-lightgrey)](LICENSE)
[![Context Hub](https://img.shields.io/badge/context--hub-community-orange)](https://github.com/andrewyng/context-hub)

> Domain knowledge for AI agents building in insurance — auto-updated every Monday by an 8-agent intelligence system.

## What This Is

Six domain-specific intelligence documents, refreshed weekly, that give any coding agent instant context on what's happening in insurance AI. Each document covers a different vertical — life insurance, P&C, regulation, climate risk, horizontal tech, or the full cross-domain view.

Every finding includes a verdict (SIGNAL / WATCH), confidence score, Technology Readiness Level, source URLs, and the identifying agent — so your agent can reason about maturity and reliability, not just keywords.

**Live endpoint:** [`GET /api/context-hub`](https://ynot-now.vercel.app/api/context-hub)

## Documents

| Document | `chub get` ID | What it covers |
|----------|--------------|----------------|
| [Insurance AI Signals](content/ynot/docs/insurance-ai-signals/DOC.md) | `ynot/insurance-ai-signals` | Full cross-domain intelligence (all 8 agents) |
| [Life Insurance Signals](content/ynot/docs/insurance-life-signals/DOC.md) | `ynot/insurance-life-signals` | Life, annuities, retirement, longevity, actuarial ML |
| [P&C Signals](content/ynot/docs/insurance-pc-signals/DOC.md) | `ynot/insurance-pc-signals` | Property & casualty, underwriting, claims, telematics |
| [Regulation Signals](content/ynot/docs/insurance-regulation-signals/DOC.md) | `ynot/insurance-regulation-signals` | NAIC, FCA, EIOPA, EU AI Act, model governance |
| [Climate Signals](content/ynot/docs/insurance-climate-signals/DOC.md) | `ynot/insurance-climate-signals` | Climate risk AI, parametric, ESG, catastrophe modelling |
| [Horizontal Tech Signals](content/ynot/docs/insurance-horizontal-signals/DOC.md) | `ynot/insurance-horizontal-signals` | Foundation models, agentic AI, synthetic data, PQC |

## Using with Context Hub CLI

```bash
# Search for insurance intelligence
chub search insurance

# Get the full cross-domain signals doc
chub get ynot/insurance-ai-signals

# Get domain-specific intelligence
chub get ynot/insurance-life-signals
chub get ynot/insurance-regulation-signals

# Machine-readable JSON (for agent pipelines)
curl "https://ynot-now.vercel.app/api/context-hub?format=json"

# Filter by domain + time window
curl "https://ynot-now.vercel.app/api/context-hub?domain=life&weeks=4"
```

## Live API

The documents in this repo are snapshots. The live API always has the latest data:

| Endpoint | Returns |
|----------|---------|
| `/api/context-hub` | Full markdown DOC.md (all domains) |
| `/api/context-hub?domain=life` | Life insurance signals only |
| `/api/context-hub?domain=pc` | P&C signals only |
| `/api/context-hub?domain=regulation` | Regulatory signals only |
| `/api/context-hub?domain=climate` | Climate & ESG signals only |
| `/api/context-hub?domain=horizontal` | Horizontal tech signals only |
| `/api/context-hub?format=json` | Machine-readable JSON with signal trajectories |
| `/api/context-hub?weeks=4` | Lookback window (default 2, max 8) |

## How It's Made

YNOT.NOW runs **8 specialist AI agents** every Monday in two phases:

**Phase 1 — Domain Agents** search the web autonomously (Tavily API), each covering a specific insurance vertical: Scout (P&C), Vita (Life), Lex (Regulation), Terra (Climate), Horizon (Horizontal Tech).

**Phase 2 — Synthesis Agents** read all Phase 1 findings, then do their own targeted research: Null (sceptic — removes noise), Weave (cross-domain patterns), Faro (18–36 month horizon signals).

Every finding goes through URL verification (HTTP HEAD checks), freshness validation (4-layer date filtering), signal status tracking (NEW → EMERGING → CONFIRMED → RECURRING), and cross-agent agreement detection.

**Signal Trajectories** track how topics evolve week-over-week with compound scoring (persistence × confidence × cross-agent agreement × TRL velocity).

## Finding Schema

Each finding includes:

| Field | Description |
|-------|-------------|
| `title` | Specific, named finding |
| `verdict` | SIGNAL (high confidence) · WATCH (emerging) |
| `signal_status` | NEW · EMERGING · CONFIRMED · RECURRING |
| `trl` | Technology Readiness Level 1–9 |
| `confidence` | Multi-agent cross-validated percentage |
| `domain` | Insurance vertical |
| `body` | 2–3 sentence evidence summary |
| `source_url` | Verified, publicly accessible source |
| `agent` | Which mind identified it |
| `regions` | Geographic tags: US, EU, UK, APAC, Global |

## Update Schedule

| When | What happens |
|------|-------------|
| Monday 06:00 UTC | Phase 1 agents run (YNOT.NOW cron) |
| Monday 06:02 UTC | Phase 2 synthesis agents run |
| Monday 07:00 UTC | GitHub Action fetches latest findings, creates PR to this repo |

Updates are fully automated. The GitHub Action syncs the fork with upstream, fetches fresh findings from the live API, validates the output, and opens a PR.

## Contributing

This content is auto-generated by YNOT.NOW's multi-agent system. To improve the intelligence:

- **Report bad signals:** Open an issue if a finding has a dead source or incorrect verdict
- **Suggest new domains:** Want a new insurance vertical covered? Open an issue
- **Improve the source:** Contributions to the [YNOT.NOW repo](https://github.com/heyshivaai/ynot-now) improve what gets exported here

## Links

- **Live platform:** [ynot-now.vercel.app](https://ynot-now.vercel.app)
- **Source repo:** [github.com/heyshivaai/ynot-now](https://github.com/heyshivaai/ynot-now)
- **Upstream Context Hub:** [github.com/andrewyng/context-hub](https://github.com/andrewyng/context-hub)
