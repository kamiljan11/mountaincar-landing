# Reguly pracy w tym repo (obowiazuja kazdego agenta AI i czlowieka)

## Zanim napiszesz JAKIKOLWIEK nowy kod
1. **Grep first.** Przeszukaj repo czy istniejaca funkcja/util/komponent robi to samo. Jesli tak — uzyj albo rozszerz. Duplikacja logiki = odrzucona zmiana.
2. Przeczytaj sasiednie pliki modulu, ktory zmieniasz. Trzymaj sie ich konwencji, nie swoich preferencji.
3. Zmiana architektoniczna (nowy modul, zaleznosc, wzorzec, schemat danych) -> najpierw ADR w `docs/adr/`, potem implementacja.

## Podczas pisania
4. **Male atomowe zmiany.** Jedna logiczna zmiana naraz. Nie mieszaj refaktoru z feature. Nie przepisuj plikow spoza zadania.
5. **Testy sa czescia zadania.** Nowa logika = testy w tej samej zmianie (happy path + najgrozniejsze edge case'y).
6. Bezpieczenstwo zawsze: parametryzowane zapytania, walidacja kazdego inputu, authz na poziomie rekordu, zadnych sekretow w kodzie — tylko env.
7. Nie wylaczaj lintera i nie uzywaj `any` / `@ts-ignore` / `eslint-disable` zeby "przeszlo". Napraw przyczyne.

## Zanim powiesz "gotowe"
8. Uruchom lint + typecheck + testy. Czerwone = nie jest gotowe.
9. Self-review diffa oczami wrogiego recenzenta: co tu sie wysypie o 3 w nocy?
10. Nie commituj z `--no-verify`. Czerwone CI to nie sugestia, to sciana.

## Kontekst projektu
- Stack: statyczny `index.html` (HTML + CSS inline, zero JS), hosting Vercel. Brak `package.json`, brak buildu, brak sekretów. Nie dodawaj bundlera/frameworka (ADR-0001).
- Komendy: lokalnie `python3 -m http.server 8000`; lint/testy/build nie istnieją (CI = Semgrep + Gitleaks)
- Plik wzorcowy: `index.html` (cały produkt); mapa i operacje: `docs/ARCHITECTURE.md`, `docs/RUNBOOK.md`
- Karta Car Rental jest zakomentowana celowo (wypożyczalnia zamknięta 2026-09-04) — nie przywracaj bez decyzji właściciela
