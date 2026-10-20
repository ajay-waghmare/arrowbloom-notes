# Claude memory for Arrow Bloom (copies)

These are the memory files Claude uses for Arrow Bloom, kept here so the project's rules travel with the notes.
On a new machine, copy them into that machine's Claude memory folder and add one index line per file to its
`MEMORY.md` (the same files, plus Block Bloom's, are also in blockbloom-notes
`02-claude-practices/starter-kit/memory/`).

| File | What it says |
|---|---|
| `feedback_notes_github_every_change.md` | **Mandatory rule:** every decision and every change goes into the notes on GitHub, pushed in the same session |
| `project_arrow_bloom.md` | Where the project stands, branches, Play state, scripts, debug hooks |
| `reference_play_api_track_update_gotcha.md` | `tracks.update` replaces a track's whole release list; stage builds with `tools/play-stage-draft.js` |

Index lines for `MEMORY.md`:

```
- [⭐⭐ FB: Notes on GitHub for EVERY change](feedback_notes_github_every_change.md) — STANDING 20 Oct: every decision/change → notes repo journal + affected doc, pushed same session with the code
- [⭐⭐ Arrow Bloom (2nd game)](project_arrow_bloom.md) — personal laptop primary from 20 Oct; build 4 on release/2026-10-20-line-arrows; vc4 DRAFT internal + closed, vc1 live; next vc 5
- [⭐⭐ Ref: Play API tracks.update gotcha](reference_play_api_track_update_gotcha.md) — a PUT with only a draft drops the live release; carry live releases over
```

When a memory file changes on either laptop, copy it here again in the same commit as the journal entry.
