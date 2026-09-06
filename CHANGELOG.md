# Changelog

Format: [Keep a Changelog](https://keepachangelog.com/en/1.1.0/), wersjonowanie: [SemVer](https://semver.org/).
Kazdy PR dopisuje zmiany do [Unreleased]; przy release przenosimy pod numer wersji z data.

## [Unreleased]
### Added
- Pipeline jakosci: CI (build/lint/typecheck/test/semgrep/audit/licencje), Claude review na PR, szablony dokumentacji
- `docs/ARCHITECTURE.md`, pierwszy realny ADR (`docs/adr/0001-static-hosting-vercel-not-lovable.md`), `LICENSE`, `.github/pull_request_template.md`, `.gitignore`, `docs/quality/BACKLOG.md` — PG v3 github-ready pass

### Changed
- README: sekcje "jak uruchomic", stack/env, deploy, linki do ARCHITECTURE/ADR/LICENSE; skorygowany opis testu E2E (nie jest jeszcze podpiety pod runner — patrz BACKLOG)

### Fixed
-
