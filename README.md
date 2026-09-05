# Mountain Car — Landing Page

![Quality Gate](https://github.com/kamiljan11/mountaincar-landing/actions/workflows/quality.yml/badge.svg)

**Status:** production · **Built & operated by** [Kamil Jan](https://kamiljan.com)

Single-page entry point for **Mountain Car** — car rental and garage services near Keflavík
airport, Iceland. One business, two halves; this page sends the visitor to the right one.

## What it is

A hand-written static `index.html`. No framework, no build step, no dependencies, no
`package.json` — the page is the artefact. For a landing page whose job is to load instantly
on airport wifi and route a visitor in one click, a bundler would be cost without benefit.
See [`docs/ARCHITECTURE.md`](docs/ARCHITECTURE.md) for the full map, and
[`docs/adr/0001-static-hosting-vercel-not-lovable.md`](docs/adr/0001-static-hosting-vercel-not-lovable.md)
for why it's built this way instead of the fleet's usual Lovable stack.

## Stack

Static HTML + CSS, deployed on Vercel (`vercel.json`). No environment variables — there is
no backend, so there is nothing to put in an `.env` file.

## Running locally

Open `index.html` directly in a browser, or serve the folder so relative paths behave the
same as production:

```bash
python -m http.server 8000
```

Then visit `http://localhost:8000`.

## Testing

`e2e/smoke.spec.ts` is a Playwright smoke spec (page loads, no console errors). It is **not
wired to a runner yet** — the repo has no `package.json`/`playwright.config.ts`, so
`npx playwright test` cannot resolve the `@playwright/test` import today (verified
2026-09-05). The "E2E smoke" CI job step-skips until that's fixed rather than failing.
Tracked in [`docs/quality/BACKLOG.md`](docs/quality/BACKLOG.md).

## Deploying

Push to `main` — Vercel builds and deploys automatically. No manual "Publish" step (this is
a Vercel project, not Lovable — see the ADR above for why).

## How security is handled

Nothing to leak here by design — no backend, no database, no keys. Still gated the same way as
every other repo in this account: each push runs Semgrep static analysis and a Gitleaks secret
scan, and a pre-commit hook blocks credential-shaped strings.

## Related

- [mountaincar-is](https://github.com/kamiljan11/mountaincar-is) — the main rental site
- [mas-garage](https://github.com/kamiljan11/mas-garage) — the garage landing page

## Licence

[All rights reserved](LICENSE) — MAS Group ehf. / Kamil Jan. Published for reference, not for reuse.
