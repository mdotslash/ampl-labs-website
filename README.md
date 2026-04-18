# AMPL Labs Site Snapshot 4/17

This archive contains the current static frontend for the AMPL Labs site, centered around a single `index.html` file plus a `content/content.json` language/content model.

## Current structure

```text
ampl-labs/
  index.html
  content/
    content.json
  images/
    hero.png
    hero2.png
    queerhero_featured.png
    case-queerencia.png
    case-sammelsucht.png
    case-loot.png
  privacy.html
  imprint.html
```

## Architecture overview

The current site is still a static site, but it is no longer a single-file-only build:

- `index.html` contains layout, CSS, and JavaScript
- `content/content.json` stores most site copy and bilingual content
- `privacy.html` and `imprint.html` are standalone legal pages
- images are loaded from the `images/` directory
- there is no framework, build step, or compiled bundle

## Major changes in this branch

### Content system
- Migrated major site copy from inline `.en` / `.de` markup into `content/content.json`
- Added runtime language rendering via `data-i18n`, `data-i18n-html`, and `data-i18n-placeholder`
- Updated `<html>` language semantics so both `lang` and `data-lang` are switched at runtime

### Sections now driven by JSON
- Navigation
- Hero
- About
- Partners stats
- Work section heading
- Case study modal copy
- Featured and standard case study card copy
- Contact section labels, placeholders, and status text
- Newsletter copy
- Footer copy
- GDPR banner copy

### Work / case study system
- Replaced hardcoded frontend case study content object with `content.json`-driven case study content
- Unified modal copy and visible work-card copy under the same content source
- Added featured-card rendering from JSON
- Added card tag/year/CTA rendering from JSON

### Lead and contact workflows
- Case study modal submits to Apps Script lead endpoint via `fetch`
- Contact form submits to Apps Script via hidden iframe to avoid CORS issues
- Buttondown newsletter embed is wired directly from the page
- Legal links now point to standalone `privacy.html` and `imprint.html`

## External services currently used

- Google Fonts (`Bebas Neue`, `DM Sans`)
- Google Apps Script web app for contact form intake
- Google Apps Script web app for case study lead capture
- Google Sheets for lead/contact logging
- Resend for case study email delivery
- Buttondown for newsletter signup

## Notes for Claudia

### What changed conceptually
This branch moves the site away from duplicated bilingual DOM and toward a single-source content model. The visual design is largely unchanged, but most editable copy now lives in `content/content.json`.

### What to edit where
- **Global site copy:** `content/content.json`
- **Layout / styles / client logic:** `index.html`
- **Legal copy:** `privacy.html`, `imprint.html`
- **Backend endpoints:** hardcoded in `index.html` JS (`LEAD_ENDPOINT`, contact form `action`)

### Important constraints
- The site is still static and dependency-light by design
- The language system now mixes generic `applyContent()` rendering with a few custom renderers for structured sections:
  - `renderAboutColumns()`
  - `renderPartnerStats()`
  - `renderCaseStudyCards()`
  - `renderInquiryOptions()`
  - `renderGDPR()`

## Recommended deployment checklist

1. Upload `index.html`, `content/`, `images/`, `privacy.html`, and `imprint.html`
2. Confirm all referenced case study images exist:
   - `images/case-queerencia.png`
   - `images/case-sammelsucht.png`
   - `images/case-loot.png`
   - `images/queerhero_featured.png`
3. Verify both Apps Script endpoints are still valid
4. Verify Buttondown form action is correct
5. Test:
   - EN/DE switching
   - hero text + hero background rotation
   - case study modal open/submit
   - contact form submit
   - footer/privacy/imprint links

## Suggested next phase

- Add final copy, images
- Add minimal GA4 and key event tracking
- QA, bb!




## AMPL — Release Notes 4/15 

### Core Additions from V5
- Added **contact form backend** using Google Apps Script + Google Sheets (logging + email notification)
- Added **case study lead capture flow** (modal → Apps Script → Resend API)
- Implemented **daily lead + contact digest** via Apps Script

---

### Major Updates
- Expanded **case study modal**
  - dynamic content (title, description, bullets, image)
  - per-case configuration via `CASE_STUDY_CONTENT`
  - in-modal success/error state (no browser alerts)
- Shifted primary conversion flow to:
  - case study capture OR contact form (removed offerings funnel)

---

### Design / Content Changes
- **Removed offerings section entirely**
  - markup, nav link, and core styling removed
- Refactored **hero layering**
  - fixed z-index so buttons remain clickable
- Simplified **hero eyebrow + supporting text**
- Cleaned up **footer + contact section**
  - removed website line
  - reduced redundancy

---

### Minor / Structural Changes
- Simplified **navigation** (removed offerings link)
- Updated **newsletter integration** to Buttondown embed
- Added **honeypot field** to contact form (spam protection)
- Improved **modal UX + loading behavior**

---

### Notes
- `.offerings-grid` still exists in responsive CSS (safe to remove later)
- Language system unchanged (`.en` / `.de`)
- Visual design preserved outside targeted fixes
