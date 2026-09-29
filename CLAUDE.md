# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Current State

This repository contains planning documents only. There is no code, `package.json`, build system, or tests yet, so there are no build/lint/test commands. `README.md` is empty apart from a title (`# sosart`).

The project is a website for **SOSART, Arte en Madera**, a furniture workshop and showroom in Peru that sells unique pieces made from rain forest wood. The planned site is a static informational site (phase 1) that later gets a CMS (phase 2) and then e-commerce (phase 3).

## How the Docs Fit Together

- [STRATEGY.md](STRATEGY.md): the general, reusable approach for a small store selling custom products (stack, hosting, domain search, CMS, gallery pattern, phase 3 options, costs).
- [FURNITURE.md](FURNITURE.md): the decisions specific to this client. It applies STRATEGY.md, so when the two differ, FURNITURE.md wins for this project.
- [WORK_ESTIMATE.md](WORK_ESTIMATE.md): phase 1 hours and calendar time.
- [EXISTING_SITES.MD](EXISTING_SITES.MD): design references. They come from search summaries and have not been reviewed. Note the uppercase `.MD` extension.

Keep general guidance in STRATEGY.md and client-specific decisions in FURNITURE.md. Cross-link rather than duplicating.

## Planned Architecture (not yet built)

- **Astro** static site generator. Node is build tooling only, not a server.
- **i18n routing:** Spanish is the default language, with English under `/en`. English is reviewed by a native speaker. Do not ship unchecked machine translation. The English pages carry the subtitle "Art in Wood".
- **Content:** a products content collection in Markdown/JSON. Each product has bilingual name and description, wood species, dimensions, optional price, up to 5 images with ES/EN alt text, and a status (available, sold, or made to order).
- **No CMS in phase 1:** the site shows a fixed set of example pieces, and the developer edits the content files. Decap CMS at `/admin` is phase 2. When it is added, the client must never have to hand-edit JSON.
- **Hosting:** Netlify free tier (deploys on push, Netlify Forms). The client owns the domain and hosting accounts.
- **Product gallery:** main image with a thumbnail strip, CSS scroll-snap and a little vanilla JS with no dependency, and a lightbox. No auto-rotating carousel. Load only the first image eagerly.
- **Contact:** a WhatsApp button in the header is the primary method, with a Netlify form for email.

## Project Facts to Respect

- Do not buy `sosart.com`, which is a premium domain listed at $11,995. FURNITURE.md ranks the candidate domains. Prefer a `.com`.
- Provenance (wood species, sourcing, certification such as FSC or CITES) is the main selling point, so it gets real space on the About page and on each product.
- Phase 3 platform choice depends on payment processors that support a Peruvian business account, and on freight quotes for large items. Decide this before choosing a platform.
- Prices in the cost tables are approximate and from memory. Verify them before quoting.
