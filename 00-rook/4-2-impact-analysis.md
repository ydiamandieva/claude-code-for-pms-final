# Release 4.2 (12 Aug 2026): what happened, to whom, how big

Working notes for me only. Re-run on 20 Oct 2026 from the raw sources, building on the earlier version.

**Source tags:** **[INT]** wiki Research > Customer interviews (4, read in full) · **[TKT]** database `support_tickets` (147, every body read) · **[PING]** database `pings` / `callouts` / `responders` (29 Jun to 6 Sep) · **[CODE]** `00-rook/code/dispatch-routing` · **[WIKI]** 4.2 release page, Releases, Q3 roadmap · **[CSV]** `00-rook/data/callout-history.csv`.
**O** = observed in the data. **I** = my inference. "Before" = pings, callouts and tickets before 12 Aug 00:00 (44 days). "After" = 12 Aug onward (26 days of pings, 27 of tickets). The groups are unequal, so I compare rates, not counts. The week of 10 Aug mixes both.
**Small sample, flagged once:** 4 interviews, all console-redesign calls and not about routing. Several other groups are small too (for example 56 pings for the four quiet responders, 48 and 49 untaken callouts). They carry their numbers in the tables.
**[CSV] is not a second source.** Its weekly sent and taken totals equal `pings` for all 10 weeks.
**Data stops on 6 to 7 Sep. Today is 20 Oct.** I cannot say whether things recovered since.

**What this version changes from the earlier one**
- Adds every 4.2 change: six that shipped (wait, ranking, filters, three defect fixes, not just the first three) plus one committed item that did not.
- Corrects the split of the damage: the 12 responders who did *not* go quiet account for about two thirds of the fall in "taken", the four quiet ones for about one third (see Step 3).
- Lowers my confidence in "the timeout cut is the main cause" from 70 to 40. New evidence: refusals never took longer than 40 seconds in either period (see Step 3).
- Moves the miss-counts-as-decline loop out of the "proximity" row. It is old code, not a 4.2 change.
- Drops the leadership-message draft (out of scope this round).

---

## Step 1. Interviews [INT]

Four calls by the product designer, 2 to 5 Sep, each with the handler of one or two responders. Topic was the console redesign.

| Theme | Raised by (of 4) | Volunteered or asked? | Short quote | Intensity |
|---|---|---|---|---|
| Offer vanishes before the responder can answer | 3: Dot (Vesper), Ambrose (Captain Vantage), Halloran (Sgt. Bulwark) | Dot and Ambrose volunteered it. Halloran only on the closing "anything else?" | "he loses it more than he wins it" (Dot) | High for Dot and Ambrose ("the closest-run I've seen"). Low for Halloran ("these things happen") |
| Work very uneven or very quiet, no explanation | 2: Kip (Meteor Mite and The Gale), Dot | Kip volunteered. Dot only when asked about quiet weeks | "Mite thinks Mite's been forgotten" (Kip) | High for Kip. Dot "hadn't really put those two things next to each other" |
| Wants a louder, clearer or different alert | 3: Ambrose, Dot, Kip | Ambrose and Kip volunteered. Dot when asked for one change | "harder to miss, not easier" (Ambrose) | Medium. The three asks differ: more visible live badge, a handler alert, a different sound per responder |
| Text too small | 2: Dot, Ambrose | Dot when asked about layout. Ambrose when asked for one change | "Larger text on the status badge" (Ambrose) | Low |
| Dark mode | 1: Kip | Volunteered, four times | "Dark mode. I am begging." | High, but console comfort only |
| Filter persistence: liked it, wants a reset warning | 1: Ambrose | Asked | "I'd rather it warned me the filter had reset" | Low |
| Capability tag legend hard to find | 1: Ambrose | Asked what he hunts for | "It sits in a drawer off the responder detail panel" | Low |

