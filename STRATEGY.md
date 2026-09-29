# Website Strategy

A strategy for a small to medium store that sells custom or unique products, such as handmade or made-to-order goods. It starts as a simple informational site and grows into a full e-commerce site later. Project-specific decisions live in a separate file; see [FURNITURE.md](FURNITURE.md).

**Goals**
1. Phase 1: a simple, fast, informational site with a fixed set of example products.
2. Phase 2: add a CMS so the owner can update content.
3. Phase 3: grow into a full e-commerce site.

**Constraints**
- The owner must be able to update content without touching code.
- Multiple languages may be needed (the examples assume two).
- Free or near-free running costs.

## Approach

Use Node.js as build tooling, not as a server. Ship a static site now. Add commerce later through a service instead of building cart, checkout and payments from scratch.

## Phase 1: Informational Site

### Stack
- **Astro** (Node-based static site generator)
  - Outputs plain HTML with minimal JavaScript, so it is fast and good for search.
  - Built-in image optimization, which matters when photos are the product.
  - Content lives in Markdown/JSON. Each product (name, materials, dimensions, photos, story) is one entry, and this structure carries into the phase 2 CMS and the phase 3 catalog.
  - Interactive components (React/Svelte) can be added only where needed, such as a cart.
  - i18n routing (for example `/es/...` and `/en/...`) when more than one language is needed.

### Pages
- Home
- Collection / Gallery (6-12 representative products)
- About the business and materials
- Visit the shop (address, hours, map), if there is a physical location
- Contact

### Hosting
| Option | Notes |
| --- | --- |
| GitHub Pages | Free and works for static Astro. No built-in forms, and custom domain and previews are more awkward. |
| Cloudflare Pages | Free, deploys on push, best CDN. CMS login needs a small OAuth setup. |
| **Netlify (recommended)** | Free, deploys on push, built-in forms, smoothest fit with Decap CMS. |

The client should own the domain registration and hosting accounts, with the developer added as a collaborator.

### Domain Name

Registrar: Namecheap. Register the domain in the client's account.

| Ending | Pros | Cons |
| --- | --- | --- |
| **.com (recommended)** | Trusted and typed by default by visitors and foreign buyers. Cheapest professional option (about $10-17/yr). Easy to say aloud. | Short names are mostly taken. No country signal. |
| Country ending (for example `.pe`) | Signals a local business, helps local trust and search. May be free when the `.com` is taken. | Often $30-50/yr. Not every registrar sells it, and registration can need extra steps. Foreign buyers may mistype it as `.com`. |
| .lat | Points at Latin America. | Little known outside the region. Renewal can be far above the intro price. |
| .xyz | Very cheap first year. | Associated with spam, some filters distrust it, and it undercuts a premium brand. Renewals are much higher than the intro price. Not recommended. |

Recommendation: buy a `.com` as the main domain. If the client wants a local presence, add the country ending as a redirect to the `.com`.

#### Searching for an available domain on Namecheap
1. Go to namecheap.com and type the wanted name into the domain search box (or open `namecheap.com/domains/registration/results/?domain=<name>.com`).
2. Read the result for the exact name:
   - A normal price means it is available.
   - A **PREMIUM** badge means a reseller owns it and is charging a speculator price, often thousands of dollars. Do not buy these.
3. Look at the **Suggested Results** list for other endings, but compare the **renewal ("Retail") price**, not the first-year promo price. Some endings show about $2 the first year and $40 or more on renewal.
4. If the exact name is taken or premium, try `.com` variations that add a word instead of switching to an unusual ending, such as `<name><country>.com`, `<name><product word>.com` in each language, or `<name>shop.com`. Also check the country ending.
5. Pick a name that is easy to spell in every language the site uses, with no accents or hyphens.
6. Check that the same name is free on Instagram, Facebook and as a WhatsApp Business name.
7. Before paying, note the renewal price and turn on auto-renew so the domain never lapses. Domain privacy (WHOIS protection) is free with Namecheap. Do not buy Namecheap hosting, since Netlify replaces it.
8. To connect to Netlify, either switch the nameservers to Netlify DNS or add records in Namecheap's DNS panel (an `ALIAS`/`A` record for the root and a `CNAME` for `www`). The second approach keeps email records working if Namecheap Private Email is added later.

### Languages
- Choose a default language and add a visible language switcher.
- Store text for each language in the content files.
- If a large share of visitors read the second language, have a native speaker review it. Do not ship machine translation unchecked.

### Contact
- **WhatsApp button in the header** as the primary contact method where WhatsApp is common.
- Email inquiries through Netlify Forms or Formspree, which email each submission to the owner.
- A Google Form embed works and is free, but it looks off-brand and the owner has to check a spreadsheet.

### Analytics and Visibility
- **Google Business Profile** is the most valuable free item for a shop with a physical location. It puts the business on Google Maps and in local searches, with photos and reviews.
- Analytics: Cloudflare Web Analytics or Plausible-style tools are simple and cookie-free (no consent banner). GA4 is free and acceptable if already familiar, but heavier for a non-technical owner.

### Content Editing for the Client (Phase 2)
The client should not edit JSON by hand. Use a Git-based CMS that writes to the repo through a web form.

