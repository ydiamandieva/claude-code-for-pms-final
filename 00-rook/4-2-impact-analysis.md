# Release 4.2 (12 Aug 2026): what happened, to whom, how big

Working notes for me only. Source tags: **[INT]** wiki Customer interviews (4) · **[TKT]** database `support_tickets` (147) · **[PING]** database `pings`/`callouts`/`responders` (29 Jun–6 Sep) · **[CODE]** `00-rook/code/dispatch-routing` · **[WIKI]** 4.2 release page and Q3 roadmap · **[CSV]** `00-rook/data/callout-history.csv`.
**O** = observed in the data. **I** = my inference. "Before" = before 12 Aug, "after" = 12 Aug onward (by timestamp). The week of 10 Aug mixes both.
Small sample, flagged once: 4 interviews, all console-redesign calls and not about routing.
The CSV's weekly sent and taken totals match `pings` exactly for all 10 weeks, so the CSV is not independent confirmation.

## Step 1. Interviews [INT]

| Theme (all 4 interviews, 2–5 Sep) | Raised by | Volunteered or asked? | Short quote | Intensity |
|---|---|---|---|---|
| Offer vanishes before the responder can answer | 3 of 4 (Dot, Ambrose, Halloran) | Dot and Ambrose volunteered. Halloran only on the closing "anything else?" | "he loses it more than he wins it" (Dot) | High (Ambrose also filed ticket 3043); low for Halloran |
| Work very uneven or very quiet, no explanation | 2 of 4 (Kip, Dot) | Kip volunteered. Dot was asked about quiet weeks | "Mite thinks Mite's been forgotten" (Kip) | High for Kip |
| Handler wants a louder or clearer alert | 3 of 4 (Dot, Ambrose, Kip) | Kip volunteered. Dot and Ambrose when asked for "one thing" | "harder to miss, not easier" (Ambrose) | Medium |
| Text too small | 2 of 4 (Dot, Ambrose) | Dot volunteered. Ambrose when asked for one thing | "Larger text on the status badge" (Ambrose) | Low |
| Filter persistence: liked, wants a reset warning | 1 of 4 (Ambrose) | Asked | "rather it warned me the filter had reset" | Low |

**Rank by count:** vanishing offers = louder alerts (3) > uneven work = small text (2) > the rest (1).
**Rank by intensity:** vanishing offers, then uneven work.
Dot had not connected the quiet weeks and the fast-vanishing offers until the interviewer asked about quiet weeks.
**Parked (outside Dispatch routing):** dark mode (Kip, said four times), capability tag legend (Ambrose), all Supply issues from Halloran (11-day vest plate wait, field failure reports "into a void", catalog search), and the positive note that Supply scheduling improved.

## Step 2. Tickets [TKT]
I read all 147 bodies. Themes come from subjects plus bodies and are mostly templated wording, so counts are approximate (O).

| Week starting | Total | Quiet phone | Offer vanished | Filters | Other |
|---|---|---|---|---|---|
| 29 Jun–3 Aug (6 wks) | 6, 6, 8, 5, 7, 7 | 0 | 0 | 2 in all | rest |
| **10 Aug** | 20 | 0 | 7 | 3 | 10 |
| 17 Aug | 27 | 8 | 3 | 7 | 9 |
| 24 Aug | 32 | 12 (+1 first-ping-missed) | 2 | 2 | 15 |
| 31 Aug | 25 | 8 (+1) | 1 | 2 | 13 |
| 7 Sep (1 day) | 4 | 2 | 0 | 0 | 2 |

- **Before:** 40 tickets, all closed. **After:** 107 tickets, 83 open (24 closed). All 45 quiet and vanished tickets are open.
- **Totals after 12 Aug:** quiet 32 (incl. 2 "first ping in 5 or 9 days, and it was missed"), vanished 13, filters 14 (2 are thank-yous; earlier notes said 12, I count more broadly), other 48.
- **Timing (O):** vanished tickets come first (7 in the first 5 days, then fading). Quiet tickets start 17 Aug and peak the week of 24 Aug. That is about a 5-day lag.
- **By responder, after 12 Aug:**

