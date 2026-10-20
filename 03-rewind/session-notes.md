# Session notes

## 2026-10-20

### Questions and answers

**1. Open `00-rook/data/callout-history.csv`. What changed after 4.2 (12 Aug)? Show the weekly numbers before and after and the rows used.**
The file has 160 rows: 16 responders for each of 10 weeks (29 Jun to 31 Aug). Summed across responders, the share of pings taken was flat at 75.0 to 77.9% for six weeks, then 54.2% (week of 10 Aug, which contains the release), then 65.8%, 66.7% and 72.7%. Six pre-weeks: 794 taken of 1,034 sent (76.8%). Three full post-weeks: 332 of 485 (68.5%). Four responders (Vesper, The Undertow, Meteor Mite, Farlight) went from 11 to 14 pings a week to 0 to 5. The week of 10 Aug straddles the release (2 days before, 5 after), so the weekly file cannot split it. One row (Farlight, week of 31 Aug) has 0 pings sent; I read it as a real zero. The chat answer said "four responders account for most of the damage". That was too strong; see Reversals.

**2. The student pasted a starter prompt: interview me one question at a time until 95% confident, then play back a one-table brief and wait. Then run Steps 1 to 5 (interviews, tickets, pings, a table per release change, a 5th-grade story with confidence scores).**
Seven questions were asked, one at a time, each followed by a confidence figure (30, 50, 58, 66, 74, 80, 88, 95%).
- Decisions it serves: roll back or not; what gets communicated to leadership; short- and long-term fixes and development work.
- Audience: the student only, for now.
- Hunch: none fixed. The student trusts the data and user feedback.
- Format: a Markdown file in this folder. Build on and update the earlier analysis instead of starting again.
- In scope: rollback recommendation, short- and long-term fixes, side issues (Supply, filters, console asks), and `callout-history.csv`. The leadership message was not ticked, so it was left out.
- Extra instruction in place of naming sources: "cover every change from 4.2 release".
The brief was played back, the student confirmed, and analysis started.

**3. Run the analysis.** Result: `00-rook/4-2-impact-analysis.md`, rewritten. Short version:
- All 4 interviews read in full and re-scored (volunteered vs asked). All 147 ticket bodies read. Ping, callout and responder tables re-queried from scratch.
- 4.2 had six shipped changes, not three: wait 90 to 60 s, ranking weights (proximity 0.45 to 0.60, recent acceptance 0.40 to 0.25), filter persistence, and three defect fixes (duplicate push when a ping is sent again, capability tag order, time zone on coverage export). A seventh item, Availability Confidence, was committed for 4.2 on the Q3 roadmap but is not in the release notes, so it did not ship.
- Missed pings rose from 2.3% to 18.0% and taken fell from 76.6% to 64.0%. It is a step on the release morning (first miss 09:04, 12 Aug), across all 16 responders, all 15 areas, all four parts of the day, all seven weekdays.
- Decisions: do not roll back 4.2 as a whole; test the 90 second wait on part of the traffic; get "yes" answer times and push logs; ask for the four's real scores to be checked or reset. Full wording is under Decisions.

### Findings

