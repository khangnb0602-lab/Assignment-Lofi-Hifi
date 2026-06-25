# ProtoType — BC Doctor Finder
## 1. Where to find the prototype

| Item | Link |
|---|---|
| Live prototype | https://khangnb0602-lab.github.io/PrototypeDemo/ |
| Source repo | https://github.com/khangnb0602-lab/Assignment-Lofi-Hifi |
| Lofi wireframes | `./Lofi/` |
| Hifi wireframes | `./Hifi/` |

This prototype is a single self-contained HTML file (interactive, click-through, all states hard-coded — no `localStorage` needed since every screen is pre-rendered per scenario/branch).

---

## 2. Product

**BC Doctor Finder** — a tool that helps people in BC find a family doctor, walk-in care, or virtual care depending on their situation, while tracking their place on the provincial family-doctor waitlist.

---

## 3. The three scenarios

Each scenario below has a **happy path** (everything goes smoothly) and an **alt path** (something is unavailable and the user is redirected to a fallback).

### Scenario 1 — Newcomer needs care tonight
**Persona:** Maya — Permanent resident, recently arrived in BC, has no family doctor yet.

| Path | Screens |
|---|---|
| Happy path | Onboarding form → Registered (waitlist #847, ~8 mo. wait) → Walk-in clinics list → Clinic detail → Booking confirmed |
| Alt path | No walk-ins available nearby → Virtual visit booked instead |

**Goal demonstrated:** getting an unmatched newcomer onto the waitlist *and* into same-day care, with a graceful fallback to telehealth when no walk-in slot exists.

### Scenario 2 — Priority registration (chronic condition)
**Persona:** David — Type 2 Diabetes, his previous doctor retired. Needs priority placement and continuity of chronic care (medication renewals).

| Path | Screens |
|---|---|
| Happy path | Health profile (condition checklist) → Priority status (#312, ~6 mo., medication countdown) → Chronic-care clinics → Appointment confirmed |
| Alt path | No chronic-care clinics open nearby → Prescription options → Refill confirmed via telehealth |

**Goal demonstrated:** chronic-condition flagging that changes queue priority, and an emergency-refill path when a prescription is about to run out and no in-person clinic is available.

### Scenario 3 — Student health coverage
**Persona:** Priya — International student at UBC. UHIP is active; provincial MSP coverage is still in its waiting period.

| Path | Screens |
|---|---|
| Happy path | Student onboarding → Coverage summary (UHIP vs. MSP waiting-period progress) → Clinics near UBC → Booking confirmed ($0 cost) |
| Alt path | No UHIP clinics open → Other care options (telehealth / book tomorrow / pay-and-claim) → Virtual visit booked |

**Goal demonstrated:** surfacing *what's covered* before showing clinics so an international student never gets an unexpected bill, plus a fallback when no UHIP-accepting clinic is open.

---

## 4. Color Scheme

The palette follows the **BC Government Design System (DS)** convention — chosen because the product is positioned as an official provincial health service, so it borrows the public sector's existing, accessibility-tested color tokens rather than inventing a new brand. Color system: **flat hex / RGB tokens**, used as CSS custom properties (`--token-name`) so every screen pulls from one source of truth.

| Token | Hex | RGB | Used for | Why this color |
|---|---|---|---|---|
| `--prim` | `#003366` | `0, 51, 102` | App bar / header, status bar | BC Government's signature navy — signals trust and an official provincial service. |
| `--gold` | `#FCBA19` | `252, 186, 25` | Accent bar under every header | The BC Gov gold accent stripe; ties the app visually to existing BC.gov services so it feels legitimate, not a 3rd-party app. |
| `--int` | `#1A5A96` | `26, 90, 150` | Primary buttons, links, interactive elements | A slightly lighter, more saturated blue than the header navy — keeps interactive elements distinguishable from static chrome while staying in-family. |
| `--good` | `#2E8540` | `46, 133, 64` | Success states (booked, covered, on waitlist) | Standard accessible green; passes WCAG AA against white and the light green background below. |
| `--goodbg` / `--agoodline` | `#E6F2E9` / `#BFDFC9` | `230,242,233` / `191,223,201` | Success alert backgrounds/borders | Low-saturation tint of the success green so alert banners don't visually shout — reserves strong green only for icons/text. |
| `--awarnbg` / `--awarnline` | `#F9F1C6` / `#E0C463` | `249,241,198` / `224,196,99` | Warning states (no clinics, expiring meds) | Warm amber rather than red — these are *redirect-to-alternative* situations, not failures, so the warning is informative, not alarming. |
| `--warnink` | `#6C4A00` | `108, 74, 0` | Warning text | Dark enough on the amber background to meet contrast requirements while staying in the warm warning family. |
| `--infobg` / `--infoline` | `#EEF4FB` / `#9DC0E0` | `238,244,251` / `157,192,224` | Informational banners (priority flag, coverage notices) | A cool, calm tint of the interactive blue — distinct from both success (green) and warning (amber) so users can scan banner type by color alone. |
| `--sfc` | `#F2F2F2` | `242, 242, 242` | Card surfaces, secondary buttons | Neutral light gray gives cards separation from the white page background without adding another hue to track. |
| `--card` | `#FFFFFF` | `255, 255, 255` | Page/screen background | Clean white keeps focus on content; standard mobile-health-app convention. |
| `--ink` | `#313132` | `49, 49, 50` | Primary text | Near-black (not pure black) for slightly softer reading contrast, still well above AA minimums. |
| `--muted` | `#65656A` | `101, 101, 106` | Secondary text, metadata (distance, time) | Mid-gray clearly de-emphasizes secondary info relative to primary text without disappearing. |
| `--line` / `--fline` | `#D9D9D9` / `#8C8C8F` | `217,217,217` / `140,140,143` | Dividers, input borders | Subtle structural lines that organize the UI without competing with content. |
| `--mapbg` | `#D6E8F0` | `214, 232, 240` | Map preview background | A pale, water-like blue evokes "map" at a glance even in a simplified placeholder visualization. |

**Rationale summary:** the palette is deliberately restrictive — one brand blue, one gold accent, and three semantic colors (green/amber/blue-info) for state communication. This keeps the interface legible for a stressed user trying to find care quickly, and reinforces the product's credibility as a Government–affiliated service.

---
