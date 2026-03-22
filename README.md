# Contract Review — Agent Skill for Legal Analysis

> AI-powered contract review with CUAD risk detection, market benchmarks, negotiation playbooks, and reinforcement learning from outcomes

[![GitHub stars](https://img.shields.io/github/stars/mkmkkkkk/claude-legal-skill)](https://github.com/mkmkkkkk/claude-legal-skill/stargazers)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Agent Skills](https://img.shields.io/badge/Agent%20Skills-Compatible-blueviolet)](https://agentskills.io)
[![CUAD](https://img.shields.io/badge/CUAD-41%20Categories-green)](https://github.com/TheAtticusProject/cuad)
[![Version](https://img.shields.io/badge/version-4.0.0-blue)]()

**Works with:** Claude Code, OpenAI Codex, Cursor, GitHub Copilot, Gemini CLI, [26+ tools](https://agentskills.io)

## Quick Install

```bash
# Claude Code
git clone https://github.com/mkmkkkkk/claude-legal-skill ~/.claude/skills/contract-review

# OpenAI Codex
git clone https://github.com/mkmkkkkk/claude-legal-skill ~/.codex/skills/contract-review

# Other Agent Skills-compatible tools — clone to your tool's skills directory
```

## Try It

```
Review this NDA - I'm the receiving party
```

### Example Output

![Demo output showing contract review with red flags, risk analysis, and redline suggestions](examples/demo.png)

---

## What's New in v4.0.0 (Shapiro Method)

This fork adds the **Shapiro reinforcement methodology** — inspired by [Zack Shapiro's "10x Lawyer" approach](https://x.com/ZackShapiro) of encoding lawyer judgment into AI skills, then improving them through negotiation outcome feedback loops.

### New capabilities over upstream v3.0.0:

1. **6-Step Chained Workflow** — Pre-Review, Position, Risk Scan, Strategy, Deliverables, Outcome Capture
2. **Negotiation Playbook** — Anchor/Target/Walk-away positions for every flagged issue
3. **Concession Sequencing** — strategic trade maps (give low-value to get high-value)
4. **Counter-Redline Analysis** — categorizes opposing counsel changes into accepted/partial/rejected/new/sleeper
5. **Reinforcement Loop** — `.legal-review-journal.jsonl` captures outcomes to calibrate future reviews
6. **3 New Checklists** — Employment Agreement, Real Estate/Lease, Privacy/DPA (8 total)
7. **Framing Language** — business justifications for each redline, not legal jargon
8. **Counter-Move Prediction** — anticipates counterparty responses with prepared replies

---

## How It Works

### The 6-Step Pipeline

```
Step 1: Pre-Review    -> Document completeness (blank fields, missing exhibits)
Step 2: Position      -> Parties, user role, power dynamics
Step 3: Risk Scan     -> CUAD 41 categories + red flags + market benchmarks
Step 4: Strategy      -> Negotiation playbook (anchors, concessions, framing)
Step 5: Deliverables  -> Redline language, memo, or counter-analysis
Step 6: Outcome       -> Capture results -> .legal-review-journal.jsonl
```

### Position-Aware Review
Tell it which party you are (customer, vendor, buyer, seller, receiving party) — the skill adjusts what it flags as risky and calibrates the negotiation strategy to your leverage.

### Reinforcement Loop (New in v4.0.0)
After each negotiation, capture what was accepted and rejected. The skill reads `.legal-review-journal.jsonl` before future reviews and adjusts:
- Benchmarks based on actual outcomes
- Negotiability ratings from real counterparty behavior
- Redline language that has been proven to work

### Counter-Redline Analysis (New in v4.0.0)
When opposing counsel sends back a markup, the skill categorizes every change:
- **Accepted** — they took your redline
- **Partially accepted** — moved toward you but not fully
- **Rejected** — restored original language
- **New issues** — terms not in the original
- **Sleeper changes** — small wording tweaks that materially change meaning (most dangerous)

---

## Features

### Document Type Checklists (8 types)
- **NDA** — confidentiality term, non-solicitation, standstill, destruction certification
- **SaaS/MSA** — SLA, data export, suspension rights, price caps
- **Payment/Merchant** — reserves, chargebacks, network rules, auto-debit
- **M&A** — earnouts, escrow, rep survival, sandbagging
- **Finder/Broker** — fee tails, covered buyer definitions, joint representation
- **Employment** (new) — non-competes, IP assignment, severance, clawback
- **Real Estate/Lease** (new) — CAM charges, personal guarantees, exclusivity
- **Privacy/DPA** (new) — sub-processor flow-down, breach notification, cross-border transfers

### Market Standard Benchmarks

| Provision | Standard | Yellow | Red |
|-----------|----------|--------|-----|
| Liability cap | 12 months | 6-11 mo | <6 mo |
| Auto-renewal notice | 90+ days | 60-89 | <60 |
| Non-compete | 1-2 years | 3-4 years | 5+ |
| Rep survival (M&A) | 12-18 mo | 24-30 mo | 36+ mo |
| SLA uptime | 99.9% | 99.5% | None |
| Price increase cap | CPI/5% | 10% | Uncapped |
| Data export | 90 days | 30 days | None |

### Red Flags Quick Scan
Instant detection of 12 danger signs including liability cap gaps, uncapped indemnification, unilateral amendment rights, perpetual obligations, offshore jurisdiction, asymmetric assignment, and sleeper language.

### Jurisdiction Awareness
- Non-competes: void in CA/ND/OK/MN, restricted in CO/WA/OR, enforceable with conditions in IL/MA
- Venue implications: Delaware (corp-friendly), NY (financial), CA (employee-friendly)
- International arbitration: AAA/JAMS, SIAC, LCIA, ICC

---

## Usage Examples

```
Review this NDA for red flags - I'm the receiving party

Analyze the indemnification in this MSA - I'm the vendor

What are the termination provisions? I'm the customer.

Review this acquisition agreement - I'm the seller

They sent back their markup of our SaaS agreement - analyze the counter-redline

We signed the deal - here's what they accepted [outcome capture]
```

See [examples/](examples/) for full sample outputs.

---

## Generate Deliverables

This skill outputs structured JSON redlines. For tracked-changes Word docs, pair with [**legal-redline-tools**](https://github.com/evolsb/legal-redline-tools):

```bash
pip install git+https://github.com/evolsb/legal-redline-tools.git

legal-redline apply contract.docx redlined.docx \
    --from-json redlines.json \
    --pdf redline.pdf \
    --memo-pdf internal-memo.pdf
```

---

## Limitations

- **Not legal advice** — always have material terms reviewed by qualified counsel
- **US law focus** — analysis defaults to US; provisions vary by jurisdiction
- **Context window** — very long contracts may need section-by-section review
- **Journal is local** — reinforcement loop data stays in project directory

## Accuracy

Based on ContractEval benchmarks, Claude achieves F1 ~0.62 on clause extraction. Best for first-pass review and issue flagging — not a replacement for attorney review on material deals.

---

## Credits

- [CUAD Dataset](https://github.com/TheAtticusProject/cuad) — Atticus Project (NeurIPS 2021)
- [LegalBench](https://hazyresearch.stanford.edu/legalbench/) — Stanford HAI
- [ContractEval](https://arxiv.org/abs/2303.07389) — Contract understanding benchmarks
- [Zack Shapiro's 10x Lawyer methodology](https://x.com/ZackShapiro) — Reinforcement loop and chained workflow concepts
- Forked from [evolsb/claude-legal-skill](https://github.com/evolsb/claude-legal-skill) (v3.0.0)

## License

MIT — see [LICENSE](LICENSE)