- **Observed (`pings`, 29 Jun to 6 Sep):** taken 76.6% (831 of 1,085) before, 64.0% (391 of 611) after. Missed 2.3% to 18.0%. Turned down 21.1% to 18.0%. Callouts per day 20.0 to 16.9 (-15%).
- **Observed:** release-day step. Missed share by day: 5 to 11 Aug 2.6, 0, 0, 4.3, 0, 0, 5.3%; 12 Aug 28.0% (7 of 25); 13 Aug 48.0% (12 of 25); 14 Aug 26.7%; 15 Aug 25.0%; 16 Aug 18.2%.
- **Observed:** the miss rise is not time of day (night 4.8 to 12.9%, morning 1.6 to 18.4%, afternoon 1.8 to 17.5%, evening 2.5 to 19.0%), not weekday (0.7 to 4.1% before, 13.2 to 22.5% after), not cascade position (first ping 2.7 to 21.4%, second 0.5 to 9.8%), and not geography (every one of 15 areas rose, from 0 to 6% to 10 to 32%).
- **Observed:** where the fall in "taken" comes from. The 12 other responders: 77.0% to 68.1% taken, missed 2.1% to 13.9%, on 779 to 555 pings. The four quiet ones: 75.5% to 23.2% taken, missed 2.9% to 58.9%, on 306 to 56 pings. Counterfactual arithmetic (inferred): the 12's slide costs about 8 of the 12.6 points, the four's collapse about 5.
- **Observed:** callouts nobody took 5.5% (48 of 879) to 11.1% (49 of 440). About 25 extra in 26 days if the old rate had held (inferred, small numbers). The rise is outside the quiet responders' own areas: 5.4% to 13.0% in the 12 other areas (37 of 685 to 44 of 339), and 5.7% to 5.0% in Uptown, Old Town and Harborside (11 of 194 to 5 of 101).
- **Observed:** first ping goes to the callout area's own responder 80.4% to 60.9% of the time. In Uptown, Old Town and Harborside 79.9% to 16.8%. In Eastgate (Meteor Mite and The Gale) 83.1% to 84.2%. In the other 11 areas 80.1% to 72.0%. Proximity weighted up should raise this, not lower it, although "home area" is only a rough stand-in for distance.
- **Observed:** out-of-area pings 17.1% (186) to 39.4% (241); out-of-area pings that were taken 0 of 186 to 86 of 241. Cause unknown.
- **Observed:** the four took 175 of 247 first pings before (28.1% of all first pings) and 3 of 40 after (9.1% of all first pings). After 12 Aug they were pinged 11, 14, 14 and 17 times. Average gap between pings rose from about 0.5 to 0.6 days to 1.2 to 1.8 days, longest gap 5.2 to 8.7 days.
- **Observed:** a missed ping's next ping goes out 91 to 93 s later before 12 Aug and 61 to 63 s later after. Every refusal took 6 to 40 s, before (184 cases, median 22 s, 90th percentile 37 s) and after (84 cases, median 23 s, 90th percentile 36 s).
- **Observed (`support_tickets`, 147 bodies read, grouped by me from subject and body, counts approximate):** 40 before (all closed), 107 after (83 open). 45 routing tickets since 4.2, none before: 13 "offer vanished" (7 in the first five days, 9 responders) and 32 "phone quiet" (Farlight 11, The Undertow 11, Corporal Ashgrove 5, Halfmoon 5). 12 of 15 handlers filed at least one routing ticket. All 45 are open.
- **Observed:** filter persistence, 14 tickets (silent reset 4, shared or other computer 4, cannot clear all 2, badge too faint 2, thank-yous 2) against 2 asks before. Defect-fix topics: 5 tickets before (3007, 3016, 3040, 3019, 3025), 0 after.
- **Observed:** old-topic tickets also pile up: 0 of 38 open before, 30 of 44 open now. 27 of 107 after-tickets reuse a pre-4.2 subject line, 15 have an identical body. "Other" tickets about 6.0 a week before, 12.4 after: not a clean signal.
- **Observed ([INT], 4 interviews):** vanishing offers 3 of 4 (Dot, Ambrose, Halloran); uneven or quiet work 2 of 4 (Kip, Dot); alerts 3 of 4; small text 2 of 4; dark mode, filters and tag legend 1 each. Only one interviewed handler (Ambrose) also filed a routing ticket.
- **Inferred, confidence 40/95:** the wait cut as the main cause of the miss spike. The change is real, and the timing fits, but no refusal ever took more than 40 s, so a 60 s window looks long enough for people who say no. "Yes" times cannot be seen.
- **Inferred, confidence 50/95:** the miss-counts-as-decline score loop explains why the four got fewer pings. A rebuilt score (everyone at 0.5 on 29 Jun) puts the four at 0.00 by early Sep and everyone else at 0.28 or more. This is an estimate, real scores are not in the database.
- **Inferred, confidence 20/95:** the proximity change helped or hurt. Built as briefed; the intended gain is not visible; harm not isolated.
- **Inferred, confidence 15/95:** the "duplicate push when a ping is sent again" fix changed push delivery and so added misses. Untested.
- **Inferred, confidence 10/95:** seasonality. No prior-year data. The step begins on the release morning and six weeks before it were flat.
- **Not shipped:** Availability Confidence (roadmap, Committed, target 4.2, last reviewed 30 Jun; not in the 4.2 release notes).
- **Small and unconfirmed:** four maintenance tickets since 4.2 (two booked on the marathon day, two reminders after the date), none before. Routing never writes availability.