- **Rank by count:** vanishing offers = alerts (3), then uneven work = small text (2), then the rest (1).
- **Rank by intensity:** vanishing offers, then uneven work and dark mode.
- **Not asked, not said (O):** no one mentioned a number of seconds, a callout that nobody took, or distance. Ambrose: "I couldn't give you seconds."
- **Leading questions (O):** the designer asked Dot about "quiet weeks" and asked Ambrose "how far into getting ready" he was. Both answers may be shaped by that.
- **Who they speak for (O, [PING], [TKT]):** Vesper and Meteor Mite are two of the four quiet responders. Captain Vantage and Sgt. Bulwark are not quiet, but their handlers still told the vanishing-offer story. Only the quiet ones' handlers mentioned quiet weeks.
- **Date wobble (O):** Ambrose says "two weeks ago" on 2 Sep, but his ticket 3043 (13 Aug) tells the same story, "coat and one boot on", as "yesterday evening" (12 Aug). Likely the same night, remembered loosely.
- **Parked (outside Dispatch):** all Halloran's Supply points. Requisition queue (11 days for a cracked vest plate, priority field does nothing), field failure reports "into a void", equipment catalog search ("plate" gives forty results), and a positive note that maintenance scheduling got smarter.

## Step 2. Tickets [TKT]

I read all 147 bodies. I grouped them myself from subject plus body. Wording is mostly templated (same sentence, new name and number), so counts are approximate (O).

**Groups, before vs after (my grouping)**

| Group | Before (40 tickets, 44 days) | After (107 tickets, 27 days) |
|---|---|---|
| Routing: offer vanished (13) + phone quiet (32) | 0 | 45 |
| Filter persistence | 2 asks | 14 (12 issues or asks, 2 thank-yous) |
| Console UX asks (dark mode, text size, alert sound, layout, logout, map) | 14 | 17 |
| Supply and gear (requisitions, gloves, masks, boots, billing) | 12 | 17 |
| Account and admin (passwords, photo, phone number, exports, second login, leave status) | 7 | 14 |
| Topics the three 4.2 defect fixes target (duplicate push, tag order, export time zone) | 5 | 0 |

**By week (Mon start)**

| Week | Total | Vanished | Quiet | Quiet, first one missed | Filters | Maintenance | Other | Open now |
|---|---|---|---|---|---|---|---|---|
| 29 Jun to 3 Aug (6 wks) | 6, 6, 8, 5, 7, 7 | 0 | 0 | 0 | 2 in all | 0 | rest | 0 |
| **10 Aug** (incl. 1 filed before the release) | 20 | 7 | 0 | 0 | 3 | 2 | 8 | 11 |
| 17 Aug | 27 | 3 | 8 | 0 | 7 | 0 | 9 | 16 |
| 24 Aug | 32 | 2 | 12 | 1 | 2 | 1 | 14 | 27 |
| 31 Aug | 25 | 1 | 8 | 1 | 2 | 1 | 12 | 25 |
| 7 Sep (one day) | 4 | 0 | 2 | 0 | 0 | 0 | 2 | 4 |

- **Timing (O):** the first vanished ticket (3041) came on 12 Aug at 15:41, seven hours after the first missed ping that morning. The first quiet ticket came on 17 Aug. Farlight's last ping before it was a "yes" on 14 Aug at 21:22, so "3 days" is accurate.
- **Open or closed:** before, 40 of 40 closed. After, 83 of 107 open. All 45 routing tickets are open. By group after: filters 6 open and 8 closed, maintenance 2 and 2, everything else 30 open and 14 closed. Tickets on old topics also pile up now (0 of 38 open before, 30 of 44 now), which suggests the support queue is saturated (I).

**By responder, after 12 Aug**

| Responder | Tickets | Open | Quiet | Vanished |
|---|---|---|---|---|
| The Undertow | 17 | 15 | 11 | 0 |
| Farlight | 16 | 14 | 11 | 0 |
| Halfmoon | 12 | 9 | 5 | 1 |
| Corporal Ashgrove | 10 | 9 | 5 | 0 |
| Ironvale, Nightwell, Sgt. Falkirk | 8 each | 7, 5, 6 | 0 | 2 each |
| Stormwrack, The Drift, The Longcast | 7 each | 5, 4, 4 | 0 | 1 each |
| Cindermark | 6 | 4 | 0 | 2 |
| Captain Vantage | 1 | 1 | 0 | 1 |
| Vesper, Meteor Mite, The Gale, Sgt. Bulwark | 0 | | | |

