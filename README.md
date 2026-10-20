# Arrow Bloom — Engineering & Decision Memory

Persistent project memory, decisions and daily journals for **Arrow Bloom** (`com.aweagle.arrowbloom`),
a calm line-arrow logic puzzle by AW EagleCraft: zero backend, fully offline, Kotlin + Jetpack Compose.

**Work continues on the personal laptop from 20 Oct 2026: start with `05-HANDOVER-PERSONAL-LAPTOP.md`.**

## Rule: every decision and every change is written here, then pushed

Mandatory (Ajay, 20 Oct 2026). After any decision or change, in the same session: add it to
`journal/YYYY-MM-DD.md`, update the doc it affects (runbook, checklist, handover), commit on branch
`journal`, push, and check the push landed (`git status` shows nothing ahead). The code branch is pushed
too. GitHub is the only bridge between the two laptops and between sessions.

## Repository map

```
arrowbloom-notes/
├── README.md                              <- this index and the notes rule
├── 00-START-HERE.md                       <- identity, tech decisions, repos, state section
├── 02-PLAY-STORE-LAUNCH-CHECKLIST.md      <- what the build satisfies, console steps, never-do list
├── 03-COPYRIGHT-AND-DIFFERENTIATION.md    <- what is protected, what makes this its own game (incl. the build-2 genre look)
├── 04-PLAY-CONSOLE-RUNBOOK-2026-10-20.md  <- browser-Claude runbook, Parts 1-9 (Part 9 = roll out the newest draft)
├── 05-HANDOVER-PERSONAL-LAPTOP.md          <- clone, files to carry, tools, proof checks, next steps, rules
├── claude-memory/                         <- Claude memory files for Arrow Bloom (incl. the mandatory notes rule)
└── journal/
    ├── TEMPLATE.md
    ├── 2026-10-19.md                      <- kickoff: engine, DAG generator, first Compose canvas
    └── 2026-10-20.md                      <- builds 1-4: publish-ready app, line-arrow game, five stars, slimmer arrows, Play setup
```

Code: `https://github.com/ajay-waghmare/ArrowBloom`. Newest work on branch `release/2026-10-20-line-arrows`
(build 4); `release/2026-10-20` is build 1; `main` is the 19 Oct scaffold until Ajay merges.
