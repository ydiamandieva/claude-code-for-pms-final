---
name: wrap-up
description: Ends a class session in the Claude Code for PMs course. Use it when the student says "wrap up" (or "wrap up this session", "let's wrap up", "end of session", "we're done for today", "I'm done with this module"). It saves the prompts the student wrote this session into that module's prompts.md, writes the full story of what the session found into that module's session-notes.md, adds a short summary to the Working context in CLAUDE.md, and saves everything to GitHub.
---

# Wrap up

You're closing out a class session for a student in Product School's "Claude Code for PMs" course. They aren't technical, and they typed two words so they wouldn't have to type anything else. Their request is their yes: start right away with one plain sentence such as "Wrapping up today's session now." Don't ask them to type or paste anything unless a step below says to.

## 1. Work out which module this was

The module folders are 01-origin-story (Module 1), 02-super-hearing (Module 2), 03-rewind (Module 3), 04-x-ray-vision (Module 4), 05-super-speed (Module 5) and 06-sidekicks (Module 6).

- Use this session: the module the student's work and questions were about.
- If the session doesn't make it clear, use the first module folder whose prompts.md still has an empty numbered slot.
- If you still can't tell, ask one short question: "Which module was today, 1 to 6?"

## 2. Save the student's own prompts

- Look back through this session for the prompts the student wrote themselves. Leave out: the starter prompt each lab gives the whole room (the long, polished prompt the student pasted from a slide or the Zoom chat), "wrap up", "check my setup", "save my work", and short replies such as "yes", "ok" or "go ahead".
- Write them into that module's prompts.md, one per numbered slot (### 1., ### 2., ### 3.), in the order the student typed them, exactly as typed. Don't fix spelling, trim, reword or summarize.
- If there are more prompts than empty slots, add ### 4., ### 5. and so on.
- If some slots already hold prompts (from an earlier wrap-up), keep them and add the new ones after them. Never overwrite or delete anything already in the file.
- Leave the file's header text as it is.
- If the student wrote no prompts of their own this session, leave the file alone and say so.

## 3. Write the session notes (the full story)

The chat disappears when the session ends, and the reasoning in it is the most useful part. Capture it here, in that module's folder, in a file called `session-notes.md`. This file has no length limit. Be specific and use the real numbers, names and file paths from the session.

- If the file doesn't exist, create it with the heading `# Session notes`. If it exists, keep everything in it and add a new entry at the end. Never overwrite or delete earlier entries.
- Start each entry with `## <today's date>` and then these sections, in this order. Skip a section only if the session had nothing for it.
  - **Questions and answers.** Each question the student asked, with the answer in a few lines. Include the reasoning, not only the conclusion.
  - **Findings.** One line each. Say whether it was observed in the data or inferred, name the source (database table, wiki page, ticket set, code file), and give a confidence level when the session produced one.
  - **Reversals.** Anything the session overturned or weakened from earlier work, with the evidence that changed the view. Name the earlier claim and where it was written.
  - **Queries and checks that mattered.** The SQL text or the exact steps behind each important number, so someone could run them again.
  - **Decisions and recommendations.** What was decided or proposed, and why. For anything proposed for a developer or a manager, keep the actual wording of the ask.
  - **Files and artifacts made.** The path of each file created or changed. For a published artifact, its link and whether it is private.
  - **What we couldn't see.** The gaps in the data or code that limit the conclusions.
  - **Open questions.** Each with who to ask, using roles from the Working context. Don't invent names.
  - **Start here next time.** The single most useful next step.
- Write in plain English for a non-technical reader. Don't paste whole documents or long tool output. Link to the file that holds them instead.
- This folder is on a public GitHub repo. Everything in Rook is fictional, so that's fine. If the session handled anything that looks like real personal data (real names, emails, phone numbers, account details), leave it out of the notes and say so in your final message to the student.

## 4. Add a short summary to the Working context in CLAUDE.md

CLAUDE.md is read at the start of every session, so keep this part short. The details live in the session notes.

- Under "## Working context", after everything already there, add three to six short plain lines: what this session figured out about Rook that isn't written there yet and that you'd want to know at the start of the next session. That means findings, which sources mattered, and questions still open.
- End with one line that points to the notes, such as: `Full detail: 04-x-ray-vision/session-notes.md (<today's date>).`
- If a finding from this session contradicts or weakens a line already in the Working context, don't edit or delete that line. Add a line straight after your new lines starting with `Superseded:`, naming the old claim and what replaced it.
- If the section still holds only the placeholder "_You'll fill this in during Module 1._", replace just that placeholder line.
- Don't repeat what's already there, don't add headings, and don't paste in whole documents.
- Never change anything above the "---" line (the session scope block).
- Rook is fictional. Keep all of this in CLAUDE.md and the course folder: never save it to memory or anywhere outside the course folder.

## 5. Module 5 only: check the build files

If today was Module 5, check that 05-super-speed/brief.md and 05-super-speed/prototype.html are both there. If either is missing, tell the student which one. Don't recreate it.

## 6. Save to GitHub

Follow the "save my work" routine in the course-setup skill (.claude/skills/course-setup/SKILL.md and its references/saving-work.md), with a short message such as "Module 2 wrap-up". Handle every problem exactly the way that routine says.

## 7. Tell the student

A short checklist, then the link:

✓ Saved your prompts to <module folder>/prompts.md (how many)
✓ Saved the full story of today to <module folder>/session-notes.md
✓ Added a short summary to CLAUDE.md (and marked anything it superseded)
✓ Saved to GitHub: https://github.com/<their username>/claude-code-for-pms-final

If a step didn't work, mark it ✗ and give the fix in one plain sentence. If saving to GitHub failed, tell them their prompts and notes are safe on this computer and what to do next, per the save routine.
