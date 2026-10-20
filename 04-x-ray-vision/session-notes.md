# Session notes

## 2026-10-20

### Questions and answers

**1. What happens from "a callout exists" to "a responder's phone buzzes", and which file is each step in?**
The routing folder (`00-rook/code/dispatch-routing/`) starts at a finished callout. Nothing in it creates a callout or takes the incident report. The steps are:
1. Find everyone marked available in the callout's region: `availability.py`, `available_for`.
2. Score each one from three weighted parts (proximity, recent acceptance, capability match): `routing.py`. The weights are in `config.py`.
3. "Recent acceptance" is a running score from 0 to 1. Everyone starts at 0.5. A yes adds 0.08, a no subtracts 0.12, and a missed offer subtracts 0.12 too: `history.py`.
4. Sort best first. Nobody is removed from the list: `routing.py`, `rank_for_callout`.
5. Push the offer to the top responder's phone and wait a fixed time, 60 seconds since 4.2 (it was 90): `offer.py`, with the value in `config.py`.
6. Taken: stop. Turned down or time ran out: score goes down and we move to the next person. At the bottom of the list with no yes, the callout returns "nobody": `offer.py`, `dispatch`.

Caveats found while reading: `availability.py` and the phone push and poll functions in `offer.py` are blank placeholders in this folder, so the real behaviour there is unseen. Scores live in an in-memory dictionary keyed by display name. A 2019 comment in `history.py` asks whether scores should drift back to neutral and leaves it open.

**2. Was 4.2 built as intended, are there bugs, and what should a developer be told?**
- Both briefs were built exactly. The wiki briefs ("Weight proximity more heavily when ranking", "Tune how long a ping waits") are one sentence each, with no goal, no success measure and no mention of how a shorter wait feeds into scores.
- Timeout check in the data: for missed pings, the gap to the next ping on the same callout was 91 to 93 seconds before 12 Aug and 61 to 63 seconds after. The setting does what it says.
- Proximity check: if proximity counts for more, the home responder should be the first ping more often. In the 11 areas without a silent responder it fell from 80% to 72%. In the four affected areas it fell from 81% to 41%. No visible benefit for wide-area responders.
- Replay of the score rules over each responder's real ping history (an estimate, everyone starting at 0.5 on 29 Jun): before 4.2 all 16 sat between 0.80 and 1.00, so the signal did no work. After 4.2 only the four silent responders (Farlight, The Undertow, Vesper, Meteor Mite) reach 0, from late August. Nobody else drops below 0.28.
- Why the loop bites: a yes is +0.08 and a no is -0.12, so anyone who fails more than 40% of the time slides to the floor for good. The average failure rate went from about 23% to about 36%, which leaves ordinary responders about 4 points from that cliff.
- Size of the ranking effect: the acceptance weight is 0.25 now (0.40 before), worth at most about 19 minutes of travel against a perfect score (40 before).
- The eight design flaws, in order of importance: scores never fade; a miss costs the same as a refusal; the 40% cliff; "recent" is not recent; callouts ending after one ping; scores held in memory by name; the clock and its blind spots (see Findings); and the unanswered question on 14 Aug about whether proximity applies to people who turn jobs down.
- Developer brief (also in the artifact): count a miss differently from a refusal; raise the lowest allowed score to 0.3 to 0.4; make "recent" mean recent (last 10 to 20 pings or drift back to 0.5); add a comeback slot for anyone unpinged for about 3 days; make silence visible (store scores by responder ID, log changes, alert when pings drop by half or 5 days pass without one); instrument the clock before changing it; stop callouts ending after one ping; decide whether proximity applies to decliners. Success test: replay the last 70 days of pings through the new rules; nobody should fall to a fraction of their peers' pings, and callouts nobody took should return to about 5%. Tell the Supply team first if the availability record gets a new field.

