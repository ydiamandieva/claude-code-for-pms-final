# Session notes

## 2026-10-20

### Questions and answers

**1. Read the four customer interviews in the Research section of Rook's wiki. What are the handlers unhappy about? Group it, say how many of the four raised each thing, and quote one line for each.**
Source: wiki database "Customer interviews" (id 83a83da8-7536-4a1a-b725-d914482fad35), four rows, all console-redesign calls by the product designer, 2 to 5 Sep 2026. Aunt Dot (Vesper), Mr. Ambrose (Captain Vantage), Halloran (Sgt. Bulwark), Kip (Meteor Mite and The Gale). I read each page in full and grouped by hand.
- Offers vanish before the responder can answer: 3 of 4 (Dot, Ambrose, Halloran). Kip did not raise it.
- Handlers not alerted well enough that something is live: 3 of 4 (Dot wants an alert for herself, Ambrose wants the live-callout signal harder to miss, Kip wants a different sound per responder).
- Very uneven work, some quiet and some swamped: 2 of 4 (Kip with Meteor Mite vs The Gale; Dot with her quiet weeks).
- Text too small: 2 of 4 (Dot, Ambrose).
- Dark mode: 1 of 4 (Kip). Filter persistence resets silently: 1 of 4 (Ambrose). Capability tag legend buried: 1 of 4 (Ambrose, "not urgent").
- Supply problems, not console: 1 of 4 (Halloran: requisition queue, 11 days for a cracked vest plate, field failure reports "go into a void", catalog search).
- Honest weighting: Halloran's vanishing offer was secondhand and only came up when asked at the end. Dot's "quiet weeks" came after the interviewer asked about them (she raised the fast-vanishing offers herself). Four people is a small sample.

**2. In one sentence, based on the interviews, what is the trouble with 4.2?**
Handlers say offers now disappear before responders can answer, while a few responders go dead quiet and others get swamped. That fits a shorter response window with a lasting penalty for missed offers, but the interviews show symptoms and cannot prove that cause.

**3. Read every support ticket in Rook's database. Same treatment: group, count, one quote each.**
Source: `support_tickets`, 147 rows (3001 to 3147, 29 Jun to 7 Sep). I read all bodies in two pages of 80, then sorted each ticket into exactly one of eight groups by ticket number (the counts add to 147; see Queries). Results:

| Group | Tickets | Before 4.2 / after | Still open |
|---|---|---|---|
| Phone gone quiet | 32 | 0 / 32 | 32 |
| Offer vanished before the responder could answer | 13 | 0 / 13 | 13 |
| Saved filters (4.2 persistence change) | 16 | 2 / 14 | 6 |
| Other console requests and gaps | 31 | 14 / 17 | 12 |
| Supply and gear | 26 | 10 / 16 | 9 |
| Account and admin | 15 | 4 / 11 | 7 |
| Dark mode (4), badge text (2), alert sound (2) | 8 | 4 / 4 | 4 |
| Phone and notification glitches | 6 | 6 / 0 | 0 |

Totals: 40 before, 107 after, 83 open. The quiet tickets are Farlight 11, The Undertow 11, Corporal Ashgrove 5, Halfmoon 5. The vanished tickets are spread across 9 responders. Within filters: 4 silent resets, 4 wrong computer or wrong person, 2 cannot clear all, 2 badge too faint, 2 thank-yous, plus 2 pre-4.2 requests to save filters. All 6 phone-glitch tickets (duplicate pings, weak signal, older phone, wrong button) are before 4.2 and closed. Many tickets are near word-for-word repeats across handlers, so counts are tickets, not people.

