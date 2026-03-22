# Changelog

## [4.0.0] - 2026-03-22

### Added (Shapiro Method Enhancement)
- **6-step chained workflow pipeline**: Pre-Review, Position, Risk Scan, Strategy, Deliverables, Outcome Capture
- **Negotiation Strategy (Step 4)**: Anchor/Target/Walk-away framework for every flagged issue
- **Concession Sequencing**: Strategic trade maps — give low-value to get high-value
- **Framing Language**: Business justifications for redlines (not legal jargon)
- **Counter-Move Prediction**: Anticipates counterparty responses with prepared replies
- **Counter-Redline Analysis**: Categorizes opposing counsel changes into accepted/partial/rejected/new/sleeper
- **Sleeper change detection**: Flags small wording tweaks that materially change meaning
- **Outcome Capture (Step 6)**: `.legal-review-journal.jsonl` reinforcement loop
- **Reinforcement learning from outcomes**: Journal data calibrates future benchmarks and negotiability ratings
- **Employment Agreement checklist**: Non-competes, IP assignment, severance, clawback, moonlighting
- **Real Estate/Lease checklist**: CAM charges, personal guarantees, exclusivity, tenant improvements
- **Privacy/DPA checklist**: Sub-processor flow-down, breach notification, cross-border transfers, DPIA
- Expanded jurisdiction notes (CO, WA, OR, IL, MA non-compete restrictions; TX venue; ICC arbitration)
- Pre-Review completeness check (blank fields, missing exhibits, version indicators)
- Power dynamic assessment (deal size, alternatives, regulated terms)
- 5 new red flag checks (as-is warranty, asymmetric assignment, sole discretion, class action waiver, pre-signed conflict waivers)
- 5 new market benchmarks (SLA uptime, data export, price increase cap, cure period, confidentiality duration)

### Changed
- Complete rewrite of skill.md from v3.0.0 to incorporate Shapiro reinforcement methodology
- Output format now includes Negotiation Playbook section with priority stack and concession map
- Risk analysis now includes negotiation strategy per issue (anchor/target/walk-away/frame)
- README updated with v4.0.0 features, new install URL, and methodology credits

## [3.0.0] - 2026-01-26

### Added
- "Why This Exists" backstory section in README
- Multi-platform support via [Agent Skills standard](https://agentskills.io) (26+ tools)
- Full example outputs for NDA, SaaS, M&A, and balanced agreements
- Optimized skill description for Claude Code discovery

### Changed
- Complete rewrite of skill.md based on real-world contract testing
- Position-aware analysis now adjusts for power dynamics
- Market benchmark thresholds refined from actual negotiation outcomes
- Redline suggestions include fallback positions

## [2.1.0] - 2026-01-26

### Added
- Markdown output format with severity badges
- shields.io badges and GitHub topics for discoverability
- Link to examples folder in README

## [2.0.0] - 2026-01-26

### Added
- Position-aware review (customer/vendor/buyer/seller)
- Complete CUAD 41-category coverage
- Document-type checklists (NDA, SaaS, M&A, Payment, Finder/Broker)
- Market standard benchmarks with color-coded thresholds
- Negotiability ratings (High/Medium/Low)
- Red flags quick scan
- Jurisdiction awareness
- M&A-specific support (earnouts, escrow, rep survival)

### Changed
- Improved redline language with specific replacement text
- Better severity classification (Critical/Important/Acceptable)

## [1.0.0] - 2026-01-26

### Added
- Initial release
- Basic contract review with risk detection
- Key terms extraction
- CUAD dataset integration
