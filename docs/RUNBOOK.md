# RUNBOOK — operacje i awarie

Statyczna strona bez backendu, bez bazy, bez formularzy, bez sekretów. Cała "awaria" to zwykle:
zła treść w `index.html`, padnięty zewnętrzny zasób (obrazy/fonty) albo problem z domeną/DNS.
Stan zweryfikowany 2026-10-05 (repo + publiczne HTTP/DNS). Czego nie dało się ustalić z repo:
oznaczone `[DO UZUPEŁNIENIA przez Kamila: …]`.

## Podstawy

| Co | Wartość |
|---|---|
| Produkcja | https://mountaincar.is (apex; `www.mountaincar.is` też odpowiada 200) |
| Adres Vercela | https://mountaincar-landing.vercel.app (pole "homepage" repo na GitHubie) |
| Hosting | Vercel (nagłówek `server: Vercel`; deploymenty tworzy `vercel[bot]` przez integrację z GitHubem) |
| Repo | https://github.com/kamiljan11/mountaincar-landing (publiczne), gałąź `main` |
| Co jest na stronie | logo + jedna karta "Garage" -> `https://garage.mountaincar.is`; karta "Car Rental" -> `https://rental.mountaincar.is` jest zakomentowana w `index.html` od 2026-09-04 |
| DNS | serwery nazw Cloudflare (`leanna.ns.cloudflare.com`, `titan.ns.cloudflare.com`); apex wskazuje na adresy Vercela |
| Panel Vercela | [DO UZUPEŁNIENIA przez Kamila: link do projektu w panelu Vercel + nazwa teamu/konta, na którym stoi] |
| Panel DNS (Cloudflare) | [DO UZUPEŁNIENIA przez Kamila: konto Cloudflare i kto ma do niego dostęp] |
| Rejestrator domeny `.is` | [DO UZUPEŁNIENIA przez Kamila: rejestrator/ISNIC, na kogo domena, data odnowienia] |
| Zmienne środowiskowe / sekrety | brak — nie ma czego trzymać (zero backendu, zero kluczy) |

Zasoby spoza repo, od których strona zależy (jeśli padną, strona się wyświetli, ale zepsuta wizualnie):
- logo i tło: pliki `.webp` na `d1yei2z3i6k35z.cloudfront.net` (URL-e w `index.html`, `<img src>` i `.bg`) —
  [DO UZUPEŁNIENIA przez Kamila: czyje to konto/CDN i skąd wziąć oryginały plików; w repo ich nie ma]
- fonty: Google Fonts (Montserrat, Open Sans), link w `<head>`.

## Uruchomienie lokalne

```bash
git clone https://github.com/kamiljan11/mountaincar-landing.git && cd mountaincar-landing
python3 -m http.server 8000   # http://localhost:8000
```
Nie ma `npm install`, buildu ani `.env`. Można też po prostu otworzyć `index.html` w przeglądarce.

## Deploy

- Standard: PR do `main` -> zielone checki (niżej) -> merge -> Vercel sam buduje i wdraża Production.
  Brak kroku "build" — Vercel serwuje pliki z roota repo (`vercel.json`: `cleanUrls: true`, `trailingSlash: false`).
- Podgląd: każdy PR dostaje deployment Preview (widać go w zakładce Deployments repo i w panelu Vercela).
- Ręczny deploy nie istnieje i nie jest potrzebny. Nie dodawaj `package.json`/bundlera (patrz ADR-0001).
- Ustawienia projektu w Vercelu (Framework Preset, Build Command, Production Branch) —
  [DO UZUPEŁNIENIA przez Kamila: potwierdzić w panelu: Framework "Other", brak Build/Output Command, Production Branch = `main`; z repo da się to tylko wywnioskować z faktu, że deployy "Production" powstają z commitów na `main`]

Sprawdzenie, czy produkcja = repo:
```bash
curl -s https://mountaincar.is | diff - index.html && echo "produkcja zgodna z main"
```

## Rollback (cel: < 5 min)

```bash
git revert <sha-zlego-commita> && git push   # albo przez PR; Vercel wdroży poprzednią treść w ciągu minut
```
Alternatywa (wymaga dostępu do panelu Vercela): w Deployments wybrać poprzedni udany deployment Production
i go przywrócić (Instant Rollback / Promote). Po takim rollbacku nadal trzeba zrobić `git revert`,
inaczej następny merge wdroży złą treść z powrotem. Nie ma bazy ani infrastruktury do cofania.