**3. Build this as an interactive artifact in a super-hero style.**
Built and published as a private artifact, "The Silent Four". It has a score replay with sliders and presets, three "built as asked?" panels, four evidence charts, eight bugs filterable by severity and a tickable developer brief with a copy button. Only a quick check in the preview pane was done, so the phone layout is unchecked.

**4. What prompt would a classmate use to make something similar?**
A reusable prompt was written: name the topic and audience, say "use only what we have already established in this session, do not invent numbers", list the seven sections, set the comic-book look, and ask for a private artifact. The main tip: run the analysis first, because the page is built from the data already in the session.

**5. What does wrap up do?**
Explained from `.claude/skills/wrap-up/SKILL.md`.

**6. How could wrap up keep more of the learnings?**
Proposed and then made: a per-module `session-notes.md` with no length limit, a short summary plus pointer in CLAUDE.md, a "Superseded:" line instead of leaving stale claims, and an updated final checklist. This file is the first use of it. One finding from testing: the skill loader served the old wording of the skill after the edit, so the new version only takes effect after the skill is reloaded, for example in a new session.

### Findings

- **Observed (database `pings`, `callouts`, `responders`, 29 Jun to 6 Sep):** every "turned down" answer came within 40 seconds, both before 4.2 (184 cases, median 22 s, 90th percentile 37 s) and after (84 cases, median 23 s, 90th percentile 36 s). Answer times for "taken" cannot be seen, because the cascade ends there.
- **Observed:** the four failed 71 to 82% of their pings after release, against about 30% for peers and 19 to 31% for the four themselves before. In their first six pings after release, 3 to 5 failed (Farlight 5, The Undertow 4, Meteor Mite 4, Vesper 3), while their replayed scores were still high. So the score loop explains why they got fewer pings. It does not explain why they missed so many in the first place.
- **Observed:** misses on release day jumped: 0 of 32 pings on 10 Aug, 1 of 19 on 11 Aug, 7 of 25 on 12 Aug, 12 of 25 on 13 Aug, 8 of 30 on 14 Aug, 6 of 24 on 15 Aug.
- **Observed:** about 1 in 5 failed first pings ended with no second ping at all: 42 of 236 before, 40 of 183 after. Riverside had 8 untaken callouts and Westbury 8, each asked only the home responder. In several cases other responders had been pinged within the previous hour.
- **Observed:** outside-area pings rose from 17.6% to 25.0% in the 11 other areas, and from 16.4% to 62.6% in the four affected areas. The jump is concentrated where the four went quiet.
- **Inferred (confidence about 40 out of 100, down from 70):** the timeout cut as the main cause of the miss spike. Everyone who says no says it within 40 seconds, so a 60 second wait looks long enough. Delivery of the push is an alternative, and the 4.2 release notes list a defect fix to "duplicate push notification when a ping is sent again", which touches that path. A third possibility is that the four are slower answerers who happened to be inside the 60 to 90 second band, which can't be tested without answer times.
- **Inferred (replay, estimate):** the score loop is what locked the four out. Confidence about 60 out of 100. It is plausible, consistent with who is affected, and not confirmed without real scores.
- **Documented intent:** the glossary says a miss lowers recent acceptance, so counting a miss as a refusal is by design, not an accidental bug.

### Reversals

- **Weakened:** "timeout cut (90s -> 60s) is very likely the main mechanism" (CLAUDE.md, Module 1 findings from the wiki and database, and the Module 3 working theory). The 40-second ceiling on every refusal is the evidence. The earlier read assumed people were answering between 60 and 90 seconds. See Findings.
- **Partly resolved:** the Module 3 "tension" (4.2 lowered the acceptance weight, which should soften the penalty, yet four collapsed). The replay shows the weight only limits how much a bad score can cost, about 19 minutes of travel, and the real driver is the number of misses. Before 4.2 almost nobody had any, so the harsher penalty rule never mattered.
- `00-rook/4-2-impact-analysis.md` still says the timeout is the "very likely main driver" at confidence 70. It was not edited in this session.

### Queries and checks that mattered

