# theresilientpathbook.com

Static site for *Managing Life With Chronic Pain: The Resilient Path*.
One HTML file, no build step, no dependencies. Deploys as-is to GitHub Pages.

---

## Adding the Amazon links

This is the only edit needed to go live. Open `index.html`, scroll to the bottom,
and find this block:

```js
const AMAZON = {
  book:     "",
  workbook: ""
};
```

Paste the Amazon product URLs between the quotes:

```js
const AMAZON = {
  book:     "https://www.amazon.com/dp/XXXXXXXXXX",
  workbook: "https://www.amazon.com/dp/YYYYYYYYYY"
};
```

Every order button on the page reads from this one object, so both edits update
all five buttons at once.

**While a link is empty**, its buttons render as non-clickable and read
"Book — coming soon on Amazon" (or "Workbook — …"). The page never ships a dead
link, and you can publish before the listings are live.

**Now that the listings are live**, the same Amazon URLs are also written into
each order button's `href` and into the structured data (the
`application/ld+json` block in `<head>`), so search engines see them without
running the script. If a listing URL, ISBN, or page count changes, update the
`AMAZON` object, the button `href`s, and the structured data together.

---

## Files

```
index.html              the entire site
404.html                shown by GitHub Pages for any missing URL (noindex)
robots.txt              allows everything, points at the sitemap
sitemap.xml             the one indexable URL; bump <lastmod> when index.html changes
favicon.ico             16/32/48px, cut from images/mark.jpg
apple-touch-icon.png    180px, cut from images/mark.jpg
images/
  book-cover.jpg        front cover, book        (web-sized from the 300 DPI master)
  book-cover-600.jpg    600px copy the page serves to most screens (srcset)
  workbook-cover.jpg    front cover, workbook
  workbook-cover-600.jpg  600px copy, as above
  book-back.jpg         back cover, book         (not currently placed on the page)
  workbook-back.jpg     back cover, workbook     (not currently placed on the page)
  wash.jpg              watercolor plate, used as the hero background
  wash.webp             WebP copy of the wash (q75), served to browsers that take it on wider screens
  wash-900.jpg          900px copy of the wash, served instead on screens 900px wide or less
  wash-900.webp         WebP of the 900px copy (q75), for browsers that take it
  mark.jpg              square crop, used as the favicon and nav mark
  app-screenshot.jpg    Digital Workbook screen (Module 1), cropped from the app
                        repo's public/screenshots/02_workbook.png, 600px wide
  bwp-logo.jpg          publisher crest (square crop of the BWP logo), footer
```

If an image such as the app screenshot is missing, the
page hides that element rather than showing a broken image icon (and the app
section's cards widen to fill the space).

If a cover or the wash changes, regenerate its `-600`/`-900`/`.webp` copy too, or the page keeps showing the old one.

---

## Network links

The footer's "From Brewster Wickersham Publications" block (and the same list in
`404.html`) links to the publisher, the other three sites, the Amazon author store,
and the book and workbook listings. The same list appears on every site in the
network, so change it on all of them together. Our own sites are never `nofollow`.

---

## Deploying

Replace `index.html` and add the new files under `images/`, keeping the two files
noted above. Commit and push to the branch GitHub Pages serves. Keep the existing
`CNAME` file so the custom domain keeps resolving.

---

## Design notes

Colors are sampled from the printed covers, not approximated:

| Token | Hex | Use |
|---|---|---|
| Cream | `#FBF8F4` | page background |
| Aubergine | `#291132` | display type, primary buttons, footer |
| Teal | `#143E46` | secondary display, links, accents |
| Gold | `#B08A3E` | rules, dividers, list markers |
| Warm cream | `#F4EDE3` | alternating section bands |

Type is the covers' own pairing: **Montserrat** at light weights with wide tracking
for display, **Spectral** for body copy. The gold hairline rule with a centered dot
is the covers' divider, reused throughout as the connecting motif.

---

## Changes from the previous version

- Shopify storefront removed. Every "Shop Now" / "Order at Brewster Wickersham
  Publications" link is now an Amazon button driven by the `AMAZON` config.
- Restyled to the cover palette and typography.
- The review submission form was removed; the reviews section is now three static
  quote cards. Replace the placeholder text with real reviews. If you want the
  submission form back, it needs a backend to post to and should be added separately.
- App pricing reads "7-day free trial · $3.99/month · Cancel anytime".
- Social media links removed from the footer (Facebook, Instagram, YouTube,
  TikTok) along with their CSS. A contact email line replaces them.
- Author portraits added to the Authors section (`images/author-wickersham.jpg`,
  `images/author-locker.jpg`). Both are cropped to headshots so the faces read at
  small sizes; the full-length photos remain on the printed back covers.
