# Lean Product Docs Site

A production-ready, content-first site for shipping product docs, playbooks, and release notes that small teams can maintain without a CMS.

## Problem & target users

- **Problem**: Teams ship features faster than they ship clear docs. Changes, runbooks, and onboarding guides get scattered across tools.
- **Target users**: Product managers, engineers, and customer-facing teams who need a single, readable source of truth.
- **Primary use cases**: Publish feature updates with next steps, maintain runbooks/troubleshooting guides, share onboarding checklists.

## Success criteria

- New doc published in minutes (Markdown) without touching layouts.
- Readers can find the right page via auto-generated nav and scannable headings.
- Clear primary/secondary actions on every page (e.g., view feature, contact support).
- Works on mobile and is keyboard-accessible.

## MVP feature set

- Document-driven routing with front-matter for navigation/SEO.
- Reusable call-to-action buttons with primary/ghost variants and safe external handling.
- Styled markdown callouts for readable examples and code.
- Light/dark mode following system preference.
- Prerendered home for fast first load; generate/build for hosting targets.
- Simple heading-based search page to find docs quickly.
- Changelog layout to keep release notes consistent.

## What it does NOT do

- No WYSIWYG or CMS admin panel (Markdown-first authoring).
- No authentication, comments, or search index baked in.
- No complex analytics; you can add your own provider.

## Assumptions & constraints

- Content is text-first and maintained in git; authors are comfortable editing Markdown.
- Small team ownership; prioritize clarity over configurability.
- Keep bundle lean; avoid extra deps unless required for a real need.

## Architecture & structure

- `content/` – Markdown pages with front-matter for navigation/SEO.
- `components/content/` – Presentation-only building blocks used inside Markdown (e.g., `ButtonLink`, `MarkdownBlock`).
- `app.config.ts` – Theme-level configuration (cover image, socials).
- `nuxt.config.ts` – Extends Content Wind and prerender rules.

## UX principles

- Clear hierarchy and whitespace; short headings and scannable bullets.
- Mobile-first layout with generous tap targets and focus-visible states.
- Single primary action plus a secondary ghost action when needed.
- Code/markdown samples are scrollable and readable on small screens.

## Getting started

```bash
npm install
npm run dev
```

Open http://localhost:3000 and edit files in `content/`.

### Available scripts

- `npm run dev` – Start local dev server with HMR
- `npm run build` – Production build (server style)
- `npm run generate` – Static export for CDN/static hosting
- `npm run preview` – Preview the production build locally
- `npm run lint:md` – Lint Markdown formatting
- `npm run lint:links` – Check Markdown links
- `npm run lint:docs` – Run both docs checks

## Example user flow

1. Create `content/feature-x.md` with `navigation.title`, `head.description`, and a concise summary.
2. Add a primary `::button-link` to the feature or support form; add a ghost link to docs or release notes.
3. Preview locally, validate mobile + keyboard navigation, then generate/build and deploy.
4. Update `content/changelog.md` using the `changelog` layout to record releases.

## Known limitations / trade-offs

- No built-in search; use a hosted search or static index if needed.
- No auth; assume docs are public or protected at the host/CDN level.
- Image hosting/CDN not configured; point image URLs to your provider.

## Roadmap (practical)

- Add lightweight client-side search refinements (highlight matches, keyboard nav).
- Add a small changelog index component for multi-release pages.
- Add Markdown/link checks to CI (done); keep extending ignore list as needed.

## Design decisions

- `ButtonLink` includes variants, sizing, focus rings, and safe external defaults for real-world CTAs.
- `MarkdownBlock` adds padding, borders, and keyboard scrolling to keep examples legible on mobile.
- Content pages emphasize outcomes and next steps instead of theme boilerplate.

## Editing guidance

- Set `navigation.title` so pages appear in the auto-generated nav.
- Add `head` metadata (description, image) for shareable links.
- Keep headings short (40–60 chars); lead with outcomes, then steps.
- Test dark/light mode and keyboard navigation before shipping.

## Deployment

- Static: `npm run generate` and deploy `dist/` (symlink to `.output/public`).
- Server: `npm run build` then run `.output/server/index.mjs` on your host.

For platform specifics, see the [Nuxt deployment guide](https://nuxt.com/docs/getting-started/deployment).

---

## Maintenance

Last maintenance update: <!--LAST_UPDATED-->2026-07-15<!--/LAST_UPDATED-->
<!-- changelog:2026-07-09 -->
<!-- Maintenance pass: 2026-07-09 -->
