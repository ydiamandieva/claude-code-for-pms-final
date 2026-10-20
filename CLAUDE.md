# Rook Industries — course working file

## Session scope — Product School lab

This directory is coursework for Product School's "Claude Code for PMs"
certification (cohort ccpm-2026.1). Everything in it is a fictional
teaching scenario.

- Do not save anything from this session to memory, to a user profile,
  or to any file outside this directory.
- Do not carry context from this directory into unrelated sessions.
- Rook Industries is not a real company. Nothing here is a fact about
  the world.
- Read and write only within this directory.
  Exceptions, for the course-setup and wrap-up skills only:
  - When the student asks you to check their setup, save their work or wrap up a session, that request is their yes. You may run the GitHub command-line program installed at ~/.ccpm/gh for those checks and saves, and look in that folder to find it.
  - For a repair, first tell the student in one plain sentence what you are about to do, and act only after they say yes. Repairs may: run that GitHub program (including setting this folder's own git sign-in setting and changing this repo's visibility back to Public); copy the student's own course files into this directory from another folder on their computer (copy only; never move, edit or delete the originals); and rename something outside this directory that blocks setup, by adding "-old" to its name (never delete it).
  Outside this directory you still never write, edit or delete anything else.

<!-- Keep the block above at the top of this file. Everything you add
     during the course goes below this line. -->

---

## Working context

I'm the new PM for Rook Dispatch at Rook Industries. This section is built
from `00-rook/company/`, which currently holds one document: the handover
note from my predecessor Priya (written 21 Aug 2026). Anything not in that
note is marked as unknown below. Don't fill the gaps with guesses.

### Products
- **Dispatch** is the flagship and the product responders stick with. An
  incident comes in, we rank available responders, offer the callout to the
  top of the list, and they accept or decline.
- **Surfaces:** the handler **console** (stable) and the **mobile** app
  (stable since 4.1). **Routing**, the logic that decides who gets pinged,
  is where the interesting work and the risk are.
- Routing code lives in `00-rook/code/dispatch-routing/`. Priya says there is
  no written description of how ranking works.

### People
Priya's note gives roles only, not names. Ask me for names rather than
inventing them.
- **Director of Product:** my manager. Described as good and gives room.
- **Engineering manager:** runs Dispatch engineering. Straight talker, the
  first stop when I'm unsure. Can usually pull numbers.
- **Staff engineer:** built the who-gets-pinged logic. The only real source
  on how ranking works, so talk to her rather than look for a document.
- **Support lead:** hears handler complaints first. Worth a standing 15 min.
- **Priya:** the previous PM, sole PM on Dispatch for 14 months. Has left and
  there was no overlap. Admits she "made calls faster than I checked them".

### Vocabulary
- **Ping / offer:** sending a callout to a responder.
- **Responder:** the person who takes callouts. **Handler:** the console user
  who runs incidents, and the one writing in with complaints.
- **Acceptance rate:** share of pings taken. The number everyone watches, so
  I need to be able to explain it early.
- **Ping timeout:** how long a responder has to respond to an offer.
- **Recent acceptance history:** the ranking signal that 4.2 weighted down.
- **4.1 / 4.2:** release numbers.

### Where things stand
- **4.2 shipped 12 Aug 2026**, and it's the live problem. It weighted
  **proximity up** relative to recent acceptance history. Responders in wide
  geographies had asked for this for three quarters.
- **Since release:** fewer pings are being taken and more handlers are
  complaining.
- **Also in 4.2:** the ping timeout was cut, and console filter persistence
  changed. Filter persistence is cosmetic. It will generate noisy tickets and
  shouldn't eat my first month.
- **Competing explanations:** August is seasonally soft every year, the
  timeout cut and the proximity change landed together, and Priya's own read
  is "mostly seasonal, back in September". That is her opinion, not data.
  Nothing in the folder tests it, and it's now October.
- **Priya's guidance:** look at seasonality first, and don't let this become
  a debate about reverting 4.2, because the change was asked for. I should
  still check the data before accepting that.
- **Open items:**
  1. Some features were squeezed out of 4.2. I need to agree with the
     Director of Product which are still Q3 commitments. That conversation
     hasn't happened.
  2. Write up how routing decides who gets pinged.
  3. Revisit decisions made in parts of the product nobody has examined
     closely. I have fresh eyes, so use them early.

