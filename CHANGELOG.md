# Changelog

Format: [Keep a Changelog](https://keepachangelog.com/en/1.1.0/), wersjonowanie: [SemVer](https://semver.org/).
Kazdy PR dopisuje zmiany do [Unreleased]; przy release przenosimy pod numer wersji z data.

## [Unreleased]
### Added
- Pipeline jakosci: CI (build/lint/typecheck/test/semgrep/audit/licencje), Claude review na PR, szablony dokumentacji
- `docs/GLOSSARY.md` — słownik trzech domen Mountain Car (apex / garage / rental) (#2)
- `docs/RUNBOOK.md` wypełniony faktami z repo (hosting, domena, deploy, rollback, monitoring, typowe awarie) — handover 2026-10-05
- `docs/ARCHITECTURE.md`, pierwszy realny ADR (`docs/adr/0001-static-hosting-vercel-not-lovable.md`), `LICENSE`, `.github/pull_request_template.md`, `.gitignore`, `docs/quality/BACKLOG.md` — PG v3 github-ready pass

### Changed
- Strona: karta "Car Rental" ukryta (zakomentowana), układ kart w jedną kolumnę, nowy opis w hero i `<meta description>` — wypożyczalnia zamknięta od 2026-09-04 (`27ccde2`); przywrócenie opisane w `docs/RUNBOOK.md`
- README: sekcje "jak uruchomic", stack/env, deploy, linki do ARCHITECTURE/ADR/LICENSE; usunięty martwy szablon E2E (`e2e/smoke.spec.ts` — statyczny HTML bez zależności Node; patrz BACKLOG), sekcja Testing dostosowana

### Fixed
- `claude-review.yml`: bez sekretu `CLAUDE_CODE_OAUTH_TOKEN` job kończy się jako pominięty zamiast fałszywie zielony (#3)

## Historia przed wprowadzeniem changelogu (z `git log`, bez tagów/wydań)

- 2026-08-10: README po angielsku (opis, stack, uruchomienie, bezpieczeństwo)
- 2026-08-08..09: CI — akcje GitHub przypięte do SHA, job Gitleaks, Claude review tylko przez OAuth (bez klucza API), poprawka publikacji komentarza review
- 2026-08-04..07: usunięcie osobistej atrybucji i kontaktu z publicznych plików; właściwy tytuł i opis w README
- 2026-07-21: ukryty (zakomentowany) kredyt autora w stopce
- 2026-06-13: dodany kredyt autora w stopce
- 2026-06-11: poprawki mobilne (przewijanie, układ kolumnowy na `100svh`), usunięty nagłówek "Your Icelandic Adventure Starts Here"
- 2026-06-09: pierwsza wersja strony (rental + garage) wraz z `vercel.json`
