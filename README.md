# Mountain Car — Landing Page

Main landing page for **Mountain Car** — car rental & garage services in Iceland (rental + garage in one place). Built and operated by [Kamil Jan](https://kamiljan.com).

## Stack
- Frontend: React 18 + TypeScript + Vite + Tailwind
- Backend/API:
- Baza:
- Hosting/deploy:

## Wymagania
- Node 20+
- npm

## Setup
```bash
npm install
cp .env.example .env   # uzupelnij wartosci (sekrety: Infisical "MAS Group")
```

## Komendy
| Komenda | Co robi |
|---|---|
| `npm run dev` | serwer deweloperski |
| `npm run build` | build produkcyjny |
| `npm run lint` | ESLint |
| `npm run typecheck` | tsc --noEmit |
| `npm test` | testy jednostkowe |
| `npm run test:coverage` | testy + prog pokrycia |
| `npx playwright test` | E2E smoke |

## Zmienne srodowiskowe
<!-- Tabela: NAZWA | wymagana? | opis. Zadnych wartosci sekretow w repo. -->

## Struktura
```
src/            # kod aplikacji
e2e/            # testy Playwright
docs/adr/       # decyzje architektoniczne
docs/RUNBOOK.md # operacje: deploy, rollback, awarie
```

## Deploy i wersjonowanie
- Flow: feature branch -> PR -> zielone CI + review -> merge do main -> deploy
- Wersje: SemVer, tag `vX.Y.Z` tworzy GitHub Release (auto-notes)
- Zmiany: `CHANGELOG.md` (Keep a Changelog) — aktualizuj sekcje [Unreleased] w kazdym PR

## Wlasciciel
MAS Group — mountainallservice@gmail.com
