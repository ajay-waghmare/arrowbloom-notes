---
name: feedback-notes-github-every-change
description: "STANDING (20 Oct 2026, Ajay): MANDATORY — every decision and every change on his personal apps (Arrow Bloom, Block Bloom) is written to the app's notes repo on GitHub and pushed in the same session, with the code branch"
metadata:
  node_type: memory
  type: feedback
  originSessionId: f4795aa1-7942-4344-a6c4-e7b6487ba3f4
  modified: 2026-10-20T06:59:25.695Z
---

Ajay, 20 Oct 2026: "It is mandatory to update the notes in Github for every decision and changes" — said
while moving Arrow Bloom work to his personal laptop ("Next setup things will be continue in personel laptop").

**Rule (ALL AIs & sessions — Gemini, Claude, Codex, Antigravity, EVERY task):**
1. **Read First:** Before starting work, read `blockbloom-notes/memory/MEMORY.md` + `topic_arrow_bloom.md` (or `topic_block_bloom.md`), latest `journal/YYYY-MM-DD.md`, and `claude-memory/project_arrow_bloom.md`.
2. **After each task, decision, audit, or change (before ending turn):**
   - Add it in clean UTF-8 to `arrowbloom-notes/journal/YYYY-MM-DD.md` (`journal`), `arrowbloom-notes/claude-memory/project_arrow_bloom.md`, `blockbloom-notes/memory/topic_arrow_bloom.md`, and `blockbloom-notes/journal/YYYY-MM-DD.md` (`journal`). For Block Bloom also update `BlockBloom/DAILY_ACTIVITY.md` (`main`) and `blockbloom-notes/memory/topic_block_bloom.md`.
   - Record exact live state, IDs, blockers, open questions, and concrete next steps so any other AI or session can resume immediately.
   - Commit, push, and verify (`git rev-list --left-right --count HEAD...@{u}` = 0 0, `git status` clean). Push the active code branch too; never merge Arrow Bloom to `main` (Ajay merges).

**Why:** the personal laptop is now primary for Arrow Bloom; GitHub notes are the only bridge between the two
laptops and between Claude sessions. Anything not pushed is invisible to the other side.
**How to apply:** treat "notes pushed" as part of done; a reply that reports a change while notes are unpushed is
incomplete. On this work laptop, `git pull` both repos before touching Arrow Bloom: the personal laptop may have
moved on. Related: [[feedback-blockbloom-daily-journal]], [[project-arrow-bloom]], [[feedback-never-merge-master]].
