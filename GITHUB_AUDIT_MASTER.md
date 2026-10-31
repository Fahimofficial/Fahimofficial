# GitHub presence audit: master report

Account: [Fahimofficial](https://github.com/Fahimofficial) · Audit started 31 Oct 2026 · Branch `audit/github-presence`

Status: **Phases 1–2 complete for all accessible repositories; phases 3–7 drafted.** See `GITHUB_AUDIT_PROGRESS.md` for exactly what was inspected and what remains.

Method:
- Account and repository metadata, branches, releases, issues, PRs and workflow runs were read through the GitHub REST API.
- Each repository was cloned (`--depth 50`) and read file by file.
- External profiles (Ko-fi, Instagram, Sponsors, Buy Me a Coffee, project websites) were checked with live HTTP requests.
- Nothing was built or run. Nothing in any existing repository was changed.

Priority scale: **Critical** (broken, misleading or unsafe now), **High** (fix before promoting the profile), **Medium**, **Low**.

Private repositories were audited with the same depth. Their findings are **not** in this public file; see the progress file.

---

## 1. Profile audit

### What a visitor sees today
1. The display name is "FAHIM" with no bio, website or social links.
2. The avatar is GitHub's default identicon.
3. The README shows only "Hi there 👋", because the rest of the default template is inside an HTML comment.
4. Nothing is pinned, so GitHub shows "Popular repositories". With only 3 public repos, that is QuantumMPV, Fern-wallet and this repo.
5. Both real projects are labelled "forked from …". Fern-wallet's description still says it is **"no longer maintained"**.

A visitor gets no sense of who you are, and is told that one of your two active projects is dead.

### Findings

| ID | Finding | Evidence | Impact | Priority | Recommendation |
|---|---|---|---|---|---|
| P1 | Profile README is the unedited template | `README.md` in this repo: "## Hi there 👋", then a `<!-- … -->` comment | The profile reads as abandoned | High | Replace with the README drafted in phase 4, after your approval |
| P2 | Bio empty | `gh api users/Fahimofficial` → `"bio": null` | Nothing identifies you | High | Use the bio in `GITHUB_BRANDING_GUIDE.md` §6 |
| P3 | Default identicon avatar | `avatar_url` renders the generated violet block pattern | Generic, and unrecognisable next to your Ko-fi and Instagram | Medium | Upload a deliberate avatar: a photo, or the "F" monogram from the branding guide. Use the same image on Ko-fi and Instagram |
| P4 | No social links | `social_accounts` → `[]` | Visitors can't find you elsewhere | Medium | Add Instagram and Ko-fi in profile settings (exact URLs in the inventory) |
| P5 | No website | `"blog": ""` | — | Low | Leave empty until a public personal site exists. Don't use a project site as your personal website |
| P6 | "Available for hire" is on | `"hireable": true` | Sends a signal you may not intend. The profile otherwise presents independent and student work | Low | Turn it off unless you want offers |
| P7 | No pinned repositories | Profile page | GitHub chooses for you | Medium | Pin as in §5 |
| P8 | Profile repo hygiene | Repo `Fahimofficial`: no description, wiki on, Dependabot security updates off | Minor | Low | Add the description "Profile README for Fahim" and turn the wiki off. Dependabot isn't needed; there are no dependencies |
| P9 | Contact and support details are inconsistent across repos | See the inventory, "Existing contact … details" | Visitors may use an outdated email or a wrong UPI ID. Upstream payment IDs ship inside QuantumMPV | High | Make the profile README the single source of truth, then align each repo to it (roadmap R-2) |
| P10 | `FUNDING.yml` points to dead destinations | QuantumMPV `.github/FUNDING.yml:1-4`. Sponsors isn't enabled; `buymeacoffee.com/Fahimofficial` returns 404 | The "Sponsor" button shows broken or empty options | High | Replace with `ko_fi: simplyfahim` and a `custom` UPI note link (roadmap R-2.3) |

---

## 2. Repository audit: QuantumMPV (public)

**Identity.** An Android media player on libmpv. It is an independent continuation and rebrand of [mpvRx](https://github.com/Riteshp2001/mpvRx), and is 1,803 commits ahead and 1,091 behind upstream `master`.
- Single `:app` module with 620 Kotlin files. `versionName "1.4.5"`, minSdk 26, targetSdk 36. Licence AGPL-3.0-or-later.
- 10 stars. 7 releases (5 stable, 2 preview). Website at quantummpv.vercel.app, plus a GitHub Pages preview channel.
- It is your most developed public project and the obvious first pin.

**Inspected:** README, CHANGELOG, CONTRIBUTING, SECURITY, PRIVACY, SUPPORT, CODE_OF_CONDUCT, CITATION, FUNDING.yml, AndroidManifest, network/backup rules, `app/build.gradle.kts`, `settings.gradle.kts`, `gradle/libs.versions.toml`, all 12 workflows (triggers, permissions, pinning, secrets), `dependabot.yml`, issue/PR templates, `AboutScreen.kt` (lines 428–743 and the OSS list 960–1275), `strings.xml`, `ytdl_wrapper.c`, the vendored quickjs directory listing, `index.html`, `preview-site/index.html`, `website/package.json`, and the screenshot and logo directories. File sizes were measured for all Kotlin files.
**Not inspected in detail:** see the progress file.

### Strengths (keep these)
- **CI posture is good.** Every `uses:` is pinned to a 40-character SHA, every workflow has top-level `permissions: contents: read`, and there is no `pull_request_target`. Signing secrets appear only in tag/master-triggered workflows, and `release.yml` uses `environment: production`.
- **Release signing is clean.** Signing happens in CI with `apksigner`, and no keystore or secret is committed (gitleaks runs on every push and PR).
- **Policy code has tests.** 51 unit test files cover policy code (intent sanitising, update integrity, log redaction, torrent consent, DB upgrades).
- **There is a real token-based design system** in `ui/theme/` (DesignTokens, Motion, Spacing, with tests).
- **README and CITATION credit upstream** (mpvRx, mpv-android, mpvKt).

### Findings

| ID | Area | File:line | Evidence | Problem / impact | Priority | Recommendation |
|---|---|---|---|---|---|---|
| Q1 | Support / trust | `app/src/main/res/values/strings.xml:479-487` + 9 locale files (`values-ar/de/es/fr/ja/pt-rBR/ru` ~368-373 & 1634-1636, `values-hi` 358-366, `values-zh-rCN` 1636-1638) | `pref_about_donate_kofi_url` = `https://ko-fi.com/adityanarvekar`, `…_paypal_url` = `https://paypal.me/aadinarvekar`, `…_upi_id` = `aadiinarvekar@upi` | Upstream developer's payment handles ship in your APK. A grep of every `.kt`/`.xml` outside `values*` finds **0 references**, so they are dead resources. If a future change wires them up, donations would go to someone else | **High** | Delete all `pref_about_donate_*` keys from every `values*` folder. Usage has been traced and nothing references them |
| Q2 | Support / docs | `CHANGELOG.md:194` | "documented UPI destination `simplyfahim@axl`" | A different UPI ID from the one used everywhere else (`SimplyFahim@Sbi`) | **High** | Correct it to `SimplyFahim@Sbi`, or state that the ID changed |
| Q3 | Support / code | `AboutScreen.kt:478,528,727,731`; `strings.xml:1730`; `README.md:17` | The ID is hardcoded 4× plus once in a resource. The payee name is `pn=FAHIM` in the app and `pn=SimplyFahim` in the README | Values can drift; the payee name is inconsistent | Medium | Keep one `translatable="false"` resource for the ID and payee name, and build the URI from it |
| Q4 | Support / UX | `strings.xml:1727` (`ui_buy_me_a_coffee`) used at `AboutScreen.kt:449` | Card titled "Buy Me a Coffee" whose actions are UPI | Labels a platform that isn't used (and whose page 404s) | Low | Rename to "Support development" |
| Q5 | Funding | `.github/FUNDING.yml:1-4` | `github: Fahimofficial` (Sponsors not enabled), `buy_me_a_coffee: Fahimofficial` (404), `custom` → the repo itself | The Sponsor button lists broken destinations | **High** | `ko_fi: simplyfahim` plus a `custom` link to the README support section |
| Q6 | Contact | `index.html:31,34,37`; `fastlane/metadata/android/preview-site/index.html:767-768,785` | `mailto:SimplyFahim@astermail.com`; `instagram.com/SimplyFahimofficial` | The email is not one of your current addresses. Instagram is written in mixed case | **High** (if the address is no longer used) | Replace with the primary Tuta address and the lowercase Instagram URL. **Needs your confirmation** on whether the astermail address should stay |
| Q7 | Contact | `SECURITY.md:21-22`; `SUPPORT.md:34`; `CODE_OF_CONDUCT.md:30-32` | "contact the maintainer through the channels listed in SUPPORT.md". SUPPORT.md lists no private channel | Circular reference: Code of Conduct reporters have no private route | Medium | Point to GitHub private vulnerability reporting for security, and to the primary email for conduct matters |
| Q8 | README | `README.md:44,50,57,58`; `index.html:29` | `phoneScreenshots/player.png`, `videoscreen.png`, `playlistwindow.png`, `chapters.png` | **These files don't exist.** The folder has `player-controls.jpg`, `playlist-window.jpg`, `chapter-navigation.jpg` and others. Broken images appear on the README and the website | **Critical** | Point the references at the existing files |
| Q9 | README structure | `README.md:13-20, 28-30, 467/473, 497-505` | The UPI callout comes before the project description. An empty `[!IMPORTANT]` callout. "Special thanks to SunnyVishnu3" appears twice. A second UPI block at the end | The first mobile screen is a payment request. The duplicates look careless. 505 lines | Medium | Order: description → screenshots → features (collapsed) → download → build → support (once) → credits |
| Q10 | README | `README.md:17` | `[Pay via UPI app](upi://pay?…)` | GitHub's sanitiser normally drops non-http(s) link schemes, so this is likely unclickable on github.com (not rendered here) | Low | Keep the copyable ID. Use the `upi://` link only in-app and on the website |
| Q11 | README | `README.md:9,33-36,489-495,500` | 8 shields.io badges, no `alt` text on 33-36, a star-history embed | Mild clutter; accessibility gap | Low | Keep release, licence and CI badges with `alt` text. Drop "Platform" and star history |
| Q12 | Security | `res/xml/network_security_config.xml:5` | `<base-config cleartextTrafficPermitted="true">` | App-wide cleartext. A comment says Jellyfin LAN enforcement lives in `JellyfinClient`, but other HTTP clients (updates, AI, subtitles) aren't covered by the platform default | Medium | Default to `false`; allow cleartext only where needed. Streams via libmpv don't use Android's stack anyway |
| Q13 | Permissions | `AndroidManifest.xml:17-18,25,27,50` | `MANAGE_EXTERNAL_STORAGE`, `REQUEST_INSTALL_PACKAGES`, `RECORD_AUDIO`, `requestLegacyExternalStorage` | Sensitive permissions without a per-permission explanation in PRIVACY.md | Medium | Add a "Permissions and why" table to PRIVACY.md |
| Q14 | Exported components | `AndroidManifest.xml` (MediaScanReceiver `exported="true"` with `file` scheme; PlayerActivity, QuickDownloadActivity and TorrentSelectionActivity exported) | — | Other apps can send intents. Sanitiser and consent tests exist, which suggests mitigation | Medium | Review QuickDownload/TorrentSelection validation; register the scan receiver at runtime if possible |
| Q15 | Backup rules | `data_extraction_rules.xml:11-20` vs `backup_rules.xml:3-8` | `sftp_known_hosts.xml` is excluded in one file only | Inconsistent backup scope | Low | Exclude it in both |
| Q16 | Native | `app/src/main/cpp/third_party/quickjs/` | Vendored quickjs-ng with no version record. 20+ closed scanner issues (#114–#136) point at `quickjs-libc.c` | Manual patching burden; it's unclear whether `os`/`std` are exposed to scripts | Medium | Record the upstream commit in a `VERSION` file and document which modules are linked |
| Q17 | Dependencies | `gradle/libs.versions.toml:34,54` | `material3 1.5.0-beta02`, `biometric 1.4.0-alpha07` | Pre-release libraries in stable builds; biometric gates the Secure Folder | Medium | Use stable biometric; track material3 stable |
| Q18 | Architecture | `PlayerActivity.kt` 8,346 lines; `PlayerViewModel.kt` 7,030; 13 more files over 1,700 | — | God classes are hard to test, review and merge from upstream | Medium | Extract subsystems (tracks, subtitles, gestures, PiP, Cast) gradually. Don't do a big-bang refactor |
| Q19 | i18n | 86 `Text("…")` literals in `ui/` (e.g. `AboutScreen.kt:574,721,723,738`) | — | Untranslatable, though the app ships 10 locales | Medium | Move them to `strings.xml`; enable lint `HardcodedText` |
| Q20 | Accessibility | 457 `contentDescription = null` across `app/src/main/java` | e.g. `AboutScreen.kt:441` | Many are decorative, but icon-only buttons need labels | Medium | Audit `IconButton`s first |
| Q21 | Attribution | `AboutScreen.kt` OSS list 960-1275 | Lists libmpv, mpvlibAndroid and quickjs-ng. **Doesn't credit mpvRx, mpvKt, mpv-android, Anime4K or hdr-toys**, though shaders from the last two ship in `assets/shaders/` | Incomplete in-app attribution for a fork. AGPL: the app links the repo but not the exact source for the build | Medium | Add an "Upstream & shaders" section with licences, and link the tag for the running version |
| Q22 | Website | `preview-site/index.html` | Names only libmpv and AGPL | No upstream credit on the preview site | Low | Add a credit line |
| Q23 | Privacy doc | `PRIVACY.md:5` | "Last updated: 2026-09-19". Last commit to the file was 2026-10-09. AI, Jellyfin, subtitle providers, torrent and similar features aren't listed | The policy lags behind the network features | Medium | List every network-calling feature; update the date when the content changes |
| Q24 | Repo hygiene | Root: `favicon.svg` (600 KB, embedded PNG), `favicon.png` (450 KB), `upi-qr.png` (355 KB; byte-identical copy in `res/drawable-nodpi/upi_qr.png`; unused third QR at `fastlane/.../upiqr-code.svg`), report files (`IMPLEMENTATION_REPORT.md`, `NAVIGATION_IMPROVEMENTS.md`, `UI_UX_REFINEMENT_SUMMARY.md`, `MPVRX_CUSTOM_COMMANDS.md` + `QUANTUMMPV_CUSTOM_COMMANDS.md`) | — | Cluttered root and oversized favicons | Low | Move reports to `docs/`, remove the MPVRX duplicate after checking links, compress the favicons, and delete the unreferenced SVG QR |
| Q25 | UPI QR | `upi-qr.png`; README:18,499 | Existing QR image | The QR's payload was **not decoded or verified** in this audit | Medium | Decode it locally (e.g. `zbarimg upi-qr.png`) and confirm it encodes `SimplyFahim@Sbi` before promoting it. The new profile README won't use a QR |
| Q26 | Templates | `.github/ISSUE_TEMPLATE/*.md`, no `config.yml` | Markdown templates | No required fields; security reports aren't routed away from public issues | Low | Convert to YAML issue forms and add `config.yml` with the advisory link |
| Q27 | Release/versioning | `app/build.gradle.kts:28-33,55-56` | `versionName` is hardcoded separately from `releaseVersionCode` | The two can drift | Low | Derive both from one property |
| Q28 | Open work | PRs #162 (CI hardening), #163 (UI/motion fixes) | `mergeable_state: blocked` | Two finished-looking PRs are blocked, probably by a required review or check | Medium | Review and merge, or close |
| Q29 | Metadata | Repo description | 220 characters, ends with a slogan | Long. The slogan duplicates the README | Low | Shorter description in §6 |
| Q30 | Leftover names | `website/package.json` `"name": "mpvrxweb"`; `ui_mpvrx_*` string keys | — | Cosmetic upstream leftovers | Low | Rename the package. Leave the DB class name alone, since renaming it risks migrations |

---

## 3. Repository audit: Fern-wallet (public)

**Identity.** A rebrand and continuation of the archived Ivy Wallet, with its own application ID `com.fernwallet.app` (`app/build.gradle.kts:18`). It is 73 commits ahead of upstream and has 40 PRs in October 2026.
- About 850 Kotlin files: 23 feature modules, 8 shared modules, and 2 `temp` legacy modules.
- GPL-3.0. Attribution to Ivy Apps is clear, in both the README (`README.md:34-39, 141-149`) and the in-app Attributions screen.
- **No Fern release has been published yet.**

**Inspected:** README, CHANGELOG, CONTRIBUTING, SECURITY, `docs/SECURITY.md`, PRIVACY, `docs/Package-Identity.md`, Gemfile, `settings.gradle.kts`, `app/build.gradle.kts`, AndroidManifest, `AppLinks.kt`, `SupportSection.kt`, `ZipUtils.kt`, `RootActivity.kt`/`RootViewModel.kt` (relevant ranges), `AppLockedScreen.kt`, the exchange-rate data source, all 11 workflows (triggers, permissions, pinning, secrets), `dependabot.yml`, issue/PR templates, CODEOWNERS, fastlane files, the branding and screenshot folders, and the PR merge states via the API.

### Strengths
- **Honest docs.** `docs/SECURITY.md` keeps a candid list of open security findings (F1–F16).
- **Zip Slip in backup import is fixed, with tests** (`ZipUtils.kt:99-109`).
- **Locked-down app config.** Cleartext is off, `allowBackup="false"`, and release signing comes from the environment only.
- **Locked-down CI.** All 11 workflows use `permissions: {}` with SHA-pinned actions. Secrets appear only in the `release` environment job.
- **Good presentation assets.** A good README with a light/dark `<picture>` wordmark and 7 screenshots, labelled as preview renders with sample data.

### Findings

| ID | Area | File / location | Evidence | Problem / impact | Priority | Recommendation |
|---|---|---|---|---|---|---|
| F1 | **Stranded work** | PRs #35–#39 | The API shows each was **merged into the previous stacked branch** (`fern/safe-restore` ← `fern/calculation-fixes` ← `fern/hardening` ← `fern/navigation-state` ← `fern/auto-backup` ← `fern/design-system`) *after* #34 had already merged `fern/safe-restore` into `main`. `compare main...fern/design-system` → 8 commits ahead, 84 files | Currency-conversion fixes, app-lock hardening, navigation-state restore, automatic backups and the Fern design tokens are **not on `main`**, though their PRs show "merged". `docs/SECURITY.md` F2/F3 remain open on `main` | **Critical** | Open one PR `fern/design-system → main` (rebase onto main first; main is 27 commits ahead), review, and merge. Then check whether #40 still applies cleanly |
| F2 | Identity | Repo description and homepage | "…no longer maintained. You can fork the code or download the final version from Google Play." Homepage `play.google.com/…id=com.ivy.wallet` | Tells visitors the project is dead and sends them to a different app owned by Ivy Apps | **Critical** | Use the description in §6. Set the homepage to the Releases page (or leave it empty) |
| F3 | App lock | `AppLockedScreen.kt:132-135` → `RootActivity.kt:137-139` | No secure lock screen → `onContinueWithoutAuthentication()` → `unlockApp()` | The lock is silently bypassed | Medium | Part of the stranded #36. Lands with F1 |
| F4 | App lock | `RootViewModel.kt:192-207` | Counts `delay(1000)` ticks | Frozen-process time isn't counted, so the app can resume unlocked | Medium | Same (#36) |
| F5 | Versioning | `gradle/libs.versions.toml:22-23` | `version-name "2025.07.17"`, `version-code "206"` = Ivy's last release | The first Fern tag would reuse upstream's version | **High** (before first release) | Bump before tagging, e.g. `2026.11.x` with versionCode > 206 |
| F6 | Releases | Releases page | 0 releases; tags are all upstream (`v2024.*`, `v2025.07.17-206`) | The README promotes "Signed APKs … on the Releases page", but none exist | **High** | Publish a first release, or reword the README until then |
| F7 | Architecture | `settings.gradle.kts`; `implementation(projects.temp.legacyCode)` in app + 20 modules | 283 Kotlin files in `temp/`; the new `feature/credit-cards` depends on it | The "temporary" legacy module is core and still growing | Medium | Stop new dependencies on `:temp:*`; migrate gradually |
| F8 | RTL | `AndroidManifest.xml:23` | `android:supportsRtl="false"` while `values-ar` ships | Arabic layout isn't mirrored | Medium | Enable RTL and fix start/end, or drop the claim of Arabic support |
| F9 | Play libraries | `libs.versions.toml:116-122`, app `:204,206` | app-update, play-services-tasks, review-ktx, security-crypto | Proprietary libraries in a GPL app; app-update and security-crypto are unused | Medium | Possibly handled by stranded #36 ("no Google Play libraries"). Verify after F1 |
| F10 | Network | `RemoteExchangeRatesDataSourceImpl.kt:17-20` | `@fawazahmed0/currency-api@latest` | Unpinned CDN, no timeouts, can't be turned off | Low/Medium | #36 lists network timeouts; verify after F1 |
| F11 | targetSdk | `libs.versions.toml:21` | `target-sdk = 34` | Below current Play requirements for new apps | Medium (if Play is planned) | Plan 35/36 |
| F12 | Code quality | `app/lint-baseline.xml` (1,311 issues); `config/detekt/baseline.yml` (11,526 lines); `abortOnError=false` | — | Large hidden debt, partly inherited | Medium | Burn down per module; keep gates on new issues |
| F13 | Tests | `feature/credit-cards` | 17 source files, 2 tests | Financial logic is under-tested, against the repo's own CONTRIBUTING:38 | Medium | Add statement and due-date tests |
| F14 | Signing | `app/build.gradle.kts:34-40, 96-97` | Fallback `"IVY7834!DEbug"` for the public `debug.jks`; `demo` builds signed with it | Documented as public (closed issue #4), so not a secret leak. Demo builds share a public signature | Low | Keep as is, or give `demo` its own key. Add a scanner suppression with a reason |
| F15 | Third-party data | `temp/legacy-code/…/OnboardingComponents.kt:105` | `TextFieldValue("<upstream author's personal Gmail address>")` in a `@Preview` (address redacted here) | Upstream author's personal email in your fork | Low | Replace with `user@example.com` |
| F16 | Branches | Remote | `paywall`, 3× `auto-update-2025*`, `deprecated-ivywallet-rewrite-2223`, `gradle-composite-build`, and merged `fern/*` branches | Clutter. `paywall` contradicts the "free" positioning | Low | Delete upstream leftovers after checking that none has unmerged work you want |
| F17 | Support | `README.md:128-132`; `AppLinks.kt:40-73`; `SupportSection.kt` | Support routes to QuantumMPV's website and issue tracker, UPI only | Fern users get sent to another project's issues. Nothing for non-Indian users | Low | Link your profile README's support section (Ko-fi + UPI) and keep Fern's own issue link |
| F18 | Funding | `.github/` | No `FUNDING.yml` | No Sponsor button | Low | Add the same `FUNDING.yml` as QuantumMPV, once fixed |
| F19 | Contact | `PRIVACY.md:48-50`; `CODE_OF_CONDUCT.md` | Only GitHub issues | No private contact for privacy or conduct matters | Low/Medium | Add the primary email to PRIVACY.md and CODE_OF_CONDUCT.md only |
| F20 | Docs accuracy | `CHANGELOG.md:60-61` vs `RootActivity.kt:499-505`; `docs/SECURITY.md` F13 vs CHANGELOG:17-18; `docs/archive/Yoda-Style-Architecture.md:100-102` | "removed Play rating" but `ReviewManagerFactory` remains; size-limit status conflicts; Ivy Telegram links | Small inaccuracies | Low | Correct after F1 lands |
| F21 | Fastlane | `fastlane/Fastfile`, `Appfile` | Play `supply` lanes and a `google-play-console-user.json` reference | Dead unless a Play listing is planned | Low | Remove, or document the plan |
| F22 | Repo hygiene | Root | `.idea/`, `all_modules.gv` committed | Noise | Low | Remove or ignore |
| F23 | Topics | — | No topics | Not discoverable | Medium | Topics in §6 |

---

## 4. Repository audit: Fahimofficial (profile repo, public)

| ID | Finding | Priority | Recommendation |
|---|---|---|---|
| H1 | `README.md` is the default template | High | Replace (phase 4) |
| H2 | No description; wiki enabled; no licence | Low | Description "Profile README for Fahim"; turn the wiki off. A licence is optional. If you add artwork, state "© Fahim, all rights reserved" for the artwork |
| H3 | No CONTRIBUTING (correct for a profile repo) | — | None needed |

---

## 5. Pinned repositories

GitHub allows up to six pins. There are only two public projects with real content, so pin those two and nothing else. Padding the pins with the profile repo adds nothing.

1. **QuantumMPV.** Most mature: releases, website, 10 stars, active.
2. **Fern-wallet.** Only after F1 and F2 are fixed. Until then, the pinned card would still say "no longer maintained".

Add more pins only when another project becomes public and has a release or a working README with screenshots.

## 6. Repository descriptions and topics (proposed)

| Repository | Proposed description | Proposed topics |
|---|---|---|
| QuantumMPV | `Android media player built on libmpv: HDR shaders, Anime4K, subtitles, Cast and Jellyfin. No ads, no trackers. Continuation of mpvRx.` | `android`, `kotlin`, `jetpack-compose`, `libmpv`, `mpv`, `media-player`, `video-player`, `anime4k`, `hdr`, `privacy`, `open-source` |
| Fern-wallet | `Fern Wallet: an open-source, offline money manager for Android. Accounts, budgets, credit cards and backups. Continuation of Ivy Wallet (GPL-3.0).` | `android`, `kotlin`, `jetpack-compose`, `personal-finance`, `money-manager`, `budget`, `expense-tracker`, `offline-first`, `privacy`, `ivy-wallet` |
| Fahimofficial | `Profile README for Fahim` | *(none needed)* |

The descriptions avoid claims that couldn't be verified (such as "production-ready" or user counts). Repository descriptions and topics can be set through the API, so this can be done for you after approval.

## 7. Additional opportunities (evaluated)

| Idea | Verdict | Reason |
|---|---|---|
| GitHub stats cards, streaks, visitor counters, trophies | **Reject** | You asked for no vanity metrics; they also load third-party images on every profile view |
| Skill-icon walls / dozens of badges | **Reject** | A short plain-text list of tools you actually use (from the repos: Kotlin, Jetpack Compose, Room, Coroutines/Flow, Hilt/Koin, Gradle, GitHub Actions, TypeScript, Astro) is easier to read |
| One banner image in the profile README | **Accept** | One SVG in your palette (light/dark via `<picture>`), as a static, lightweight identity marker |
| Shared `FUNDING.yml` | **Accept** | One correct file per public repo: QuantumMPV (fix), Fern (add) |
| Account-level `.github` repository for default community health files (issue forms, SECURITY, CODE_OF_CONDUCT) | **Defer** | Both public repos already ship their own, better-tailored files. Revisit when you have 4+ public repos |
| YAML issue forms in QuantumMPV | Accept (Low) | Fern already has them; this makes the two consistent |
| Social preview images | Accept (Medium) | Fern already has `docs/branding/social-preview.png`, but it has to be uploaded manually in Settings. QuantumMPV needs one |
| Release notes template (`.github/release.yml` categories) | Accept (Low) | Both repos already generate releases; categories make the notes readable |
| Project roadmap file | Accept for QuantumMPV and Fern (Low) | A short `ROADMAP.md` stating status ("preview", "first release pending") supports honest presentation |
| Cross-linking | Accept | Each project README links back to the profile README's support section instead of repeating payment details |
| Personal website link | **Blocked** | No public personal site exists yet |