- **Reach (O):** 12 of the 15 handlers filed at least one routing ticket. The three who did not are Dot, Kip and Halloran, all of whom raised it in interviews instead.
- **Repeated wording (O):**
  - "Ping moved on while X was reaching for the phone... Is that expected?" ×4.
  - "phone buzzed, by the time i unlocked it, gone" ×3. "Lost one... happened more than once lately" ×3.
  - "Is there a set amount of time before it moves on?" ×2.
  - Quiet tickets come in eight templates: "has not gone off in N days, not like him at all" ×5, "Hardly anything... N pings in the past seven days" ×8, "much quieter than usual" ×5, "Still very quiet" ×4, "Nothing coming through since <date>" ×4, "Is X still on the list?" ×2, "starting to wonder if im still even in the system" ×2, "First one in N days and it was missed" ×2.
- **Filter persistence, 14 tickets (O):** silent reset or no warning 4, shared computer or other computer 4, cannot clear all 2, badge too faint 2, thank-yous 2.
- **Maintenance, 4 tickets, none before (O):** two "booked on the marathon day", two "reminder after the date". Four different responders, so small and unconfirmed. Routing code never writes availability.
- **Complaints nobody filed (O):**
  - Callouts that nobody took (doubled, see Step 3).
  - A job going to someone outside the responder's area.
  - The unfair split between The Gale (+42% pings) and Meteor Mite (-66%). Kip raised it only in his interview.
  - Anything about distance or the proximity change.
  - Vesper and Meteor Mite, the two quiet responders with no ticket at all.
- **Noise caution (O):** 27 of the 107 after-tickets reuse a subject line from a pre-4.2 ticket word for word, and 15 have a body identical to one. So the doubling of "other" tickets (about 6.0 to 12.4 a week) is not a clean signal.
- **Support lead's split (O):** on 26 Aug the page says "roughly two thirds quiet, one third gone". My count that day was 14 quiet and 11 vanished. Overall now it is 32 and 13. The direction is right; the 26 Aug proportion was not.

## Step 3. Pings [PING]

**Outcomes**

| | Before (44 days) | After (26 days) |
|---|---|---|
| Pings | 1,085 | 611 |
| Taken | 76.6% (831) | 64.0% (391) |
| Turned down | 21.1% (229) | 18.0% (110) |
| Missed | **2.3% (25)** | **18.0% (110)** |
| Callouts nobody took | 5.5% (48 of 879) | **11.1% (49 of 440)** |
| Pings per callout | 1.23 | 1.39 |
| Callouts per day | 20.0 | 16.9 (-15%) |

- **Weekly taken % (O):** 76.7, 77.1, 76.4, 75.0, 77.6, 77.9, then **54.2** (10 Aug), 65.8, 66.7, 72.7 (31 Aug). Weekly missed %: 1.7, 2.4, 3.4, 2.8, 2.4, 1.2, then 21.5, 17.7, 14.8, 12.7. Recovering, not recovered, and with no known fix.
- **Release day (O):** the first miss was at 09:04 on 12 Aug, matching "published on the morning of release". Missed share per day, 5 to 11 Aug: 2.6, 0, 0, 4.3, 0, 0, 5.3%. Then 12 Aug 28% (7 of 25), 13 Aug 48% (12 of 25), 14 Aug 27%, 15 Aug 25%, 16 Aug 18%. The jump is a step, not a slope.
- **How long the system waits (O):** when a ping is missed, the next ping goes out 91 to 93 seconds later before 12 Aug and 61 to 63 seconds later after. So the 90 to 60 change is real and shipped as written.

**Who: the split I got wrong before**

| | Pings before → after | Taken | Missed |
|---|---|---|---|
| The 12 other responders | 779 → 555 | 77.0% → 68.1% | 2.1% → 13.9% |
| The four quiet ones (Farlight, The Undertow, Vesper, Meteor Mite) | 306 → 56 | 75.5% → 23.2% | 2.9% → 58.9% |

- **Arithmetic (I, from the table):** if the 12 had held 77.0%, overall taken after would be about 72%, so their slide costs about 8 of the 12.6 points. If the four had held 75.5%, it would be about 69%, so their collapse costs about 5. The two overlap a little. The timeout-style miss spike is wide; the quiet four are a second, narrower effect.

**Per responder (O)**