## Częste zmiany (gdzie sięgnąć)

| Chcę… | Zrób |
|---|---|
| Przywrócić kartę Car Rental | w `index.html` usuń otwierający znacznik `<!-- [ukryte 2026-09-04 …` i zamykające `-->` nad kartą Garage; ewentualnie przywróć `grid-template-columns: 1fr 1fr` i `max-width: 640px` w `.cards` (zmienione w commicie `27ccde2`). Najpierw sprawdź, czy wypożyczalnia realnie przyjmuje rezerwacje (GLOSSARY) |
| Zmienić tekst / adres / telefon | `index.html`: `.tagline`, `.subtitle`, `.footer` (telefon i adres to zwykły tekst, nie linki `tel:`) |
| Zmienić kolory | `:root` w bloku `<style>` (`--primary`, `--accent`, `--white`) |
| Podmienić logo / tło | zmienić URL w `<img src>` / `.bg`; plik musi być gdzieś hostowany (w repo nie ma katalogu na assety) |
| Zmienić cel kafla | atrybut `href` odpowiedniej karty `<a class="card">` |

## Formularze i dane

Brak. Strona nie zbiera żadnych danych: zero formularzy, zero JS, zero analityki, zero cookies własnych.
Jedyny kontakt to telefon w stopce (tekst). Zapytania/rezerwacje obsługują osobne aplikacje:
`garage.mountaincar.is` (repo `mas-garage`) i `rental.mountaincar.is` (repo `mountain-car-rental`) —
ich formularze i operacje opisane są w ich własnych repo.

## Monitoring

- Błędy runtime: brak (nie ma JS, nie ma Sentry).
- Uptime / healthcheck: brak skonfigurowanego monitoringu. Ręcznie: `curl -I https://mountaincar.is` (oczekiwane `200`, `server: Vercel`).
  [DO UZUPEŁNIENIA przez Kamila: czy jest zewnętrzny monitor uptime (np. w Cloudflare/UptimeRobot) i dokąd idą alerty]
- Status deployów: zakładka Deployments w repo na GitHubie / panel Vercela.
- CI: zakładka Actions. Wymagane checki na `main`: `Build + Lint + Typecheck + Test`, `Semgrep SAST`,
  `E2E smoke (Playwright)`, `Gitleaks secrets scan`. W tym repo kroki npm i E2E pomijają się same
  (brak `package.json`), więc realnie działają Semgrep i Gitleaks.
- Review PR przez Claude (`claude-review.yml`) działa tylko, gdy repo ma sekret `CLAUDE_CODE_OAUTH_TOKEN`;
  bez niego job kończy się jako pominięty i nie blokuje merge.

## Typowe awarie

| Objaw | Pierwszy krok |
|---|---|
| Strona nie wstaje / zły wygląd po deployu | rollback (wyżej), potem debug na branchu z podglądem Preview |
| Brak logo lub tła, strona "goła" | sprawdź `curl -I` na URL-e `d1yei2z3i6k35z.cloudfront.net` z `index.html`; jeśli nie żyją — podmień na nowo hostowane pliki |
| Zła czcionka | Google Fonts niedostępne -> przeglądarka użyje fontów systemowych; zwykle sam przechodzi |
| `mountaincar.is` nie odpowiada, `*.vercel.app` działa | problem DNS/domeny: panel Cloudflare, domena w projekcie Vercela, ważność domeny u rejestratora |
| Karta Garage/Rental prowadzi w próżnię | to nie ta strona: sprawdź `garage.mountaincar.is` / `rental.mountaincar.is` (osobne projekty); tu ewentualnie popraw `href` |
| Czerwone CI na PR | Semgrep/Gitleaks: otwórz log joba w Actions; nie omijaj bramek (`--no-verify`) |
| Merge nie wdrożył się | Deployments w repo: czy `vercel[bot]` utworzył deployment dla sha z `main`; jeśli nie — panel Vercela (integracja z GitHubem, limity planu) |

## Kontakty

- Właściciel (podmiot): Mountain All Service ehf. (MAS Group), Njarðarbraut 3i, Reykjanesbær — dane publiczne ze strony.
- Osoba techniczna / kontakt do awarii / SLA: [DO UZUPEŁNIENIA przez Kamila: kontakt właściciela repo i ewentualny SLA wobec klienta — celowo nie wpisuję adresu e-mail, bo repo jest publiczne, a kontakt osobisty był z niego usunięty w sierpniu 2026]