| Option | Notes |
| --- | --- |
| **Decap CMS (recommended)** | Free, open source. The client logs in at `/admin`, fills in a form (name, description per language, photos, price), and hits Publish. It commits to the repo and the site rebuilds in about a minute. Best with Netlify. |
| Tina CMS | Free tier, visual editing, but depends on their cloud. |
| Keystatic | Good Astro fit, content stored in repo, free local and GitHub modes. |

Plan about an hour of training for the client.

**Phase 1 skips this.** The site shows a fixed set of example pieces, kept as Markdown/JSON files in the repo and changed by the developer. The CMS is phase 2.

### Photography
- Shoot in landscape at high quality.
- Consistent lighting and a neutral background for catalog shots.
- A few in-context and behind-the-scenes shots for the About page.
- Keep uploaded originals under about 5 MB so the CMS stays quick. Astro resizes and compresses at build time.

### Product Gallery (several photos per item)

Use a **main image with a thumbnail strip** rather than a classic carousel.

| Pattern | Pros | Cons |
| --- | --- | --- |
| **Main image + thumbnails (recommended)** | All angles visible at once, jump to any. Familiar from shopping sites. | Needs some layout work on small screens. |
| Swipe carousel (CSS scroll-snap) | Natural on phones, simple, no library. | Later images are hidden, so add dots or a "1/5" counter. |
| Auto-rotating carousel | Looks lively. | Moves while people look, hurts accessibility, slows the page. Avoid. |
| Grid of all photos | Nothing hidden, easy to build. | Uses a lot of space, no image gets attention. |

Setup:
- Large main image, and clicking a thumbnail swaps it.
- On phones the main image is swipeable with a "1/5" indicator, thumbnails underneath.
- Tapping the main image opens a full-screen **lightbox** to zoom into material and construction detail.
- Image order: clean hero shot first, then side view, detail close-up, back, and an in-context shot.

Implementation:
- Small custom Astro component using CSS scroll-snap and a little vanilla JS, with no dependency. **PhotoSwipe** is a small option if the lightbox is not built by hand. Swiper is heavier than needed.
- Astro's `<Image>` generates responsive sizes. Load only the first image eagerly and lazy-load the rest.
- In the CMS each product has an `images` list (for example up to 5 entries), each with a file and alt text per language. Decap supports this natively, and the client can drag to reorder.
- Always write alt text for search and accessibility.

### Provenance and Story
For handmade or custom goods, the story is a selling point, so give it real space:
- Materials and how they are sourced.
- Any relevant certification. Buyers abroad will ask, and it matters for export later.

## Phase 3: E-commerce

Do not build a cart, checkout and payment system from scratch. Options, in rough order of effort:

1. **Stripe Payment Links or Snipcart** on the existing site. Lowest effort and suits a handful of unique products.
2. **Shopify with Astro as a headless front end** (Storefront API). Shopify handles inventory, tax, shipping and orders, and gives the client an admin they can run themselves. Most practical if the client will manage the shop day to day.
3. **Medusa.js** (open-source, Node.js). Full control and a custom backend, but the developer owns hosting, updates and security.

### Questions to decide early for custom or unique products
- Many items may be one-of-a-kind, so inventory is often 1 of 1. Platforms differ in how well they handle this.
- Large or heavy items need freight quotes rather than flat shipping rates. This often decides the platform.
- International sales bring customs, export documentation and currency questions.
- Decide whether made-to-order items take a deposit or full payment.
- Payment processing: check which processors support a business account in the client's country before choosing a platform. This may decide the platform.

## Costs

Prices are approximate and from memory. Verify them at checkout.

### Phase 1
| Item | Cost |
| --- | --- |
| `.com` domain, first year | About $6-11 (often a promo price) |
| `.com` renewal | About $15-18/yr, billed yearly, not monthly |
| Domain privacy and SSL | Free |
| Hosting (Netlify free tier) | $0. Limits are about 100 GB bandwidth, 300 build minutes and 100 form submissions per month, which is plenty for a small site |
| Astro, analytics, Google Business Profile, WhatsApp | $0 |
| Branded email (optional): Namecheap Private Email | About $1-3 per mailbox per month, billed yearly. The client can start with Gmail. Google Workspace is about $7 per user per month, so skip it unless wanted |

Phase 1 comes to roughly $12 per year with no monthly fees. Free-tier limits can change, but the site is static files, so moving to another free host takes about an hour.

### Phase 3 (rough)
- Stripe Payment Links: no monthly fee, about 3-4% plus a fixed fee per sale.
- Snipcart: about 2% per sale, with a minimum monthly fee of about $20 once sales start.
- Shopify: about $30-40/month plus payment fees.
- Medusa: free software, but about $10-30+/month for server and database hosting plus maintenance time.

## Recommended Stack Summary
- Astro, with i18n routing if more than one language is needed
- Netlify (hosting, forms) on the client's own domain
- Phase 2: Decap CMS for content editing
- WhatsApp button, plus a Netlify form for email inquiries
- Google Business Profile, plus Cloudflare Analytics or GA4
- Phase 3: Shopify headless or Snipcart, depending on how much the client wants to manage

## Next Steps
1. Choose the business's domain (see Domain Name) and check whether the client has existing photos.
2. Scaffold the Astro project with the language structure and a products content collection.
3. Add placeholder products as content files.
4. Photograph 6-12 representative products.
5. Write copy in each language and have it reviewed.
6. Deploy to Netlify, set up Google Business Profile, and hand over.
7. Phase 2: add the Decap CMS config and train the client on it.
8. Phase 3: choose and add a commerce platform.