### Not yet known
Team and responder numbers, the acceptance-rate baseline and current
figures, which features were cut from 4.2, the Q3 commitments, and anyone's
name. The other lesson folders (`01-` to `06-`) and Rook's wiki and database
may fill some of this in.

### Added at wrap-up (Module 1)
- Rook has a second product, **Rook Supply** (equipment servicing). It reads
  Dispatch's availability record, so changing that record's shape means
  telling the Supply team first.
- The routing code explains a likely mechanism: a missed offer (timeout)
  counts as a decline (-0.12, vs +0.08 for a yes), scores never decay, and
  4.2 cut the offer window from 90s to 60s. Misses now cost responders
  ranking, and the penalty sticks. This is from code only, unconfirmed.
- Working theory, in order: timeout cut, then the penalty loop, then
  proximity weight, then seasonality. Restoring the timeout is the cheapest
  test and doesn't undo the proximity change.
- Still open: no real acceptance-rate data seen yet, whether September
  recovered, how "acceptance rate" is defined, and which features were cut
  from 4.2. Rook's wiki and database were not reachable from this session.


### Findings from the wiki and database (Module 1)
- **Rook's database** (5 tables: callouts, pings, responders, handlers,
  support_tickets; data runs 29 Jun to 6/7 Sep 2026). `pings` has outcome
  (taken / turned down / missed) but **no answer-time column**, so the
  60-90s test can't be run yet.
- **Before vs after 4.2 (12 Aug):** taken 76.6% -> 64.0%; missed 2.3% ->
  18.0%; turned down 21.1% -> 18.0%. The whole loss went into "missed".
  Weekly taken was flat at about 77% until 4.2, then 54%, 66%, 67%, 73%
  (week of 31 Aug), with misses still 12.7%. Recovering, not recovered.
- **Four responders went almost silent:** Vesper, The Undertow, Meteor
  Mite, Farlight (pings per day down about 65-75%, most of their remaining
  pings missed). They are in four different areas and area demand fell
  evenly, so geography doesn't explain it. Eastgate has Meteor Mite (quiet)
  and The Gale (busier, about +40%), same area, opposite outcome.
- **Wiki interviews (Research > Customer interviews, 2-5 Sep):** four
  handlers, console-redesign calls, not about routing. 3 of 4 said offers
  vanish before the responder can answer; 2 of 4 described very uneven
  work (Dot/Vesper, Kip/Meteor Mite vs The Gale). Console asks: bigger
  text, better handler alerts, dark mode, a warning when filters reset.
  Halloran raised Supply issues (11-day wait on a cracked vest plate).
- **Current read:** timeout cut (90s -> 60s) is very likely the main
  mechanism; the miss-counts-as-decline penalty loop likely explains the
  four silent responders; seasonality is weak as the main cause.
  Proximity weight not ruled out. Still untested: answer times, actual
  responder scores, prior years, data after 6 Sep.

### Findings from support tickets (Module 1)
- **147 tickets, 29 Jun to 7 Sep.** Before 4.2: about 5-8 a week, all closed.
  After 4.2: 20, 27, 32, 25 a week; 83 of 107 still open. Themes were
  sorted from subject lines and sampled bodies, so counts are approximate.
- **New since 4.2 (none existed before):** 32 "quiet" tickets (phone not
  going off) and 13 "offer vanished / lost one" tickets. All 45 are open.
  First quiet ticket 17 Aug.
- **Quiet tickets come from four responders only:** Farlight 11, The
  Undertow 11, Corporal Ashgrove 5, Halfmoon 5. A handler says Farlight went
  from about 12 pings a week to 4, matching the database. Vanished-offer
  tickets are wider: 13 across 9 responders.
- **Spiral evidence:** two handlers wrote that the first ping in 5 or 9 days
  was missed. Responders quoted: "starting to wonder if im still even in
  the system." Tickets from 3-5 Sep show Farlight and The Undertow still
  silent for 6-9 days, even as the overall taken rate recovered.
- **Tickets undercount:** Vesper and Meteor Mite (pings down about two
  thirds) filed no tickets; their handlers raised it in interviews instead.