### Reversals

- **Weakened:** "the timeout cut is very likely the main driver, confidence 70" (earlier version of `00-rook/4-2-impact-analysis.md`; also the Module 1 and Module 3 lines in CLAUDE.md). Now 40. Evidence: no refusal over 40 s in either period. The Module 4 notes (`04-x-ray-vision/session-notes.md`) reached the same view from the same data and say that file "was not edited in this session". It has since been rewritten (this session), and the rewritten file holds the lower figure.
- **Corrected:** "four responders account for most of the damage" (my chat reply to the first question, from the weekly CSV). The 12 responders who did not go quiet account for about two thirds of the fall in "taken"; the four for about one third.
- **Moved:** the miss-counts-as-decline loop sat in the "proximity" row of the old Step 4 table. It is old code (`history.py`), not a 4.2 change, so it is now in the companion table. The three 4.2 changes in CLAUDE.md became six shipped changes plus one unshipped.
- **Extended:** the earlier line "roughly half the doubling of untaken callouts is more failed first pings and half worse rescue" now has a location: the extra untaken callouts are outside the quiet responders' own areas, so they come from the wide miss spike, not from the four going quiet.
- **Not reversed, still open:** the Module 3 "tension" that 4.2 lowered the acceptance weight yet four collapsed. The Module 4 notes treat it as mostly resolved (the weight only caps the cost of a bad score). I left it open in the rewritten file until real scores are seen.

### Queries and checks that mattered

All against the Rook database (`pings`: callout_number, responder, sent_at, outcome; `callouts`: callout_number, happened_at, area; `responders`: name, handler, area; `support_tickets`).

Weekly CSV numbers (Python, standard library only): read the 160 rows, sum `pings_sent` and `pings_taken` by `week_starting`. Weeks 29 Jun to 3 Aug are "before", 17 to 31 Aug "after", 10 Aug "straddle".

Before and after outcomes, and the split between the 12 others and the four:

    select (sent_at >= '2026-08-12') after, (responder in ('Farlight','The Undertow','Vesper','Meteor Mite')) four,
      count(*) pings, sum((outcome='taken')::int) taken, sum((outcome='turned down')::int) declined, sum((outcome='missed')::int) missed
    from pings group by 1,2 order by 2,1

Gap after each ping (a missed ping gives the wait, a refusal gives the answer time):

    with g as (select callout_number, sent_at, outcome, lead(sent_at) over (partition by callout_number order by sent_at, responder) nxt from pings)
    select (sent_at >= '2026-08-12') after, outcome, count(*), min/median/p90/max of extract(epoch from nxt-sent_at)
    from g where nxt is not null group by 1,2

Callouts nobody took, by area group:

    with c as (select c.callout_number, c.happened_at, c.area, sum((p.outcome='taken')::int) taken from callouts c join pings p using (callout_number) group by 1,2,3)
    select (happened_at >= '2026-08-12') after, case when area in ('Uptown','Old Town','Harborside') then 'quiet three' else 'other' end grp,
      count(*), sum((taken=0)::int) from c group by 1,2

First ping to the home responder: number pings in each callout with `row_number() over (partition by callout_number order by sent_at, responder)`, keep position 1, join `responders` and `callouts`, and compare `responders.area = callouts.area`, split before and after and by area group.

Score replay (estimate): a recursive query per responder, starting at 0.5 on the first ping, adding 0.08 for taken and subtracting 0.12 for anything else, clamped to 0 to 1 (rules from `00-rook/code/dispatch-routing/config.py` and `history.py`).

Tickets: grouped with regular expressions on `subject` (vanished: "moved on while", "callout moved on", "gone before", "vanished before", "lost one"; quiet: "has not gone off", "hardly anything", "quieter than usual", "still very quiet", "nothing coming through", "still on the list", "asked me to pass this on"; filters; maintenance), then counted by week, responder and status. Re-use check: `exists (select 1 from support_tickets b where b.filed_at < '2026-08-12' and b.subject = a.subject)` gives 27, same with `b.body = a.body` gives 15.