| Responder | Tickets | Open | Quiet | Vanished |
|---|---|---|---|---|
| The Undertow | 17 | 15 | 11 | 0 |
| Farlight | 16 | 14 | 11 | 0 |
| Halfmoon | 12 | 9 | 5 | 1 |
| Corporal Ashgrove | 10 | 9 | 5 | 0 |
| Cindermark, Ironvale, Sgt. Falkirk, Nightwell | 6–8 each | | 0 | 2 each |
| The Drift, The Longcast, Stormwrack | 7 each | | 0 | 1 each |
| Captain Vantage | 1 | 1 | 0 | 1 |
| Vesper, Meteor Mite, The Gale, Sgt. Bulwark | 0 | | | |

- **Repeated wording (O):**
  - "Ping moved on while X was reaching for the phone" appears 4 times.
  - "phone buzzed, by the time i unlocked it, gone" appears 3 times.
  - "Lost one… happened more than once lately" appears 3 times.
  - "Is there a set amount of time before it moves on?" appears twice.
  - The quiet tickets share one template: "not like him at all… availability set correctly".
  - Farlight and The Undertow: "starting to wonder if im still even in the system".
- **Never filed (O):** Vesper and Meteor Mite filed zero tickets, though their pings fell about two thirds. Their handlers (Dot, Kip) raised it only in interviews. Nobody filed about callouts nobody took, about answer speed in seconds, or about uneven pay-off between responders.
- **Noise (I):** 27 of the 107 after-tickets reuse a pre-4.2 subject word for word under a different responder. The "other" bump (38 → 48) is not a clear signal.

## Step 3. Pings [PING]

| | Before (44 days) | After (26 days) |
|---|---|---|
| Taken | 76.6% (831 / 1,085) | 64.0% (391 / 611) |
| Turned down | 21.1% | 18.0% |
| Missed | 2.3% (25) | **18.0% (110)** |
| Callouts nobody took | 5.5% (48 / 879) | **11.1% (49 / 440)** |
| Pings per callout | 1.23 | 1.39 |
| Pings to a responder outside their usual area | 17% | 39% |
| Takes by someone outside their usual area | 0 of 831 | 86 of 391 (22%) |

- **The nobody-took-it flow (O, [PING]).** A callout pings responders one at a time until someone takes it:

| | Before | After |
|---|---|---|
| First ping failed (turned down or missed) | 236 of 879 (27%) | 183 of 440 (42%) |
| of those, first ping *missed* | 24 (3% of callouts) | 94 (21% of callouts) |
| Failed first ping rescued by a later responder | 188 (80%) | 134 (73%) |
| Failed first ping ended with nobody taking it | 48 (20%) | 49 (27%) |
| Untaken callouts that had only one ping sent | 42 of 48 | 40 of 49 |

  - Weekly share of callouts nobody took: 3–8% before, then 13%, 14%, 13% and 6% (week of 31 Aug).
  - **Split of the doubling (I, simple arithmetic):** if failed first pings had been rescued as often as before, nobody-took would have been about 8.5% after, not 11.1%. So roughly half the rise comes from more first pings failing and half from worse rescue. Only 48 and 49 callouts, so rough.
  - **Open question:** the code walks the whole list of available responders, so a one-ping ending most likely means only one responder was available (I). That points at availability as much as ranking. Staff engineer to confirm.
  - Visual of this and the home-area grid: [ping-geography.html](ping-geography.html), also published as a private artifact, "Ping blast map".
- **Weekly taken (O):** 77, 77, 76, 75, 78, 78, then 54, 66, 67, 73 (week of 31 Aug). Missed was 1–3% a week before and 21.5, 17.7, 14.8, 12.7% after. Recovering, not recovered.
- **Four responders (O).** Pings per day fell about 66–75% and about 53–64% of their remaining pings are missed:

