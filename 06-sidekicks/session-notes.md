# Session notes

## 2026-10-20

### Questions and answers

- **Can my "decisions and owners" habit become a skill?** Yes: `meeting-recap`. It returns decisions (only things actually settled), a follow-ups table (action, owner, due), "Not settled" and "Gaps to chase". It never guesses an owner or a date: missing ones are marked "No owner named" / "No date". It prints in chat and saves nothing.
- **"Save the skill" and "make it available in every project".** Saving meant committing and pushing (done through the course save routine). Making it available everywhere would mean copying it to `~/.claude/skills/`, which is outside the course folder. `CLAUDE.md` forbids writing there, and the exceptions listed cover only course setup and wrap-up, so I did not do it. I gave the student a `cp -R` command to run themselves.
- **Can a skill check a brief on four tests?** Yes: `review-checklist` (owner named, success defined, scope consistent start to finish, problem before fix). Each test scores Pass / Partial / Fail with a quote as evidence, then a "Fix before sharing" list. Verdict is "Ready" only if all four pass.
- **What does review-checklist say about the Module 5 brief?** Needs changes: owner Fail (Helen is the reader, not an owner; Kip and the staff engineer are only consulted), success Partial (no targets: "threshold to set", "fewer tickets"), scope Partial (the "Quiet" trigger is "pings halve" but the problem is missed offers; "ease back" and "Check in reset" are two ways back and the brief doesn't say how they relate), problem-before-fix Pass.
- **"Do these two checks."** I read this as the two items in the review's "Not checked" list: (1) do the brief's numbers match the database, (2) does the push-delivery caveat hold. Results below.
- **Schedule review-checklist every Monday.** First built as a real scheduled task (`monday-brief-review`, saved to `~/.claude/scheduled-tasks/`) after the student said to lift the folder rule for it. The student then reversed ("I was wrong"): task deleted, replaced by a session-only reminder. Session-only reminders fire only while the session is open and idle, and expire after 7 days.
- **How do I keep the reminder alive?** `renew-reminders` skill: re-creates each recurring reminder (create the copy first, then delete the old one), then sets a one-shot renewal for day 6. A skill cannot fire by itself, so the first renewal was set by hand (below).

### Findings

- **Observed (database `pings`, first ping per callout, 12 Aug as the 4.2 cut-off):** the four quiet responders (Farlight, The Undertow, Vesper, Meteor Mite) took 3 of 40 first pings after 4.2 and 175 of 247 before. Matches the brief exactly. After 4.2 on those 40: 28 missed, 9 turned down.
- **Observed (`pings`):** 19 Aug to 5 Sep the four had 20 pings: 15 missed, 4 turned down, 1 taken. Matches the brief ("about once a day" is roughly right: 20 in 18 days).
- **Observed (`support_tickets` subjects):** no quiet-type ticket before 12 Aug; the only earlier ping-related ones are #3016 duplicate ping, #3020 console logouts, #3034 "Push notifications unreliable on older phones" (4 Aug). First quiet ticket is #3060 on 17 Aug. I count 31 quiet-themed tickets by subject line (33 if the two "asked me to pass this on" tickets, #3120 and #3121, count). The brief's "32" is within that range. Confidence: medium, because I read subject lines, not bodies.
- **Observed:** about 10 of those quiet tickets are about Corporal Ashgrove (5) and Halfmoon (5), whose quiet earlier work read as falling area demand. About 22 are about Farlight and The Undertow. So the ticket measure partly counts something this brief doesn't fix.
- **Observed, then inferred (delivery vs slow answers):** refusals held steady after 4.2 while yeses fell: the four 21.6% to 17.9% turned down, taken 75.5% to 23.2%, missed 2.9% to 58.9% (56 pings after); the other twelve 20.9% to 18.0% turned down, taken 77.0% to 68.1%, missed 2.1% to 13.9%. The inference is that random push failures would have cut refusals too, so this leans toward yeses being slower than refusals and running out of the 60s, not toward delivery. Confidence: low to medium; no answer times, no push logs, only 56 pings for the four.
- **Observed:** `06-sidekicks/scheduled-run-output.txt` already existed (dated 13 Oct, from the course) with a sample run over `06-sidekicks/briefs/` (4 files: bulk-callout, routing-override-audit-log, requisition-approval-chains, handler-phone-app, one flag each). That `briefs/` folder is not in the course folder.

### Reversals

- **Scheduled task to session-only reminder.** Student's earlier "let's go with the first one" (real scheduled task) was reversed in the same session. Evidence: the student said they were wrong. The task is deleted, but its file is still at `~/.claude/scheduled-tasks/monday-brief-review/SKILL.md` because the scheduler leaves it on disk and I can't remove it from outside the folder.
- **My own error.** I told the student `scheduled-run-output.txt` "doesn't exist yet". It did exist (see above). The reminder's prompt appends and never overwrites, so nothing was lost, but the statement was wrong.
- **Module 5 brief, "32 phone quiet tickets" measure.** Weakened in `05-super-speed/brief.md`: now "about 22 of the 32" are about the four, the other 10 are Ashgrove and Halfmoon. The brief's "If it is delivery, the score is a side issue" caveat now carries the refusal-rate evidence against delivery.

### Queries and checks that mattered

First pings, four quiet responders, before/after 12 Aug:

```sql
with first_ping as (select distinct on (callout_number) callout_number, responder, sent_at, outcome from pings order by callout_number, sent_at),
q as (select * from first_ping where responder in ('Farlight','The Undertow','Vesper','Meteor Mite'))
select case when sent_at < '2026-08-12' then 'before' else 'after' end as period,
  count(*) as first_pings,
  count(*) filter (where outcome='taken') as taken,
  count(*) filter (where outcome='missed') as missed,
  count(*) filter (where outcome='turned down') as turned_down
from q group by 1 order by 1
```

Their pings 19 Aug to 6 Sep:

```sql
select count(*) as pings, count(*) filter (where outcome='missed') as missed,
  count(*) filter (where outcome='turned down') as turned_down,
  count(*) filter (where outcome='taken') as taken
from pings where responder in ('Farlight','The Undertow','Vesper','Meteor Mite')
  and sent_at >= '2026-08-19' and sent_at < '2026-09-07'
```

Refusal-rate comparison, four vs the other twelve:

```sql
select case when responder in ('Farlight','The Undertow','Vesper','Meteor Mite') then 'four' else 'twelve' end as grp,
  case when sent_at < '2026-08-12' then 'before' else 'after' end as period,
  count(*) as pings,
  round(100.0*count(*) filter (where outcome='taken')/count(*),1) as taken_pct,
  round(100.0*count(*) filter (where outcome='turned down')/count(*),1) as turned_down_pct,
  round(100.0*count(*) filter (where outcome='missed')/count(*),1) as missed_pct
from pings group by 1,2 order by 1,2
```

Tickets: `select ticket_number, filed_at::date, about_responder, subject from support_tickets where filed_at >= '2026-08-12' order by ticket_number` (107 rows), then counted by subject pattern: "phone has not gone off" 5, "Hardly anything for" 8, "much quieter than usual" 5, "Still very quiet" 4, "Nothing coming through" 5, "still on the list" 2, "First one in N days" 2 = 31. Ashgrove/Halfmoon tickets by `about_responder`: 5 each.

Scheduling: `CronCreate` cron `13 9 * * 1` (Mondays), result next run 26 Oct about 9:43 (the tool adds a delay). One-shot renewal `7 9 25 10 *`, job id 12718722, next run 25 Oct 9:07.

### Decisions and recommendations

- Skills live in the course folder under `.claude/skills/`, not in `~/.claude/skills/`, because of the write rule. The student can copy `meeting-recap` to `~/.claude/skills/` themselves.
- Monday review: session-only reminder (id 4459296a). Its prompt: "Monday brief review. In /Users/yanitadimitrova/claude-code-for-pms-final, run the review-checklist skill ... on every brief.md under the module folders 00-rook to 06-sidekicks ... append the FULL output to 06-sidekicks/scheduled-run-output.txt ... never overwrite earlier runs." It is read-only for the briefs and commits nothing.
- Renewal: `renew-reminders` skill, first renewal set for Sunday 25 Oct about 9:07, the day before the Monday job's last run.
- Recommended for the brief (not yet done): name one accountable owner; give each success measure a number and a date; make the "Quiet" trigger cover missed offers, or say it only catches drops in ping volume; say how "ease back" and "Check in" relate.

### Files and artifacts made

- `.claude/skills/meeting-recap/SKILL.md` (new, committed `c92767e`)
- `.claude/skills/review-checklist/SKILL.md` (new, committed `bc17107`)
- `.claude/skills/renew-reminders/SKILL.md` (new, committed `ad74d58`)
- `05-super-speed/brief.md` (edited: ticket measure and delivery evidence; committed `90932a8`)
- `06-sidekicks/prompts.md` (this wrap-up), `06-sidekicks/session-notes.md` (this file)
- Outside the folder: `~/.claude/scheduled-tasks/monday-brief-review/SKILL.md`, left on disk after the task was deleted.
- No artifacts published.

### What we couldn't see

- No answer times and no push logs, so slow yeses vs delivery vs the 60s wait can't be separated.
- All data still ends 6-7 Sep; today is 20 Oct.
- Ticket counts come from subject lines only.
- `meeting-recap` and `review-checklist` have each been run only once or not at all: `meeting-recap` was never tested on real notes (the student switched to saving), `review-checklist` ran once on the Module 5 brief.
- The `06-sidekicks/briefs/` folder named in the existing sample output is not in the course folder, so the Monday run will find only `05-super-speed/brief.md` unless those files are added.

### Open questions

- Is the `briefs/` folder behind the 13 Oct sample output supposed to be in the course folder? Ask the instructor.
- Real answer times and push delivery logs for the four: engineering manager.
- Who is accountable for the quiet-responder brief (the owner test failed)? Director of Product.
- Whether the Monday reminder and its renewal will still be alive on 26 Oct depends on this session staying open.

### Start here next time

Check `06-sidekicks/scheduled-run-output.txt` for a Monday 26 Oct entry. If there isn't one, the session closed before it fired: re-create the Monday reminder and run `renew-reminders`. Then run `meeting-recap` on a real set of notes.
