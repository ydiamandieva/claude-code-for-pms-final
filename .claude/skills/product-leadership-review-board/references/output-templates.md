# Output templates

Scale to the mode (Quick, Deep, Executive Challenge). Start every output with this line:

> **Review board:** <mode> · **Reviewers:** Head of Product, Lead Engineer, Head of Architecture and Head of Design are simulated perspectives, not real stakeholders; nothing here is stakeholder approval. · **Approach:** <separate passes in one session, which share a model and context, so their agreement is weaker evidence | separate agents with models: ...>

## Finding format (Stage 1)

```
**P1 · High · Confidence: Medium**
Where: <section, claim, number, assumption or omission in the artifact>
Basis: <fact in the artifact | interpretation | risk | recommendation>
Issue: <one sentence>
Evidence or reasoning: <why this is a weakness>
If unresolved: <consequence>
Recommendation: <the specific change>
```

Severity: Critical (the artifact's conclusion or safety is at stake), High (material flaw), Medium (real but contained), Low (minor, or a preference, labelled as such).

## A. Executive review summary

```
## Executive review summary: <artifact name>

**Readiness:** <one or two sentences on overall quality for its intended use>
**Most consequential weaknesses**
1. <weakness> (<finding IDs>)
... (three to five)
**Major cross-functional risks:** <the ones that cut across disciplines>
**Recommended improvements:** <the Must and Should items in one line each>
**Outstanding decisions:** <what a human must decide, with the suggested owner role>
**What is strong and should be kept:** <one or two lines>
```

## B. Stakeholder feedback matrix

```
| Reviewer | ID | Finding | Severity | Recommendation | Confidence |
|---|---|---|---|---|---|
| Head of Product | P1 | ... | High | ... | Medium |
| Lead Engineer | E1 | ... | ... | ... | ... |
| Head of Architecture | A1 | ... | ... | ... | ... |
| Head of Design | D1 | ... | ... | ... | ... |
```

A reviewer with nothing relevant gets one row: "Limited relevance: <reason>".

## C. Cross-functional decision log (Deep Review, Executive Challenge)

```
**Agreed recommendations**
- <recommendation> · supported by <IDs>

**Disputed recommendations**
- <issue>: <Reviewer X says ... / Reviewer Y says ...>
  Trade-off: <what is traded against what>
  Strongest case for each option: <option 1: ...; option 2: ...>
  Accountable decision owner (role): <role>

**Positions changed in discussion**
- <ID withdrawn or revised, and why> (or "None")

**Outstanding questions**
- <question> · evidence needed: <...> · from: <role>
```

## D. Prioritised improvement backlog

```
| # | Priority | Proposed change | Expected benefit | Complexity | Dependencies | Acceptance criteria | From |
|---|---|---|---|---|---|---|---|
| 1 | Must | ... | ... | Small, <reason> | ... | <how we know it is done> | P1, A2 |
```

Priority: **Must incorporate**, **Should incorporate**, **Consider**, **Do not incorporate**. Complexity is small, medium or large with a reason, never hours. Every finding appears in this table or in the decision log. Rejected items list the reason in the Proposed change column.

## E. Revised artifact (Deep Review)

- The complete revised document, saved as `<artifact-name>-reviewed.<ext>`.
- Places where a consequential choice is needed are marked **[DECISION NEEDED: ...]**.
- A change log:

```
| # | What changed | Why | Finding(s) |
|---|---|---|---|
```

- And a list of changes needed in other files, if the artifact is more than one file.

## Executive Challenge output

Replace B to E with:

```
## Strongest case against, by reviewer
**Head of Product:** <paragraph>
... (four)

## Objections and what would resolve them
| # | Objection | Reviewer | Severity | Evidence or change that would resolve it | Who could provide it |
|---|---|---|---|---|---|

## What would change each reviewer's mind
- <reviewer>: <specific facts, tests or commitments>

## Recommendation: proceed, delay or modify
<one of the three, with the reasons and the conditions>
```

Then the decision log (C) and verdict (F).

## F. Final verdict

```
**Verdict:** <Ready | Ready with conditions | Requires revision | Not recommended>
**Acceptance criteria met:** <list>
**Acceptance criteria not met:** <list, each with the finding ID>
**To move up:** <the specific changes that would improve the verdict>
```

Criteria:
- **Ready:** no open Must items, no Critical or High finding unresolved, and the main claims are supported by the evidence given.
- **Ready with conditions:** open Must items exist, but each is specific and can be fixed without changing the approach. List them as the conditions.
- **Requires revision:** several Must items or High findings change the content materially, or key claims lack support. The approach may stand.
- **Not recommended:** a Critical finding invalidates the approach itself (for example the problem is not shown to exist, or the solution cannot meet a hard constraint).

The verdict applies to the artifact's evidence and reasoning as written. It is not stakeholder approval.