| Responder | Pings/day before → after | Missed after |
|---|---|---|
| Farlight | 1.70 → 0.42 | 7 of 11 |
| The Undertow | 1.70 → 0.54 | 9 of 14 |
| Vesper | 1.95 → 0.65 | 9 of 17 |
| Meteor Mite | 1.59 → 0.54 | 8 of 14 |

  - Longest gap between pings after 12 Aug: 5–8.7 days (was about 2.5 days at most).
  - They were not heavy decliners before (15–29% turned down, the same range as everyone else).
  - For Farlight and The Undertow (the two I read ping by ping), the first misses came on 12–13 Aug, then pings thinned out.
  - Meanwhile the Gale (same area as Meteor Mite) went 1.86 → 2.65 pings/day and most others rose 15–42%.
- **The other 12 responders (O):** about 77–79% taken before, 58% in the 10 Aug week, then 71, 69, 74%. Missed per responder is 10–18%.
- **What it is NOT (O):**
  - **Time of day:** missed rose in all four day-parts (1.6–4.8% → 12.9–19.0%).
  - **Cascade position:** first ping missed 2.7% → 21.4%, second ping 0.5% → 9.8%.
  - **Geography:** callouts per day fell 20.0 → 16.9 (about -15%), and in every area but Southport (0%), by 5–32%. The four silent responders sit in four different areas that fell only 11–18%.
  - **Seasonality:** untestable. There is no prior-year data, and the break lines up with 12 Aug. July to early Aug was flat. Demand did dip about 15%, but the taken rate is not demand.
  - **The two quiet-but-not-collapsed responders (I):** Ashgrove's pings fell 22% and Halfmoon's 19%, close to their areas' demand fall (Northfield -32%, Westbury -30%). Their "quiet" tickets are probably demand, not the loop.

## Step 4. Release changes

"I am a ___, trying to ___, but I cannot because ___, which makes me feel ___"

| Release change | Statement | Interviews | Tickets | Pings | Verdict |
|---|---|---|---|---|---|
| **Ping wait 90s → 60s** | Responder, trying to answer an offer, cannot because it is withdrawn at 60s, feels they are losing a race they used to win | 3 of 4 | 13 vanished, 7 in the first 5 days | Missed 2.3% → 18%, up for all 16 responders | **Very likely the main driver of the miss spike (I).** Not proven: no answer-time data |
| **Ranking: proximity 0.45 → 0.60, recent acceptance 0.40 → 0.25** | Responder who has missed offers, trying to get pinged again, cannot because a miss counts as a decline (-0.12 vs +0.08) and scores never decay, feels forgotten | 2 of 4 (quiet, forgotten) | 32 quiet tickets, 4 responders | 4 responders -66–75% pings; 53–64% missed | **The silence is real (O). The loop mechanism is plausible (I, from [CODE]) but unproven.** Proximity effect itself is not isolated |
| **Console filters persist** | Handler, trying to keep filters between shifts, cannot because they sometimes reset silently, are shared per computer, or cannot be cleared; feels unsure the list is right | 1 of 4 (positive) | 14 (2 thank-yous), vs 2 asks before | n/a | **Real, small, a net positive.** Priya's "noise" call holds. Fixes: reset warning, clear-all, per-sign-in |

### Companion table: findings that did not fit

