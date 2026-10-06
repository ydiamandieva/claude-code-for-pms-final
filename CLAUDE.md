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

