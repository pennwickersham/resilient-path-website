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

---

## Files

```
index.html              the entire site
images/
  book-cover.jpg        front cover, book        (web-sized from the 300 DPI master)
  workbook-cover.jpg    front cover, workbook
  book-back.jpg         back cover, book         (not currently placed on the page)
  workbook-back.jpg     back cover, workbook     (not currently placed on the page)
  wash.jpg              watercolor plate, used as the hero background
  mark.jpg              square crop, used as the favicon and nav mark
  app-screenshot.png    KEEP FROM THE EXISTING REPO
  bwp-logo.jpg          KEEP FROM THE EXISTING REPO
```

`app-screenshot.png` and `bwp-logo.jpg` are not included here — they already exist
in the repo and should stay. If either is missing the page hides that element
rather than showing a broken image icon.

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
