# Karepoint Website & Internal Platform

Behavioral health revenue cycle management (RCM) — internal ops app, facility client portal, and marketing site for **Karepoint Billing Service LLP**.

Karepoint is an India-based team serving US behavioral health and substance use disorder (SUD) treatment facilities (detox, residential/RTC, PHP, IOP, outpatient). Current service focus: **Verification of Benefits (VOB)** and **Prior Authorization (PA)**. Full RCM (denial management, underpayment recovery, payment posting) is on the roadmap.

---

## Repo Structure

All site files live inside the `Karepoint/` subfolder — this is set as the Cloudflare Pages **root directory**, not the repo root.

```
Karepoint/
├── index.html            # Public marketing website
├── kp/
│   └── index.html        # KP Internal Ops app (agent/manager workspace)
├── facility/
│   └── index.html        # Facility Client (FC) portal
├── vob/
│   └── index.html        # Printable/shareable VOB report view
├── _redirects             # Cloudflare Pages redirect rules
├── _headers                # Cloudflare Pages custom headers
└── assets/
    ├── logo/
    │   └── KAREPOINT-logo-only.svg
    └── fonts/
        └── mokoto_regular.ttf
```

---

## Live URLs

| Surface | URL |
|---|---|
| Marketing website | `mykarepoint.com` / `www.mykarepoint.com` |
| KP Internal Ops app | `mykarepoint.com/kp` |
| Facility Client portal | `mykarepoint.com/facility` |
| VOB report view | `mykarepoint.com/vob` |
| Cloudflare Pages preview | `karepoint.pages.dev` |

---

## Hosting & Deployment

- **Repo:** `github.com/karepoint/karepoint-website`
- **Host:** Cloudflare Pages, project name `karepoint`
- **Deploy trigger:** Auto-deploys on every push to `main` (~60 seconds)
- **Root directory (Cloudflare Pages setting):** `Karepoint/`

**To deploy a change:**
1. Edit the relevant file locally
2. Commit and push to `main` (or use GitHub's web UI: *Add file → Upload files → Commit changes*)
3. Cloudflare Pages picks up the push automatically — no manual build step

There is no build toolchain. Each app (`kp/index.html`, `facility/index.html`) is a **single compiled HTML file** containing React + ReactDOM + the app's JS bundle inline, served as a static file.

---

## Tech Stack

- **Frontend:** React (compiled to a single-file HTML bundle, no separate build pipeline in the repo)
- **Backend:** [Supabase](https://supabase.com) — Postgres DB, Auth, and REST API via PostgREST
  - Project: `karepoint-ops`, region: East US (North Virginia)
- **Auth:** Supabase Auth (email/password) + Microsoft Azure AD SSO
- **Hosting:** Cloudflare Pages
- **Domains:** `mykarepoint.com` (PHI/HIPAA-reserved), `karepoint.space` (outreach-only, kept separate to protect the PHI domain's sending reputation)

---

## KP Internal Ops App (`/kp`)

The primary workspace for Karepoint's billing agents and managers.

**Core features:**
- Email/password + Microsoft SSO login, with pending-approval flow for new signups
- Role-based access: CEO, COO, VOB Manager, VOB Agent, PA Agent
- **Trust Tier system** (1–3) controlling how much manager review an agent's work requires before delivery
- Schema-driven VOB form (17 sections), with a Form Builder for managers to adjust fields/sections without code changes
- Facility Directory — multi-location NPI/TIN/address/phone, auto-populates into VOB forms on facility selection
- Payer Directory — manager-managed master list of payers and SOPs; agents select from a dropdown, cannot add directly
- Manager Queue / Agent Queue for VOB request assignment and review
- **User Admin Panel** (CEO/COO only) — create users with temp passwords, edit role/tier/status, deactivate/reactivate, trigger password resets
- Sticky notes + call timer for live-call workflow support
- Prelim Panel + mock EDI eligibility check

**Known limitations (not yet built):**
- No EMR integration — patient/clinical data entry is manual
- No Availity or payer-portal submission — PA delivery is manual (email/fax/phone)
- No AI-based approval prediction or denial risk scoring
- No automated carve-out routing (Optum BH / Carelon / Magellan discovery is manual)
- No automated concurrent-review expiration alerts — tracking is currently manual
- AI Assistant panel calls `api.anthropic.com` directly from the browser and will not work until a backend proxy is added

---

## Facility Client (FC) Portal (`/facility`)

Lets facility staff submit VOB/PA requests and check status without contacting Karepoint directly.

- Facility signup flow
- VOB/PA request submission
- Status visibility on submitted requests
- Clients tab (contract management, PA-only → VOB+PA upgrade) — **on roadmap, not yet built**

---

## Database (Supabase)

Key tables:

| Table | Purpose |
|---|---|
| `users` | App users — note: real columns are `full_name` and `trust_tier`, **not** `name`/`tier`. The app normalizes these on read; all writes must use the real column names. |
| `vob_requests` | VOB/PA request records |
| `payer_sops` | Master payer list + SOP rules |
| `facilities` | Facility directory, multi-location NPI/TIN |
| `form_schema` | Configurable VOB form sections/fields (Form Builder) |
| `loc_schema` | Level-of-care definitions (no `updated_at` column — don't send one) |

Row Level Security (RLS) must have an `allow_all` policy on each of the above tables for writes to succeed. See handoff notes for the exact SQL if RLS gets reset.

Free-tier Supabase **pauses after 7 days of inactivity** — upgrade to Pro ($25/mo) before onboarding paying clients to avoid this.

---

## Authentication

- **Email/password:** Standard Supabase Auth, restricted to `@mykarepoint.com` addresses for internal users
- **Microsoft SSO:** Azure AD App Registration, configured as a Supabase Auth provider
- New signups land in a `pending` state until a manager approves them and assigns a trust tier in the Team tab
- CEO account (`suvraneelm@mykarepoint.com`) has a bypass that auto-corrects its status/role on login regardless of DB state

---

## Roadmap

Karepoint's product roadmap moves in phases, from a manual-hybrid service to a fully automated, AI-assisted RCM platform:

1. **Phase 1 (current):** Manual VOB/PA workflows, organized through this app, delivered by offshore billing agents
2. **Phase 2:** EMR connectors, Availity integration, carve-out routing automation, expanded payer database, call recording
3. **Phase 3:** Predictive approval-likelihood scoring, automated concurrent review tracking and expiration alerts
4. **Phase 4:** Full RCM — denial management, underpayment recovery, payment posting; transition toward managed-services/revenue-share pricing

---

## Brand

| Color | Hex | Use |
|---|---|---|
| Teal | `#377985` | Primary / accent |
| Ash | `#EFF4F5` | Backgrounds / panels |
| White | `#FFFFFF` | Base |

---

## Contact

- **Founder/CEO:** Suvraneel Mukherjee — `suvraneelm@mykarepoint.com`
- **COO:** Shilpita — `shilpitad@mykarepoint.com`

---

*This is an internal/private repository for Karepoint Billing Service LLP. Not for public distribution.*
