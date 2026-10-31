# Audit progress and checkpoint

Last updated: 31 Oct 2026 · Branch: `audit/github-presence` (not merged; the live profile is unchanged)

## Last completed checkpoint

**Checkpoint 2: phases 1 and 2 complete for all 5 accessible repositories; phases 3 and 7 drafted.**

## Exact next action

Wait for your answers to the questions below. Then:
1. Phase 4: produce the banner SVGs (light/dark) and the profile README as `drafts/README.md` on this branch. Render and check them, then publish only after approval.
2. Start the critical fixes R-1.1 to R-1.3 as separate PRs in the public repositories.

## Phases

| Phase | Status | Output |
|---|---|---|
| 1. Account inventory | ✅ Complete | `GITHUB_REPOSITORY_INVENTORY.md` |
| 2. Individual repository audits | ✅ Complete (5/5); gaps listed below | `GITHUB_AUDIT_MASTER.md` §2–4 + private appendix |
| 3. Personal branding | 📝 Drafted, awaiting approval | `GITHUB_BRANDING_GUIDE.md` |
| 4. Profile README and contact information | ⏳ Pending: contact and support URLs **verified**, README not yet written | Verified URLs in the inventory |
| 5. Profile improvements | 📝 Recommendations written | Master §1, §5, §6; branding guide §6 |
| 6. Additional opportunities | 📝 Evaluated | Master §7 |
| 7. Consolidated roadmap | 📝 Drafted | `GITHUB_IMPLEMENTATION_ROADMAP.md` |

## Repositories

| Repository | Status | Areas not inspected in depth (honest gaps) |
|---|---|---|
| QuantumMPV (public) | ✅ Fully inspected (12 areas) | Body of `static-analysis.yml` (whether detekt actually runs); full intent-validation code in the exported activities; quickjs-ng version and which `quickjs-libc` modules are linked; Anime4K/hdr-toys licence files in `assets/`; README not visually rendered on GitHub |
| Fern-wallet (public) | ✅ Fully inspected (12 areas) | `BackupArchive.kt` internals; credit-card statement logic; full CODE_OF_CONDUCT; merged-manifest permissions; contents of the stranded branch `fern/design-system` (only diff size measured: 8 commits, 84 files) |
| Fahimofficial (public) | ✅ Fully inspected | — |
| Private repository A | ✅ Fully inspected (12 areas) | Listed in the private appendix |
| Private repository B | ✅ Fully inspected (12 areas) | Listed in the private appendix |
| Not yet inspected | — none — | |

Couldn't be read from the sandbox: Dependabot alerts and code-scanning alerts (HTTP 403 for all repos), and whether "private contributions" is shown on the profile.

## Findings documented

| Group | IDs | Count |
|---|---|---|
| Profile | P1–P10 | 10 |
| QuantumMPV | Q1–Q30 | 30 |
| Fern-wallet | F1–F23 | 23 |
| Profile repo | H1–H3 | 3 |
| Private A | D1–D16 (appendix) | 16 |
| Private B | A1–A14 (appendix) | 14 |

The highest-impact findings:
- **Fern F1:** five "merged" PRs never reached `main`.
- **Fern F2:** the description says the project is unmaintained and links Ivy Wallet's Play listing.
- **QuantumMPV Q8:** four broken screenshot images in the README and on the website.
- **QuantumMPV Q1/Q2/Q5/Q6:** wrong or upstream payment IDs, dead funding links, and an email address that isn't one of yours.
- **One account-level critical item** affecting private repos (see the appendix).

## Where the private findings are

`/projects/sandbox/github-audit-private/PRIVATE_REPOSITORIES_AUDIT.md`, in the sandbox workspace, deliberately **not** committed to this public repository. A permanent private location needs your decision (question 1).

## Questions for you (blocking phase 4 / implementation)

1. **Private findings storage.** Where should the private appendix live permanently? Options:
   - (a) A new private repo, e.g. `Fahimofficial/github-audit`, created via the API.
   - (b) A docs-only branch in one of the private repos.
   - (c) Delivered in chat only.
2. **astermail address.** QuantumMPV's websites use `SimplyFahim@astermail.com`. Should it be replaced by your primary (Tuta) address, or is it still in use?
3. **Display name.** `Fahim` or `FAHIM`?
4. **Avatar.** A photo of your choice, or the monogram from the branding guide?
5. **Hireable.** Keep "Available for hire" on?
6. **Approve** the branding guide (palette, fonts, ring motif, bio text) and the descriptions/topics in master §6.
7. **Fern stranded work.** OK to open a PR that brings `fern/design-system` onto `main` (a new branch, no force-push)?