| Responder | Pings per day | Taken % | Missed % | Average gap between pings (days) |
|---|---|---|---|---|
| Farlight | 1.70 → 0.42 | 73 → 18 | 4 → 64 | 0.56 → 1.63 (longest 5.2) |
| The Undertow | 1.70 → 0.54 | 77 → 21 | 1 → 64 | 0.59 → 1.77 (longest 8.7) |
| Vesper | 1.95 → 0.65 | 81 → 29 | 3 → 53 | 0.52 → 1.21 (longest 5.7) |
| Meteor Mite | 1.59 → 0.54 | 69 → 21 | 3 → 57 | 0.59 → 1.81 (longest 7.2) |
| Corporal Ashgrove | 1.43 → 1.12 | 78 → 66 | 2 → 14 | 0.70 → 0.87 |
| Halfmoon | 1.57 → 1.27 | 72 → 64 | 0 → 15 | 0.61 → 0.79 |
| The Gale | 1.86 → 2.65 | 78 → 70 | 5 → 12 | 0.54 → 0.36 |
| Nightwell | 2.16 → 2.69 | 76 → 67 | 3 → 11 | 0.45 → 0.37 |
| Stormwrack | 1.86 → 2.42 | 79 → 71 | 0 → 14 | 0.53 → 0.41 |
| Captain Vantage | 1.73 → 2.27 | 74 → 71 | 3 → 10 | 0.57 → 0.44 |
| Sgt. Falkirk | 1.43 → 2.00 | 79 → 69 | 3 → 15 | 0.68 → 0.51 |
| Cindermark | 1.30 → 1.62 | 79 → 69 | 2 → 12 | 0.75 → 0.61 |
| Ironvale | 1.16 → 1.50 | 76 → 67 | 2 → 18 | 0.85 → 0.66 |
| Sgt. Bulwark | 1.30 → 1.50 | 75 → 67 | 0 → 18 | 0.78 → 0.66 |
| The Longcast | 1.02 → 1.23 | 76 → 66 | 2 → 16 | 1.00 → 0.80 |
| The Drift | 0.89 → 1.08 | 85 → 64 | 3 → 18 | 1.12 → 0.96 |

- **Rows behind "four quiet" (O):** after 12 Aug they were pinged 11, 14, 14 and 17 times. Their share of all first pings went from 28.1% (247 of 879) to 9.1% (40 of 440). When they were the first ping, they took 175 of 247 (71%) before and 3 of 40 (8%) after.
- **Ashgrove and Halfmoon (I):** their areas' demand fell about 30% (Northfield -32%, Westbury -30%), close to their ping drop. Their "quiet" tickets are probably demand, not the same problem.
- **Callouts nobody took (O):**
  - First ping failed: 26.8% → 41.6% of callouts. First ping *missed*: 2.7% → 21.4%.
  - A failed first ping was rescued by a later ping 80% → 73% of the time.
  - Weekly share nobody took: 6.4, 5.8, 3.6, 8.3, 3.6, 2.9, then 12.7, 14.0, 12.9, 5.5 (31 Aug).
  - Where: in the 12 areas outside Uptown, Old Town and Harborside it went 5.4% → 13.0% (37 of 685 → 44 of 339). In those three it went 5.7% → 5.0% (11 of 194 → 5 of 101). So the extra untaken callouts did not happen where the quiet responders live.
  - Size (I, simple arithmetic): at the old 5.5% rate, 440 callouts would leave about 24 untaken, not 49. About 25 extra callouts nobody took in 26 days.
  - 42 of 48 before and 40 of 49 after had only one ping. The code walks the whole available list, so probably only one responder was available (I). Staff engineer to confirm.
- **Own area (O):**

| | Before | After |
|---|---|---|
| Pings to a responder outside their usual area | 17.1% (186) | 39.4% (241) |
| First ping went to the callout area's own responder | 80.4% | 60.9% |
| ...in Uptown, Old Town, Harborside (homes of Farlight, Vesper, Undertow) | 79.9% | 16.8% |
| ...in Eastgate (Meteor Mite and The Gale) | 83.1% | 84.2% |
| ...in the other 11 areas | 80.1% | 72.0% |
| Out-of-area pings that were taken | 0 of 186 | 86 of 241 (36%) |

  Proximity weighted *up* should raise the home share, not lower it. It fell even where nobody went quiet (80 → 72). That is the opposite of the hoped-for effect (O), but "home area" is only a rough stand-in for distance, and I cannot see the rank scores.

