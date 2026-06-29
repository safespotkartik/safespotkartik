# SafeSpot — Landing Page

A single-page B2B marketing site for **SafeSpot** smart self-service lockers
(footwear & bag lockers for high-footfall facilities in India). Goal: get
facility owners to call / WhatsApp.

Built as a **plain static site** (HTML + CSS, no build step, no dependencies),
so it can be hosted for free on GitHub Pages.

## Files
```
index.html      Landing page — all 11 sections (nav, hero, stats, problem,
                products, how-it-works, where-it-fits, why, specs, contact, footer)
terms.html      Terms of Service page
privacy.html    Privacy Policy page
styles.css      All styling. Design tokens (colours, fonts, radii, shadows)
                are CSS custom properties in :root at the top.
assets/         Photography + logos (the active pages use 7; the rest are
                spares kept for future use).
```
`terms.html` and `privacy.html` share the same header/footer and styling as the
landing page, and are linked from every page's footer. They cover the whole
service (website, locker platform, mobile apps) under Indian law / Bengaluru
jurisdiction. **These are solid starting drafts — have a lawyer review them
before launch** and fill in any specifics (registered entity details, refund
specifics, a named grievance officer + email for DPDP Act compliance).
Fonts (Archivo + Plus Jakarta Sans) load from Google Fonts via `<link>` in
`index.html`. No other external dependencies.

## Run it locally
It's just static files — open `index.html` in a browser, or serve the folder:
```
python -m http.server 5180
# then visit http://localhost:5180
```

## Editing common things
- **Phone number** — appears in 5 places in `index.html`. Search for the digits
  `9380206421` (used in `tel:` and `wa.me/` links) and the display text
  `93802-06421`, and update every occurrence.
- **Hide the "E-commerce — Coming soon" teaser** — delete the single
  `<!-- E-commerce teaser ... -->` block in the Products section of
  `index.html`. (Content there is provisional until the client supplies details.)
- **Colours / fonts / spacing** — edit the tokens in `:root` at the top of
  `styles.css`; they cascade everywhere.

## Deploy free on GitHub Pages
1. Create a new GitHub repo (e.g. `safespot-landing`) and push this folder's
   contents to the `main` branch.
2. In the repo: **Settings → Pages → Build and deployment → Source: Deploy
   from a branch**, branch `main`, folder `/ (root)`. Save.
3. After ~1 minute the site is live at
   `https://<your-username>.github.io/<repo>/`.

### Point the domain at it (do this when ready — DNS lives at GoDaddy)
The landing page should live at the apex `safespot.in` + `www.safespot.in`.
The AWS product subdomain (e.g. `app.safespot.in`) is **independent — leave its
DNS record untouched.**

In GitHub: **Settings → Pages → Custom domain** → enter `www.safespot.in`, Save.
Then in **GoDaddy DNS**, add only:
- A `CNAME` record: host `www` → value `<your-username>.github.io`
- Four `A` records for the apex `@` → GitHub Pages IPs:
  `185.199.108.153`, `185.199.109.153`, `185.199.110.153`, `185.199.111.153`
  (and optionally the matching AAAA records for IPv6)

Leave **GitHub's "Enforce HTTPS"** ticked once the certificate is issued.

> Do not touch the existing record that points the product subdomain to AWS.

## Notes for whoever maintains this
- No contact form by design — contact is call / WhatsApp only.
- Mobile-first: most traffic is expected on phones. Responsive breakpoints are
  980 / 760 / 620 px (see the bottom of `styles.css`).
- Recreated from the design handoff in `../SafeSpot Locker Landing Page -
  Design Handout.zip`. See that bundle's README for the full spec.
