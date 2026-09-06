# Słownik

Repo to jedna statyczna strona (`index.html`, ~6 KB), która rozdziela ruch z domeny głównej na
dwa osobne produkty. Cała trudność jest w tym, że „Mountain Car" znaczy co innego w zależności
od subdomeny — stąd ten plik.

| Pojęcie | Znaczenie |
|---|---|
| **Mountain Car** | Marka motoryzacyjna MAS Group (Mountain All Service ehf.) w Keflavíku. Pod marką działają dwie osobne usługi i dwie osobne aplikacje. |
| **mountaincar.is** (apex) | To repo. Rozdzielacz ruchu: tło, logo i kafle prowadzące do właściwych usług. Nie ma tu logiki, formularzy ani danych klienta. |
| **garage.mountaincar.is** | Warsztat samochodowy — osobna aplikacja (repo `mas-garage`). |
| **rental.mountaincar.is** | Wypożyczalnia aut — osobna aplikacja (repo `mountain-car-rental`). Usługa została wygaszona; strona żyje jako demo, dlatego kafel na landingu bywa ukrywany. Zanim przywrócisz kafel, sprawdź, czy wypożyczalnia realnie przyjmuje rezerwacje. |
| **kafel** | Blok na landingu prowadzący do jednej usługi. Ukrycie kafla = jedna zmiana w `index.html`; nic po stronie usługi się nie zmienia. |
| **MAS Group** | Nazwa handlowa Mountain All Service ehf. — podmiot, który jest właścicielem marki i obu aplikacji. |

## Czego tu nie ma

Backendu, bazy, analityki i formularzy. Jeśli pojawia się potrzeba zbierania danych od
użytkownika, właściwym miejscem jest aplikacja usługi (garage albo rental), nie ten landing.
