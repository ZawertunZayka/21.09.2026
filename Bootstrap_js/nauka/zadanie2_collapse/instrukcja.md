# Nauka – collapse

## Cel

Dodasz przycisk w treści strony, który pokazuje i chowa akapit — ten sam mechanizm co przy hamburgerze, tylko zastosowany do zwykłej sekcji pod paskiem nawigacji.

## Przydatne (ściąga)

Przycisk: `btn btn-primary`, `data-bs-toggle="collapse"`, `data-bs-target="#opis"`. Ukryty blok: `div` z klasą `collapse` i `id="opis"`. Navbar i skrypt `bundle.min.js` ustaw tak jak w zadaniu 1.

## Wymagania

1. Ustaw w `<title>` tekst: `Komponenty JS — collapse`.
2. Zostaw hamburger w navbarze i skrypt `bundle.min.js` jak w zadaniu 1.
3. Dodaj przycisk z etykietą „Pokaż opis”, który otwiera element `#opis`.
4. Element `div#opis` musi mieć klasę `collapse` i zawierać krótki opis sali.
5. W stopce zostaw autora.

## Przykład

Przed kliknięciem opis nie widać. Po kliknięciu „Pokaż opis” tekst się rozwija; drugi klik znów go chowa. Pasek nawigacji nadal zwija się na wąskim oknie jak w zadaniu 1.
