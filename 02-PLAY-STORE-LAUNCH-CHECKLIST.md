# Arrow Bloom — Google Play launch checklist

**Status (20 Oct 2026):** build is publish-ready on branch `release/2026-10-20` of `ArrowBloom`
(1.0.0, versionCode 1). What remains is console work and the closed test.
**Package:** `com.aweagle.arrowbloom` · **Tracks:** internal → closed (12 testers / 14 days) → production

## 1. What the build already satisfies

| Requirement | State |
|---|---|
| Android App Bundle, signed | `./gradlew :app:bundleRelease` with `keystore.properties` at the repo root (same upload key as Block Bloom, `aw-eagle-upload.jks`). Output: `~/.build-arrowbloom/app/outputs/bundle/release/app-release.aab` |
| Target API | **compileSdk / targetSdk 36.** Play requires API 36 for new apps and updates since 31 Aug 2026 (the 19 Oct checklist said 35 was fine; it is not) |
| R8 / shrinking | on, with line numbers kept for readable traces |
| Permissions | `VIBRATE` only. No INTERNET: nothing leaves the device |
| Data safety | "No data collected, no data shared" is true for 1.0.0. The app has no analytics, ads or billing SDK |
| Privacy policy | own page `https://ajay-waghmare.github.io/app-policy/arrow-bloom-privacy.html` (written 20 Oct on branch `arrow-bloom-policy` of the `app-policy` repo; Ajay merges it to `main` so the page is live BEFORE the listing is submitted; the in-app Settings link points at the same URL) |
| Languages | en, de, es, ja, ko, pt-BR, tr, with a per-app language picker on Android 13+ |
| Orientation | portrait only, declared and documented |
| Lint | 0 errors (`:app:lintDebug`, `abortOnError = true`) |
| Tests | 50 unit tests: every generated level 1–140 is proven solvable; scoring, gardens, daily, streak, resume codec, prefs |
| Emulator walkthrough | level 1 → outcome → level 2 → resume after a force-stop → all six gardens → Daily Bloom cleared → settings → German; no crashes |

## 2. Console steps, in order (all Ajay; the first release of a new app cannot be created by API)

1. Play Console → Create app: name **Arrow Bloom**, Game, Free, default language en-US.
2. Store listing: title / short / full description for the 8 locales are in `ArrowBloom/store/listing_v1.json`
   (push them later with `play-listings-set-multi.js` once the app exists); icon `store/icon-512.png`;
   feature graphic `store/feature-1024x500.png`; phone screenshots `store/screenshots/*.png` (1080×1920).
3. App content: privacy policy URL; **Ads: No** (true for 1.0.0; change it in the same release that adds AdMob);
   Data safety: no collection; content rating questionnaire (IARC, puzzle, no violence); target audience 13+;
   not Designed for Families; app access: everything available without a login.
4. Upload the AAB to **Internal testing** first, install from the Play link on a real phone, play three gardens
   and a Daily Bloom.
5. **Closed testing** with at least 12 opted-in testers for 14 continuous days: this is the production gate
   for a new app on this account. Start it the day the internal build is fine; keep shipping updates to the
   same closed track while the clock runs (updates do not reset it).
6. Apply for production access when the console says the gate is met, then roll out to production staged.

## 3. Things never to do (learned on Block Bloom)

- Never claim "no ads" or "no in-app purchases" in the listing, even while true: it becomes a policy
  problem the day monetisation ships. The listing copy avoids both claims.
- Never reuse Block Bloom's AdMob app ID or ad units; when ads come, Arrow Bloom gets its own AdMob app
  (the `app-ads.txt` on ajay-waghmare.github.io already covers the publisher).
- Never put Firebase in with Block Bloom's `google-services.json`; create a separate Firebase project
  (or at least a separate app) so the two games' analytics never mix.
- Add analytics (the `Analytics` seam is in the code) BEFORE monetising, not after.
- Set the Play Console contact website and the AdMob consent messages on day one of ads.

## 4. After launch (1.1 and beyond)

- Firebase Analytics + Crashlytics behind an `ANALYTICS_ENABLED` flag (same pattern as Block Bloom, debug builds dark).
- Rewarded ads only, opt-in: "+3 hints" and "skip this level"; banner and interstitial behind Remote Config
  dials, default off.
- Store listing experiments for the icon and the first screenshot.
