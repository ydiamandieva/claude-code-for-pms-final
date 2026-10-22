# Bringing quiet responders back

**Owner:** [owner name], Dispatch PM · **For:** Helen · 22 Oct 2026 · Not yet checked with engineering · **Click-through:** [prototype.html](prototype.html)

## 1. Executive overview

Four responders are still asked about once a day, but they missed 15 of their last 20 offers. Our rules count a miss like a "no" and never forgive it, so they appear to be stuck low on the list (my estimate from the code, not the real scores). We want to build a way back: scores that heal, a "Quiet" tag for handlers, and a message that tells the responder they are still on the list. We need Helen's yes on the direction, and the real scores from engineering before anyone builds.

## 2. Decisions we need from Helen

| Decision | My recommendation |
|---|---|
| Hold [engineering's small fix: to confirm] until [date], when the staff engineer shares the real scores? If the scores are not in by [date], you decide again whether it ships. | Yes. If the real cause is the 60-second wait, a score change only softens the damage. |
| Go ahead with a way back for quiet responders, and build it only if the real scores show the four are at the bottom? | Yes, as set out in section 5. |
| Are these the right three things to measure (section 5)? The numbers get set later, after two weeks of data. | Confirm or change them. |

## 3. Decisions we need from other teams

| Team | Decision | Why it matters |
|---|---|---|
| Staff engineer | How much a miss costs, and how fast scores heal | The numbers are theirs to set. |
| Engineering manager | Can we test the 90-second wait on part of the traffic, alongside this plan? | It is the other lever. It runs next to this plan, not instead of it. |
| Kip and other handlers | How a handler should be told (badge, daily digest or push) | 3 of 4 handlers asked for an alert. |

## 4. The problem and why now

When a responder misses an offer, we treat it like a "no" and push them down the list. Points come back only from a "yes", and they never fade on their own. The four are still asked about once a day (20 pings, 19 Aug to 6 Sep), but 15 were missed. Healing scores gets them asked again. It does not make them faster to answer. That is what the wait test is for.

**Why now:** our data stops on 6 Sep, six weeks ago, so we do not know how the four are doing today. Each day we wait they may stay quiet, and engineering can ship [engineering's small fix: to confirm] any day.

## 5. The ideal state and the plan to get there

**Ideal state:** a responder who goes quiet is told they are still on the list, and one "yes" starts bringing them back. Their handler sees it the same day.

**What it looks like** (a sample, with invented details; [click through it](prototype.html)):
- **Kip, the day a responder goes quiet.** He opens the console and sees a **Quiet** tag on Meteor Mite: 4 pings this week, usually 11. He calls them, confirms they can take offers, taps **Check in**, and the tag clears.
- **Meteor Mite, the same day.** Their app says "You've had fewer offers lately. You're still on the list." After Kip checks in, it says Kip checked in. Offers still go to whoever is best placed, but a miss no longer costs them as much.

| Step | What happens |
|---|---|
| 1. Learn | Get the real scores, answer times and push logs, and data after 6 Sep. |
| 2. Decide | Set the numbers with the staff engineer and Kip. |
| 3. Build | A miss costs less than a "no". Scores heal toward neutral on their own, never above it. A **Quiet** tag shows when pings drop by half or most offers are missed. A **Check in** button resets a responder right away. It is only for the handler who has reached the responder and confirmed they can take offers, and each press is logged with the handler's name, so someone answers for a wrong one (my recommendation). The app says "You're still on the list." |
| 4. Measure | Test with the four and Kip, and check the measures below. |

**How this fits with the 60-second wait.** The wait may be the real cause, so we test it alongside this plan, not instead of it. If the real scores show the four are not at the bottom, or the answer times show the wait is the cause, we shrink or drop this plan.

| What we measure | Today (to 6 Sep) | Target |
|---|---|---|
| How soon a handler notices a quiet responder | About 3 days later, from a ticket | Same working day |
| Offers missed, per quiet responder, over a fixed 2-week window | The four: 58.9% missed (2.9% before 4.2) | Back toward their own rate before 4.2 |
| "Phone quiet" tickets about Farlight and The Undertow | 22 from 12 Aug to 7 Sep (27 days) | Fewer, per 27 days after launch |

The numbers for the last two get set after two weeks of data, against each responder's own rate before 4.2. I won't guess them. The ticket count covers two of the four, because Vesper and Meteor Mite filed none.

**It does not:** promise offers, change the 60-second wait or how much distance counts, fix the wider drop (this covers about one third of it), grade responders, or change what Rook Supply reads. It is for anyone who goes quiet. The four are the proof.

## 6. Supporting data

Source: Rook database (to 6 Sep) and 147 support tickets. The scores are my estimate from the code, not the real ones.

| The four quiet responders | Before 4.2 | After 4.2 |
|---|---|---|
| First-choice pings taken (the first person asked on each callout) | 175 of 247 (71%) | 3 of 40 (7.5%) |
| All pings taken (first-choice and later) | 75.5% | 23.2% |
| All pings missed | 2.9% | 58.9% |
| Pings missed, 19 Aug to 6 Sep | | 15 of 20 |

| Same area, Eastgate | Pings a day before | Pings a day after |
|---|---|---|
| Meteor Mite | 1.59 | 0.54 |
| The Gale | 1.86 | 2.65 |

| Who is in the drop | All pings taken |
|---|---|
| All 16 responders | 76.6% to 64.0% |
| The 12 others | 77.0% to 68.1% |
| The four | 75.5% to 23.2% |

- **Refusals held steady** (the four 21.6% to 17.9%, the other twelve 20.9% to 18.0%) while misses went up. That points at yeses running out of time in the 60-second window, not at phones failing. There are no answer times or push logs to confirm it.
- **Tickets:** 22 of the 32 "phone quiet" tickets are about Farlight and The Undertow. The other 10 are about Corporal Ashgrove and Halfmoon, whose quiet looks like falling demand, so this plan does not aim at them. Vesper and Meteor Mite filed none.

## 7. Open questions and who owns them

| Question | Owner |
|---|---|
| What are the real scores, and are the four at the bottom? | Staff engineer |
| Why do they miss: slow yeses, push delivery or phones? | Engineering manager |
| What has happened since 6 Sep? | Engineering manager |
| Does a handler's reset count as a "yes", and do scores survive a restart? | Staff engineer |
| Can the console show last yes and recent outcomes, and how big is the work? | Engineering manager |
| What counts as "quiet" (the window), and what is "usual" measured against? | Staff engineer and Kip |
