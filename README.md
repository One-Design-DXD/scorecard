# ODC EOS Scorecard — proof of concept

Sample-data prototype of the EOS scorecard used in L10 meetings. Shown to
leadership ahead of a real build. No live data is connected.

## What's here

- `public/index.html` — the whole prototype, one self-contained file.
  React and Babel load from a CDN and compile in the browser.
- `wrangler.jsonc` — tells Cloudflare to serve `/public` as a static site.

## How it deploys

Pushing to `main` triggers Workers Builds, which deploys automatically.
No build step — the file is served as-is.

Build command: (leave empty)
Deploy command: `npx wrangler deploy`

## Editing

Small copy or number changes can be made in GitHub's web editor: open
`public/index.html`, click the pencil, commit to `main`. The site updates in
about a minute. Anything larger should go through a branch and a pull request.

## Known limitations — this is a prototype, not the build

- Sample data only, seeded so every viewer sees identical numbers.
- In-browser Babel compilation is fine for a demo and too slow for production.
- Inline hex values throughout; ODC Design System 3.0 tokens are Phase 4.
- Edits to goals don't persist — they reset on reload.

The production version replaces this with Vite + React and moves goals and
owners into an editable config store so they can change without a deploy.
