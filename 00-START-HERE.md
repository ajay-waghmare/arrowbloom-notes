# Arrow Bloom — Architecture & Decision Baseline

Created 19 Oct 2026.

## 1. Project Identity
- **Working Name**: Arrow Bloom (Package: `com.aweagle.arrowbloom`)
- **Publisher**: AW EagleCraft
- **Inspiration**: Easybrain's *Arrow Puzzle: Tap Puzzle Games* (50M+ downloads, 4.5★)
- **Genre**: 2D Spatial Logic & Arrow Escape Puzzle
- **Target Audience**: Casual logic puzzle, brain training, offline commuters

---

## 2. Core Technical Decisions (Stored for Permanence)

### Decision A: Kotlin Native (Android) over Flutter or Unity
- **Rationale**:
  1. **Download Size**: Unity/Flutter engines add 25–65 MB of overhead (Easybrain's APK is 73 MB). Kotlin Native with Jetpack Compose Canvas produces a tiny **~8–12 MB APK**, which dramatically increases organic store conversion in markets with cellular/metered data.
  2. **Zero Startup Latency**: Instant cold-start (0.0s) vs engine splash screens.
  3. **Infrastructure Reuse**: Directly reuses the existing, production-hardened toolchain built for Block Bloom (AGP 8.13, Google Play Publisher API scripts, BillingClient 8.0, AdMob 23.2.0, Firebase SDK 33.7.0).

### Decision B: Zero-Backend Architecture ($0/month hosting forever)
- **Rationale**:
  1. **Offline-First**: Players demand casual puzzles that work 100% offline (airplanes, metro, poor signal).
  2. **$0 Infrastructure Cost**: Scales from 10 to 1,000,000 players without AWS/GCP server hosting bills.
  3. **Deterministic Local Math**: Levels are procedurally verified via a Backward Raycast DAG Generator. Daily challenges generate deterministically from the current date seed (`seed = YYYYMMDD`).
  4. **Managed Cloud Services**: Google Play handles payments; AdMob handles ads; Firebase handles analytics and crash reporting at zero server cost.

### Decision C: Build Directory Isolated from OneDrive
- To prevent file-lock conflicts with OneDrive sync on Windows, Gradle build output is directed to:
  `layout.buildDirectory.set(file("${System.getProperty("user.home")}/.build-arrowbloom/${project.name}"))`

---

## 3. Repositories
- **Codebase**: `ArrowBloom` (`https://github.com/ajay-waghmare/ArrowBloom.git`)
- **Engineering Memory**: `arrowbloom-notes` (`https://github.com/ajay-waghmare/arrowbloom-notes.git`)

---

## 4. State as of 20 Oct 2026
- **1.0.0 is publish-ready** on branch `release/2026-10-20` (compileSdk / targetSdk 36, versionCode 1). `main` is still the 19 Oct scaffold until Ajay merges.
- Build output lives in `~/.build-arrowbloom/app`; the signed bundle is `outputs/bundle/release/app-release.aab`. Signing needs `keystore.properties` at the repo root (gitignored, never committed).
- Store kit is in the code repo under `store/` (icon, feature graphic, screenshots, `listing_v1.json`).
- What ships and what does not: see `02-PLAY-STORE-LAUNCH-CHECKLIST.md`. Why it is not a clone: `03-COPYRIGHT-AND-DIFFERENTIATION.md`.
- The "Inspiration" in section 1 is market context only; nothing of that game's art, text, sounds or levels is in this repo.

## 5. From 20 Oct 2026: personal laptop, notes rule
- Work continues on Ajay's **personal laptop**. Start there with `05-HANDOVER-PERSONAL-LAPTOP.md`
  (clone, files to carry by hand, tools, proof checks, next steps).
- **Mandatory:** every decision and every change is written to this repo (journal + affected doc), committed
  and pushed in the same session, with the code branch. See README.
- Current build: 4 (1.0.0, versionCode 4) on branch `release/2026-10-20-line-arrows`; drafts on internal and
  closed testing; build 1 live there. Next free versionCode: 5.
