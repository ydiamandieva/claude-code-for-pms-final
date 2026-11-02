# Artifact types and depth of review

The board works as a quality gate after any substantial output. Adapt the depth to the type: the reviewers who matter most look hardest, and the others say "Limited relevance" or limit themselves to what they can ground.

| Artifact | Lead scrutiny | Secondary | Often limited relevance | Typical mode |
|---|---|---|---|---|
| Competitive intelligence report | Product (materiality, customer relevance, interpretation); evidence quality | Design (is it usable by leaders) ; Engineer and Architect only on proposed responses | Architect, Engineer, when no technical response is proposed | Quick (monthly), Deep (baseline) |
| Product strategy | Product | Architect (dependencies), Design | Engineer, unless it commits delivery | Deep |
| Roadmap or investment proposal | Product, Engineer | Architect, Design | none | Deep |
| Business case | Product | Engineer (cost and effort claims) | Design | Deep |
| PRD or specification | Product, Engineer, Design | Architect | none | Deep |
| AI capability proposal | Product, Architect, Design (trust and explainability), Engineer | none | none | Deep or Executive Challenge |
| Architecture or implementation plan | Architect, Engineer | Product (value, cost) | Design, unless user-facing | Deep |
| UX concept or prototype evaluation | Design, Product | Engineer | Architect | Quick or Deep |

If the type isn't in the table, decide from what the artifact asks the reader to decide, and say which reviewers you weighted and why.

## Challenging a competitive intelligence report

Use this when the artifact comes from **Fleet Telematics Competitive Intelligence & Strategic Market Radar** (for example `fleet-intel/reports/MCF_Competitive_Intelligence_YYYY-MM.md` and its repository). The reviewers may open the repository files the report cites (evidence register, change log, action register, capability matrix) to spot-check. They must **not** invent internal MCF capabilities, architecture, roadmap or numbers. Where a finding depends on them, it becomes a question for a named role.

First check the intelligence skill's own rules are honoured, as a baseline before the reviewers start:
- Every material claim has a source and date; "not publicly verified" is never read as "missing".
- Facts, inferences, hypotheses and recommendations are separated.
- Scores come with reasons and are not presented as facts; departures from the action rules are explained.
- Limitations and coverage gaps are stated.

**Head of Product challenges**
- Are the developments strategically material, or only prominent in the news?
- Are recommendations tied to customer value and business outcomes?
- Is competitor activity being mistaken for customer demand? What customer evidence is there?
- Would the findings justify changing MCF's priorities, and what would be given up?
- Do the "Act" items have owners, measures and a stated reason that they beat other uses of the same effort?

**Lead Engineer challenges**
- Are the proposed responses technically feasible as described?
- Are engineering dependencies, data availability and delivery constraints recognised?
- Are any implementation estimates supported by evidence? Estimates without evidence are a finding.
- Does the report ask for work that depends on information only MCF's engineers hold?

**Head of Architecture challenges**
- Could a proposed response compromise the platform's architecture or add coupling or lock-in (for example reliance on a competitor's marketplace)?
- Are vendor dependencies, data interoperability, privacy and security considered, including regulatory ones the report itself cites (for example the EU Data Act)?
- Do the recommendations fit sustainable evolution of the platform, as far as the report allows anyone to judge?

**Head of Design challenges**
- Do the competitive developments show a real shift in user expectations, or just a feature race?
- Are proposed differentiators likely to improve customer workflows? What evidence is there?
- Are adoption, trust and usability addressed, especially for AI features (explainability, grounding, consent for video)?
- Can a leader read the report and find the decision, the evidence and the next step quickly?

**Extra checks for the board**
- Does the executive brief match the scored table, the change log and the action register?
- Are the top recommendations consistent with the stated confidence and coverage limits?
- Is there a recommendation that rests only on a rival's marketing claim or a single low-authority source?
- For a monthly report: is it about material change, or is it repeating the baseline?
- Conclusions must stay balanced. Don't favour MCF or a competitor without evidence.
