# Bringing quiet responders back

**Owner:** Yanita, Dispatch PM · **For:** Helen · 22 Oct 2026 · Not yet checked with engineering · [Click-through](prototype.html)

## 1. Executive overview

Four responders are still asked about once a day but missed 15 of their last 20 offers. A miss counts like a "no" and is never forgiven, so they appear stuck low on the list (my estimate from the code). We would add a way back for anyone who goes quiet: scores that heal, a **Quiet** tag and **Check in** button for handlers, and a message telling the responder they are still on the list.

**Scope:** what handlers and responders see when a responder stops getting jobs, and how they get back. The 60-second timer is a later decision.

The first decision we need from Helen is whether to hold engineering's small fix until the real scores are in. That is the one-number change engineering told Helen could ship in an afternoon, most likely lowering the 0.12 penalty that refusals and misses share. It is a blunter version of the first item in build step (3) (a miss costs less than a "no"): no separate cost for a miss, no healing, no Quiet tag, no Check in and no responder message. Like the build, it helps only if the real scores show the four at the bottom.

## 2. Decisions we need from Helen

| Decision | My recommendation |
|---|---|
| Hold engineering's small fix until the real scores are in (end date to be agreed with the staff engineer)? If not, you decide again. | Yes. If the 60-second wait is the cause, a score change only softens the damage. |
| Pursue a way back, and build it only if the real scores show the four at the bottom? | Yes. |
| Are the three measures in section 5 right? Numbers are set after two weeks of data. | Confirm or change. |

## 3. Decisions we need from other teams

- **Staff engineer:** how much a miss costs, and how fast scores heal.
- **Engineering manager:** could a 90-second test on part of the traffic run later, separate from this plan?
- **Kip and handlers:** how a handler is told (badge, daily digest or push).

**Set aside, not decided here:** the 60-second timer (a later decision), Availability Confidence (committed for 4.2, did not ship) and Rook Supply (reads the availability record, which this plan does not change). Owners are in section 7.

## 4. The problem and why now

Points come back only from a "yes" and never fade on their own. Healing scores gets the four asked again, but does not make them faster to answer. **Why now:** our data stops on 6 Sep, so we do not know how they are today, and engineering can ship the small fix at any time.

## 5. The ideal state and the plan to get there

**Ideal state:** a quiet responder is told they are still on the list, one "yes" starts bringing them back, and their handler sees it the same day. Kip sees **Quiet** on Meteor Mite, calls, then taps **Check in**.

**Plan:** (1) get real scores, answer times and data since 6 Sep; (2) set the numbers with the staff engineer and Kip; (3) build: a miss costs less than a "no", scores heal toward neutral (never above), **Quiet** shows when pings halve or most offers are missed, **Check in** resets the score to neutral and is only for a handler who has reached the responder, logged with their name (my recommendation), and the responder gets a message that they are still on the list; (4) measure.

If the real scores show the four are not at the bottom, or answer times show the wait is the cause, we shrink or drop this. It promises no offers and covers about one third of the wider drop.

| Measure | Today (to 6 Sep) | Target |
|---|---|---|
| Handler notices a quiet responder | About 3 days, from a ticket | Same working day |
| Offers missed per quiet responder, over a fixed 2 weeks | The four: 58.9% (2.9% before 4.2) | Back toward their own pre-4.2 rate |
| "Phone quiet" tickets about Farlight and The Undertow | 22 in 27 days | Fewer per 27 days |

## 6. Supporting data

Rook database to 6 Sep. The scores are my estimate from the code.

| The four quiet responders | Before 4.2 | After 4.2 |
|---|---|---|
| First-choice pings taken | 175 of 247 | 3 of 40 |
| All pings missed | 2.9% | 58.9% |

- **The drop** in pings taken (76.6% to 64.0%) is about one third the four and two thirds the other twelve.
- **Refusals held steady** (about 21% to 18%) while misses rose. That points at slow yeses, not phones failing, though there are no answer times or push logs yet.

## 7. Open questions and owners

| Question | Owner |
|---|---|
| Real scores: are the four at the bottom? Does a reset count as a "yes"? | Staff engineer |
| Why do they miss? What has happened since 6 Sep? Can the console show it, and how big is the work? | Engineering manager |
| What counts as "quiet", and what is "usual"? | Staff engineer and Kip |
| Is the small fix the shared 0.12 penalty, or another number such as the 60-second wait? When can the real scores be pulled, so the hold has an end date? | Engineering manager and staff engineer |
| How do Check in and healing fit together? Proposed: scores heal on their own; Check in is a one-time reset to neutral by a handler who has reached the responder, and healing carries on from neutral. | Staff engineer |
| Set aside: the 60-second timer | Engineering manager |
| Set aside: Availability Confidence (still a Q3 commitment?) | Helen |
| Set aside: Rook Supply and the availability record | Supply team, told first if the record changes |
