---
name: contract-review
description: Review legal contracts, NDAs, employment agreements, SaaS terms, and M&A documents. Identifies unfavorable terms, suggests redlines, and compares to market standards. Use for contract analysis, due diligence, negotiation prep, counter-redline analysis, or outcome tracking. Supports chained workflows — review → redline → memo → counter-analysis → outcome capture.
version: 4.0.0
---

# Contract Review Skill

Review legal contracts for risks, extract key terms, and suggest redlines. Built on the CUAD dataset (41 risk categories), ContractEval benchmarks, LegalBench, and the **Shapiro reinforcement methodology** — a feedback loop that learns from negotiation outcomes to improve future judgment.

## When to Activate

- User mentions "review contract", "analyze agreement", "check this contract"
- User uploads or references a PDF/DOCX legal document
- User asks about specific clauses, risks, or terms
- User says "counter-redline", "they sent back changes", "opposing counsel responded"
- User says "we signed", "deal closed", "they accepted", "they rejected" (outcome capture)

---

## Workflow Pipeline

This skill operates as a **chained workflow**. Each step builds on the previous:

```
Step 1: Pre-Review    → Document completeness check
Step 2: Position      → Identify parties, user position, power dynamics
Step 3: Risk Scan     → CUAD 41 + Red flags + Benchmarks
Step 4: Strategy      → Negotiation playbook with anchors & concessions
Step 5: Deliverables  → Redline language, memo, or counter-analysis
Step 6: Outcome       → Capture what was accepted/rejected → journal
```

The user may invoke any step directly. Default: run Steps 1-5 sequentially.

---

## Step 1: Pre-Review Checklist

Before analyzing content, verify document completeness:

- [ ] **Blank fields**: Flag any "$X", "TBD", "[amount]", "____" placeholders
- [ ] **Missing exhibits**: List all referenced schedules/exhibits and note which are missing
- [ ] **Signature status**: Draft or already executed?
- [ ] **All pages present**: Check for truncation or missing sections
- [ ] **Version indicators**: Is this a redline? A counter-draft? Which iteration?

If blank fields or missing exhibits exist, flag prominently in output header.

---

## Step 2: Identify Document Type & User Position

**Ask if unclear:** "Which party are you? (customer, vendor, buyer, seller, licensor, licensee, receiving party, disclosing party)"

This affects what's "risky":
- Customer reviewing vendor agreement → flag vendor-favorable terms
- Vendor reviewing own template → flag customer-favorable terms
- Buyer in M&A → flag seller-favorable terms
- Seller in M&A → flag buyer-favorable terms
- Receiving party in NDA → flag disclosing party-favorable terms

**Assess power dynamic:**
- Startup vs. large enterprise? (limited negotiating leverage)
- Standard form vs. negotiated? (some terms non-negotiable)
- Regulated industry? (some terms legally required)
- Deal size relative to counterparty? (leverage indicator)
- Alternative options? (competitive bids = leverage)

---

## Step 3: Risk Analysis (CUAD 41 + Extensions)

### Red Flags Quick Scan

Check these danger signs FIRST before deep analysis:

| Red Flag | Why It Matters |
|----------|----------------|
| Liability cap < 6 months | Inadequate protection |
| Uncapped indemnification | Unlimited exposure |
| "As-is" with no warranty | No recourse for defects |
| Unilateral suspension without notice | Service can vanish |
| Unilateral amendment rights | Terms can change |
| No termination for convenience | Locked in |
| Perpetual obligations (tails, non-competes) | Indefinite exposure |
| Offshore jurisdiction (BVI, Cayman) | Expensive to enforce |
| Pre-signed conflict waivers | No recourse for conflicts |
| "Sole discretion" language favoring counterparty | No objective standard |
| Class action waiver + mandatory arbitration | Limited remedies |
| Asymmetric assignment rights | They can assign, you can't |

### Risk Categories (CUAD 41 + Extensions)