| Finding | Source | Note |
|---|---|---|
| Callouts nobody took doubled (5.5% → 11.1%) | [PING] | This is the actual incident impact. No ticket or interview mentions it. Roughly half is more failed first pings, half is worse rescue (I) |
| 42 of 48 untaken callouts before, and 40 of 49 after, had only one ping sent | [PING], [CODE] | The code walks the full available list, so probably only one responder was available (I). Staff engineer to confirm |
| Out-of-area pings 17% → 39%; before, none of 186 out-of-area pings were taken | [PING] | Cause unclear. May be a longer cascade after misses, not intended proximity behaviour (I) |
| **Tension in the loop story:** 4.2 *lowered* the acceptance weight, which should shrink the penalty's effect, yet four responders collapsed | [CODE], [PING] | Needs real scores and ranks from the staff engineer |
| Engineering manager asked on 14 Aug if proximity was meant to apply to decliners. No answer on the page | [WIKI] | Open question for the staff engineer |
| "Availability Confidence" is Committed for 4.2 on the roadmap but not in the 4.2 release notes | [WIKI] | Probably one of the squeezed-out features. Confirm with the Director of Product |
| Demand fell about 15% (callouts 137–144/wk → 110–127/wk) | [PING] | The one place "soft August" shows up, but it does not explain the taken rate |
| Vanished tickets arrive first, quiet tickets about 5 days later | [TKT] | Fits two stages of one problem (I) |

## Step 5. The story (5th-grade level)

When we launched 4.2, we gave responders less time to say yes. They used to get 90 seconds. Now they get 60. Many offers vanished before people could tap them.
Our system counts a missed offer like a "no." A few responders missed offers, and we think that pushed them down the list. Then they stopped getting offers at all. Four of them went almost silent. The others picked up the extra work.
So more jobs went to nobody. That number doubled. Things are getting a little better, but they are not fixed. Fewer people said yes, and the phones of those four stayed quiet. A slow August does not look like the main reason.

*The timeout and the score loop in this story are my inference. The numbers are observed.*

## Confidence (0–95)

| Group of numbers | Score | What would firm it up | Who has it |
|---|---|---|---|
| Ping outcomes before/after (76.6 → 64.0; missed 2.3 → 18.0) | 90 | Data after 6 Sep | Engineering manager |
| Four silent responders, work moved to others | 85 | Same, plus their actual scores | Staff engineer |
| Callouts nobody took doubled | 80 | Definition of "took" and any outside data | Engineering manager |
| Half-and-half split of that doubling | 35 | More weeks of data (only 48 and 49 callouts) | Engineering manager |
| Ticket counts and timing | 70 | Re-read by a second person. Keyword sorting | Support lead |
| Timeout cut as main cause of the miss spike | 70 | **Answer times** (seconds to answer) per ping | Engineering manager |
| Penalty loop explains the four | 55 | **Recent-acceptance score history** per responder | Staff engineer |
| Proximity weight effect | 25 | Ranking order before and after for sample callouts | Staff engineer |
| Seasonality as the cause | 15 | Prior-year Aug–Sep acceptance | Engineering manager |
| Interview themes | 40 | Interviews with the four silent responders' handlers and responders | Support lead, Dot, Kip |

**Data we don't have (and who to ask):**
- Answer times per ping: engineering manager.
- Score values and rank order: staff engineer.
- Who was available for the callouts that got only one ping: staff engineer.
- Prior-year numbers: engineering manager.
- Anything after 6–7 Sep, including whether September recovered: engineering manager.
- How "acceptance rate" is defined: engineering manager.
- Which features were cut from 4.2: Director of Product.
- Responders' own account of what they see: handlers via the support lead.

## Reading for my three decisions (I, mine to confirm)
1. **Rollback:** the evidence points at the timeout. Restoring 90s is the cheapest test and does not undo the proximity change. A rollback of 4.2 as a whole is not supported by this data.
2. **Leadership message:** "Fewer offers are being answered because of how 4.2 interacts with how we score misses. Four responders are effectively locked out. We are testing the timeout first."
3. **Fix plan:** short term, restore the timeout and have support reply to the 45 open tickets. Medium term, decide whether a miss should count the same as a decline, and add score decay (the 2019 TODO). Long term, expose answer times and per-responder scores so this is visible before tickets arrive.
