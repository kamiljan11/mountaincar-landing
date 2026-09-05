# BACKLOG jakosci — dlug swiadomie odlozony

Format: co + dlaczego odlozone + ryzyko + kto decyduje. Nie sprzatamy automatycznie
(zasada 2026-08-09) — pozycje znikaja stad tylko na wskazanie Kamila.

## E2E smoke test nie jest podpiety pod runner

`e2e/smoke.spec.ts` istnieje i importuje `@playwright/test`, ale repo nie ma
`package.json` ani `playwright.config.ts`. Zweryfikowane empirycznie 2026-09-05:

```
$ npx --yes playwright test --list
Error: Cannot find module '@playwright/test'
...
Total: 0 tests in 0 files
```

Job "E2E smoke" w `.github/workflows/quality.yml` jest gated na
`hashFiles('playwright.config.ts', 'playwright.config.js')` — przy ich braku krok
"Install + smoke test" cicho sie pomija. Efekt: zielony job, zero realnej weryfikacji.

**Dlaczego nie naprawione w tym PR:** wlasciwa naprawa (dodanie `package.json` +
`playwright.config.ts` z `webServer`/`baseURL`) wykracza poza zakres tego PR
(README/LICENSE/ARCHITECTURE/ADR) i ma wlasne ryzyko: generyczny krok "Tests" w
`quality.yml` odpala `npm test --if-present -- --run` — skrypt `test` w nowym
`package.json` musialby NIE kolidowac z flaga `--run` (konwencja Vitest; Playwright CLI
jej nie zna i konczy sie bledem). To latwo zepsuc bez pelnego przebiegu w prawdziwym
GitHub Actions, ktorego ten agent nie moze zaobserwowac przed mergem PR-a.

**Ryzyko dzis:** niskie — brak testu oznacza brak weryfikacji, nie falszywy zielony
wynik (job nic nie twierdzi o smoke tescie, po prostu go nie uruchamia).

**Decyzja:** zostawione jako osobne zadanie (zgloszone przez `spawn_task`). Kamil
decyduje, czy warto dodawac Node/npm tooling do repo, ktorego cala idea to zero
zaleznosci — patrz `docs/adr/0001-static-hosting-vercel-not-lovable.md`.