#### Document Basics
- Document Name and Type
- Parties (legal names, roles)
- Agreement Date / Effective Date
- Expiration Date
- Renewal Terms
- **Document Status** (draft/executed)
- **Blank Fields / Placeholders**

#### Term & Termination
- Contract Term / Duration
- Termination for Convenience
- Termination for Cause
- Post-Termination Services
- Survival Clauses
- **Suspension Rights** (immediate vs. with notice)
- **Cure Periods**

#### Assignment & Control
- Anti-Assignment Clause
- Change of Control
- Consent Requirements
- **Asymmetric Assignment** (they can, you can't)

#### Financial Terms
- Payment Terms
- Price Restrictions / Adjustments
- Most Favored Nation (MFN)
- Minimum Commitment
- Volume Restrictions
- Audit Rights
- **Price Escalation Caps**
- **Reserve/Holdback Requirements**
- **Auto-Debit Authority**

#### Liability & Risk
- Limitation of Liability
- Cap on Liability
- Uncapped Liability Carve-outs
- Indemnification
- Insurance Requirements
- Warranty Duration
- **Warranty Disclaimer (As-Is)**
- **Exclusive Remedy Clauses**
- **Chargeback/Return Liability**

#### IP & Confidentiality
- IP Ownership Assignment
- License Grant
- Affiliate License - Licensor/Licensee
- Covenant Not To Sue
- Non-Compete
- Non-Solicitation (Employees/Customers)
- Competitive Restriction Exception
- Exclusivity
- Non-Disparagement
- Confidentiality Duration
- Third Party Beneficiary
- **Residuals Clause**
- **Feedback Ownership**

#### Dispute Resolution
- Governing Law
- Jurisdiction / Venue
- Arbitration vs Litigation
- Jury Trial Waiver
- **Class Action Waiver**
- **Offshore Jurisdiction Flags**

#### Special Provisions
- ROFR / ROFO / ROFN
- Revenue/Profit Sharing
- Joint IP Ownership
- Source Code Escrow
- Irrevocable or Perpetual License
- **Data Export Rights**
- **Uptime/Availability SLA**
- **Sublicensing Rights**
- **Unilateral Amendment Rights**

### Market Standard Benchmarks

| Provision | Standard | Yellow Flag | Red Flag |
|-----------|----------|-------------|----------|
| **Liability cap** | 12 months' fees | 6-11 months | <6 months |
| **Non-compete duration** | 1-2 years | 3-4 years | 5+ years |
| **Non-compete geography** | Where business operates | State-wide | Nationwide |
| **Auto-renewal notice** | 90+ days | 60-89 days | <60 days |
| **Termination notice** | Mutual, 60-90 days | One-sided, 30 days | Immediate |
| **Indemnification** | Mutual, capped | Asymmetric | Uncapped |
| **Rep survival (M&A)** | 12-18 months general | 24-30 months | 36+ months |
| **Escrow (M&A)** | 10-15% for 12-18 mo | 15-20% for 18-24 mo | >20% or >24 mo |
| **Confidentiality (NDA)** | 3 years general | 2 years | 5+ years |
| **Fee tail (broker)** | 12-18 months | 24 months | Perpetual |
| **SLA uptime** | 99.9% with credits | 99.5% | No SLA |
| **Data export** | 90 days, standard format | 30 days | None |
| **Price increase cap** | CPI or 5% annual | 10% annual | Uncapped |
| **Cure period** | 30 days | 15 days | None |

---

## Step 4: Negotiation Strategy (Shapiro Method)

This is the core Shapiro enhancement. Don't just identify issues — **build a negotiation playbook**.

### 4a. Anchor & Target Framework

For each flagged issue, define three positions:

| Position | Definition | Purpose |
|----------|-----------|---------|
| **Anchor** | Best-case ask (aggressive but defensible) | Sets the negotiation ceiling |
| **Target** | Realistic outcome given power dynamics | What you actually expect to get |
| **Walk-away** | Minimum acceptable term | Below this, escalate or walk |

**Example:**
```
Issue: Liability cap at 3 months
  Anchor:    24 months' fees (aggressive but standard in enterprise)
  Target:    12 months' fees (market standard)
  Walk-away: 6 months' fees (minimum acceptable)
```

### 4b. Concession Sequencing

Rank issues by importance AND negotiability. Build a concession map:

```
GIVE on:                          TO GET:
- Governing law (low impact)  →   Liability cap increase
- Shorter cure period         →   Mutual termination rights
- Accept their arbitration    →   Data export rights added
```

**Rules:**
- Never concede Critical issues for Important ones
- Give on form (jurisdiction, notice methods) to get on substance (caps, rights)
- Concede early on low-value items to build goodwill for hard asks
- Save your biggest concession for their biggest — don't spend it early

### 4c. Framing Language

For each redline, provide the **business justification** — not legal jargon:

| Don't say | Say instead |
|-----------|-------------|
| "This clause is unconscionable" | "Our risk team requires liability coverage proportional to contract value" |
| "This is below market" | "In our last 3 vendor agreements, we've had 12-month caps — consistency matters for our compliance team" |
| "Delete this section" | "We'd propose mutual language here — happy to extend the same right to you" |
| "This is a red flag" | "We want to make sure this works for both sides long-term" |

### 4d. Counter-Move Prediction

For each redline you propose, predict the counterparty's likely response and prepare your reply:

```
Your redline:     Liability cap → 12 months
Their likely response: "We can do 6 months"
Your prepared reply:   "We can accept 6 months if you add
                        uncapped liability for data breach
                        and willful misconduct"
```

---

## Step 5: Output & Deliverables

### Default Output Format

Use **markdown** for readable, scannable output:

```markdown
# Contract Review: [Document Name]

**Document Type:** SaaS Subscription Agreement
**Your Position:** Customer
**Counterparty:** Acme Software Inc.
**Risk Level:** [RED/YELLOW/GREEN] [High/Medium/Low]
**Document Status:** Draft / Executed on [date]

## Pre-Signing Alerts

- **Blank field:** Fee amount in Section 4.1 is "$____"
- **Missing exhibit:** Exhibit B (SLA) referenced but not attached

## Executive Summary

[2-3 sentences: overall assessment, biggest risks, deal-breaker potential]

---

## Key Terms

| Term | Value | Location |
|------|-------|----------|
| Initial Term | 12 months | Section 8.1 |
| Auto-Renewal | 12-month periods, 60-day notice | Section 8.2 |
| Liability Cap | 3 months' fees | Section 10.2 |
| Governing Law | Delaware | Section 12.1 |

---

## Red Flags (Quick Scan)

| Flag | Found | Location |
|------|-------|----------|
| Liability cap < 6 months | Yes | Section 10.2 |
| Uncapped indemnification | No | — |

---

## Risk Analysis

### CRITICAL

**Limitation of Liability** (Section 10.2)
> "Liability shall not exceed fees paid in the preceding three (3) months"

- **Issue:** 3-month cap is below market standard (typically 12 months)
- **Risk:** For $120K annual contract, liability capped at $30K
- **Market Standard:** 12 months' fees
- **Negotiability:** Medium
- **Redline:** Change "three (3) months" to "twelve (12) months"
- **Fallback:** Accept 6 months as compromise

**Negotiation Strategy:**
- Anchor: 24 months
- Target: 12 months
- Walk-away: 6 months
- Frame: "Our procurement policy requires liability proportional to annual spend"
- If they counter with 6 months: Accept if they add uncapped carve-outs for data breach and willful misconduct

---

### IMPORTANT

[...]

### Reviewed & Acceptable

| Category | Status | Notes |
|----------|--------|-------|
| Data Ownership | OK | Customer owns all customer data |
| IP Rights | OK | Clear separation |

---

## Missing Provisions

| Provision | Priority | Suggested Language |
|-----------|----------|--------------------|
| Data Export | Critical | "Upon termination, Vendor shall..." |

---

## Internal Consistency Issues

- Section 5.2 references "Exhibit C" but no Exhibit C exists

---

## Negotiation Playbook

### Priority Stack (negotiate in this order)

| # | Issue | Anchor | Target | Walk-away | Negotiability |
|---|-------|--------|--------|-----------|---------------|
| 1 | Liability cap | 24 mo | 12 mo | 6 mo | Medium |
| 2 | Termination | Mutual 30d | Mutual 60d | Mutual 90d | High |
| 3 | Data export | 180 days | 90 days | 30 days | High |

### Concession Map

| Give on | To get |
|---------|--------|
| Accept Delaware law | Liability cap increase |
| Shorter cure (30→15 days) | Mutual termination |

---

*This review is for informational purposes only. Material terms should be reviewed by qualified legal counsel.*
```

---

## Step 6: Outcome Capture (Reinforcement Loop)

After negotiation concludes, capture the result. This is the Shapiro reinforcement methodology — encoding negotiation outcomes to improve future judgment.

### When to Capture

Trigger when user says:
- "They accepted our redlines"
- "We signed the deal"
- "They rejected [specific term]"
- "Here's what they agreed to"
- "Negotiation is done"

### What to Capture

Save to `.legal-review-journal.jsonl` in the project directory:

```json
{
  "date": "2026-03-22",
  "document_type": "SaaS Agreement",
  "counterparty_type": "Enterprise vendor",
  "user_position": "Customer",
  "power_dynamic": "Startup vs. large vendor",
  "deal_value": "$120K/year",
  "issues": [
    {
      "category": "liability_cap",
      "original": "3 months",
      "our_ask": "12 months",
      "outcome": "6 months + uncapped for data breach",
      "accepted": true,
      "notes": "They countered at 4 months, we pushed to 6 with carve-outs"
    },
    {
      "category": "termination",
      "original": "Vendor only, 30 days",
      "our_ask": "Mutual, 60 days",
      "outcome": "Mutual, 90 days",
      "accepted": true,
      "notes": "Easy win — they agreed immediately"
    }
  ],
  "lessons": "Enterprise SaaS vendors will move on liability cap if you offer carve-outs as alternative to higher cap"
}
```

### How to Use the Journal

Before each new review, check if `.legal-review-journal.jsonl` exists. If it does:

1. **Load historical outcomes** for the same document type and counterparty type
2. **Adjust benchmarks** — if past negotiations show vendors in this category accept 6-month caps but not 12, set Target = 6 months instead of 12
3. **Surface patterns** — "In your last 3 SaaS reviews, liability cap was the #1 issue. Vendors accepted 6-month caps 2/3 times."
4. **Recommend proven language** — prefer redline language that was accepted in past negotiations over generic templates

**The journal is append-only. Never delete or modify past entries.**

---

## Counter-Redline Analysis

When the user receives a counter-draft or markup from opposing counsel:

### Trigger
- "They sent back their version"
- "Here's the counter-redline"
- "Opposing counsel marked up our draft"

### Process

1. **Diff analysis** — Compare original vs. counter to identify every change
2. **Categorize changes:**
   - **Accepted**: They took your redline as-is
   - **Partially accepted**: They moved toward you but not fully
   - **Rejected**: They restored original language
   - **New issues**: They added terms not in the original
   - **Sleeper changes**: Small wording tweaks that materially change meaning

3. **Assess each change:**

```markdown
## Counter-Redline Analysis

### Accepted (No Action Needed)
| Our Ask | Their Response | Section |
|---------|----------------|---------|
| Mutual termination | Accepted as-is | 8.5 |

### Partially Accepted (Evaluate)
| Our Ask | Their Counter | Gap | Recommendation |
|---------|---------------|-----|----------------|
| 12-month liability cap | 6 months | 6 months | Accept if they add data breach carve-out |

### Rejected (Re-Negotiate or Concede)
| Our Ask | Their Position | Impact | Strategy |
|---------|----------------|--------|----------|
| Price cap at 5% | Uncapped | High | Offer CPI + 3% as compromise |

### NEW ISSUES (Review Carefully)
| Change | Section | Impact | Hidden Risk? |
|--------|---------|--------|--------------|
| Added audit rights for vendor | 11.3 | Medium | Scope too broad — limit to financial records |

### SLEEPER CHANGES (Most Dangerous)
| Original | Changed To | Section | Impact |
|----------|-----------|---------|--------|
| "material breach" | "any breach" | 7.2 | Lowers termination threshold dramatically |
```

4. **Updated negotiation strategy** — Adjust priorities based on what they revealed matters to them

---

## Document Type Checklists

### NDA Checklist

| Category | Check For |
|----------|-----------|
| Direction | One-way or mutual? |
| Definition scope | "All information" too broad? Standard exceptions? |
| Term | 2 years short, 3-5 typical, indefinite for trade secrets |
| Permitted disclosure | "Representatives" defined? Flow-down required? |
| Residuals clause | Can use general knowledge retained in memory? |
| Non-solicitation | Employees protected? |
| Standstill | Prevents hostile acquisition actions? |
| No-contact | Customers, suppliers, employees protected? |
| Return/destruction | Certification required? |
| Public announcement | Prohibits disclosure of discussions? |
| Compelled disclosure | Notice required? Time to seek protective order? |
| Injunctive relief | Pre-agreed specific performance? Bond waiver? |

### SaaS/MSA Checklist

| Category | Check For |
|----------|-----------|
| Liability cap | 12+ months = standard |
| Uptime SLA | 99.9% with credits = standard |
| Suspension rights | Unilateral? Notice required? |
| Data ownership | Customer owns customer data? |
| Data export | Format, duration, cost on termination? |
| Price increases | Capped? Notice period? |
| Auto-renewal notice | 90+ days = good, <60 = risk |
| Termination | Mutual for convenience? Cure period for cause? |
| Subprocessors | Notice of changes? Approval rights? |
| Insurance | Vendor carries E&O, cyber? |

### Payment/Merchant Agreement Checklist

| Category | Check For |
|----------|-----------|
| Reserve/holdback | Amount, duration, release conditions? |
| Chargeback liability | Capped? Fraud protection? |
| Network rules | Incorporated by reference? Access provided? |
| Auto-debit authority | Notice before debits? |
| Settlement timing | When do you receive funds? |
| Volume commitments | Realistic? Penalty for shortfall? |
| Suspension rights | Immediate or notice? |
| Termination tail | How long do obligations survive? |
| Audit rights | Frequency, notice, cost allocation? |
| PCI compliance | Who bears cost? |

### M&A Agreement Checklist

| Category | Check For |
|----------|-----------|
| Purchase price | Cash vs. stock vs. earnout mix? |
| Earnout mechanics | Measurement, discretion, audit rights, acceleration? |
| Escrow/holdback | Amount (10-15% typical), duration (12-18 mo), release? |
| Rep survival | 12-24 months general, longer for fundamental |
| Indemnification cap | 10-20% of purchase price typical |
| Basket type | True deductible vs. tipping? |
| Sandbagging | Pro-buyer or anti-sandbagging? |
| Non-compete | 2-3 years, geographic scope? |
| Working capital | Target, collar, true-up mechanism? |
| MAC definition | Carve-outs for market conditions? |
| Employment comp | Counted in purchase price or separate? |

### Finder/Broker Agreement Checklist

| Category | Check For |
|----------|-----------|
| Fee percentage | Specified or blank? |
| Fee calculation | What's included in deal value? Employment comp? |
| "Covered buyer" definition | How broad? Any prior relationship carve-out? |
| Tail period | 12-24 months typical; perpetual = red flag |
| Exclusivity | Exclusive or non-exclusive? |
| Minimum fee | Floor amount? |
| Joint representation | Consent required? Conflict waiver? |
| Escrow deduction | Auto-pay from proceeds? |
| Term/termination | Can you exit? |
| Broker status | BD registered if securities involved? |

### Employment Agreement Checklist

| Category | Check For |
|----------|-----------|
| At-will vs. term | Fixed term with cause-only termination? |
| Non-compete | Duration, geography, scope — enforceable in this state? |
| Non-solicitation | Customers and/or employees? Duration? |
| IP assignment | Present and future? "Related to" scope? |
| Prior inventions | Excluded list attached? |
| Severance | Triggered by termination without cause? Change of control? |
| Clawback | Bonus/equity subject to repayment? |
| Garden leave | Paid or unpaid during restriction period? |
| Moonlighting | Permitted with notice? Blanket prohibition? |
| Arbitration | Mandatory? Class waiver? |

### Real Estate/Lease Checklist

| Category | Check For |
|----------|-----------|
| Base rent + escalation | CPI, fixed %, or market reset? |
| CAM charges | Capped? Audit rights? |
| Personal guarantee | Required? Limited or unlimited? |
| Assignment/sublease | Consent standard (reasonable vs. sole discretion)? |
| Exclusivity | Use restrictions? Radius restriction? |
| Renewal options | Terms specified or "market rate"? |
| Tenant improvements | Allowance? Ownership at termination? |
| Force majeure | Pandemic, government orders included? |
| Early termination | Kick-out clause? Penalty? |
| Subordination/NDA | Lender can terminate on foreclosure? |

### Privacy/DPA Checklist

| Category | Check For |
|----------|-----------|
| Data processing role | Controller vs. processor vs. joint controller? |
| Sub-processor flow-down | Notice? Approval rights? Liability? |
| Data breach notification | 24/48/72 hours? Who notifies data subjects? |
| Cross-border transfers | SCCs? Adequacy decision? Binding corporate rules? |
| Data subject requests | Response time? Cost allocation? |
| Audit rights | On-site? Third-party? Frequency limits? |
| Data retention | Deletion timeline? Certification? |
| Security standards | SOC 2? ISO 27001? Specific technical measures? |
| Liability allocation | Fines, regulatory costs, individual claims? |
| DPIA required? | High-risk processing triggers assessment |

---

## Negotiability Guide

| Rating | Meaning | Examples |
|--------|---------|----------|
| **High** | Usually accepted | Mutual termination, cure periods, data export |
| **Medium** | Depends on leverage | Liability cap increase, price caps |
| **Low** | Rarely changed | Network rules (payments), regulatory requirements |
| **None** | Non-negotiable | Card network mandates, banking regulations |

**Power dynamic factors:**
- Large customer + small vendor = more leverage
- Startup + enterprise vendor = less leverage
- Competitive market = more leverage
- Sole-source vendor = less leverage
- Regulated terms = no leverage (legally required)

---

## Jurisdiction Notes

**Non-Competes:**
- California, North Dakota, Oklahoma, Minnesota: Generally void
- Colorado, Washington, Oregon: Restricted (income thresholds)
- Illinois, Massachusetts: Enforceable with garden leave/consideration
- Other states: Reasonableness test applies

**Choice of Law:**
- Delaware: Corp-friendly, predictable
- New York: Financial agreements, sophisticated courts
- California: Employee-friendly, tech industry
- Texas: Business-friendly, growing tech presence
- BVI/Cayman: Offshore, expensive to litigate, potential red flag

**Arbitration Venues:**
- AAA, JAMS: Standard US commercial
- SIAC (Singapore), LCIA (London): International, expensive
- ICC (Paris): International, well-established
- Mandatory + class waiver: Limits remedies significantly

---

## Guardrails

- **Not legal advice**: Recommend attorney review for material terms
- **Not tax advice**: Flag but don't opine
- **Jurisdiction matters**: Note when enforceability varies
- **Express uncertainty**: Say when interpretation is unclear
- **No hallucination**: Only reference text actually in the document
- **Show what's acceptable**: Always include "Reviewed & Acceptable" section
- **Document status matters**: Note if already executed (review is informational)
- **Journal is private**: Never share journal contents with counterparties or in external output
- **Anchors are not advice**: Negotiation strategy is tactical guidance, not legal recommendation
