# Prompt: Complete the Navkar Orthodontic & Dental Clinic Website

Use this prompt with a coding assistant (Claude Code, Claude CLI, or similar) that has file access to the `navkar-dental-site` project folder, to take the current prototype to a client-ready, production-quality site.

---

## Context

You are finishing a 5-page static website for **Navkar Orthodontic & Dental Clinic**, a real dental clinic in Thaltej, Ahmedabad. A first design pass already exists in this folder:

```
navkar-dental-site/
├── index.html      (Home)
├── about.html
├── services.html
├── gallery.html
├── contact.html
├── css/style.css
└── js/script.js
```

**Stack**: plain HTML/CSS/JS, no build tools, no framework. Keep it that way unless told otherwise — it needs to be easy to host anywhere without a build step.

**Design system already in place** (defined as CSS variables in `css/style.css` — read it before changing anything):
- Colors: ivory `#F7F3EC` background, charcoal `#2B2A28` text, sage `#6B8F82` / deep teal `#1F3A34` as the primary structural colors, clay `#C98B6B` as the warm accent.
- Type: `Fraunces` (display/serif, warm and characterful) + `Plus Jakarta Sans` (body), loaded from Google Fonts.
- Signature interaction: a restrained CSS 3D hero scene (layered shapes with mouse-parallax tilt) plus tilt-on-hover cards elsewhere. This is deliberately subtle — the brief was "3D, subtle, attracting," not flashy or gimmicky. Do not add heavy WebGL, particle effects, or aggressive scroll-jacking animation. Respect `prefers-reduced-motion` everywhere (already partially handled — verify it fully disables motion).

**Brand facts to keep accurate anywhere they appear** (don't invent new claims beyond these):
- Lead doctor: Dr. Aesha Acharya Thakkar, B.D.S., M.D.S. — Orthodontics and Dentofacial Orthopedics, Certified Invisalign Practitioner, Senior Lecturer at College of Dental Sciences and Research Center, Ahmedabad.
- Address: Ground Floor-12, Maple Trade Center, Near Surdhara Circle, Thaltej, Ahmedabad – 380054.
- Phone: 079 4604 7016 / +91 87587 53888.
- Hours: Mon–Sat 10am–1pm & 4pm–8pm, Sunday on prior appointment.
- Social: Instagram @navkar_orthodontics, Facebook "Navkar dental Clinic."

---

## What's already built (don't redo)

- Full page structure and navigation across all 5 pages, responsive down to mobile with a slide-in nav.
- Homepage: 3D parallax hero, trust strip, about split, services grid, doctor spotlight, before/after results, testimonials, CTA band, footer.
- About, Services, Gallery (filterable masonry), Contact (booking form UI + map embed placeholder) pages.
- Scroll-reveal animations, tilt-card hover mechanics, mobile nav toggle.

---

## What needs to be finished — work through this list in order

### 1. Real content & imagery
- Replace every image currently borrowed from `navkardental.com` (hero, doctor photo, services, gallery, before/afters) with final, licensed, high-resolution photography of the actual clinic, doctor, and patient results (with consent). Flag clearly which images are still placeholders if real ones aren't available yet.
- Optimize every image: correct dimensions for its container, WebP with a JPEG/PNG fallback, `loading="lazy"` on anything below the fold, explicit `width`/`height` attributes to prevent layout shift.
- Add a real favicon and social share image (Open Graph / Twitter Card meta tags) using the clinic's actual logo/branding.

### 2. Contact form — make it functional
The form in `contact.html` currently only shows a fake success message. Wire it to actually deliver appointment requests — e.g. via Formspree, a simple serverless function, or an email API (ask which the clinic already has, e.g. do they use Gmail/Outlook for the business). Include:
- Server-side (or service-side) validation, not just HTML `required` attributes.
- A real success/error state, not a `setTimeout` fake.
- Spam protection (honeypot field or equivalent — keep it invisible and simple, no CAPTCHA friction for patients).

### 3. Map
Replace the generic search-query map embed with the clinic's actual pinned Google Maps location (get the correct place ID/coordinates from their Google Business listing) so the pin lands exactly on Maple Trade Center, Thaltej.

### 4. SEO & metadata
- Unique, accurate `<title>` and meta description per page (don't just reuse the homepage copy).
- Add structured data (schema.org `Dentist` / `LocalBusiness` JSON-LD) with NAP (name, address, phone), hours, and geo-coordinates — this matters a lot for a local clinic's Google visibility.
- Add a `sitemap.xml` and `robots.txt`.
- Confirm heading hierarchy (one `<h1>` per page) is correct across all 5 pages.

### 5. Accessibility pass
- Verify color contrast (especially charcoal-soft text on ivory, and any text over the dark teal sections) meets WCAG AA.
- Add proper `alt` text to every image (descriptive, not filenames).
- Confirm every interactive element (nav, form fields, filter buttons, mobile toggle) is reachable and operable by keyboard, with visible focus states (a base `:focus-visible` style already exists — check it isn't being overridden anywhere).
- Test with a screen reader (VoiceOver/NVDA) on the contact form and gallery filters specifically, since those are the most interactive parts.

### 6. Performance
- Audit with Lighthouse; target 90+ on Performance, Accessibility, Best Practices, SEO.
- Self-host or preconnect the Google Fonts to reduce render-blocking delay.
- Minify `style.css` and `script.js` for production (keep unminified source versions too).
- Confirm the mouse-parallax hero listener is throttled/cheap enough not to jank on lower-end phones — it currently runs on every `mousemove`; consider `requestAnimationFrame` batching if profiling shows jank.

### 7. Cross-device QA
- Test real device rendering at minimum: iPhone SE-size (375px), a mid-size Android (390–412px), iPad (768px), and a standard laptop (1440px).
- Specifically check: the mobile nav slide-in, the masonry gallery at 1-column, the hero scene on touch devices (parallax should gracefully do nothing on touch, not break layout — current code already gates it behind `pointer: fine`, verify this holds).

### 8. Small completeness items
- Add a simple custom 404 page matching the site's design.
- Add a WhatsApp click-to-chat link/button (the original site had a WhatsApp widget — decide with the client whether to keep it, and if so keep it unobtrusive, bottom-corner, not blocking content).
- Double check every phone number and address string is a working `tel:`/map link.
- Remove or replace any remaining placeholder/lorem content if you find it.

---

## Constraints — do not change these without asking

- Keep the existing color/type tokens and the restrained 3D interaction style — the brief specifically asked for **subtle**, not maximalist.
- No frontend framework or build step unless explicitly requested — this must stay deployable as static files.
- Don't invent new medical claims, credentials, or statistics about the clinic beyond what's listed under "Brand facts" above — verify anything else with the client first.

---

## Deliverable

A finished `navkar-dental-site/` folder, still plain HTML/CSS/JS, ready to upload to any static host (or the clinic's existing hosting), with a short summary of what was changed and a list of anything that still needs the client's input (final photos, form-delivery email address, Google Business place ID, WhatsApp number if applicable).
