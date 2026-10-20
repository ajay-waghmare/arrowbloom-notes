# Arrow Bloom — Play Console runbook for Claude in the browser (20 Oct 2026)

Written for: Claude in Chrome, working in Ajay's Play Console with Ajay watching. Ajay does the steps marked **AJAY**.

**Status 20 Oct, 11:45:** Parts 1-8 done (build 1 live on internal and closed testing, closed release in review). Build 2 is staged as a draft on both tracks: Part 9 rolls it out.

## Facts you work with
- App: **Arrow Bloom**, package `com.aweagle.arrowbloom`, a free offline puzzle game. versionCode 1, versionName 1.0.0, targetSdk 36.
- It has **no ads, no analytics, no login, no in-app purchases and no internet permission**. It collects no data. Every declaration below follows from that; do not answer anything differently.
- Developer account: AW EagleCraft (ajaywaghmare00a@gmail.com). Block Bloom already lives in this account. **Never change anything on Block Bloom.**
- Privacy policy URL: `https://ajay-waghmare.github.io/app-policy/arrow-bloom-privacy.html` (open it in a tab before you paste it anywhere; if it 404s, stop and tell Ajay to merge the `arrow-bloom-policy` pull request in the `app-policy` repo).
- Contact email for Play and IARC: ajaywaghmare00a@gmail.com. Website: `https://ajay-waghmare.github.io`.
- Store listing text (8 languages) and all graphics are pushed later by script from Ajay's laptop. You do not type descriptions and you never upload files.

## Rules
1. Never click **Send for review**, **Send changes for review**, **Start rollout**, **Apply for production**, **Submit** on the Data safety form, or anything under Monetize, Payments profile, Tax, AdMob or Firebase. Those are Ajay's clicks.
2. Never delete, unpublish or edit anything that is not Arrow Bloom.
3. Saving and submitting the individual App content declarations (content rating questionnaire, ads, app access, target audience, government, financial, health, advertising ID, news, COVID) is fine: they are questionnaires, not the app review.
4. If a page shows a field this runbook does not mention, leave the default and report it.
5. After each part, report back in the format at the end.

## Part 1 — Create the app (you)
1. Open `https://play.google.com/console`, pick the AW EagleCraft account, **All apps → Create app**.
2. App name: `Arrow Bloom`. Default language: `English (United States) – en-US`. App or game: **Game**. Free or paid: **Free** (a free app can never be changed to paid later; that is intended).
3. Declarations: tick Developer Program Policies, US export laws and, if shown, Play App Signing terms. If a contact email is asked, use ajaywaghmare00a@gmail.com. Click **Create app**.
4. On the new app's **Dashboard**, read the task list and report, word for word, any task about **testing requirements**, **closed testing with 12 testers** or **Apply for production**. This tells us whether the 14-day closed test applies to this second app (Google's help text is written per app, so expect it).

