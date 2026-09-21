# Nauka – modal

## Cel

Przycisk w treści otworzy okno modalne z godzinami na półprzezroczystym tle; krzyżyk w nagłówku okna je zamknie.

## Przydatne (ściąga)

Otwarcie: `data-bs-toggle="modal"`, `data-bs-target="#okno"`. Struktura: `modal fade` → `modal-dialog` → `modal-content` → `modal-header` / `modal-body`. Zamknięcie: `btn-close` z `data-bs-dismiss="modal"`.

## Wymagania

1. Ustaw w `<title>` tekst: `Komponenty JS — modal`.
2. Zostaw hamburger w navbarze i skrypt `bundle.min.js` jak w zadaniu 1.
3. Dodaj przycisk „Godziny”, który otwiera modal o `id="okno"`.
4. Zbuduj pełną drabinkę modalu: nagłówek z tytułem Godziny oraz treść z godzinami otwarcia pracowni.
5. W nagłówku umieść `btn-close`, który zamyka okno. W stopce zostaw autora.

## Przykład

Klik w „Godziny” przyciemnia stronę i pokazuje wyśrodkowaną kartę z tekstem godzin. Krzyżyk w rogu karty zamyka modal i wraca widok całej strony. Hamburger i pozostałe elementy działają jak wcześniej.
