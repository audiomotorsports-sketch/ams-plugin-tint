# Cursor / Grok Bot — LA Car Tint plugin

Copy everything below the line. **lacartint.com only.** Branch **v1**. Screenshot phone before production.

---

You are editing **sites/lacartint/** on branch **v1** only. One pass. Do not open other network repos. Do not invent images. Do not rewrite the homepage.

Repo: github.com/audiomotorsports-sketch/audiomotorsport
Vercel root: sites/lacartint
Push to **v1**. Not main. Not redesign-home-five-sites.

## Job
1. Insert the quote plugin **immediately under the existing banner**.
2. **Move** offer-cards so the homepage order becomes:

```
hero-banner
THE NEW PLUGIN
page-short-band
ams-tint-est-band   (simulator)
offer-cards         (MOVED here — contents unedited, keep id="offers")
everything else
cta-band
```

Ask for the customer's information first. Let them play the shade preview. Show ads after.

## Files
1. Save `ams-plugin-tint.css` as `/assets/css/ams-plugin-tint.css`
2. In the homepage `<head>`, after the other stylesheets, add:
   `<link rel="stylesheet" href="/assets/css/ams-plugin-tint.css">`
3. Paste `ams-plugin-tint.html` as specified below.
4. No new photos. Use images already on this site.

## Reorder — cut and paste, do not edit contents

On `sites/lacartint/index.html` the current order (verified on v1) is:

```
<section class="hero-banner">
<section class="offer-cards" id="offers">
<section class="page-short-band page-short-band--home">
<section class="ams-tint-est-band"
```

Cut the **entire** `<section class="offer-cards" id="offers">` block (it currently starts right after the hero). Paste it **immediately after** the estimator band closes (`</section>` of `ams-tint-est-band`). Do not drop `id="offers"`. Do not edit tickets.

## HTML insert

After the move, find this close on the homepage:

```
</section>
<section class="page-short-band
```

That `</section>` belongs to `<section class="hero-banner">`.

Paste the full contents of `ams-plugin-tint.html` **between** those two tags.

If you insert before moving offer-cards, the old anchor is:

```
</section>
<section class="offer-cards"
```

Do the move first, then insert under the banner. Final DOM must match the order list above.

## Do not
- Touch `<section class="hero-banner">` or its images
- Touch estimator internals except (a) moving offer-cards around it and (b) deleting the admin block in P1
- Touch chat (`ams-chat.js`, `#ams-chat`)
- Delete `#offers` or change its contents — MOVE it
- Delete `.mobile-cta-bar` HTML
- Change `:root` colors. This desk is `--accent: #8AA8BC`. Not pods gold. Not alarm steel. Not Beats red. `theme-color` stays `#0B1014`
- Invent photos. Use:
  - `/assets/img/shop-drop-2026-08-20/tint-bmw-after.jpg`
  - `/assets/img/inner/ceramic-film-desktop.jpg`
  - `/assets/img/inner/tesla-tint-desktop.jpg`
  - `/assets/img/inner/hand-cut-desktop.jpg`
  - `/assets/img/shop-drop-2026-08-20/cullinan-day-3m-web.jpg`
- Use the word warranty / guaranteed / lifetime / financing
- Spell the brand "Los Angeles Car Tint"
- Invent reviews
- Print any 3M / Color Stable / Ceramic IR dollar amount
- Invent, infer, average, or do arithmetic on a price
- Struck-through "was" prices

## Prices in the plugin — locked
Only these two, both as **starting at**:
- Solar, full car — **$249** starting
- Solar Ceramic, full car — **$329** starting

3M Color Stable and 3M Ceramic IR are **quote only**. Do not print $399 / $469 / $499 / $549 / $649 / $599 from `tint-pricing.json`. Owner rule and JSON disagree. Do not resolve it. Flag only.

## Sticky bar
`.ams-plug-sticky` has `right: 88px` so `#ams-chat` keeps the bottom-right corner on mobile.
**Hide the sticky at 1024px and up:**

```css
@media (min-width: 1024px) { .ams-plug-sticky { display: none; } }
```

Do not use `left: auto; right: auto` with a fixed width — that parked the pods/alarm bar on the left of desktop content.

Plugin CSS hides `.mobile-cta-bar` only while `#ams-plug-tint` is on the page. Do not delete the old bar HTML.

## Phone / email
- Call: `tel:+13105138800` — (310) 513-8800
- Text: `sms:+12134291092` — (213) 429-1092
- Email: audiomotorsports@gmail.com
- Copy: **Ask for Nick**

## Door URLs
- Solar → `/services/`
- Solar Ceramic → `/services/ceramic-film/`
- Tesla → `/tesla-tint/`
- Hand-cut → `/services/hand-cut/`
- 3M (quote only) → `/services/ceramic-film/`

There is no `/services/solar/` page. Do not invent one.

## P1 — delete the live price editor (same pass)

`sites/lacartint/index.html` has a working admin inside the estimator:

```
<div class="admin" id="admin" hidden>
```

Delete the **entire** `#admin` block. Also remove inline JS listeners for `#addfilm`, `#addveh`, `#asave`, `#areset` or they throw on null and break the simulator.

Same block is in:
- `sites/lacartint/index.html`
- `sites/lacartint/estimator/index.html`
- `sites/lacartint/estimator/la-car-tint-estimator.html`

Click through car → shade → price after the delete. Confirm no console errors. After this pass, served HTML must not contain "Shop admin", "Reset to shop defaults", or "tint-pricing.json".

## P2 — source file in the web root (same pass if cheap)

`sites/lacartint/estimator/la-car-tint-estimator.html` is a 644 KB designer source artifact (no doctype, Preview badge, working Shop admin). Move it **out of the web root** (e.g. `scripts/assets/`). Do not add markup to it.

## P3 — build notes on customer pages (same pass)

Replace **both** the visible FAQ copy **and** the matching FAQPage JSON-LD, word for word:

- `"Payment Plan only — never call it anything else. No 0%. No credit pitch."`
  → `"We quote the film first. If a Payment Plan is the right fit, you can apply at the counter."`
- `"Google shows 4.8 from 654 reviews — that is the schema aggregate only."`
  → `"Google shows 4.8 from 654 reviews for the shop overall, not for this page alone."`

Delete: `"Not a Long Beach Del Amo find-replace."`

Fix generators too or the next build restores them: `scripts/lib/tint-city-*.mjs`

## Flag only — do not do in this pass
- **P4** `/privacy/` and `/terms/` do not exist. Separate pages. Claude writes them later.
- **P5** unused WebP twins (~17 MB). Markup change later. If you touch the hero, change preload and `<img>` together.
- **P6** 109 city pages, zero noindex. Owner decision. Do not bulk-noindex.
- 3M public prices in `tint-pricing.json` vs owner rule. Do not pick a winner.

## Done when
- Banner is byte-identical
- DOM order: banner → plugin → page-short → simulator → offer-cards
- `#offers` still exists, contents unedited, just relocated
- Simulator still works after the admin block is removed
- No "Shop admin" / "Reset to shop defaults" / "tint-pricing.json" in served HTML
- `grep -ci "never call it anything else" sites/lacartint` → 0
- `grep -ci "schema aggregate only" sites/lacartint` → 0
- `grep -ci "warrant\\|guarantee\\|financing" sites/lacartint` → 0
- Only $249 and $329 in the plugin, both "starting at"
- Visible FAQ and FAQPage JSON-LD match word for word
- Every JSON-LD block still parses
- chat, `.mobile-cta-bar`, GTM-5G9HJLQ intact
- Sticky bar hidden above 1024px
- Phone screenshot: Text | Call left, chatbot clear bottom-right
- SMS opens to +1 213-429-1092 with year/make/model if filled

## Post-deploy checks
```
curl -s https://www.lacartint.com/ | grep -c 'id="ams-plug-tint"'
curl -s https://www.lacartint.com/ | grep -ci "shop admin"
curl -s https://www.lacartint.com/ | grep -ci "schema aggregate only"
curl -sI https://www.lacartint.com/estimator/la-car-tint-estimator -o /dev/null -w '%{http_code}\\n'
```

Screenshot **phone** before production merge to branch `v1`.
