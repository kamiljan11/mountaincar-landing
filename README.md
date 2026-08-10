# Mountain Car — Landing Page

**Status:** production · **Built & operated by** [Kamil Jan](https://kamiljan.com)

Single-page entry point for **Mountain Car** — car rental and garage services near Keflavík
airport, Iceland. One business, two halves; this page sends the visitor to the right one.

## What it is

A hand-written static `index.html`. No framework, no build step, no dependencies — the page is
the artefact. For a landing page whose job is to load instantly on airport wifi and route a
visitor in one click, a bundler would be cost without benefit.

## Stack

Static HTML + CSS · deployed on Vercel (`vercel.json`) · Playwright for E2E smoke tests.

## Running locally

Open `index.html` in a browser, or serve the folder:

```bash
python -m http.server 8000
```

```bash
npx playwright test    # E2E smoke
```

## How security is handled

Nothing to leak here by design — no backend, no database, no keys. Still gated the same way as
every other repo in this account: each push runs Semgrep static analysis and a Gitleaks secret
scan, and a pre-commit hook blocks credential-shaped strings.

## Related

- [mountaincar-is](https://github.com/kamiljan11/mountaincar-is) — the main rental site
- [mas-garage](https://github.com/kamiljan11/mas-garage) — the garage landing page

## Licence

Proprietary. Published for reference, not for reuse.