**Answer times, a proxy that exists (O).** The table has no answer-time column, but in a callout each ping is followed by the next, so the gap after a "no" is how long that "no" took. Gaps after a refusal: 6 to 40 seconds, median 22 before and 23 after, 90th percentile 37 and 36. No refusal ever took longer than 40 seconds, in either period, even when the window was 90. Taken pings end the callout, so "yes" times cannot be measured this way. If "yes" is as quick as "no", cutting 90 to 60 should not have created misses (I). A "yes" might take longer (read details, then swipe), which I cannot rule out.

**What it is NOT (O)**
- **Time of day:** missed rose in all four parts: night 4.8 → 12.9, morning 1.6 → 18.4, afternoon 1.8 → 17.5, evening 2.5 → 19.0.
- **Day of week:** missed was 0.7 to 4.1% each day before and 13.2 to 22.5% each day after.
- **Cascade position:** first ping missed 2.7 → 21.4%, second 0.5 → 9.8%, third 0 → 7.7%.
- **Geography:** missed rose in all 15 areas (0 to 6% → 10 to 32%). Demand fell 15% overall, in every area but Southport (0%), by 5 to 32%. The three quiet responders' areas fell only 11 to 18%.
- **Seasonality:** cannot be tested here. No prior-year data. But six flat weeks come before, the step begins on the release morning, and a 15% fall in demand should lower ping counts, not raise the missed share.
- **4.1 effects:** 4.1 (16 Jun: travel-time proximity, bulk callout, push reliability) landed before my data starts. It is part of the baseline.

## Step 4. One row per release change

"I am a ___, trying to ___, but I cannot because ___, which makes me feel ___"

| 4.2 change [WIKI] | Statement | Interviews [INT] | Tickets [TKT] | Pings [PING] | Verdict |
|---|---|---|---|---|---|
| **1. Ping wait 90 → 60 s** [CODE] | I am a responder, trying to answer an offer on my phone, but I cannot because it is withdrawn after 60 seconds, not 90, which makes me feel I am losing a race I used to win | 3 of 4 (Dot, Ambrose, Halloran). No one gave seconds | 13 vanished, 7 in the first 5 days, 9 responders, all open. 2 ask "is there a set amount of time?" | Missed 2.3 → 18.0%. Gap after a miss 91 to 93 s → 61 to 63 s. Up in all 16 responders, 15 areas, 4 day-parts. But no refusal ever took more than 40 s | **The change is real and the timing matches (O). Whether it *causes* the misses is plausible, not shown (I).** Needs "yes" answer times. Confidence 40 |
| **2. Ranking: proximity 0.45 → 0.60, recent acceptance 0.40 → 0.25** [CODE] | I am a responder who covers a wide area, trying to get the callouts nearest me, but I could not because far offers ranked as high as near ones, which made me feel overlooked | 0 mention distance. 2 of 4 describe uneven work | 0 mention distance. The 32 "quiet" tickets are about a different thing (no pings at all) | Home responder is first ping 80% → 61% (72% in areas with no quiet responder). Out-of-area pings 17 → 39% | **Built as briefed. The intended gain is not visible; harm is not isolated.** The earlier-flagged question (does it apply to responders who turn jobs down?) was never answered. Confidence 20 |
| **3. Console filters persist** | I am a handler, trying to keep my filters between shifts, but I cannot trust them because they reset silently, are shared per computer and cannot be cleared at once, which makes me feel unsure the list I am reading is right | 1 of 4 (Ambrose): liked it, wants a reset warning | 14 (12 issues, 2 thank-yous) vs 2 asks before; 8 closed, 6 open | n/a | **Real, small, a net positive.** Not linked to the drop. Fixes: reset warning, clear-all, per-sign-in |
| **4. Fix: duplicate push when a ping is sent again** | I am a responder, trying to answer a job once, but I cannot because my phone buzzed again after I said yes, which makes me feel confused | 0 | 3 before (3007, 3016, 3040), 0 after | n/a | **Fix looks to have worked (O: 0 after).** But it changes the push path, and misses are "no answer". A delivery side effect is possible and untested (I). Confidence 15 |
| **5. Fix: capability tag order in detail panel** | I am a handler, trying to check tags at a glance, but I cannot because they come in a different order each time, which makes me feel slowed down | 0 | 1 before (3019), 0 after | n/a | Fixed, tiny, no link to the drop |
| **6. Fix: time zone on coverage report export** | I am a handler, trying to hand over a coverage report, but I cannot because the times are out by hours, which makes me feel I cannot trust it | 0 | 1 before (3025), 0 after. Two later "availability hours use my time zone" tickets (3050, 3116) are a different feature | n/a | Fixed, tiny, no link to the drop |
| **7. Availability Confidence** (committed for 4.2 on the roadmap, absent from the release notes) | I am a handler, trying to know whether my responder is really reachable, but I cannot because the console shows only what is set, which makes me feel in the dark | 0 | All 32 quiet tickets say availability "is set correctly"; none mention this feature | n/a | **Did not ship (O: not in release notes), so cannot be a cause.** Only item squeezed out that I can see. Roadmap last reviewed 30 Jun. Ask the Director of Product |

