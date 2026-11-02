# Session notes

## 2026-10-20

### Questions and answers

- **"Draft me a one-page brief for what we'd build instead: who it's for, what changes for that person, what it deliberately doesn't do."** Read `00-rook/company/` first. It holds only one file, Priya's handover note (`notes/handoff-from-priya.docx`). The glossary, team roster and Slack thread the student expected were not there. Read `05-super-speed/director-request.txt`, the routing code (`history.py`, `config.py`, `routing.py`, `offer.py`, `availability.py`, `CHANGELOG.md`) and `00-rook/4-2-impact-analysis.md`. Wrote `05-super-speed/brief.md`. Two people it is for: the responder who has gone quiet, and the handler (Kip). The brief says what changes for each, what it deliberately does not do, how we'd know it worked, and what must be checked before anyone builds.
- **The student's framing was "being quiet is exactly what stops them being asked".** Corrected in the brief and in chat: the four quiet responders were still pinged about once a day between 19 Aug and 6 Sep (20 pings, 15 missed). The loop is that a miss costs the same as a "no" (-0.12), only a "yes" gives +0.08, and scores never ease back. The blocker is answering when asked, not being asked at all.
- **"Walk me through what Kip would see change next time Meteor Mite goes quiet."** Walked through a timeline with the brief against today. Found two gaps: the brief did not say how a handler notices the Quiet marker (3 of 4 interviewed handlers asked for an alert, no ticket did), and a two-week window is slow (Mite's pings stopped around 14-15 Aug; a 14-day trigger would fire near the end of August, the first quiet ticket was 17 Aug). Both were added to the brief.
- **"Rework the brief to one pager."** Cut from about 700 words to about 450 without dropping any section.
- **"One-line pitch for the person it happens to."** To the responder: "If your phone's gone quiet, you're still on the list. We'll tell you what happened to your last few offers, and one answered call now starts bringing you back." To Kip: "When one of your responders goes quiet, you'll see it that week, with the reason, and one tap to check in on them." Caveat given: "one answered call starts bringing you back" is not proven until real scores are seen.
- **"Build a clickable prototype."** Built `05-super-speed/prototype.html`, a single file with no dependencies. It has a handler console and a responder phone view. Clicking Check in opens a dialog with the evidence and a confirm box, then clears the Quiet marker, adds an override-log line and changes the phone message. Tested in the browser pane, in its narrow layout only.
- **"If I'd only described this, what would I still not know?"** Building forced four decisions the brief had skipped: who vouches for the reset (the confirm checkbox was my addition), what "usual" means as a baseline, whether the console can read each responder's last yes and last outcomes, and the wording of the phone message (it claims missed offers count for less, which holds only if built). It still cannot show whether the idea works, whether Kip would use it, or how a responder would feel.

### Findings

- Today's rule: a miss and a refusal both cost 0.12, a yes gives 0.08, scores never ease back (observed in `history.py`; the 2019 TODO asks whether they should). Source: code.
- The four quiet responders took 3 of 40 first pings after 4.2 against 175 of 247 before (observed, `00-rook/4-2-impact-analysis.md`, from the database `pings` table). Their scores in the brief are my replay, not real data (inferred). Confidence in the score slide: about 50 (earlier analysis).
- Meteor Mite: about 1.59 to 0.54 pings a day, 57% missed after 4.2. The Gale in the same area: about 1.86 to 2.65 a day (observed, same analysis).
- The four account for about one third of the fall in "taken"; the 12 other responders about two thirds (observed). So this feature addresses only about one third of the damage.
- Time to notice: first quiet ticket 17 Aug, about 3 days after the four's pings stopped; Vesper and Meteor Mite filed no ticket at all (observed, tickets).
- The 4.0 release added a routing override audit log (observed, `CHANGELOG.md`), which the Check in action would write to.

### Reversals

- The student's opening framing, "being quiet is exactly what stops them being asked", is too strong. It matches the earlier correction already in CLAUDE.md ("Four responders are effectively locked out" is too strong). Evidence: 20 pings, 16 of them first choice, 19 Aug to 6 Sep.
- No other earlier claim was overturned.

### Queries and checks that mattered

- No new queries this session. Every number comes from the earlier analysis in `00-rook/4-2-impact-analysis.md`. Checks made: read the handover docx (its comments, footnotes and endnotes are empty); `grep -n "TODO\|should\|why"` over `00-rook/code/dispatch-routing/*.py` found the 2019 TODO in `history.py` line 30; clicked through the prototype in the browser pane (Check in, confirm box, confirm, phone tab, reset).

### Decisions and recommendations

- Build the brief's four parts: a miss costs less than a refusal; scores ease back toward neutral, never above; a Quiet marker for handlers with evidence; a Check in action that resets to neutral and logs in the override log. A responder message says they are still on the list. Numbers to be set by the staff engineer.
- Deliberately not done: promising offers or moving a quiet responder ahead of someone better placed, touching the 60s wait or proximity weights, fixing the wider miss spike, grading responders, changing the availability record that Supply reads, console extras.
- Caution given: do not ship the "small fix this afternoon" before real scores are seen (agrees with the 20 Oct wrap-up worry already in CLAUDE.md).

### Files and artifacts made

- `05-super-speed/brief.md` (one-page brief, rewritten twice).
- `05-super-speed/prototype.html` (clickable prototype, sample data).
- `05-super-speed/prompts.md` (six prompts saved).
- `05-super-speed/session-notes.md` (this file).
- No published artifact this session.
- The Module 5 wrap-up expects `05-super-speed/brief.md` and `05-super-speed/prototype.html`. The files were first saved as `quiet-responder-brief.md` and `quiet-responder-prototype.html`. At the student's request they were renamed to `brief.md` and `prototype.html` after the first wrap-up, and the references in CLAUDE.md and these notes were updated.

### What we couldn't see

- Real recent-acceptance scores and rank orders (database has none; staff engineer has them).
- Why the four miss: slow answers, push delivery or phones. No answer-time column and no push logs.
- Anything after 6-7 Sep. Today is 20 Oct.
- The real console layout, and whether it can show a responder's last yes and last outcomes.
- Prototype values for "last yes: 6 days ago", the last three outcomes and the phone offer times are invented.

### Open questions

- How should a handler be told a responder is Quiet (badge, daily digest or push)? Kip and the staff engineer.
- What is the right window for "quiet", and what is "usual" measured against? Staff engineer and the engineering manager.
- Does a handler override count as a "yes", and do scores survive a restart? Staff engineer.
- Can the console read each responder's last yes and recent outcomes? Engineering manager.
- Should Check in require the handler to confirm they spoke to the responder? Director of Product (Helen) and Kip.
- Role of Marcus (mentioned in Helen's note) is unknown. The "Wen" who left a note is assumed to be the author of the 2019 TODO in `history.py` (the code names no author). Ask the student to confirm.

### Start here next time

Ask the staff engineer for the four quiet responders' real scores and rank order. If they aren't at the floor, the brief changes before anything is built. Then show Helen the brief and prototype, with the sample-data note.

## 2026-11-02

Work in this entry ran in one session that started on 22 Oct, after the first wrap-up above. Other sessions edited the brief and prototype afterwards (1 to 2 Nov, see "Files and artifacts made"). Those later edits are not part of this entry.

### Questions and answers

- **"Rename them, please."** `quiet-responder-brief.md` became `brief.md` and `quiet-responder-prototype.html` became `prototype.html`, with `git mv`. The old names in CLAUDE.md and the notes were updated. Committed and pushed as `b9db89d`.
- **"What does the director want to read?"** Helen's note (`director-request.txt`) asks for a one-pager on what we'd build instead of the small fix engineering could ship that afternoon, seen from the person it happens to (a handler like Kip, a responder who has gone quiet), rough rather than polished, with something clickable as a bonus. She does not ask for a root cause, a rollback or a comparison of fixes. I flagged that "Wen" is assumed to be the author of the 2019 TODO in `history.py`, which names no author.
- **"What's still missing before this could be built?" (using Meteor Mite).** CLAUDE.md records no "picked" responder, so I used Meteor Mite, whom the student named earlier. Missing: (1) brief gaps from the review (no owner, no success numbers, a Quiet trigger that missed offers, ease-back versus Check in unexplained); (2) unknowns about the cause (real scores, why Mite misses, data after 6 Sep, whether a reset counts as a "yes"); (3) undecided design points (how Kip is told, the Quiet window, what "usual" means, whether the console can show last yes and outcomes, who vouches for Check in); (4) nothing from engineering yet.
- **"Write the brief first."** Rewrote `brief.md`: named owner role, proposed success targets, a Quiet trigger that also catches missed offers, and a line on how ease-back and Check in relate. `review-checklist` then gave Needs changes (scope Partial: Check in and "anyone who goes quiet" were missing from the overview). Fixed with one line.
- **"Simplify: 1-2 sentences per section, key data, tables, 5th-grade level."** Rewrote with short sections and three data tables.
- **"Organise as seven sections."** Overview, decisions from Helen, decisions from other teams, problem and why now, ideal state and plan, supporting data, open questions with owners.
- **"Be Helen, use multiple models, don't come back until aligned."** Ran three reviews in parallel on Opus, Sonnet and Haiku. A Fable run failed because that model needs usage credits, so it was not retried. All three agreed on eight must-fix changes: add what Kip and the responder see and link the prototype; resolve the contradiction between "the 60-second wait may be the cause" and "this plan doesn't touch it"; give the hold a date; name the owner and take it out of Helen's decisions; mark every "Today" figure "(to 6 Sep)" and stop guessing targets; soften "stuck at the bottom"; rewrite "Why now" (stale 7 Sep ticket count, odd leaning on Wen's note); fix the section 6 labels ("first pings taken" and "offers taken" use different bases). One split: whether Helen can say yes to "a way back" now (Opus yes; Sonnet and Haiku not yet). Applied the eight changes.
- **"They used sources outside the brief (e.g. prototypes). Judge on the brief alone."** Made a copy of the brief with the prototype links removed and told three fresh reviewers (Opus, Sonnet, Haiku) to read only that copy. Their tool-use counts (2 each) fit one file read plus the report. Most of the earlier findings came back, so they came from the brief. They agreed on six must-fix changes: fill the placeholders with a real date and a "what if scores aren't in" rule; make the direction a conditional yes; ask Helen to confirm the measures, not the numbers; close the logic gap (the four are still asked once a day but miss 15 of 20, so healing scores gets them asked again but does not make them faster to answer); give Check in a default (handler must have reached the responder, logged with their name); name the small fix. Applied all six.
- **"Cut to get it under one page."** About 1,150 words down to about 680, keeping all seven sections. Page length could not be measured (no PDF tool); I said so.
- **"Apply v3 and rerun the check."** No file called v3 existed. I treated the current brief as v3 and ran `review-checklist`: Needs changes (one Partial on scope). After the cut, "apply another check" gave Ready (all four pass), with the placeholders still unfilled.
- **"Ask me questions until you're 95% confident, then build."** Three rounds. Answers: click-through plus score simulator in one HTML file; audience is Helen's walkthrough; invented labelled sample data; show all three handler alerts (badge, digest, push) with a switch; rule numbers as adjustable placeholders; the simulator takes clicked outcomes with two score lines side by side; replace `prototype.html`; add the three measures; Quiet fires on pings halving or most offers missed, with a pings-this-week control; show rank cost in minutes of travel. Then "go".

### Findings

- Three-model Helen reviews converged on most fixes (observed). First round: five of the eight must-fix items were raised by all three reviewers and three by two of them (soften "got stuck", rewrite "Why now", fix the section 6 labels). Second round: five of the six must-fix items were raised by all three; "name the small fix" came from Opus alone. Caveat: same prompt, same model family, so shared blind spots are possible; in the second round none could see the prototype.
- The prototype's sample replay (14 offers, 8 misses, 2 yeses, 2 days between offers) ends with today's rules at 0.00 and the fixes at 0.04, about 18 minutes of travel cost either way (observed in the prototype, placeholder numbers: miss cost 0.06, healing 0.01 a day). So a cheaper miss alone does not rescue a responder who misses 57% of offers. Healing and Check in do: skipping 14 days lifts the fixes line to 0.18, and Check in resets it to 0.50.
- Rank cost is about 18.75 minutes of travel per point of score (inferred from `config.py`: recent acceptance weight 0.25, proximity weight 0.60 over 45 minutes). Confidence: medium; it ignores capability and ties.
- The brief's figures (175 of 247 first pings, 15 of 20 missed, 22 of 32 quiet tickets for Farlight and The Undertow) were not re-checked this session; the Module 6 notes cover that check.

### Reversals

- The brief's "got stuck at the bottom of the list" (section 1, earlier drafts) is weakened: the four are still asked about once a day and miss 15 of 20, and the real scores have not been seen. It now says "appear stuck low" with "my estimate from the code".
- The earlier draft's "75% of old rate in 2 weeks" and "fewer than 5 tickets" targets were my guesses and contradicted "promises no offers". They were replaced by measures without numbers, set after two weeks of data against each responder's own pre-4.2 rate.
- The Module 5 open item "whether Check in needs the handler to confirm they spoke to the responder (a checkbox I added)" is now a recommendation in the brief.

### Queries and checks that mattered

- `review-checklist` run on `05-super-speed/brief.md` three times: Needs changes (scope Partial), Needs changes (scope Partial, after the first rewrite), Ready (after the cut).
- Word count after stripping table pipes: `sed -e 's/|//g' -e 's/[-]\{3,\}//g' -e 's/\*//g' brief.md | wc -w`. Result about 677 words.
- Prototype tests run in the browser pane with scripted clicks: replay, skip days, Check in with the confirm box disabled until ticked, cancel, click-outside to close, all three alert modes, each slider, Quiet by misses (fires at 3 of 4, not at 2) and by pings (3 of 11), and no sideways overflow at 375 px wide. No console errors.

### Decisions and recommendations

- **Hold the small fix** until the real scores are in, with a date agreed with the staff engineer. If the scores are not in by then, Helen decides again. Reason: if the 60-second wait is the cause, a score change only softens the damage.
- **Pursue a way back, and build it only if the real scores show the four at the bottom.** The 90-second wait test runs alongside, not instead.
- **Check in** only for a handler who has reached the responder, resets to neutral, logged with the handler's name (my recommendation; Helen and Kip to confirm).
- **Ask of Helen, kept in the brief:** "Hold engineering's small fix until the real scores are in?", "Pursue a way back, and build it only if the real scores show the four at the bottom?", "Are the three measures right? Numbers are set after two weeks of data."

### Files and artifacts made

- `05-super-speed/brief.md`: rewritten several times (commits `4deb340`, `670408a`). Later edited by other sessions on 1 Nov (`8811697`, `a5703d5`: named owner, scope line, small fix described, placeholders removed).
- `05-super-speed/prototype.html`: rebuilt on 22 Oct as three tabs (Kip's console, Meteor Mite's phone, score simulator), commit `deb2c50`. Later changed by another session on 2 Nov (`2392ed0`, "apply three-pro review changes"). I did not review that later edit.
- `05-super-speed/prompts.md`: 18 prompts saved (12 added today).
- `05-super-speed/session-notes.md`: this entry.
- A brief-only copy for the second round of reviews was kept outside the course folder and is not saved to GitHub.
- No published artifact this session.

### What we couldn't see

- Real recent-acceptance scores, rank orders, answer times, push logs, and any data after 6 to 7 Sep. This still limits every conclusion.
- What the prototype looks like on screen: the browser pane was too small for a readable screenshot, so only the logic and the layout metrics were tested.
- Page length of the brief when printed (no PDF tool).
- What engineering's "small fix" actually is. No file says; the brief now says "most likely lowering the shared 0.12 penalty" (inferred, from later edits).
- The Fable model did not run, so only three model families' views were used.

### Open questions

- What is the small fix, and when can the real scores be pulled so the hold has an end date? Engineering manager and staff engineer.
- Are the four at the bottom? Does a handler's reset count as a "yes", and do scores survive a restart? Staff engineer.
- Why do they miss (slow yeses, push delivery or phones), and what has happened since 6 Sep? Engineering manager.
- How is a handler told (badge, digest or push), and what counts as "quiet"? Kip and the staff engineer.
- Does Helen agree to the Check in rule and to the three measures? Director of Product.

### Start here next time

Get the real scores, answer times and push logs from the staff engineer and engineering manager before anyone builds; every decision in the brief depends on them. Then open `prototype.html` in a full-size browser window and check how it looks, since I could not see it.
