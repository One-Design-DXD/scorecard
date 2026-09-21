# Project context for AI assistants

Read this before proposing changes. Working on this repo is constrained in ways
that aren't obvious from the code.

## What this is

A proof-of-concept EOS scorecard for One Design Company, a design studio in
Chicago. Leadership reviews it in weekly L10 meetings. It currently runs on
sample data — nothing is connected to a live system.

## Hard constraints — do not violate these

1. **`public/index.html` is one self-contained file.** React, ReactDOM and
   Babel load from a CDN and the JSX compiles in the browser. There is no
   build step, no `package.json`, no `node_modules`.
2. **Do not add a build step, a bundler, or npm dependencies.** Cloudflare
   deploys this file as-is. Introducing a build breaks deployment silently —
   the site will still serve, just the old version.
3. **Do not add `localStorage`, `sessionStorage`, or any browser storage.**
   State lives in React state and resets on reload. That's intentional.
4. **Do not add external network calls.** No fetch to Harvest, Copper, Google
   Sheets, or any API. Live data arrives in a later phase through a server-side
   function, never from the browser. A browser-side API call would expose
   credentials.
5. **No secrets, API keys, or tokens in this file, ever.** It is served
   publicly to anyone who signs in.

## Style

- Inline styles with hardcoded hex values throughout. This is deliberate for
  now — the ODC Design System 3.0 token migration is a later phase. Match the
  surrounding style rather than introducing Tailwind or CSS modules.
- Plain function components. Existing code mixes `var`/`function` style with
  hooks; follow whatever the surrounding block does.
- The `rnd()` function is a seeded pseudo-random generator so every viewer sees
  identical demo numbers. Do not replace it with `Math.random()`.

## Who edits this

One developer (Brad) plus several non-developers. Favor clear, obvious code
over clever code. If a change needs explaining, it probably needs simplifying.

## How it deploys

Pushing to `main` deploys to production automatically, where leadership sees
it. Work on a branch and open a pull request. Non-production branches get
their own preview URL.

## Known future work — don't start these unprompted

- Rebuild as Vite + React with a real build step
- Move goals, owners and targets to an editable config store
- Connect live data via a single Google Sheet read server-side
- Migrate hardcoded colors to ODC Design System 3.0 tokens