**4. Where do the two piles disagree? What is loud in the interviews but rare in the tickets, and what is all over the tickets that nobody raised in the interviews?**
- What leads: interviews lead with vanishing (3 of 4); tickets lead with quiet (32 vs 13). Same problem from two ends. A vanished offer is a vivid moment a handler tells a researcher; a quiet stretch is slow and becomes a ticket after days.
- The overloaded side exists only in the interviews (Kip's The Gale). No ticket says a responder has too much work; nobody files a ticket about being busy.
- Maintenance scheduling: Halloran says it "has gotten smarter". Four tickets after 4.2 say the opposite (3054 and 3109 suit booked on the marathon day, 3057 and 3126 reminder after the service date). One handler vs four tickets.
- Loud in interviews, rare in tickets: a better live-callout alert for handlers (2 of 4 interviews, 0 tickets), small text (2 of 4 vs 2 of 147), dark mode (Kip vs 4 of 147), per-responder alert sound (1 vs 2).
- All over the tickets, absent from interviews: the quiet spiral at scale (day counts, "is X still on the list?", "first one in 9 days and he missed it"), Farlight and The Undertow (not interviewed), filter persistence (16 tickets vs 1 interview), 31 ordinary console gaps, 15 account and admin tickets, and the pre-4.2 duplicate-ping tickets that stopped.
- Where they agree: Halloran's Supply gripes match the tickets almost word for word (priority field changes nothing, "plate" returns forty results, failure reports get no reply).

**5. If I had only read the interviews, what would I have got wrong?**
Five things. (1) Called it a speed problem, when quiet tickets outnumber vanished ones 32 to 13 and are the longer, still-open problem. (2) Called it an old problem: Kip said work "has always been a little lumpy" and Ambrose said "not the first time this year", but there is no quiet or vanished-offer ticket before 12 Aug (first vanished 3041 on 12 Aug; first quiet 3060 on 17 Aug). (3) Put console polish too high: dark mode 4 of 147, small text 2. (4) Missed Farlight and The Undertow, 11 tickets each, who were not interviewed. (5) Thought it was settling: Farlight and The Undertow were still silent 6 to 9 days in the same week as the interviews, and 83 of 107 after-tickets are open. The interviews also nudge toward "the window is too short" as the only explanation, which neither pile tests.

### Findings

- **Observed** (wiki, 4 interviews): vanishing offers 3 of 4; handler alerts 3 of 4; uneven work 2 of 4; small text 2 of 4; dark mode, filter resets, tag legend 1 each. Confidence: high on counts, low on weight (n = 4, some points prompted).
- **Observed** (`support_tickets`, all 147 read): 45 routing tickets since 4.2 (32 quiet + 13 vanished), none before, all open. First vanished ticket 3041 at 15:41 on 12 Aug; first quiet ticket 3060 on 17 Aug. Confidence: high on counts of subject-matched groups, medium on edge cases (grouped by hand).
- **Observed:** quiet tickets come from four responders only (Farlight 11, The Undertow 11, Corporal Ashgrove 5, Halfmoon 5). Same figures as the Module 1 note.
- **Observed:** filter persistence is 16 tickets in my grouping (14 after 4.2, 2 before), more than the "12" in the Module 1 note. The difference is how broadly I counted (badge, wrong computer, clear-all, thank-yous).
- **Observed:** 12 distinct handlers filed tickets (11 plus Mr. Ambrose with one ticket, 3043). Desmond Okafor 21, Linda Pruitt 19, Simone Fischer 15, Yusuf Demir 14, Teresa Alvarez 12, Marjorie Sung 12, Beatrice Calloway 11, Graham Petrov 11, Owen Bramwell 11, Farid Haddad 10, Renata Kovač 10.
- **Observed:** of the four interviewees, only Ambrose filed a ticket. Dot, Kip and Halloran never did. Vesper and Meteor Mite (two of the four silent responders) filed none; Farlight and The Undertow appear only in tickets.
- **Inferred:** quiet end shows in tickets, overloaded end cannot, because busy responders do not file tickets. Confidence: medium.
- **Inferred:** the duplicate-push fix in 4.2 worked as far as tickets go (6 pre-4.2 glitch tickets, 0 after). Not verified against push logs.
- **Observed:** Supply and gear is 26 of 147 tickets (18%), 16 of them after 4.2. Not routing, but real.

### Reversals

- Module 1 note ("Findings from support tickets") says filter persistence is "12 tickets, 2 are thank-yous". This session counted 16 related tickets (14 after 4.2, 2 before), with the same 2 thank-yous. The point that it is small next to routing still holds.
- In chat I wrote that the tickets were "147 filings from 15 handlers". That is wrong: 12 distinct handlers filed (query below). The 15 in the Module 3 note is the number of handlers in the handlers table, not ticket filers.
- Nothing else from earlier work was overturned. The interview and ticket counts match the Module 1 notes (3 of 4 vanish, 2 of 4 uneven, 45 routing tickets, 32 + 13).

### Queries and checks that mattered

- Table shape: `describe_table support_tickets` (columns ticket_number, filed_at, filed_by, about_responder, subject, body, status).
- Read all rows: `SELECT ticket_number, filed_at, filed_by, about_responder, subject, status, body FROM support_tickets ORDER BY ticket_number LIMIT 80`, then the same with `OFFSET 80 LIMIT 80` (80 + 67 = 147 rows).
- Subject frequency: `SELECT subject, count(*) n, sum(case when filed_at >= '2026-08-12' then 1 else 0 end) after_42, sum(case when status='open' then 1 else 0 end) open_n FROM support_tickets GROUP BY subject ORDER BY n DESC, subject` (96 distinct subjects).
- Group tally: a `WITH g AS (SELECT ... CASE WHEN ticket_number IN (...) THEN '<group>' ... ELSE '8 other console' END grp FROM support_tickets) SELECT grp, count(*), before/after 12 Aug, open ... GROUP BY grp`. Ticket numbers per group:
  - Vanished (13): 3041, 3043, 3047, 3048, 3052, 3055, 3056, 3065, 3077, 3078, 3091, 3113, 3123.
  - Quiet (32): 3060, 3070, 3088, 3130, 3131, 3071, 3073, 3083, 3086, 3114, 3129, 3135, 3145, 3080, 3081, 3097, 3098, 3147, 3089, 3104, 3108, 3118, 3096, 3099, 3138, 3139, 3103, 3112, 3120, 3121, 3110, 3140.
  - Filters (16): 3005, 3012, 3042, 3044, 3046, 3061, 3062, 3064, 3066, 3072, 3076, 3085, 3100, 3115, 3124, 3134.
  - Dark mode, badge text, alert sound (8): 3018, 3029, 3105, 3117, 3013, 3142, 3031, 3127.
  - Phone and notification glitches (6): 3007, 3014, 3016, 3033, 3034, 3040.
  - Supply and gear (26): 3001, 3004, 3011, 3021, 3022, 3027, 3030, 3032, 3036, 3038, 3054, 3057, 3063, 3069, 3074, 3092, 3093, 3095, 3101, 3102, 3109, 3111, 3122, 3125, 3126, 3128.
  - Account and admin (15): 3020, 3107, 3023, 3075, 3049, 3079, 3053, 3141, 3059, 3132, 3067, 3136, 3010, 3144, 3024.
  - Everything else (31) is "other console".
- Who filed: `SELECT filed_by, count(*) n, min(ticket_number) FROM support_tickets GROUP BY filed_by ORDER BY n DESC` (12 rows).
- Interviews: `search_wiki("interviews")` and `search_wiki("Research")`, then `read_database` on id 83a83da8-7536-4a1a-b725-d914482fad35 and `read_page` on each of the four row ids.

### Decisions and recommendations

- Treat "phone gone quiet" as the main support problem, not "offer vanished". Reason: 32 vs 13 tickets, longer lasting, all open, and the interviews cannot see it well.
- Support should reply to the 45 open quiet and vanished tickets (the same ask as the Module 1 note). Proposed wording: "Reply to the 45 open quiet and vanished-offer tickets with what we know and when we will update them, starting with Farlight and The Undertow, who have been silent longest."
- Do not rank console polish (dark mode, text size, alert sound) above routing, but note the alert-for-handlers ask is strong in interviews and invisible in tickets, so it is worth asking a few handlers directly.
- Do not treat either pile as proof of cause. Next evidence to get: answer times for yes, push delivery logs, real score history (engineering).

### Files and artifacts made

- `02-super-hearing/session-notes.md` (this file, new).
- `CLAUDE.md` (short summary added under Working context).
- No other files created or changed. No artifacts published. `02-super-hearing/prompts.md` left alone (see below).

### What we couldn't see

- Tickets say what handlers chose to file. There are no tickets about being too busy, and no way to tell how many people stayed quiet instead of writing in.
- Grouping is by hand from subject and body. Edge cases (for example "show when gear is due back", counted as Supply; 3006 "bulk callout" counted as other console) could be argued either way.
- The interviews are four console-redesign calls with different responders from the ticket piles. Only Ambrose is in both.
- Ambrose's ticket 3043 (filed 13 Aug) says the callout moved on "yesterday evening" (12 Aug). In his 2 Sep interview he says "two weeks ago" (about 19 Aug) with the same details (coat on, one boot on). Probably the same event told loosely, but I could not tell.
- No answer-time column, no score history, no data after 7 Sep (today is 20 Oct).

### Open questions

- Why do the four responders stay quiet? Staff engineer (real scores) and engineering manager (answer times, push logs).
- Was the "back in September" recovery real, and did Farlight and The Undertow recover? Engineering manager (data after 6 Sep).
- Are the handler alerts a real unmet need? Support lead and two or three handlers, since no ticket mentions it.
- Why do maintenance tickets say bookings are worse after 4.2 while Halloran says better? Supply team, via Director of Product.
- Are the near-identical tickets typed by different handlers or generated from a template? Support lead.

### Start here next time

Ask the engineering manager for "yes" answer times and push delivery logs for the four quiet responders (Farlight, The Undertow, Vesper, Meteor Mite), and ask support to reply to the 45 open quiet and vanished-offer tickets.

**Student prompts this session:** all the prompts typed this session were the lab's room prompts, so none of the student's own wording was saved to `prompts.md`.
