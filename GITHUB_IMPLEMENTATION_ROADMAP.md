# Implementation roadmap (draft, awaiting approval)

Status: **Draft.** Nothing below has been implemented. Every repository change waits for your approval.

Each item lists:
- **Who:** *Kiro* (can be done from the sandbox via commits, PRs or the API), or *You* (needs GitHub UI or account settings that the sandbox can't change).
- **Depends on:** items that must be done first.

Finding IDs (P, Q, F, H) refer to `GITHUB_AUDIT_MASTER.md`. Items for private repositories are held in the private appendix and only counted here.

## 1. Critical issues

| # | Item | Findings | Priority | Who | Depends on |
|---|---|---|---|---|---|
| R-1.1 | Land Fern Wallet's stranded work: rebase `fern/design-system` onto `main`, open one PR, and review the 84 changed files | F1, F3, F4, F9, F10 | Critical | Kiro opens the PR (no force-push; a new branch); you review and merge | — |
| R-1.2 | Fix Fern-wallet's description and homepage | F2 | Critical | Kiro (API `PATCH repos/…` with `description`/`homepage`). If the proxy blocks it, you do it in Settings | — |
| R-1.3 | Fix the 4 broken screenshot paths in QuantumMPV README and `index.html` | Q8 | Critical | Kiro (PR) | — |
| R-1.4 | Private repositories: 1 critical item (account-level; see appendix) | — | Critical | You | — |

## 2. Profile improvements

| # | Item | Findings | Priority | Who | Depends on |
|---|---|---|---|---|---|
| R-2.1 | Publish the new profile README and banner | P1, H1 | High | Kiro (PR to `main` of this repo) | Approval of the branding guide; R-3.1 |
| R-2.2 | Set the bio, display name, social links (Instagram, Ko-fi) and the hireable flag | P2, P4, P6 | High | You (Settings → Public profile) | Branding guide §6 |
| R-2.3 | Correct `FUNDING.yml` in QuantumMPV and add it to Fern | P10, Q5, F18 | High | Kiro (PR) | — |
| R-2.4 | Align contact details: replace astermail and mixed-case Instagram in the QuantumMPV websites; fix the CHANGELOG UPI; add a private contact route to SECURITY/SUPPORT/CoC | P9, Q2, Q6, Q7, F19 | High | Kiro (PR) | **Your decision on the astermail address** |
| R-2.5 | Pin QuantumMPV, then Fern-wallet | P7 | Medium | You (profile → Customize your pins) | R-1.1, R-1.2 for Fern |
| R-2.6 | Avatar | P3 | Medium | You (upload); Kiro can produce the monogram SVG/PNG | R-3.1 |
| R-2.7 | Profile repo: description and wiki off | P8, H2 | Low | Kiro (API) | — |
| R-2.8 | Turn on "Include private contributions on my profile" (shows activity counts only, no repo names) | — | Low | You (profile → Contribution settings) | — |

## 3. Branding and visual design

| # | Item | Priority | Who | Depends on |
|---|---|---|---|---|
| R-3.1 | Produce the banner (light and dark SVG, outlined text) and the optional monogram | High | Kiro | Branding guide approval |
| R-3.2 | Social preview images: upload Fern's existing `docs/branding/social-preview.png`; create one for QuantumMPV from its logo | Medium | Kiro creates the file; **you upload** (Settings → Social preview, no API) | — |
| R-3.3 | QuantumMPV About card label "Buy Me a Coffee" → "Support development" | Low | Kiro (PR) | — |

## 4. Repository presentation

| # | Item | Findings | Priority | Who | Depends on |
|---|---|---|---|---|---|
| R-4.1 | Set descriptions and topics (master §6) | Q29, F23 | Medium | Kiro (API) | Your approval of the text |
| R-4.2 | Restructure the QuantumMPV README: description first, one support block, no duplicates, `alt` text on badges | Q9–Q11 | Medium | Kiro (PR) | R-1.3 |
| R-4.3 | Fern: publish the first release with a bumped version, or reword the README's Download section until then | F5, F6 | High | You trigger "Prepare release"; Kiro can bump the version via PR | R-1.1 |
| R-4.4 | Review and merge or close the blocked PRs: QuantumMPV #162, #163; Fern #40 | Q28 | Medium | You | R-1.1 for #40 |
| R-4.5 | Delete stale Fern branches (`paywall`, `auto-update-2025*`, `deprecated-ivywallet-rewrite-2223`, merged `fern/*`) | F16 | Low | Kiro lists unmerged commits per branch first; you confirm; then delete | R-1.1 (the `fern/*` branches carry the stranded work) |
| R-4.6 | `.github/release.yml` release-note categories in both public repos | — | Low | Kiro (PR) | — |
| R-4.7 | Short `ROADMAP.md` with honest status in QuantumMPV and Fern | — | Low | Kiro drafts; you edit | — |

## 5. Technical improvements

| # | Item | Findings | Priority | Who |
|---|---|---|---|---|
| R-5.1 | QuantumMPV: remove dead `pref_about_donate_*` resources (10 files) | Q1 | High | Kiro (PR) |
| R-5.2 | QuantumMPV: one source for the UPI ID and payee name | Q3 | Medium | Kiro (PR) |
| R-5.3 | QuantumMPV: move 86 hard-coded strings to resources; audit icon-button labels | Q19, Q20 | Medium | Kiro (PR, in batches) |
| R-5.4 | QuantumMPV: stable `biometric`; track `material3` stable | Q17 | Medium | Kiro (PR) after a CI build |
| R-5.5 | QuantumMPV: incremental extraction from `PlayerActivity` / `PlayerViewModel` | Q18 | Medium | Separate, planned effort, not part of this audit's implementation |
| R-5.6 | Fern: enable RTL or drop the Arabic claim; targetSdk plan; credit-card tests; stop new `:temp:*` dependencies | F7, F8, F11, F13 | Medium | Kiro (PRs), after R-1.1 |
| R-5.7 | Fern: replace the upstream author's email in the preview; hygiene (`.idea/`, `all_modules.gv`) | F15, F22 | Low | Kiro (PR) |
| R-5.8 | QuantumMPV: compress favicons, move reports to `docs/`, remove the unused SVG QR | Q24 | Low | Kiro (PR) |

## 6. Security and privacy

| # | Item | Findings | Priority | Who |
|---|---|---|---|---|
| R-6.1 | QuantumMPV: decode and verify `upi-qr.png` encodes `SimplyFahim@Sbi` | Q25 | Medium | Kiro can decode it in the sandbox (read-only) on approval, or you scan it with a UPI app without paying |
| R-6.2 | QuantumMPV: cleartext default off with scoped exceptions | Q12 | Medium | Kiro (PR), plus your device test on LAN Jellyfin |
| R-6.3 | QuantumMPV: permissions table in PRIVACY.md; list all network features | Q13, Q23 | Medium | Kiro (PR) |
| R-6.4 | QuantumMPV: review exported activities; backup-rule consistency; quickjs version record | Q14–Q16 | Medium/Low | Kiro (PR) |
| R-6.5 | QuantumMPV: complete in-app upstream and shader attribution | Q21, Q22 | Medium | Kiro (PR) |
| R-6.6 | Check Dependabot and code-scanning alerts in each repo's Security tab (not readable from the sandbox) | — | Medium | You |
| R-6.7 | Private repositories: 4 security/privacy items (see appendix) | — | High–Low | Mixed |

## 7. Additional opportunities

| # | Item | Priority | Who |
|---|---|---|---|
| R-7.1 | YAML issue forms + `config.yml` in QuantumMPV (Fern already has forms) | Low | Kiro (PR) |
| R-7.2 | Cross-link: each project README's support line points to the profile README's Support section | Low | Kiro (PR), with R-2.4 |
| R-7.3 | Personal website field: add once a public personal site exists | Low | You |
| R-7.4 | Account-level `.github` repo for default community files | Deferred | — |

## Suggested order

1. **Approve** the branding guide and the decisions in "Questions for you" in the progress file.
2. R-1.2 and R-1.3: quick, low-risk fixes visitors notice first.
3. R-1.1: the largest functional item. Its review takes the longest, so start it early.
4. R-3.1 → R-2.1 → R-2.2 → R-2.6: the new profile.
5. R-2.3, R-2.4, R-5.1, R-5.2: make contact and support consistent everywhere.
6. R-4.1, R-2.5: descriptions, topics and pins, once Fern's identity is fixed.
7. Everything else, by priority.
