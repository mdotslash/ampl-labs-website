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
