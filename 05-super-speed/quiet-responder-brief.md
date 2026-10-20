# Bringing quiet responders back: one-page brief

Draft for Helen · Dispatch · 20 Oct 2026 · Not yet checked with engineering

## The problem

A missed offer costs the same as a "no" (-0.12). Only a "yes" gives points back (+0.08), and scores never ease back (the 2019 TODO in `history.py`). So the only way back is to answer an offer, and every miss makes that harder.

Farlight, The Undertow, Vesper and Meteor Mite took 3 of 40 first pings after 4.2, against 175 of 247 before. They are still asked about once a day, but 15 of their 20 pings from 19 Aug to 6 Sep were missed. This is my replay of the code, not real scores.

## Who it's for

- **The responder who has gone quiet.** Today it is four people. Their phone goes silent and nobody says why: "starting to wonder if im still even in the system."
- **The handler, like Kip.** He learns by noticing or from a ticket days later. Vesper and Meteor Mite never got one. "Mite thinks Mite's been forgotten."

## What changes for them

**Responder**
- A miss costs less than a refusal, and scores ease back toward neutral over time, never above it. Numbers are for the staff engineer.
- The app says: "You've had fewer offers lately. You're still on the list. Here's what happened to your last three."

**Handler**
- The console marks a responder **Quiet** when their pings halve, showing pings this week against usual, last "yes" and last outcomes.
- One action, **Check in**: confirm availability and reset to neutral, logged in the override audit log.
- Still open: how the handler notices (badge, daily digest or push; 3 of 4 handlers asked for an alert), and the window. Two weeks would have fired near the end of August, after the first ticket on 17 Aug. Set both with Kip and the staff engineer.

## What it deliberately doesn't do

- **Promise offers.** A quiet responder is never ranked ahead of someone better placed. These are real incidents.
- **Touch the 60s wait or the proximity weights.** Testing 90s on part of the traffic is separate.
- **Fix the wider miss spike.** The other 12 responders account for about two thirds of the fall in "taken", so this addresses about one third.
- **Rank or grade responders.** "Quiet" is a prompt to check in.
- **Change the availability record** that Rook Supply reads, or take on the console asks (dark mode, filter warnings).

## How we'd know it worked

- Going quiet to a handler seeing it: from days, via a ticket, to the same day.
- A responder with a "yes" after a quiet spell is back near their area's usual rate within 2 weeks (threshold to set).
- Fewer "phone quiet" tickets: 32 in the 27 days after 4.2, none before.

## Before anyone builds

1. Real score history and rank order from the staff engineer. If the four aren't at the floor, this brief changes.
2. Why they miss (slow answers, push delivery, phones), from the engineering manager. If it is delivery, the score is a side issue.
3. Data after 6 Sep. All of the above is six weeks old.
4. Whether a handler override counts as a "yes", and whether scores survive a restart.
