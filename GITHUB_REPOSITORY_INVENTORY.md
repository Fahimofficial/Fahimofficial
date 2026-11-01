# GitHub repository inventory

Account: [Fahimofficial](https://github.com/Fahimofficial) · Snapshot taken 31 Oct 2026 via the GitHub REST API (`gh api user/repos`, `gh api users/Fahimofficial`).

> **Privacy note.** This file lives in a public repository. The account also has private repositories. Their
> names, descriptions and findings are deliberately left out of this branch and kept in a private appendix
> (see `GITHUB_AUDIT_PROGRESS.md` → "Where the private findings are").

## Account profile (as found)

| Field | Current value | Note |
|---|---|---|
| Display name | `FAHIM` | All caps; matches the name used in QuantumMPV, Fern Wallet and Ko-fi |
| Bio | *(empty)* | Nothing tells a visitor who you are |
| Avatar | Default GitHub identicon (violet blocks) | Not a chosen image |
| Website (`blog`) | *(empty)* | |
| Location / company | *(empty)* | Fine to leave empty |
| Public email | *(not set)* | |
| Hireable | `true` | Shows "Available for hire"; decide deliberately |
| Social accounts | *(none)* | `GET users/Fahimofficial/social_accounts` returns `[]` |
| Twitter/X | *(none)* | |
| Followers / following | 1 / 0 | |
| Public repos / gists | 3 / 0 | |
| Organisations (public) | none | |
| Account created | 25 Sep 2019 | |
| Profile README | Present but still GitHub's default template (all content inside an HTML comment, so the profile shows only "Hi there 👋") | |

## Repositories

| # | Repository | Visibility | Fork of | Language | Licence | Default branch | Stars | Open PRs | Releases | Last push | Status | Audit |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| 1 | [QuantumMPV](https://github.com/Fahimofficial/QuantumMPV) | Public | [Riteshp2001/mpvRx](https://github.com/Riteshp2001/mpvRx) (active upstream) | Kotlin | AGPL-3.0 | `master` | 10 | 2 (#162, #163) | 7 (latest `v1.4.5-preview.2`, 27 Oct 2026; latest stable `v1.4.0`, 18 Oct 2026) | 31 Oct 2026 | Active | **Inspected** |
| 2 | [Fern-wallet](https://github.com/Fahimofficial/Fern-wallet) | Public | [Ivy-Apps/ivy-wallet](https://github.com/Ivy-Apps/ivy-wallet) (archived upstream) | Kotlin | GPL-3.0 | `main` | 0 | 1 (#40) | 0 (only upstream tags `v2024.*`/`v2025.07.17-206`) | 31 Oct 2026 | Active | **Inspected** |
| 3 | [Fahimofficial](https://github.com/Fahimofficial/Fahimofficial) | Public | — | — | none | `main` | 0 | 0 | 0 | 31 Oct 2026 | Profile README repo, created 31 Oct 2026 | **Inspected** |
| 4 | *(private repository A)* | Private | — | — | — | — | — | — | — | — | Active | **Inspected** (findings in private appendix) |
| 5 | *(private repository B)* | Private | — | — | — | — | — | — | — | — | Active | **Inspected** (findings in private appendix) |

No repositories are archived. No repository has topics except QuantumMPV.

## Repository metadata

| Repository | Description (exact) | Homepage | Topics | Wiki | Pages |
|---|---|---|---|---|---|
| QuantumMPV | "QuantumMPV - a powerful, efficient, feature-rich Android media player built on libmpv. HDR, shaders, Anime4K, subtitles, Cast, and deep customization. No ads. No trackers. No noise." | https://quantummpv.vercel.app/ (HTTP 200, title "QuantumMPV \| Android Media Player") | android, kotlin, libmpv, media-player, mpv, open-source | on | on (https://fahimofficial.github.io/QuantumMPV/, HTTP 200, "QuantumMPV — Preview & Stable Releases") |
| Fern-wallet | "Fern Wallet is an open-source money manager app for Android, no longer maintained. You can fork the code or download the final version from Google Play." | `https://play.google.com/store/apps/details?id=com.ivy.wallet` (**Ivy Wallet's listing, not Fern's**) | *(none)* | on | off |
| Fahimofficial | *(none)* | *(none)* | *(none)* | on | off |

## Security settings visible through the API (`security_and_analysis`)

| Repository | Dependabot security updates | Secret scanning | Push protection | Non-provider patterns | Validity checks |
|---|---|---|---|---|---|
| QuantumMPV | enabled | enabled | enabled | disabled | disabled |
| Fern-wallet | enabled | enabled | enabled | disabled | disabled |
| Fahimofficial | disabled | enabled | enabled | disabled | disabled |

Dependabot and code-scanning **alert lists could not be read** from this environment (HTTP 403 from the proxy), so alert counts are not part of this audit. Check them under each repository's **Security** tab.

## Remote branches

| Repository | Branches |
|---|---|
| QuantumMPV | `master`, `ci/security-release-hardening` (#162), `ui/motion-audit-2026-10` (#163), `fix/preview4-vetro-navigation-completion`, `kilo/deep-meteor-m30` |
| Fern-wallet | `main` + 25 others, including upstream leftovers `auto-update-20250720003331`, `auto-update-20250727003336`, `auto-update-20250803003358`, `deprecated-ivywallet-rewrite-2223`, `gradle-composite-build`, `paywall`, three `dependabot/*` branches, and 14 `fern/*`/`fix/*`/`ci/*`/`chore/*` work branches |
| Fahimofficial | `main`, `audit/github-presence` (this audit) |

## Existing contact, social and support details found across public repositories

Searched every file of every cloned repository (excluding `.git`, `node_modules` and lockfiles) for Ko-fi, UPI, Tuta, Gmail, Instagram, PayPal, Buy Me a Coffee and Sponsors references.

| Detail | Where it appears today | Consistent with what you supplied? |
|---|---|---|
| UPI `SimplyFahim@Sbi` | QuantumMPV `README.md:17,18,503`, `AboutScreen.kt:478,528,727,731`, `strings.xml:1730`; Fern-wallet `README.md:131`, `AppLinks.kt:49` | Yes |
| UPI `simplyfahim@axl` | QuantumMPV `CHANGELOG.md:194` | **No**, a different UPI ID |
| Upstream UPI/Ko-fi/PayPal (`aadiinarvekar@upi`, `ko-fi.com/adityanarvekar`, `paypal.me/aadinarvekar`) | QuantumMPV `app/src/main/res/values*/strings.xml` (10 locale files). Not referenced by any code. | **No**, these belong to the upstream developer |
| Email `SimplyFahim@astermail.com` | QuantumMPV `index.html:31,34,37` and `fastlane/metadata/android/preview-site/index.html:768,785` | **No**, not one of the two addresses you supplied |
| Instagram `instagram.com/SimplyFahimofficial` | QuantumMPV `index.html:31,34,37`, `preview-site/index.html:767,785` | Same account (Instagram usernames are case-insensitive), but written in mixed case |
| `.github/FUNDING.yml` | QuantumMPV: `github: Fahimofficial`, `buy_me_a_coffee: Fahimofficial`, `# ko_fi` commented out, `custom` → the repo itself | **No.** GitHub Sponsors is not enabled (`github.com/sponsors/Fahimofficial` redirects to the profile) and `buymeacoffee.com/Fahimofficial` returns 404 |
| Ko-fi | Nowhere in your repositories | Missing |
| Primary (Tuta) / alternative (Gmail) emails | Nowhere | Missing |

## Verified external profiles

| Profile | Verified URL | How it was verified |
|---|---|---|
| Ko-fi | **https://ko-fi.com/simplyfahim** | Page returns HTTP 200; `<title>Support FAHIM</title>`; `og:url` = `https://ko-fi.com/SimplyFahim`; canonical = `https://ko-fi.com/simplyfahim` |
| Instagram | **https://www.instagram.com/simplyfahimofficial/** | Instagram's public profile endpoint returns `username: simplyfahimofficial`, `full_name: FAHIM`, `is_private: false` |
| QuantumMPV website | https://quantummpv.vercel.app/ | HTTP 200 |
| A personal website | **None publicly available.** The only personal-site deployment found sits behind Cloudflare Access (sign-in page), so it cannot be used as the profile website yet. | HTTP 200 to a "Sign in ・ Cloudflare Access" page |