## Part 2 — AJAY: upload the first bundle (file picker, so not you)
1. Test and release → Testing → **Internal testing** → Create new release.
2. If asked to choose a signing key: **Use Google-generated key** (default). The same upload keystore as Block Bloom signs the bundle; Google only discourages sharing the app signing key, and with Google-generated keys each app gets its own, so this is fine. The key that signs this first upload becomes the upload key for Arrow Bloom.
3. Drag in `C:\Users\Ajay.Waghmare\.build-arrowbloom\app\outputs\bundle\release\app-release.aab` (2 MB; it must show versionCode 1, 1.0.0, API 36).
4. Release name: leave `1 (1.0.0)`. Release notes (en-US): `First release of Arrow Bloom.` Click **Save** (not Next, not rollout). The bundle now exists on the app, which is what the Play Developer API needs before any script can touch the app (Google's rule: the first upload must come through the console).

## Part 3 — Ajay's laptop pushes the listing and graphics (Claude Code, not you)
Pause and make **no edits in the console** while this runs (about two minutes); a console edit made while an API edit is open discards the API edit. Ajay runs, from `D:\DevTools\ArrowBloom-pub`:

```
node tools\play-status.js <sa-key.json> com.aweagle.arrowbloom
node tools\play-listings-set-multi.js <sa-key.json> com.aweagle.arrowbloom store\listing_v1.json --dry-run
node tools\play-listings-set-multi.js <sa-key.json> com.aweagle.arrowbloom store\listing_v1.json
node tools\play-images-upload.js <sa-key.json> com.aweagle.arrowbloom en-US --dry-run
node tools\play-images-upload.js <sa-key.json> com.aweagle.arrowbloom en-US
```

Listing text goes to 8 locales (en-US, de-DE, es-ES, ja-JP, ko-KR, pt-BR, tr-TR and the default); graphics (icon, feature graphic, 6 phone screenshots) go to en-US and the other languages fall back to them. If `edits.insert` returns 403, the service account `play-publisher@avid-airway-498216-e5.iam.gserviceaccount.com` has no access to the new app: do Part 6 first, then rerun.

## Part 4 — Store settings (you)
Grow users → Store presence → **Store settings**:
- App category: **Game → Puzzle**. Tags: pick up to five that exist in the list, preferring Puzzle, Logic, Brain games, Casual, Offline.
- Store listing contact details: email ajaywaghmare00a@gmail.com, website `https://ajay-waghmare.github.io`, phone empty.
- External marketing: leave the default. **Save**.

## Part 5 — App content (you) — Policy → App content
Complete every item that is listed. Expected answers:
1. **Privacy policy**: paste the URL above. Save.
2. **Ads**: *No, my app does not contain ads*. Save.
3. **App access**: *All functionality in my app is available without special access*. Save.
4. **Content rating**: Start questionnaire → email ajaywaghmare00a@gmail.com → category **Game** → answer **No** to every question (violence, sexual content, language, controlled substances, gambling, discrimination, miscellaneous, user interaction, sharing location, digital purchases, unrestricted internet). Save → Next → **Submit** (this is the IARC questionnaire; expected result: Everyone / PEGI 3 / all ages). Report the ratings shown.
5. **Target audience and content** (unlocks after 1 to 3): target age groups **13–15, 16–17, 18 and over** (never any group 12 and under). Store presence question "could the listing unintentionally appeal to children": **No**. Save.
6. **News apps**: *No*. Save.
7. **COVID-19 contact tracing and status apps**: *My app is not a publicly available COVID-19 contact tracing or status app*. Save.
8. **Data safety**: "Does your app collect or share any of the required user data types?" → **No**. Continue to the end and **Save** the form. **Do not click Submit**; tell Ajay it is ready for his click.
9. **Government apps**: *No*. Save.
10. **Financial features**: *My app does not provide any financial features*. Save or submit the declaration.
11. **Health**: *My app does not have any health features*. Save.
12. **Advertising ID**: **No**, the app does not use advertising ID. Save.
13. Anything else shown (for example Child safety standards or a permissions declaration): answer *not applicable / no* and report its exact name. Photo and video, contacts and SMS declarations must not appear because the app requests only VIBRATE; if one appears, stop and report.

## Part 6 — Service account access (you)
Users and permissions → open `play-publisher@avid-airway-498216-e5.iam.gserviceaccount.com`.
- If its **Account permissions** tab shows permissions that apply to all apps, report that and change nothing.
- Otherwise on **App permissions** → Add app → Arrow Bloom → tick: View app information and download bulk reports; Edit store listing, pricing and distribution; Release apps to testing tracks; Manage testing tracks and edit tester lists. **Apply / Save**. Do not grant production release rights.

## Part 7 — Verify (you), after Part 3 has run
1. Main store listing: 8 languages present, app name `Arrow Bloom – Tap Logic Puzzle`, icon, feature graphic and 6 phone screenshots visible on en-US. Report any error flag on the page.
2. Dashboard: list every remaining task and its wording.
3. Policy → App content: every item shows a green tick except Data safety (waiting for Ajay).

## Part 8 — AJAY, in order
1. Merge the `arrow-bloom-policy` pull request in `app-policy` (if not done before Part 5).
2. Data safety → review → **Submit**.
3. Internal testing → the saved release → **Next → Review → Start rollout to Internal testing**; add yourself as a tester (Testers tab, create a list with your Gmail), open the opt-in link on your phone, install, play three gardens and a Daily Bloom.
4. If the Dashboard carries the testing requirement: Testing → **Closed testing** → create a track (name `Closed Alpha`), tester list with at least 12 Gmail addresses or a Google Group, promote the same bundle, **Send for review**, then keep 12 testers opted in continuously for 14 days. After 14 days: Dashboard → **Apply for production** and answer the questionnaire.
5. If the Dashboard does NOT carry it: Production → create release from the same bundle → Send for review → staged rollout 20% → 100%.
6. Merge `release/2026-10-20` into `main` in the ArrowBloom repo once the bundle is uploaded (only Ajay merges to main).

## Part 9 — build 2 (versionCode 2), staged 20 Oct by API
Build 2 (the line-arrow game) is a DRAFT "1.0.0 (2)" on Internal testing AND on Closed testing (track `alpha`, "Closed Alpha"). Build 1 stays live on both until the drafts are rolled out.
1. Test and release → Testing → Internal testing → Releases → the draft "1.0.0 (2)" → Edit release → Next → report every error and warning → ask "GO?" → on GO: Save and publish.
2. Testing → Closed testing → Closed Alpha → Releases → the draft "1.0.0 (2)" → Edit release → Next → report errors and warnings → ask "GO?" → on GO: Save, then Publishing overview → Send for review (ask "GO?" again; this sends build 2, the new listing text and the new graphics for review together).
3. Grow users → Store presence → Main store listing: confirm the new icon (ink and green arrows), the light feature graphic and six light screenshots; report any error flag.
4. Testers tab of Closed Alpha → copy the opt-in links and report them.

## Report-back format (one message per part)
```
PART n — done / blocked
Done: <bullet per step, with the value entered>
Seen but not in runbook: <field names and defaults left>
Blocked: <exact on-screen message>
Needs Ajay: <clicks left for Ajay>
```
