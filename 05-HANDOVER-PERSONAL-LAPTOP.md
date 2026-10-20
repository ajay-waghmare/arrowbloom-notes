# Arrow Bloom — continue on the personal laptop

Written 20 Oct 2026, 12:30 IST, on the work laptop, for Ajay and for Claude on the personal laptop.
From now on the **personal laptop is where Arrow Bloom work continues**. GitHub is the only bridge:
everything below is pushed; anything not in git is listed in section 2.

## Where things stand

| Area | State |
|---|---|
| Game | Build 4 = 1.0.0, versionCode 4: winding line arrows that slide out, 3 hearts, up to 5 stars (each heart lost or hint used costs one), shaped boards, light theme, 7 languages |
| Code | `ArrowBloom`, branch **`release/2026-10-20-line-arrows`** (newest work). `release/2026-10-20` = build 1 (history). `main` = 19 Oct scaffold, merge only after the closed test is approved (Ajay merges) |
| Play app | Created; every App content declaration done; listing (8 locales), icon, feature graphic and six screenshots committed by API |
| Internal testing | build 1 live, **build 4 DRAFT** |
| Closed testing (track `alpha`, "Closed Alpha") | testers = email list "Block Bloom Testers" (34 users); build 1 sent for review 20 Oct; **build 4 DRAFT** |
| Production | locked until 12 testers stay opted in for 14 days and "Apply for production" is approved |
| Privacy policy | live: `https://ajay-waghmare.github.io/app-policy/arrow-bloom-privacy.html` |
| Tester opt-in link | `https://play.google.com/apps/testing/com.aweagle.arrowbloom` |
| versionCodes | 1 live; 2 and 3 burnt (staged, replaced before rollout); 4 = current draft; **next free = 5** |

## 1. Clone

```
git clone https://github.com/ajay-waghmare/ArrowBloom.git D:\DevTools\ArrowBloom
cd D:\DevTools\ArrowBloom
git checkout release/2026-10-20-line-arrows
git clone -b journal https://github.com/ajay-waghmare/arrowbloom-notes.git D:\abc\ArrowBloom-notes
```

The Claude starter kit (memory files, practices) is in `blockbloom-notes`, branch `journal`, folder
`02-claude-practices/starter-kit/`, if it is not on the personal laptop yet.

## 2. Files that are not in git (carry by hand)

Move them on a USB stick or in an encrypted archive; never through chat, email or a shared drive.
If Block Bloom's handover (`blockbloom-notes/01-blockbloom/08-files-to-carry-manually.md`) is already
done, items 1 and 3 are on the personal laptop already: Arrow Bloom signs with the same upload key.

| # | On the work laptop | What it is | On the personal laptop |
|---|---|---|---|
| 1 | `D:\DevTools\keystores\aw-eagle-upload.jks` | upload keystore, alias `aw-eagle`, shared by all AW EagleCraft apps | `D:\DevTools\keystores\` (or change `storeFile`) |
| 2 | `D:\DevTools\ArrowBloom-pub\keystore.properties` | `storeFile`, `storePassword`, `keyAlias`, `keyPassword` (same values as Block Bloom's) | root of the ArrowBloom clone (gitignored) |
| 3 | `D:\Downloads\avid-airway-498216-e5-9f357c8e6b11.json` | Play service-account key (`play-publisher@avid-airway-498216-e5`) | anywhere; every script takes its path as the first argument |
| 4 | `local.properties` | only `sdk.dir` | let Android Studio regenerate it |

## 3. Tools

- JDK 17 (`JAVA_HOME`), Android SDK: platform 36, build-tools 36, platform-tools, emulator.
  The Gradle wrapper (8.13) brings AGP 8.13, Kotlin 1.9.24, Compose compiler 1.5.14.
- Node.js 16 or newer (Play and store scripts), Google Chrome (renders the icon, the feature graphic
  and the framed screenshots), Git Bash (emulator scripts).
- An emulator like `bloomtest`: 1080×2400, 420 dpi, API 34. The scripts' tap coordinates assume that size.
- Build output goes to `%USERPROFILE%\.build-arrowbloom\app` (set in `build.gradle.kts`), outside the repo.
- Work-laptop-only quirk: there Gradle needed `JDK_JAVA_OPTIONS=--patch-module java.base=...jdkpatch...`
  because `Selector.open()` fails on that machine. Do not set it on the personal laptop unless Gradle
  fails with a loopback or `Selector` error.

## 4. Prove the setup (all must pass before any new work)

```
gradlew :app:testDebugUnitTest        53 tests, 1 skipped (a dev-only report)
gradlew :app:lintDebug                0 errors
gradlew :app:bundleRelease            signs with the upload key; AAB in %USERPROFILE%\.build-arrowbloom\app\outputs\bundle\release\
node tools\play-status.js <sa.json> com.aweagle.arrowbloom      build 1 live and build 4 draft on internal and alpha
gradlew :app:assembleDebug  then  bash tools/emulator/stars-check.sh    5 / 3 / 4 stars, "crash lines: 0"
```

## 5. Next steps, in order

1. Runbook Part 9 (`04-PLAY-CONSOLE-RUNBOOK-2026-10-20.md`): roll out build 4 on internal (Save and
   publish) and closed testing (Save, then Send for review). Ajay's clicks.
2. Send testers the opt-in link. At least 12 must stay opted in for 14 days in a row.
3. Each new build while testers play: bump `versionCode` (next is 5), `gradlew :app:bundleRelease`,
   `node tools\play-stage-draft.js <sa.json> com.aweagle.arrowbloom <aab> "1.0.0 (5)" internal,alpha --notes "..."`,
   then roll it out in the console.
4. After the 14 days: Dashboard → Apply for production → staged rollout.
5. After production approval: Ajay merges `release/2026-10-20-line-arrows` into `main`.
6. Open offers to Ajay, nothing started: colour the difficulty chip and show it on Home and the result
   card; a player-chosen difficulty setting.

## 6. Rules that come with the project

- **Mandatory: every decision and every change goes into this notes repo** (journal/YYYY-MM-DD.md plus
  the affected doc), committed and pushed in the same session, together with the code branch. A change
  that is not in the notes on GitHub has not happened as far as the other laptop knows.
- Never merge into `main`; Ajay merges. Branches: `release/YYYY-MM-DD` or `release/YYYY-MM-DD-topic`.
- Ask for "GO" before any rollout, Send for review, Apply for production, and anything about ads or money.
- Never claim "no ads" or "no in-app purchases" in the listing.
- Before analytics or ads: Arrow Bloom gets its own Firebase project and AdMob app; never Block Bloom's.
- Bump the saved-run header in `RunCodec` whenever the generator changes what a level number produces (v2 now).
- Play API: `tracks.update` replaces a track's whole release list. Stage builds with
  `tools/play-stage-draft.js`, which keeps live releases and refuses to commit if one would vanish.

## 7. Claude memory on the personal laptop

Copy these from this repo's `claude-memory/` folder (or from `blockbloom-notes/02-claude-practices/starter-kit/memory/`) into the personal laptop's
Claude memory folder and keep their lines in its `MEMORY.md`: `project_arrow_bloom.md`,
`feedback_notes_github_every_change.md`, `reference_play_api_track_update_gotcha.md` (plus the Block
Bloom files already there). Paths inside them name the work laptop's folders (`D:\DevTools\ArrowBloom-pub`);
on the personal laptop read them as the clone paths in section 1.
