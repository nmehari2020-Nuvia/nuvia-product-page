# Setup Guide — Nuvia Product Page

This repo contains custom Shopify sections, snippets, and a product
template that build the Nuvia product page on top of your existing Dawn
theme. Nothing here touches your live theme until you choose to publish it.

This guide assumes you've never edited Shopify theme code before. Follow it
top to bottom — every click is spelled out.

---

## Step 0 — Duplicate your live theme (do this first)

You'll install everything into a **copy** of your theme, not the live one.
That way you can preview the whole page before anyone else sees it.

1. In your Shopify admin, go to **Online Store → Themes**.
2. Find the theme labeled **"Current theme"** / **"Published"** — that's
   your live theme.
3. Click the **"…"** (three-dot) menu next to it.
4. Click **Duplicate**.
5. Shopify creates a copy in your theme library, usually named something
   like "Copy of [Your Theme Name]". This copy is **not live** — customers
   won't see it until you explicitly publish it.
6. Do all the work below inside this duplicate. If anything goes wrong,
   your live theme is untouched and you can just delete the duplicate and
   start over.

---

## Step 1 — Add the files

You're going to copy each file from this repo into your duplicated theme
using Shopify's built-in code editor. No software to install for this
method.

1. On the duplicated theme's card, click the **"…"** menu → **Edit code**.
2. You'll see a file browser on the left with folders: `Layout`,
   `Templates`, `Sections`, `Snippets`, `Assets`, `Config`, `Locales`.

For **every file** in the table below:

- Click **Add a new section** (or **Add a new snippet**, or **Add a new
  template** — match the column) at the bottom of the relevant folder.
- Type the **exact filename** shown (no `.liquid` needed in the dialog for
  sections/snippets — Shopify adds it automatically; for the template, pick
  **JSON** as the type).
- Shopify opens a blank file. Delete any placeholder content it inserts.
- Open the matching file in this repo, select all, copy, and paste it into
  the Shopify editor.
- Click **Save** (top right of the code editor).

| Repo file | Shopify folder | "Add a new…" filename to type |
|---|---|---|
| `snippets/nuvia-placeholder.liquid` | Snippets | `nuvia-placeholder` |
| `snippets/nuvia-icon.liquid` | Snippets | `nuvia-icon` |
| `snippets/nuvia-price.liquid` | Snippets | `nuvia-price` |
| `snippets/nuvia-fonts.liquid` | Snippets | `nuvia-fonts` |
| `sections/nuvia-announcement-bar.liquid` | Sections | `nuvia-announcement-bar` |
| `sections/nuvia-buy-box.liquid` | Sections | `nuvia-buy-box` |
| `sections/nuvia-lifestyle-strip.liquid` | Sections | `nuvia-lifestyle-strip` |
| `sections/nuvia-testimonials.liquid` | Sections | `nuvia-testimonials` |
| `sections/nuvia-science.liquid` | Sections | `nuvia-science` |
| `sections/nuvia-trust.liquid` | Sections | `nuvia-trust` |
| `sections/nuvia-timeline.liquid` | Sections | `nuvia-timeline` |
| `sections/nuvia-problem.liquid` | Sections | `nuvia-problem` |
| `sections/nuvia-review-feed.liquid` | Sections | `nuvia-review-feed` |
| `sections/nuvia-faq.liquid` | Sections | `nuvia-faq` |
| `sections/nuvia-footer.liquid` | Sections | `nuvia-footer` |
| `templates/product.nuvia.json` | Templates | `product.nuvia` (type: **JSON**) |

**Tip:** add the snippets first, then the sections, then the template last
— the template refers to the sections, and the sections refer to the
snippets, so this order avoids any "not found" warnings while you work
(they're harmless either way and resolve once everything's in place).

### Optional but recommended: faster font loading

Open `Layout → theme.liquid` in the same code editor. Find the closing
`</head>` tag near the top of the file, and just **above** it, add this
one line:

```liquid
{% render 'nuvia-fonts' %}
```

This loads the Playfair Display headline font in a way that never blocks
the page from painting (see "Performance notes" below). **If you skip this
step, nothing breaks** — headlines just render in a plain serif fallback
font instead of Playfair Display until you add it.

---

## Step 2 — Assign the template to your product

