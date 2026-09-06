# BACKLOG jakosci — dlug swiadomie odlozony

Format: co + dlaczego odlozone + ryzyko + kto decyduje. Nie sprzatamy automatycznie
(zasada 2026-08-09) — pozycje znikaja stad tylko na wskazanie Kamila.

## E2E smoke test — ROZWIAZANE 2026-09-05

`e2e/smoke.spec.ts` byl szablonem skopiowanym przez bootstrap bez sprawdzenia, czy repo ma zaleznosci Node
(to statyczny HTML bez `package.json`, wiec `@playwright/test` nigdy nie istnial). Plik usuniety; job E2E
w `quality.yml` dalej gated na `playwright.config.*` i pomija sie jawnie. Przyczyna naprawiona u zrodla:
`mas-quality-init.ps1` kopiuje szablony Node tylko przy obecnym `package.json`.
Jesli kiedys powstanie realny smoke test dla landingu: `npm init` + `@playwright/test` + `playwright.config.ts`
z `webServer` serwujacym `index.html`.
