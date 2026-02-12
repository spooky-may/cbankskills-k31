# CN Finance — Claude AI Skills for Financial Services

[![License](https://img.shields.io/badge/license-Apache%202.0-blue.svg)](LICENSE)
[![Next.js](https://img.shields.io/badge/Next.js-14-black)](web/)
[![Claude](https://img.shields.io/badge/Powered%20by-Claude-orange)](https://claude.ai)

Production-ready Claude AI skill plugins for financial services workflows — investment banking, equity research, private equity, fund administration, and wealth management.

---

## What's inside

| Vertical | Key commands | Use case |
|---|---|---|
| **Financial Analysis** | `/dcf` `/lbo` `/comps` `/xlsx-author` | Core modeling — the foundation layer |
| **Investment Banking** | `/cim-builder` `/pitch-deck` `/buyer-list` | Deal workflow from mandate to close |
| **Equity Research** | `/earnings-analysis` `/morning-note` `/sector-overview` | Coverage lifecycle automation |
| **Private Equity** | `/deal-screening` `/ic-memo` `/returns-analysis` | Sourcing to IC memo |
| **Fund Administration** | `/nav-tieout` `/gl-recon` `/roll-forward` | Month-end close operations |
| **Wealth Management** | `/financial-plan` `/portfolio-rebalance` `/client-report` | Client relationship workflows |
| **Operations** | `/kyc-doc-parse` `/kyc-rules` | KYC onboarding automation |

Plus **10 end-to-end agents** (pitch-agent, earnings-reviewer, model-builder, kyc-screener, and more) and **11 MCP data connectors** (FactSet, Bloomberg/LSEG, PitchBook, Morningstar, S&P Global, and others).

---

## Quick start

### Install a vertical plugin

```bash
# Core financial analysis (install this first)
claude plugin install anthropic/financial-analysis

# Add any vertical
claude plugin install anthropic/investment-banking
claude plugin install anthropic/equity-research
claude plugin install anthropic/private-equity
claude plugin install anthropic/fund-admin
claude plugin install anthropic/wealth-management
claude plugin install anthropic/operations
```

### Use a skill

Once installed, skills are available as slash commands in Claude:

```
/dcf Apple Q2 2025 10-Q
/comps Build comps table for US mid-cap software
/morning-note Prepare morning note for NVDA ahead of earnings
/nav-tieout Tie out NAV for fund close 2025-03-31
```

### Run the showcase site locally

```bash
cd web
npm install
npm run dev
# → http://localhost:3000
```

---

## Repo structure

```
cn-finance/
├── skills/                        ← Claude skill collection
│   ├── plugins/
│   │   ├── vertical-plugins/      ← 7 installable FSI verticals
│   │   ├── agent-plugins/         ← 10 end-to-end workflow agents
│   │   └── partner-built/         ← LSEG, S&P Global integrations
│   ├── managed-agent-cookbooks/   ← Anthropic API deployment templates
│   └── scripts/                   ← Validation and deploy utilities
│
└── web/                           ← Next.js 14 showcase site (Vercel)
    ├── app/                       ← App Router pages
    ├── components/                ← UI + layout components
    └── content/verticals.ts       ← Skill metadata
```

---

## Deployment

The showcase site deploys automatically to Vercel on push to `main`.

```
Root directory: web
Framework:      Next.js
```

No environment variables required — entirely static, no API calls at runtime.

---

## Architecture

Skills follow a simple, portable format:

```
skills/[vertical]/
├── .claude-plugin/plugin.json    ← Plugin metadata and version
├── skills/[skill-name]/
│   └── SKILL.md                  ← System prompt + instructions (Markdown)
└── commands/                     ← Slash command definitions
```

Each `SKILL.md` is a self-contained markdown file with YAML frontmatter. No build step, no runtime dependencies. Skills can be deployed two ways:

1. **Claude for Work plugins** — install via marketplace or `claude plugin install`
2. **Managed Agents (API)** — deploy as API-callable agents via the Anthropic SDK

---

## Data connectors

The financial-analysis vertical ships with MCP connectors for:

| Provider | Data type |
|---|---|
| FactSet | Fundamentals, estimates, pricing |
| LSEG / Refinitiv | Market data, fixed income, FX |
| Morningstar | Fund data, ratings, ESG |
| S&P Global / Capital IQ | Company profiles, credit ratings |
| PitchBook | PE/VC deal and company data |
| Chronograph | Portfolio monitoring (LP/GP) |
| Daloopa | AI-structured earnings data |
| Aiera | Earnings call transcripts |
| MT Newswires | Real-time financial news |
| Egnyte | Document management |

---

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines on adding new skills, verticals, or improving the showcase site.

---

## License

Apache 2.0 — see [LICENSE](LICENSE).

The `skills/` directory is adapted from [anthropics/financial-services](https://github.com/anthropics/financial-services). CN Finance is an independent project and is not affiliated with or endorsed by Anthropic.

> **Disclaimer:** All skill outputs are draft work product for professional review. Nothing in this repository constitutes investment, legal, tax, or financial advice.