### Companion table: findings that did not fit

| Finding | Source | Note |
|---|---|---|
| **A miss counts as a "no", and scores never ease back** (not a 4.2 change). Rebuilt from outcomes, starting everyone at 0.5 on 29 Jun, the four end at 0.00 by early Sep. No one else drops below 0.28 | [CODE], [PING] (replay is my estimate) | Real scores are not in the database. 4.2 cut the acceptance weight's reach from about 40 to about 19 minutes of travel, which should *soften* this, yet four collapsed. Needs real scores from the staff engineer |
| The four miss 59% of their pings and took 3 of 40 first pings | [PING] | They look unresponsive, not just unlucky. That fits something specific to them (phones, push delivery, habit, or answering slower than the others). Untested |
| The slide in the other 12 responders is about two thirds of the damage | [PING] | Corrects my earlier "four responders are most of it" |
| Misses are recovering (21.5 → 12.7% a week) with no fix shipped | [PING] | Maybe responders adapting, maybe fewer pings to the four. Still 5x the old rate |
| Out-of-area pings were never taken before (0 of 186), now 36% are | [PING] | Responders' behaviour changed, or the pings changed. Unexplained |
| Extra untaken callouts are outside the quiet responders' home areas | [PING] | Points at the wide miss spike, not at the four |
| Only one interviewed handler (Ambrose) also filed a routing ticket. 12 handlers filed, 1 was interviewed | [INT], [TKT] | The two piles are nearly different people. Same story from two ends |
| Tickets say "phone too quiet" (32); interviews say "offers vanish" (3 of 4) | [TKT], [INT] | Vanished tickets come first (12 to 16 Aug), quiet ones about 5 days later |
| Staff engineer was away 14 to 24 Aug, Priya left 21 Aug, the engineering manager's 14 Aug question was unanswered | [WIKI] | The first fortnight had no owner |
| The 26 Aug page blames the "August dip"; the data shows a step on release morning | [WIKI], [PING] | Opinion in the page, not data |
| Support queue: old-topic tickets now 30 of 44 open (0 of 38 before) | [TKT] | Worth asking the support lead |
| Maintenance tickets (4) and Supply link | [TKT], [CODE] | Unconfirmed. Supply reads the availability record; routing never changes it |
| Ambrose's date (2 weeks ago in Sep, 12 Aug in the ticket) | [INT], [TKT] | Same story, loose memory |

## Step 5. The story (5th-grade level)

On 12 August we made three changes. We gave responders less time to say yes. We changed who gets asked first. And we made the console remember filters.

Right away, more offers went unanswered. Before, almost none did. After, about one in five. This happened for every responder. It happened at every hour. It happened in every part of the city.

Four responders went almost silent. They used to get a call every day. Now they get one every few days. They are in four different places. When we did call them, most of the calls went unanswered. Our rules count an unanswered call like a "no," and a "no" pushes you down the list. So we think they slid down and could not climb back. We have not seen their real scores yet.

The wait is not the whole story. The people who said "no" always did it in 40 seconds or less. So 60 seconds should have been enough for them. We cannot see how long a "yes" takes.

More jobs went to nobody. That number doubled. It is getting a little better, but it is not fixed. A slow August does not fit. The drop started on the morning of the release.

*The cause, the score slide, and the push idea are my guesses. The counts are observed.*

## Confidence (0 to 95)

