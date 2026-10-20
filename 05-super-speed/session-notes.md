# Session notes

## 2026-10-20

### Questions and answers

- **"Draft me a one-page brief for what we'd build instead: who it's for, what changes for that person, what it deliberately doesn't do."** Read `00-rook/company/` first. It holds only one file, Priya's handover note (`notes/handoff-from-priya.docx`). The glossary, team roster and Slack thread the student expected were not there. Read `05-super-speed/director-request.txt`, the routing code (`history.py`, `config.py`, `routing.py`, `offer.py`, `availability.py`, `CHANGELOG.md`) and `00-rook/4-2-impact-analysis.md`. Wrote `05-super-speed/quiet-responder-brief.md`. Two people it is for: the responder who has gone quiet, and the handler (Kip). The brief says what changes for each, what it deliberately does not do, how we'd know it worked, and what must be checked before anyone builds.
- **The student's framing was "being quiet is exactly what stops them being asked".** Corrected in the brief and in chat: the four quiet responders were still pinged about once a day between 19 Aug and 6 Sep (20 pings, 15 missed). The loop is that a miss costs the same as a "no" (-0.12), only a "yes" gives +0.08, and scores never ease back. The blocker is answering when asked, not being asked at all.
- **"Walk me through what Kip would see change next time Meteor Mite goes quiet."** Walked through a timeline with the brief against today. Found two gaps: the brief did not say how a handler notices the Quiet marker (3 of 4 interviewed handlers asked for an alert, no ticket did), and a two-week window is slow (Mite's pings stopped around 14-15 Aug; a 14-day trigger would fire near the end of August, the first quiet ticket was 17 Aug). Both were added to the brief.
- **"Rework the brief to one pager."** Cut from about 700 words to about 450 without dropping any section.
- **"One-line pitch for the person it happens to."** To the responder: "If your phone's gone quiet, you're still on the list. We'll tell you what happened to your last few offers, and one answered call now starts bringing you back." To Kip: "When one of your responders goes quiet, you'll see it that week, with the reason, and one tap to check in on them." Caveat given: "one answered call starts bringing you back" is not proven until real scores are seen.
- **"Build a clickable prototype."** Built `05-super-speed/quiet-responder-prototype.html`, a single file with no dependencies. It has a handler console and a responder phone view. Clicking Check in opens a dialog with the evidence and a confirm box, then clears the Quiet marker, adds an override-log line and changes the phone message. Tested in the browser pane, in its narrow layout only.
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

- `05-super-speed/quiet-responder-brief.md` (one-page brief, rewritten twice).
- `05-super-speed/quiet-responder-prototype.html` (clickable prototype, sample data).
- `05-super-speed/prompts.md` (six prompts saved).
- `05-super-speed/session-notes.md` (this file).
- No published artifact this session.
- The Module 5 wrap-up expects `05-super-speed/brief.md` and `05-super-speed/prototype.html`. The files made have different names, and nothing was renamed or recreated.

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
