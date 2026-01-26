# Content Wind Starter (Refreshed)

A production-ready, content-first site powered by Nuxt 3, Nuxt Content, and the Content Wind theme. This repo focuses on clarity, accessibility, and maintainability so it can serve as a portfolio-quality starter or a lightweight documentation site.

## What’s inside

- Nuxt 3 with document-driven routing from Nuxt Content
- TailwindCSS utilities with dark/light mode baked in by the theme
- Reusable UI primitives for Markdown-driven pages (e.g., `::button-link`, `::markdown-block`)
- Prerendering for `/` out of the box; generate or build for other hosting targets

## UI/UX principles applied

- Clear hierarchy and generous whitespace for readable, scannable pages
- Mobile-first layout; comfortable tap targets and line lengths
- Accessible focus states and keyboard-friendly code samples
- Primary/secondary call-to-action patterns with subtle transitions

## Project structure

- `content/` – Markdown pages with front-matter for navigation and SEO
- `components/content/` – Presentation-only building blocks used inside Markdown
- `app.config.ts` – Theme-level configuration (cover image, social links)
- `nuxt.config.ts` – Extends the Content Wind theme and prerender rules

## Getting started

```bash
npm install
npm run dev
```

Then open http://localhost:3000. Edit files in `content/` to see instant updates.

### Available scripts

- `npm run dev` – Start local dev server with HMR
- `npm run build` – Production build (server style)
- `npm run generate` – Static export for CDN/static hosting
- `npm run preview` – Preview the production build locally

## Design decisions

- **Purposeful actions**: `ButtonLink` supports primary and ghost variants plus external handling with proper rel/target attributes and focus rings.
- **Readable demos**: `MarkdownBlock` adds padding, borders, and keyboard scrolling so examples stay legible on mobile and desktop.
- **Content-first copy**: Home/about pages describe the value of the starter instead of the theme internals.

## Editing guidance

- Keep front-matter `navigation.title` set so pages appear in the auto-generated nav.
- Add `head` metadata (description, image) for shareable links.
- Prefer short headings and concise paragraphs; avoid walls of text.
- Test both dark and light modes and keyboard navigation before shipping.

## Deployment

- Static: `npm run generate` and deploy the `dist/` (symlink to `.output/public`).
- Server: `npm run build` then run `.output/server/index.mjs` on your host.

For platform specifics, see the [Nuxt deployment guide](https://nuxt.com/docs/getting-started/deployment).
