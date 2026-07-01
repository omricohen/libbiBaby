# libbibaby.com

Marketing site + legal pages for **Libbi** — a sound diary for the womb (iOS/Android).

Static HTML/CSS, no build step. Hosted on **Cloudflare Pages**.

## Structure

```
index.html        Marketing landing page
privacy.html      Privacy Policy   → served at /privacy
terms.html        Terms of Service → served at /terms  (the app's EULA link)
assets/
  styles.css      Shared design system (Fraunces + Hanken Grotesk, night-sky theme)
  icon.png        App icon
_headers          Cloudflare security + caching headers
robots.txt, sitemap.xml
```

Cloudflare Pages serves extensionless URLs automatically, so `privacy.html` is
reachable at `/privacy` and `terms.html` at `/terms`. The iOS app links to
`https://libbibaby.com/terms` and `/privacy` from the paywall — **do not rename
these files** without updating `_termsUrl` / `_privacyUrl` in the app's
`paywall_screen.dart`.

## Local preview

```sh
python3 -m http.server 8000
# open http://localhost:8000
```

## Deploy (Cloudflare Pages)

1. Push this repo to GitHub.
2. Cloudflare dashboard → **Workers & Pages → Create → Pages → Connect to Git** →
   pick this repo.
3. Build settings: **Framework preset: None**, **Build command: (empty)**,
   **Build output directory: `/`**. Save and deploy.
4. **Custom domain:** Pages project → **Custom domains → Set up a custom domain** →
   `libbibaby.com` (and `www.libbibaby.com`). Cloudflare provisions SSL
   automatically once DNS resolves.

DNS for `libbibaby.com` must be on Cloudflare for the custom domain to attach
cleanly (move the nameservers at the registrar to the ones Cloudflare assigns).

## Editing prices / legal

Legal copy mirrors `lynn/docs/legal/*.md` in the app repo. Subscription pricing
appears in `terms.html` (§5) and `index.html` (#premium / #faq): currently
**$1.99/mo, $20/yr, 7-day trial**. Keep these in sync with App Store Connect /
Play Console and the app paywall.