1. Go to **Products** in your Shopify admin.
2. Open your Nuvia massager product (or create it first if you haven't —
   set its title, price ($59.99), compare-at price ($119.99), and upload
   product photos to the product's own **Media** section, since the buy
   box's image gallery pulls directly from there).
3. Scroll down the right-hand sidebar to the **Theme template** dropdown.
4. Change it from "Default product" to **`product.nuvia`**.
5. Click **Save**.

---

## Step 3 — Preview before publishing

1. Back on **Online Store → Themes**, find your duplicated theme.
2. Click **Preview** (not Publish).
3. Navigate to your Nuvia product page in the preview.
4. Check it on your phone too: click **Preview** again and open the link on
   your phone, or use the device toggle in the preview bar. Over 80% of
   your traffic is mobile, so this is the view that matters most.
5. Everything will look mostly empty/placeholder at first — see "What's
   placeholder vs. real" below. That's expected before you've added photos
   and real copy.

Only once you're happy with it:

6. Go back to **Online Store → Themes**, click the **"…"** menu on your
   duplicated theme, and click **Publish**. This makes it your live theme.

---

## Editing content afterward

Everything editable lives in the Shopify theme editor, not in code:

1. **Online Store → Themes → Customize** (on whichever theme is currently
   live, or your duplicate while testing).
2. Use the page picker at the top to navigate to your Nuvia product page.
3. Click any section in the left-hand list to edit its settings — headline
   text, images, benefit bullets, FAQ questions, etc.
4. Click **Add block** inside a section to add more benefit bullets,
   testimonials, FAQ items, timeline milestones, and so on.

---

## What's placeholder vs. real, and what you need to do before launch

This build follows two hard rules: **never hardcode a spec you haven't
confirmed**, and **never publish invented review data**. That means several
things need your input before this is launch-ready:

- **Specs** — `research/specs-to-confirm.md` is a checklist of every spec
  (node count, heat range, battery, runtime, weight, etc.) with market
  ranges for reference. None of these numbers are in the page copy. Once
  your supplier confirms them, you can optionally add them into section
  text via the theme editor.
- **Star rating & review count** (Buy Box section) — defaults to a
  labeled placeholder. Turn off "Show star rating" until you have real
  numbers, or replace the values once you do.
- **Testimonials** (Testimonial Wall section) — all 6 quotes and names are
  obviously-fake placeholder text. Replace every one with a real, permitted
  customer quote before publishing.
- **The Trust section** (professional endorsements) — **off by default**.
  It will not appear on your page until you turn on "Show this section" in
  its settings, which you should only do after replacing the placeholder
  photo, name, credentials and quote with a real, permissioned endorsement.
- **Review Feed section** — an empty, styled container. If you use
  Judge.me, Loox, or another review app, follow that app's install
  instructions to get its embed snippet, then paste it into this section's
  "Embed code" block via the theme editor. Without that, it shows a quiet
  placeholder note.
- **Policy links** (Footer section) — pulled automatically from
  **Settings → Policies**. Set up your Refund, Privacy, Shipping and Terms
  of Service policies there and they'll appear in the footer with no extra
  work.
- **Payment badges** (Buy Box section) — pulled automatically from
  **Settings → Payments**. Whatever you've enabled there shows up
  automatically.
- **Images** — every editorial image on the page (lifestyle strip, the
  science mechanism image, the problem section image, trust photos) is an
  upload slot in the theme editor. Until you upload one, that slot shows a
  neutral gray box labeled with the setting name — the page stays fully
  laid out and usable, nothing looks broken.

---

## Performance notes

- **Fonts don't block first paint.** `snippets/nuvia-fonts.liquid` loads
  Playfair Display using a non-blocking pattern: the stylesheet request
  never delays rendering, and text displays immediately in a fallback
  serif font, swapping to Playfair Display once it's ready. If you skip
  adding the snippet to `theme.liquid` (Step 1's optional step), text
  simply stays in the fallback font — no broken layout either way.
- **Images are lazy-loaded and responsive.** Every image below the fold
  uses `loading="lazy"` with a `srcset` built from Shopify's `image_url`
  filter, so phones on mobile data don't download desktop-sized images.
- **No jQuery, no external JS libraries.** The only custom JavaScript is
  the buy box's variant/cart logic and the announcement bar's rotation,
  both vanilla JS, both scoped to their own section.
- **Empty sections cost nothing.** Sections with no content to show (e.g.
  The Trust when turned off, or blocks-based sections with zero blocks)
  render nothing rather than empty wrapper markup.

---

## Alternative: Shopify CLI (optional, for developers)

If you're comfortable with the command line, this is faster than the
admin code editor for pushing many files at once.

```bash
# 1. Install the Shopify CLI if you don't have it
npm install -g @shopify/cli @shopify/theme

# 2. From this repo's root directory, connect to your store
shopify theme dev --store your-store.myshopify.com

# 3. When ready, push to a new unpublished theme on your store
#    (this creates a fresh theme in your theme library — it does NOT
#    touch your live theme)
shopify theme push --unpublished --theme "Nuvia Product Page"
```

Then follow **Step 2** and **Step 3** above using the theme the CLI just
created, instead of a duplicate made in the admin.

**Note:** this repo only contains the Nuvia-specific sections, snippets,
and template — it is not a full Dawn theme checkout. `shopify theme push`
expects a complete theme directory. If you want to use the CLI method,
either:
- Pull your existing theme first (`shopify theme pull`) into a local
  folder, copy this repo's `sections/`, `snippets/`, and `templates/`
  files into it, then `shopify theme push --unpublished`; or
- Use the admin code editor method (Step 1 above), which works file-by-file
  without needing a full theme checkout.
