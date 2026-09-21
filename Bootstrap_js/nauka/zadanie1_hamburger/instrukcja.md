# Nauka – hamburger

## Cel

Zbudujesz pasek nawigacji, który na wąskim oknie zwija linki za przyciskiem hamburgera, a po kliknięciu rozwija je mechanizmem `collapse`. Na końcu strony podłączysz skrypt Bootstrapa, bez własnego JavaScriptu.

## Przydatne (ściąga)

Użyj `navbar-expand-md`, przycisku `navbar-toggler` z `data-bs-toggle="collapse"` i `data-bs-target="#menu"`. Linki trzymaj w bloku `collapse navbar-collapse` z tym samym `id="menu"`. Tuż przed `</body>` wstaw `bootstrap.bundle.min.js` z CDN w wersji **5.3.3**. Nie piszesz `addEventListener`.

## Wymagania

1. Ustaw w `<title>` tekst: `Komponenty JS — hamburger`.
2. Na elemencie `nav` ustaw klasy: `navbar navbar-expand-md navbar-dark tlo-nav`.
3. Dodaj `navbar-brand` z tekstem Pracownia 12, przycisk hamburgera oraz menu w elemencie z `id="menu"`.
4. W menu umieść dwa linki `nav-link`: Start i Stopka.
5. Podłącz skrypt `bundle.min.js` przed `</body>`. W stopce zostaw autora. Klasę `tlo-nav` w CSS nie usuwaj.

## Przykład

Na szerokim oknie linki w pasku widać od razu w jednym rzędzie. Po zwężeniu okna (np. poniżej 768 px) zostaje logo i ikona hamburgera; pierwszy klik rozwija listę linków, kolejny klik ją chowa.
