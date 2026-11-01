# Lakeland Epoxy Flooring — lead-generation / quote-request site

**Live:** https://lifeofmorr.github.io/lakeland-epoxy-flooring/
**Repo:** lifeofmorr/lakeland-epoxy-flooring (GitHub Pages, `main`)
**What it is:** A referral/marketing service that connects Polk County (Lakeland–Winter Haven, FL)
homeowners and businesses with independent, licensed epoxy flooring installers. It is NOT a
flooring contractor and performs no installations — the site says so in its footer disclosure
on every page. No fake reviews, testimonials, business profile, or phone number anywhere.

## Pages
- `index.html` — hero, services, instant ballpark estimator (interactive, ends at the quote form), pricing ranges, FAQ (with FAQ schema), service-area list
- `garage-epoxy-flooring.html` / `metallic-epoxy-floors.html` / `commercial-epoxy-flooring.html` — service pages
- `epoxy-flooring-winter-haven.html` / `epoxy-flooring-auburndale.html` / `epoxy-flooring-bartow.html` / `epoxy-flooring-plant-city.html` — city pages
- `get-a-quote.html` — native quote form (see below)
- `thanks.html` — post-submit landing (noindex)
- `style.css` + `cinematic.css` — design system (Fraunces + Inter, full-bleed photo hero, glass nav, reveal motion)

## Lead capture (form route)
The quote form posts to **FormSubmit** (activated 2026-11-01):
- AJAX endpoint: `https://formsubmit.co/ajax/b90a59fa12c2c1505f2ff2a47f71afbe`
- Plain-POST fallback (no JS): `https://formsubmit.co/b90a59fa12c2c1505f2ff2a47f71afbe` with `_next` → `thanks.html`
- The alias resolves to `donmondemorrison+epoxy@gmail.com`; submissions arrive as table-formatted
  email in that Gmail inbox. Honeypot (`_honey`) on; failure shows a visible fallback alert with a
  backup Google Form link and the email address.
- **Test-verified 2026-11-01:** test submission returned `{"success":"true"}` and the lead email
  landed in the inbox with all fields (name/phone/email/city/service/size/message).

**Why not FormRelay?** FormRelay (portfolio business #10) is live at
`http://143.47.118.34/formrelay/health` (200, v0.2.0), but it has **no `forms.json` configured** —
every form POST returns `unknown_form` — and the Oracle VM is not SSH-reachable from the agent
environment (`Permission denied (publickey)`; SSH was already flagged "Deny" in the 2026-10-24
audit). A keyed FormRelay form therefore cannot be onboarded agent-side today. When SSH access is
restored, onboard form id `lakeland-epoxy` on FormRelay and swap the two endpoint URLs in
`get-a-quote.html`. The backup Google Form (ID `1FAIpQLSfQyINvX7UorRSDFL8rUIEO5IIanMhuqkMj7ysS4AwbsF5irA`)
remains the documented fallback.

## Contractor outreach (PREP ONLY — nothing sent)
- `prospects.md` — 16 researched local epoxy contractors (public contacts + personalization notes)
- `CALL-SHEET.md` + `outreach/` — call order, scripts, per-prospect drafts. **Do not send without Don's gate.**
