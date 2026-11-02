# Repository, file formats and report layout

## Repository layout (default `fleet-intel/`)

```
fleet-intel/
  STATUS.md                 version, cut-off, stage progress, limitations, last quarterly review
  methodology.md            scoring, taxonomy and definitions, versioned
  market-baseline.md        market overview and strategic baseline, dated
  competitors.md            universe, classes, primary group, watchlist, last review date
  profiles/<name>.md        one per priority competitor, plus mcf.md
  capability-matrix.md      the positioning dashboard (deliverable 3)
  radar.md                  the AI and innovation radar (deliverable 4)
  action-register.md        the strategic action register (deliverable 5)
  evidence-register.csv     every source
  change-log.csv            every logged development, all months
  reports/
    MCF_Competitive_Intelligence_YYYY-MM.md
```

If a file does not exist yet, create it. Never overwrite an earlier report. Never delete history: revise with a dated note.

## STATUS.md

- Repository version (baseline is 1.0; a monthly update raises the minor number)
- Methodology version
- Last research cut-off date and the period the last report covers
- Stage progress during a baseline (stage, done or not, date)
- Last quarterly universe review
- Known limitations and unresolved questions
- Scheduling: not set up, or what was set up, when and what kind

## evidence-register.csv

`id, claim_summary, source_url, publisher, source_type, publication_date, event_or_availability_date, accessed_date, corroborated_by, confidence, notes`

- `source_type`: primary or secondary, and the kind (product page, release notes, filing, trade media, review, webinar, job posting)
- IDs look like `E-0001` and never change.

## change-log.csv

`id, report_month, competitor, development, event_date, evidence_ids, novelty, customer_problem, total_score, band, confidence, recommended_action, status, links_to_earlier_id`

- `novelty`: new, expansion, or previously existing
- IDs look like `C-2026-11-01`.
- Check this file before adding anything, so nothing is counted twice.

## Competitor profile (`profiles/<name>.md`)

Dated heading and last-checked date, then:
- Core proposition and target customers
- Primary geographies and fleet segments
- Platform capabilities (by taxonomy domain)
- Positioning and differentiation
- AI and advanced analytics, with the evidence ladder label
- Partnerships and integrations
- Publicly disclosed pricing or commercial model (or "not disclosed")
- Recent launches and strategic announcements
- Strengths, limitations, and evidence gaps
- Sources (evidence IDs)

Profile for MCF (`profiles/mcf.md`) adds: public positioning and value proposition, portfolio, communications, and evidence of differentiation. Use *not publicly verified* for anything with no public evidence.

## Source types for monthly research

Official sites and product pages, release notes and documentation, newsrooms and investor material, regulatory and industry publications, reputable trade and technology media, public case studies and reviews, public webinars, conference talks and demos, and public job postings (directional only).

## Capability matrix (`capability-matrix.md`)

One table per taxonomy domain. Rows are capabilities, columns are MCF and each primary competitor. Each cell: status, evidence ID, source date, confidence. A separate block holds relative position per domain. Keep a "Moved this month" list at the top.

## Action register (`action-register.md`)

| ID | Action | Class | Rationale | Priority | Accountable function | Horizon | Evidence and confidence | Status | Reassess when |
|---|---|---|---|---|---|---|---|---|---|

Status: open, in progress, done, closed (no longer needed), revised. Carry open items forward. When you close or revise one, write why and cite the new evidence.

## Radar (`radar.md`)

| Capability | Level | Evidence for the level | Vendors | What would move it |
|---|---|---|---|---|

Levels: Emerging, Experimenting, Scaling, Mainstream.

## Monthly report layout

File: `reports/MCF_Competitive_Intelligence_YYYY-MM.md`, where YYYY-MM is the month covered.

```
# MCF Competitive Intelligence: <Month YYYY>

**Period covered:** <dates> · **Research cut-off:** <date> · **Baseline version:** <n> · **Methodology:** <n>
**Comparison:** <month-on-month verified | partial | not available, and why>

## 1. Executive intelligence brief
- Five most significant developments (one or two lines each, with score)
- What materially changed this month
- Implications for MCF
- Three highest-priority recommendations
- Key uncertainties and watchpoints

## 2. Competitive change log
| Competitor | Development | Event date | Evidence | Strategic impact | Confidence | Recommended action |
|---|---|---|---|---|---|---|

## 3. What moved
- Positioning dashboard: changes in capability, position or evidence status
- Radar: changes in level
- Action register: opened, closed and revised

## 4. AI competitive intelligence
Evidence-ladder labels, progression per competitor, implications for MCF's AI Assistant and MyCF.

## 5. Scored developments
Ranked table with the five dimension scores, one-line reasons, total, band and confidence.

## 6. Research coverage and limitations
What was searched, what could not be reached, what conflicts or is out of date, and what was not covered.

## 7. Revisions
Any change to earlier assessments and why. Any methodology change.
```

Tag claims as [F], [I], [H] or [R] throughout. Cite evidence IDs with links.