| Group of numbers | Score | What would firm it up | Who has it |
|---|---|---|---|
| Ping outcomes before and after (76.6 → 64.0; missed 2.3 → 18.0) | 90 | Data after 6 Sep | Engineering manager |
| Step on the release morning (first miss 09:04) | 88 | Exact release and rollout time | Engineering manager |
| The 12 others vs the four split of the fall | 80 | Same data, re-run on the full set | Engineering manager |
| Four quiet responders (volume, misses, gaps) | 85 | Their real scores and ranks | Staff engineer |
| Callouts nobody took doubled (5.5 → 11.1%) | 70 | Only 48 and 49 events; more weeks; definition of "took" | Engineering manager |
| "About 25 extra untaken callouts" | 50 | Same | Engineering manager |
| Home-area first-ping share fell (80 → 61%) | 80 as a count; 35 as "proximity isn't working" | Ranking order for sample callouts | Staff engineer |
| Ticket counts and timing | 75 | A second reader; I grouped by subject and body | Support lead |
| Interview themes | 40 | Calls with the quiet four's handlers about routing | Support lead, Dot, Kip |
| Timeout cut as main cause of misses | 40 | **Answer time of every "yes"; push delivery and open times** | Engineering manager |
| Score slide explains the four | 50 | **Real recent-acceptance score history** | Staff engineer |
| Proximity change, helped or hurt | 20 | Rank order before and after | Staff engineer |
| Defect fix on push changed delivery | 15 | Push delivered and opened timestamps | Engineering manager |
| Seasonality as the cause | 10 | Prior-year Aug to Sep acceptance | Engineering manager |

**Data we don't have, and who to ask**
- "Yes" answer times, and when each push was delivered and opened: engineering manager.
- Real score values and rank order per callout: staff engineer.
- Who was available on the one-ping callouts: staff engineer.
- Anything after 6 to 7 Sep, up to today: engineering manager.
- Prior-year Aug to Sep numbers: engineering manager.
- How "acceptance rate" is defined: engineering manager.
- Which features were cut from 4.2, and which Q3 items are still commitments: Director of Product.
- How 4.2 rolled out (all at once or in stages): engineering manager.
- The support lead's own running count of the two ticket themes: support lead.
- The quiet responders' own account, and what phones they use: handlers via the support lead (Dot for Vesper, Kip for Meteor Mite, then Farlight's and The Undertow's).
- Whether Supply's scheduler reads anything 4.2 changed: Supply team (name unknown).

## Reading for my decisions (I, mine to confirm)

**1. Roll back or not.**
- Do not roll back 4.2 as a whole. Filters, three fixes and the ranking change show no harm I can pin on them, and filters are a net positive.
- Do test the wait. Restoring 90 seconds is one constant in `config.py`, it is cheap, and it does not undo the ranking change. If misses fall back toward 2%, the wait was the cause. If they do not, push delivery and the quiet four's phones move to the top. Ask engineering whether it can run on half the callouts (or alternate days) so the result is clean.
- Do not touch the proximity weights until someone has seen real scores and ranks.
- First pull the data since 6 Sep. Six weeks have passed and the picture may already be different.

**2. Short term (a few days).**
- Get "yes" answer times and push delivery logs for 12 Aug onward. This is the single most useful new number.
- Ask the staff engineer to reset the four quiet responders' recent-acceptance scores to neutral, or to confirm they are at the floor. This is a data fix that works whatever the cause.
- Support replies to the 45 open routing tickets. Reach Vesper and Meteor Mite through Dot and Kip; neither filed one.
- Watch Ashgrove and Halfmoon; probably demand.

**3. Long term (development work).**
- Treat a missed offer differently from a refusal, and let scores ease back over time (the 2019 TODO in `history.py`).
- Log answer time and push delivery per ping.
- Make rank and score visible to the staff engineer and to support.
- Alert when a responder's pings fall by half over two weeks. That would have fired around 15 Aug, two days before the first quiet ticket.
- Settle what proximity should do for responders who turn jobs down (the unanswered 14 Aug question).
- Console asks that predate 4.2: reset warning and clear-all for filters, dark mode, larger badge text, different alert sounds, handler alert.
- Supply: if the availability record's shape ever changes, tell the Supply team first.

**4. Leadership message:** not drafted this round (out of scope).
