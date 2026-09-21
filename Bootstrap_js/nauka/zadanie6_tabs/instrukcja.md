# Nauka – zakładki

## Cel

Dodasz dwa przyciski-zakładki (HTML i CSS); użytkownik widzi treść tylko aktywnej zakładki, bez przeładowania strony.

## Przydatne (ściąga)

Pasek: `nav nav-tabs`, przyciski `nav-link` z `data-bs-toggle="tab"` i `data-bs-target` wskazującym `#panel-…`. Treść: `tab-content` z panelami `tab-pane fade`. Zakładka i panel startowe mają klasę `active`; widoczny panel dodatkowo `show active`.

## Wymagania

1. Ustaw w `<title>` tekst: `Komponenty JS — zakładki`.
2. Zostaw hamburger w navbarze i skrypt `bundle.min.js` jak w zadaniu 1.
3. Zbuduj pasek zakładek HTML i CSS z klasą `nav-tabs`.
4. Dodaj panele `#panel-html` i `#panel-css` z krótkim opisem; na starcie widoczny ma być panel HTML.
5. W stopce zostaw autora.

## Przykład

Po otwarciu strony aktywna jest zakładka HTML i widać jej tekst. Klik w CSS podświetla drugą zakładkę, chowa panel HTML i pokazuje panel CSS. Adres w pasku przeglądarki się nie zmienia i strona się nie przeładowuje.
