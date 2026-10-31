# Branding guide (draft for approval)

Status: **Draft (phase 3).** Nothing here has been applied to the profile or any repository yet.

## 1. Starting point: what already exists

The guide builds on what is already in your work instead of inventing a new look:

| Source | What it already establishes |
|---|---|
| Your personal-site codebase (private) | Warm-paper light theme and ink-black dark theme; Newsreader (serif) + Inter (sans); a violet accent (`hsl(256 52% 48%)` light, `hsl(258 88% 77%)` dark) next to an ember/coral signature; restrained motion with reduced-motion support |
| QuantumMPV logo (`docs/quantummpv-logo-rounded.png`) | Black tile, white ring, **violet** play triangle, orange dot |
| Fern Wallet wordmark (`docs/branding/wordmark-*.png`) | Its own green identity. Keep it; projects should keep their own brands |
| Ko-fi and Instagram | Both display the name "FAHIM" |
| GitHub avatar | Default identicon, so there is no deliberate identity yet |

Decision: the **personal** identity uses charcoal, warm paper and a single violet accent. The ember/coral from your site stays a project-level colour (it already appears as QuantumMPV's orange dot) and is not used on the profile. This matches your brief, "subtle violet accents, no excessive gradients", and still feels related to your existing site.

## 2. Principles

1. **Editorial over dashboard.** The page should read like a short magazine column, not a control panel. Text first, then a few well-chosen links.
2. **One accent.** Violet marks at most one or two things per screen: a link, a rule, a single node in the motif.
3. **Honest content.** No numbers you can't stand behind, no "expert" labels, no stats widgets.
4. **Projects keep their own brands.** The personal identity frames them and doesn't recolour them.
5. **Works in both GitHub themes and on mobile.** Every image has a light and a dark variant through `<picture>`, and nothing depends on side-by-side layout.

## 3. Colour

Contrast ratios were calculated with the WCAG 2.x formula.

| Token | Hex | Use | Contrast |
|---|---|---|---|
| `ink` | `#1A1A1F` | Text on paper; dark banner background alternative | 15.5:1 on `paper` |
| `charcoal` | `#151518` | Dark surface (banner, dark variant) | — |
| `charcoal-2` | `#1E1E23` | Raised dark surface, hairlines | — |
| `paper` | `#F6F2EA` | Warm light surface (light banner) | — |
| `paper-2` | `#EDE6DA` | Raised light surface, rules | — |
| `bone` | `#ECE7DE` | Text on charcoal | 14.8:1 on `charcoal` |
| `muted-light` | `#5B5763` | Secondary text on paper | 6.3:1 on `paper` |
| `muted-dark` | `#9C97A3` | Secondary text on charcoal | 6.4:1 on `charcoal` |
| `violet` | `#6A4DC4` | Accent on light surfaces | 5.4:1 on `paper`, 4.9:1 on `paper-2` (AA for text) |
| `violet-soft` | `#B4A0F7` | Accent on dark surfaces | 8.1:1 on `charcoal`, 7.4:1 on `charcoal-2` |

Rules:
- No gradients in personal artwork.
- No pure black (`#000`) and no pure white (`#FFF`). The warm off-tones are the identity.
- Violet covers no more than about 5% of any artwork's area.

## 4. Typography

| Role | Typeface | Fallback | Notes |
|---|---|---|---|
| Display (name, section titles in artwork) | **Newsreader** (OFL) | Georgia, serif | Already your site's display face; editorial and slightly literary |
| Text / UI | **Inter** (OFL) | system-ui, sans-serif | Already used on your site |
| Code, IDs (UPI ID, email) | System monospace | — | In Markdown, wrap these in backticks so they render monospace and are easy to copy |

**Technical constraint.** GitHub renders README images through its image proxy. An SVG loaded as an `<img>` **cannot load web fonts**, and Newsreader is not installed on viewers' devices. The banner's text must therefore be **converted to outlined paths** (Inkscape: *Path → Object to Path*, or `fonttools`-based conversion), or it will fall back to Georgia. The banner in phase 4 will use outlined paths for the name, so it looks the same on every device.

Inside the README itself, GitHub controls the fonts. Hierarchy comes only from Markdown structure:
- One `#`-level heading (or none, if the banner carries the name)
- `###` for sections
- Short paragraphs

## 5. Motif, artwork and icons

**Motif: "the ring".** It is a thin hexagonal ring of six small nodes joined by hairlines, with **one node in violet**.
- It nods to chemistry (a benzene ring) without being a literal molecule diagram.
- It reads as a network or graph, which suits software, and works as a small geometric mark.
- It echoes the ring in the QuantumMPV logo.

| Asset | Spec | Status |
|---|---|---|
| Profile banner | 1280×320 SVG, light (`paper` bg, `ink` text) and dark (`charcoal` bg, `bone` text). Left: "Fahim" in Newsreader (outlined), and below it in Inter, muted: "Independent developer · Chemistry student". Right: the ring motif, 1.5 px strokes, one violet node. Nothing else. Target under 15 KB | To be produced in phase 4 |
| Monogram / avatar option | 512×512: a lowercase serif "f" (or "F") centred in the ring on `charcoal`, violet node top-right | Optional; only if you don't want a photo |
| Section dividers | **None.** Markdown `---` is enough | — |
| Icons | **None in the README body.** Links are labelled in plain text ("Instagram", "Email"), which is more accessible and avoids icon clutter. If icons are ever needed elsewhere, use one set (Lucide, ISC licence, 1.5 px stroke, round caps) | — |
| Badges | None on the profile. In project READMEs, only badges that carry live information: latest release, licence, CI status | — |

## 6. Voice and profile copy

- **Voice:** first person, plain and calm. Say what you build and why, without hype.
- **Display name:** `Fahim`. Title case reads more personal than "FAHIM" on GitHub, where the name sits above the username. If you want the all-caps wordmark used on Ko-fi and Instagram, keep "FAHIM"; either works, but choose one and use it everywhere.
- **Bio** (154 of 160 characters):

  > Independent developer and chemistry student. I build Android apps and care about UI/UX, privacy and open source. Also: science, philosophy, books, cinema.

- **Pronouns, location, company:** leave empty unless you want them.

## 7. Contact and support presentation rules

- **Connect** and **Support** are separate sections, with Connect first.
- Connect, in this order:
  1. Instagram https://www.instagram.com/simplyfahimofficial/
  2. Primary email (Tuta), as a `mailto:` link
  3. Alternative email (Gmail), as a `mailto:` link
- Support, in this order:
  1. Ko-fi https://ko-fi.com/simplyfahim
  2. UPI ID `SimplyFahim@Sbi` in a code span. **No QR code.** The existing QuantumMPV QR image hasn't been verified.
  3. One sentence saying that support is voluntary and helps you maintain independent projects.
- Email addresses appear only in the profile README and, where a private contact is genuinely needed, in a repository's SECURITY / PRIVACY / CODE_OF_CONDUCT file. They never go in source code, commit messages or other files.
- Project READMEs link to the profile's support section instead of repeating payment details.