Cross-check: Farlight's ticket 3071 (20 Aug) says 4 pings in 7 days and The Undertow's ticket 3073 says 6. The ping table gives 4 and 6.

### Decisions and recommendations

(Proposals for the student to confirm; nothing was sent to anyone.)
1. Do not roll back 4.2 as a whole. Test the wait: "Restoring 90 seconds is one constant in `config.py`... Ask engineering whether it can run on half the callouts (or alternate days) so the result is clean." If misses return to about 2%, the wait was the cause; if not, push delivery and the four's phones come first.
2. Do not touch the proximity weights until someone has seen real scores and ranks.
3. Pull data since 6 Sep first. Six weeks have passed.
4. Short term: "Get 'yes' answer times and push delivery logs for 12 Aug onward." "Ask the staff engineer to reset the four quiet responders' recent-acceptance scores to neutral, or to confirm they are at the floor." Support replies to the 45 open routing tickets; reach Vesper and Meteor Mite through their handlers (Dot, Kip), since they filed none.
5. Long term: treat a miss differently from a refusal and let scores ease back (the 2019 TODO in `history.py`); log answer time and push delivery per ping; make rank and score visible; alert when a responder's pings fall by half over two weeks (would have fired around 15 Aug, two days before the first quiet ticket on 17 Aug); settle what proximity does for responders who turn jobs down (the engineering manager's unanswered 14 Aug question); console asks that predate 4.2 (reset warning and clear-all for filters, dark mode, larger badge text, different alert sounds); tell the Supply team first if the shape of the availability record changes.
6. Leadership message: not drafted (out of scope this round).

### Files and artifacts made

- `00-rook/4-2-impact-analysis.md`: rewritten with Steps 1 to 5, the per-change table, the companion table, confidence scores and the decision reading. It was swept into the Module 4 wrap-up commit (0277638) because that session saved while this one was running, so the earlier version is in git history (commit c22ebb3).
- `03-rewind/prompts.md`: four prompts added (14 to 17).
- `03-rewind/session-notes.md`: this file.
- `CLAUDE.md`: short summary added at the end of Working context.
- No new artifact was published this session. Earlier private artifacts: "Ping blast map" (https://claude.ai/artifact/BRznK5T3qmzMHcFeo2ZZNX) and "The Silent Four" (https://claude.ai/artifact/VSSt7sfw6qSUdtbZy6f8Ks). Both are private by default and were not changed.

### What we couldn't see

- How long a "yes" takes. Taken pings end the callout, so there is no next ping to measure against.
- Real recent-acceptance scores and rank order per callout. The replay is an estimate that assumes everyone started at 0.5 on 29 Jun.
- Push delivered and opened times, device types, and whether 4.2 rolled out to everyone at once.
- Anything after 6 to 7 Sep. Today is 20 Oct.
- Prior-year numbers, so seasonality can't be tested.
- Who was available on the one-ping callouts (42 of 48 untaken before, 40 of 49 after).
- Ticket groups are my own, from subject and body. Wording is templated.
- Small groups: 4 interviews, 56 pings for the four after 12 Aug, 48 and 49 untaken callouts.
- Real personal data: the interview transcripts and ticket data include people's full names. I kept them out of these notes and refer to handlers by the first name or short name used in the wiki and to responders by their cover names.

### Open questions

- Engineering manager: "yes" answer times and push delivery logs for 12 Aug onward; how 4.2 rolled out; data since 6 Sep; prior-year Aug to Sep; how "acceptance rate" is defined.
- Staff engineer: real scores and ranks for the four; whether proximity was meant to apply to responders who turn jobs down (unanswered since 14 Aug); who was available on the one-ping callouts; whether the duplicate-push fix changed delivery.
- Director of Product: which features were cut from 4.2 (Availability Confidence looks like one) and which Q3 items are still commitments.
- Support lead: their own running count of the two ticket themes (their 26 Aug split was "two thirds to one third"; my count that day was 14 to 11); why old-topic tickets now sit open; the quiet responders' own account.
- Supply team (name unknown): whether the four maintenance tickets relate to anything 4.2 changed.

### Start here next time

Ask the engineering manager for two things at once: the "yes" answer times and push logs since 12 Aug, and ping data since 6 Sep. They settle whether the wait is the cause and whether the problem is still there.