- **Filter persistence:** 12 tickets, 2 are thank-yous. Real but small.
  Priya's "noise" call holds.
- **Actions:** support should reply to the 45 open quiet/vanished tickets;
  watch Ashgrove and Halfmoon (pings down about 20%); overall "other"
  tickets also roughly doubled and that is unexplained.

- The interviews and the tickets cover almost entirely different responders (only Captain Vantage overlaps, with one ticket). Interviews lead with "offers vanish too fast" (3 of 4); tickets lead with "phone too quiet" (32 vs 13). Both are the same problem seen from two ends.
- The four silent responders are split across the piles: Vesper and Meteor Mite only in interviews, The Undertow and Farlight only in tickets. Dot, Kip and Halloran never filed a ticket, so ticket counts undercount.
- Possible Supply link, unconfirmed: since 4.2 tickets say maintenance was booked on the marathon day and reminders came after the date, while Halloran said scheduling had improved.
- Evidence is strong on timing and shape (misses 2.3% to 18%, declines flat) but the timeout is not isolated from the proximity change. Next: get answer times from engineering, talk to Farlight's and The Undertow's handlers, and get support to answer the 45 open quiet/vanished tickets.

### Findings from the ping analysis (Module 3)
- Write-up is in `00-rook/4-2-impact-analysis.md`. Visuals are in `00-rook/ping-geography.html`, also a private artifact, "Ping blast map" (https://claude.ai/artifact/BRznK5T3qmzMHcFeo2ZZNX). `callout-history.csv` matches the database weekly totals exactly, so it is not independent evidence.
- Timing: missed pings jump on release day (12 Aug, 28% vs 0-5% a day before), and the first "offer vanished" ticket was filed the same day. The four silent responders' pings stop about 14-15 Aug, and handlers wrote in about 3 days later. Every "N pings in the last 7 days" ticket matches the database exactly.
- Callouts nobody took doubled, 5.5% to 11.1%. Roughly half is more failed first pings (27% to 42%) and half is worse rescue (20% to 27%). 42 of 48 before and 40 of 49 after had only one ping sent, which probably means only one responder was available (to confirm).
- Pings outside a responder's home area went from 17% to 39%, and takes outside it from 0 of 831 to 86 of 391. Cause unknown: proximity working, or a side effect of the four going quiet.
- Ashgrove and Halfmoon's quiet looks like demand (their areas fell about 30%). The four silent ones are in areas that fell only 11-18%. Tension: 4.2 lowered the acceptance weight, which should soften the penalty, yet four collapsed, so the loop story needs real scores.
- Still needed: answer times, score history, prior-year numbers, data after 6 Sep, and who was available on the one-ping callouts.

- Routing code walkthrough (Module 4): offer, then score (proximity, recent acceptance, capability), then rank, push, 60s wait, and a score change. A yes is +0.08, a no or a miss is -0.12, and scores never fade. The availability, travel-time and phone-push functions are blank placeholders in the folder.
- Replaying each responder's pings through those rules (an estimate, starting at 0.5): only the four silent responders reach 0. The break-even failure rate is 40%, and average failure rose from about 23% to about 36%, so ordinary responders are now close to the edge.
- Both 4.2 briefs were built exactly (missed pings now move on at 61-63s, not 91-93s), but they were one line each with no goal. In the 11 unaffected areas the home responder's share of first pings fell from 80% to 72%, so no visible proximity benefit. The 14 Aug question on whether proximity applies to decliners is still unanswered.
- New: every "no" arrives within 40s, before and after 4.2 (184 and 84 cases). Speed alone may not explain misses going 2.3% to 18%; push delivery is an alternative. About 1 in 5 failed first pings had no second ping at all (42 of 236 before, 40 of 183 after).
- Open: answer times for yes, real score history, what the 4.2 duplicate-push fix changed, and who was available on one-ping callouts. Private artifact "The Silent Four" (https://claude.ai/artifact/VSSt7sfw6qSUdtbZy6f8Ks), source in `00-rook/silent-four-case-file.html`.
- Superseded: "timeout cut is very likely the main mechanism" (Module 1 wiki and database read, and the Module 3 working theory order) is now unproven, because of the 40s ceiling on refusals. Likewise the Module 3 "tension" about the lowered acceptance weight is mostly resolved: the weight only caps how much a bad score can cost (about 19 minutes of travel), and the miss count drives the loop.
- Full detail: 04-x-ray-vision/session-notes.md (2026-10-20).

- Re-run of the 4.2 analysis (Module 3, 20 Oct): the 12.6-point fall in "taken" (76.6% to 64.0%) is about 8 points from the 12 responders who did not go quiet (77.0% to 68.1%, missed 2.1% to 13.9%) and about 5 from the four (75.5% to 23.2%, on 56 pings). The miss spike is wide: all 16 responders, all 15 areas, all day-parts and weekdays, starting 09:04 on 12 Aug.
- The extra untaken callouts are outside the quiet responders' own areas (5.4% to 13.0%; inside them 5.7% to 5.0%). First ping to the callout area's own responder fell 80% to 61% (72% in areas with no quiet responder), the opposite of the proximity goal.
- 4.2 shipped six changes: wait 90 to 60s, ranking weights, filter persistence, and three defect fixes (duplicate push, tag order, export time zone: 5 tickets before, 0 after). Availability Confidence was committed for 4.2 but is not in the release notes, so it did not ship.
- Support: 12 of 15 handlers filed routing tickets. Old-topic tickets are also piling up (0 of 38 open before, 30 of 44 now), and 27 of 107 after-tickets reuse a pre-4.2 subject, so "other" tickets are not a clean signal.
- Open: "yes" answer times, push delivery logs, real scores, and any data after 6 Sep (today is 20 Oct). Decision reading in `00-rook/4-2-impact-analysis.md`: no whole-release rollback, test the 90s wait on part of the traffic, check or reset the four's scores.
- Superseded: the Module 3 chat claim that the four silent responders are "most of the damage" is now about one third; the wider miss spike is about two thirds.
- Full detail: 03-rewind/session-notes.md (2026-10-20).

- Score mechanics (Module 4, second part): one thing in the code adds points (a yes, +0.08) and one takes them off (any non-yes, -0.12), both in `history.py`. There is no decay, reset or bonus, so a month of silence changes nothing. From 0, about 7 yeses in a row reach neutral and 11 to 12 match a typical peer.
- Between 19 Aug and 6 Sep the four were still pinged about once a day (20 pings, 16 of them first choice, 11 in their home area), but 15 were missed, 4 turned down and 1 taken. A bad score costs at most about 17 to 19 minutes of travel, so a close responder can still rank first. The blocker is answering when asked, not being asked.
- My score replay has The Undertow near 0 on 5 Sep yet first pick that day: either proximity won or real scores differ. Staff engineer to confirm, and whether a handler override counts as a yes and whether scores survive a restart.
- Method that paid off: ask what the code does not do (no recovery, no miss-versus-no split, no answer-time or score log, no alert on silence, no handling of one-name lists, no check of how the two 4.2 changes interact).
- Superseded: "Four responders are effectively locked out" (draft leadership message in `00-rook/4-2-impact-analysis.md`) is too strong. They are still asked about once a day and fail 19 of 20.
- Full detail: 04-x-ray-vision/session-notes.md (2026-10-20, second part).

- Interviews vs tickets (Module 2, 20 Oct): interviews lead with "offers vanish" (3 of 4) and handler alerts (3 of 4); tickets lead with "phone quiet" (32 vs 13 vanished). No quiet or vanished ticket exists before 12 Aug, so Kip's "always lumpy" and Ambrose's "not the first time" read as an old problem but the record says new. Only Ambrose is in both piles.
- Interviews can't see the overloaded end (The Gale) and tickets can't either: nobody files about too much work. Handler alerts (2 of 4 interviews, 0 tickets) and dark mode (4 of 147 tickets) are loud in talk, small in tickets.
- Ticket groups (147): quiet 32, vanished 13, filters 16, other console 31, Supply and gear 26, account and admin 15, dark mode/badge text/alert sound 8, phone glitches 6 (all before 4.2, none after). 12 handlers filed tickets, not 15. Maintenance tickets after 4.2 (marathon-day booking, late reminders) disagree with Halloran's "scheduling improved".
- Open: why the four stay quiet (answer times, push logs, real scores from engineering), whether handlers really need a live-callout alert, and the Ambrose date mismatch (ticket 13 Aug "yesterday", interview 2 Sep "two weeks ago").
- Superseded: the Module 1 "Filter persistence: 12 tickets, 2 are thank-yous" is now 16 related tickets (14 after 4.2, 2 before), same 2 thank-yous; still small next to routing.
- Full detail: 02-super-hearing/session-notes.md (2026-10-20).

- Worries raised at the latest wrap-up (20 Oct): all data ends 6-7 Sep, six weeks stale, so current state is unknown. Q3 ended 30 Sep, so the "which cut features are still Q3 commitments" talk with the Director of Product is now overdue.
- Everything rests on one database (the CSV matches it exactly). Nobody has checked whether 4.2 changed how a "missed" ping is logged, which could mimic the jump to 28% on release day.
- Don't reset scores or restore the timeout on the penalty-loop theory alone until real scores are seen. Raise first with the engineering manager: callouts nobody took doubled, one-ping callouts (thin coverage?), and the "missed" definition.
- Supply safety flag for the Supply team: an 11-day wait on a cracked vest plate (Halloran) and an open vest plate ticket (Nightwell).

- Module 5 (20 Oct): the Director of Product, Helen, asked for a one-pager on what we'd build instead of quietly changing a number, seen from the person it happens to, ideally clickable. Engineering says the small fix could ship that afternoon. Her note names Marcus (role unknown) and Wen, who left a note in the code; I took that to be the 2019 TODO in `history.py`, which names no author. Kip is the handler for both Meteor Mite and The Gale (Eastgate).
- The brief (`05-super-speed/brief.md`) and a clickable prototype (`05-super-speed/prototype.html`, sample data) propose: a miss costs less than a refusal, scores ease back toward neutral and never above it, handlers see a Quiet marker with evidence and a Check in action that resets to neutral and logs in the 4.0 override log, and the responder is told they are still on the list. They deliberately do not promise offers, touch the 60s wait or proximity weights, or fix the wider miss spike (about two thirds of the fall in "taken", this addresses about one third).
- Open: how a handler is told (badge, digest or push), the "quiet" window (two weeks would fire near the end of August, after the 17 Aug first ticket), what "usual" is measured against, whether the console can show each responder's last yes and outcomes, and whether Check in needs the handler to confirm they spoke to the responder (a checkbox I added). The prototype's last yes, last outcomes and offer times are invented.
- The brief still needs the four's real scores first. If they aren't at the floor, it changes. Pitch to a responder: "You're still on the list, and we'll tell you what happened to your last few offers."
- Full detail: 05-super-speed/session-notes.md (2026-10-20).

- Module 6 (20 Oct): three project skills now exist in `.claude/skills/`: `meeting-recap` (decisions and owners from notes), `review-checklist` (a brief against four tests: owner, success measure, consistent scope, problem before fix) and `renew-reminders` (renews session-only reminders before their 7-day expiry). Only `review-checklist` has been run, once, on `05-super-speed/brief.md`: Needs changes (owner Fail; success and scope Partial; problem-before-fix Pass).
- Checks on that brief: its main figures match the database (the four took 3 of 40 first pings after 4.2 vs 175 of 247 before; 15 of 20 pings 19 Aug to 5 Sep missed). The "32 phone quiet tickets" measure is about 22 for the four and about 10 for Ashgrove and Halfmoon. Refusals held steady (about 21% to 18%) while yeses fell, which leans toward slow yeses or the 60s wait and away from push delivery. Not proven: no answer times or push logs.
- A Monday review of briefs is a session-only reminder (next run 26 Oct, about 9:43), with a one-shot renewal on 25 Oct. Both die if the session closes. Output goes to `06-sidekicks/scheduled-run-output.txt`, which already held a 13 Oct sample run over a `06-sidekicks/briefs/` folder that is not in the course folder. Writing outside the course folder stays off-limits, so skills are not in `~/.claude/skills/`.
- The Module 5 brief (`05-super-speed/brief.md`) was edited with the ticket and delivery findings; it still has no named owner and no success targets.
- Full detail: 06-sidekicks/session-notes.md (2026-10-20).