All run against the Rook database. Tables: `pings` (callout_number, responder, sent_at, outcome), `callouts` (callout_number, happened_at, area, what_happened), `responders` (name, handler, area), `support_tickets`.

- **Timeout and answer times:** gap between a ping and the next ping on the same callout, by outcome and period.
  `WITH g AS (SELECT callout_number, responder, outcome, sent_at, EXTRACT(EPOCH FROM (lead(sent_at) OVER (PARTITION BY callout_number ORDER BY sent_at) - sent_at)) AS gap FROM pings) SELECT (sent_at>='2026-08-12') AS after, outcome, count(gap), min(gap), percentile_cont(0.5) WITHIN GROUP (ORDER BY gap), percentile_cont(0.9) WITHIN GROUP (ORDER BY gap), max(gap) FROM g WHERE gap IS NOT NULL GROUP BY 1,2`
- **Home responder first:** join the first ping of each callout (row_number over callout, ordered by sent_at) to `responders` and compare `responders.area` with `callouts.area`, split by the four affected areas (Uptown, Harborside, Old Town, Eastgate) and the other 11, before and after 12 Aug.
- **Single-ping dead ends:** group callouts by first-ping outcome, number of pings, and whether any ping was taken. Then list the callouts that failed on one ping with the number of other responders pinged in the previous hour.
- **Score replay:** for each responder, `string_agg` of outcomes as T, D, M in time order, split at 12 Aug, then applied in a short script with +0.08 for T, -0.12 for D and -0.12 for M, clamped between 0 and 1, starting at 0.5. The script is a scratch file and is not saved here. The rule is simple enough to rebuild from this line.
- **Wiki pages read:** "Change to who gets pinged", "Ping timeout tuning", "Availability Confidence", the 4.2 release page with its comments, Rook Dispatch one-pager, Glossary, Routing Override Audit Log.

### Decisions and recommendations

- **Recommended:** fix the scoring rules before touching the timeout again. Count misses differently from refusals, raise the floor and make "recent" recent. Instrument first, then test 90 against 60 seconds behind a switch. The full list is above under question 2.
- **Open decision:** does the proximity weight apply to people who turn jobs down? The engineering manager asked on 14 Aug ("was it a decision or did it just fall out that way?") and nobody has answered.

### Files and artifacts made

- `00-rook/silent-four-case-file.html`: the artifact source.
- Published artifact "The Silent Four" (private, only the owner can open it until it is shared from the Share menu): https://claude.ai/artifact/VSSt7sfw6qSUdtbZy6f8Ks
- `.claude/skills/wrap-up/SKILL.md`: updated to add the session-notes step, the "Superseded:" rule and the new checklist line.
- This file, `04-x-ray-vision/session-notes.md`.
- `00-rook/4-2-impact-analysis.md` shows as modified in git. That change was not made by Claude in this session.

### What we couldn't see

- Real score history per responder. The replay is an estimate.
- How long people take to say yes.
- The working code for availability, travel time and phone push. These are blank placeholders in the folder.
- Who was available on the callouts that got only one ping.
- Why those four responders missed so much from the first days.
- Prior-year numbers and anything after 6 Sep.

### Open questions

- **Staff engineer:** real score history and rank order for sample callouts; why callouts end after one ping; what the 4.2 duplicate-push fix changed; whether scores survive a restart; was the proximity weight meant to apply to decliners.
- **Engineering manager:** answer times for yes; delivery time of pushes; data after 6 Sep and from last year; how "acceptance rate" is defined, and where the "time-to-accept" number on the wiki comes from, since it is not in the database.
- **Support lead and handlers:** are the four's phones or app versions different from their peers'? Did they see the notifications at all?

### Start here next time

Ask the engineering manager for answer times (for yes as well as no) and push delivery times for the 12 Aug to 6 Sep window. That one request decides between "the wait is too short" and "the offer isn't reaching the phone". Then update `00-rook/4-2-impact-analysis.md` with the new confidence levels.
