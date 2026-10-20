---
name: renew-reminders
description: Renews the user's session-only recurring reminders (cron jobs) before their 7-day expiry, and sets the next renewal for the day before they expire again. Use it when the user says "renew reminders", "renew my reminder", "my reminder is about to expire", or when a scheduled renewal prompt tells you to run it.
---

# Renew reminders

Session-only recurring reminders (made with CronCreate) delete themselves 7 days after they are created. This skill keeps them alive by re-creating each one, which restarts its 7-day clock, and by scheduling the next renewal for day 6, the day before the new copy would expire.

## 1. List what exists

Call CronList. If there are no jobs, say "No reminders to renew" and stop; don't create anything.

Skip one-shot jobs (they fire once and delete themselves). Renew only recurring jobs, and treat the renewal job from step 4 (its prompt starts "Renew reminders") as a recurring job to replace, not renew.

## 2. Renew each recurring job

For each recurring job, in this order, so nothing is lost if a step fails:

1. CronCreate a new job with the same cron expression and the same prompt, word for word. Don't edit, shorten or improve the prompt.
2. Only after that succeeds, CronDelete the old job.

If creating a job fails, leave the old one in place and tell the user which one failed.

## 3. Report

Print a short list, one line per reminder: what it does, its next run time as the tool reports it, and "renewed" or "failed". Say the new copies expire in 7 days.

## 4. Set the next renewal

Create one one-shot reminder (CronCreate with recurring false) for 6 days from today at a time like 9:07 local, avoiding :00 and :30. Pin minute, hour, day of month and month to specific values. Its prompt:

> Renew reminders: run the renew-reminders skill in /Users/yanitadimitrova/claude-code-for-pms-final. Renew every recurring session reminder, report which were renewed, and set the next renewal.

Tell the user the date of the next renewal.

## Limits to tell the user

- The renewal reminder is itself session-only. If the Claude app or this session is closed before it fires, nothing renews and the reminders are gone.
- Reminders fire only while the session is open and idle.
- Each renewal is a copy: the old job's run history doesn't carry over.
