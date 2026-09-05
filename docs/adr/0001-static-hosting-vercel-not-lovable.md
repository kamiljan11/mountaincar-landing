# ADR-0001 — Static landing page hosted on Vercel, not Lovable

Data: 2026-09-05 | Status: przyjete (obowiazuje od pierwszego commita, 2026-06-09)

**Kontekst:** Mountain Car potrzebuje jednego apex URL (`mountaincar.is`) ktory natychmiast
kieruje odwiedzajacego do jednej z dwoch osobnych domen biznesowych: wypozyczalnia
(`rental.mountaincar.is`) i warsztat (`garage.mountaincar.is`). Cala funkcja strony to
routing dwoma linkami — zero stanu, zero formularzy, zero bazy danych.

**Decyzja:** Strona zyje jako reczny, statyczny `index.html` (HTML + CSS, zero
JS-frameworka, zero build stepu, zero `package.json`) i jest hostowana na Vercelu
(`vercel.json`: `cleanUrls`, brak trailing slash). Deploy = `git push` na `main`.

**Rozwazone alternatywy:**
- **Lovable** — domyslny wybor dla reszty floty MAS (generuje aplikacje React + Supabase).
  Odrzucone: strona nie ma niczego, co Lovable mialoby generowac ani czym zarzadzac (brak
  stanu, formularzy, bazy). Lovable dodalby React runtime i pipeline AI-edycji tam, gdzie
  wystarczy jeden plik tekstowy. [NIEPEWNE: ta decyzja nie jest nigdzie zapisana wprost —
  ani w historii commitow, ani w starym README. Powyzsze to rekonstrukcja z faktow: `vercel.json`
  istnieje od pierwszego commita (`0d1cf4b`, 2026-06-09), a repo nigdy nie mialo zadnych
  artefaktow Lovable (`lovable-tagger` w zaleznosciach, `src/integrations/supabase`).]
- **Ten sam hosting/repo co `mountaincar-is`** (glowna wypozyczalnia) — odrzucone: to osobny,
  duzo prostszy przypadek (0 zaleznosci, 0 backendu); dzielenie infrastruktury z aplikacja,
  ktora ma baze danych, nie dawaloby nic poza przypadkowym sprzezeniem.

**Konsekwencje:** Deploy to jeden `git push`, bez logowania do UI Lovable i bez kolejki
AI-edycji. Kazdy, kto umie edytowac HTML/CSS, moze wprowadzic zmiane bez znajomosci
Lovable czy Supabase. Koszt: brak wizualnego edytora — zmiany tekstu czy layoutu wymagaja
recznej edycji kodu i PR-a.

**Pulapki dla przyszlego siebie:** Nie dodawaj `package.json` ani bundlera "dla porzadku" —
zmienioby to model "1 plik = cala strona" na projekt z krokiem budowania, ktorego ten
produkt nie potrzebuje (patrz `docs/ARCHITECTURE.md`). Jesli strona kiedys dostanie
formularz, stan albo integracje z API — to sygnal do nowego ADR, nie do cichej rozbudowy
tego pliku wokol niego.
