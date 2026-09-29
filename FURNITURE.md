# SOSART, Arte en Madera: Project Specifics

Applies the general approach in [STRATEGY.md](STRATEGY.md) to this client.

## Client
- **Business name:** SOSART, Arte en Madera ("art in wood"). Confirmed: it is on the business cards and the shop sign.
- Furniture workshop and showroom in Peru.
- Unique pieces made from Peruvian rain forest wood.
- The showroom is in a town with many English-speaking tourists.
- The client is not very web savvy. Phase 1 shows a fixed set of example pieces, so it has no editing interface. Changes go through the developer. The CMS is phase 2 and e-commerce is phase 3.

## Decisions for This Project
- **Languages:** Spanish (default) and English. Tourists are a key audience, so a native English speaker reviews the English.
- **Tagline:** keep "Arte en Madera" in the header. The English pages carry the subtitle "Art in Wood".
- **Hosting:** Netlify free tier. Products are Markdown/JSON files in the repo, edited by the developer. Decap CMS is phase 2 (see STRATEGY.md).
- **Contact:** WhatsApp button in the header as the primary method, plus a Netlify form for email inquiries.
- **Visibility:** set up a Google Business Profile for the showroom. It matters most for tourists searching nearby.
- **Photos:** the developer shoots them. Plan 6-12 representative pieces with 4 photos each for version 1 (hero, side, detail close-up, back). In-room shots can be added in later updates, and the product fields already allow up to 5 images.

## Domain
`sosart.com` is a premium domain on Namecheap, listed at $11,995. Do not buy it.

Candidates to check, best first:
1. `sosartmadera.com`
2. `sosartenmadera.com`
3. `sosartperu.com`
4. `sosartwood.com` (for English-speaking tourists)
5. `sosart.pe` or `sosart.com.pe`, if the client wants a Peruvian domain

Notes from the Namecheap search:
- `sosart.lat` showed $1.80 for the first year but $40.98/yr retail.
- `sosart.to` was $39.98/yr and has no connection to the business.
- Prefer a `.com` and consider adding a `.pe` later as a redirect to it.
- Check that the name is free on Instagram and Facebook before buying.
- Register in the client's own Namecheap account.

## Provenance
Provenance is the main selling point, so give it real space on the About page and on each product:
- Wood species and how it is sourced.
- Any certification (FSC, or CITES paperwork if applicable). Buyers abroad will ask, and it matters for export later.

## Product Fields
Each product entry (a content file in the repo) includes:
- Name and description in Spanish and English
- Wood species
- Dimensions
- Price (optional in phase 1)
- Up to 5 images, each with ES/EN alt text
- Status: available, sold, or made to order

## Phase 3 Questions Specific to This Client
- Most pieces are one-of-a-kind, so inventory is often 1 of 1.
- Large furniture needs freight quotes rather than flat shipping rates.
- Sales outside Peru bring customs, export paperwork and currency questions.
- Decide whether custom orders take a deposit or full payment.
- **Payment processing in Peru:** check which processors work for a Peruvian business account before choosing a platform. Stripe availability there is limited (verify current support). Alternatives include PayPal, Culqi and MercadoPago. This may decide the platform.

## Next Steps
1. Search Namecheap for the candidate domains above, and check whether the client has existing photos.
2. Scaffold the Astro project with ES/EN structure and a products collection.
3. Photograph 6-12 pieces and write bilingual copy.
4. Deploy to Netlify and set up the Google Business Profile.
