# Nauka – accordion

## Cel

Zbudujesz dwa składane panele (Godziny i Kontakt) tak, aby po otwarciu drugiego sekcja pierwsza automatycznie się zamykała.

## Przydatne (ściąga)

Owijka `accordion` z `id`, w środku `accordion-item`, nagłówki `accordion-header` z przyciskiem `accordion-button`, panele `accordion-collapse` z `accordion-body`. Na panelach ustaw `data-bs-parent` wskazujący `id` całego accordionu. Pierwszy panel: `collapse show` i przycisk bez `collapsed`; drugi: `accordion-button collapsed` i `collapse` bez `show`.

## Wymagania

1. Ustaw w `<title>` tekst: `Komponenty JS — accordion`.
2. Zostaw hamburger w navbarze i skrypt `bundle.min.js` jak w zadaniu 1.
3. Dodaj `div.accordion` z `id="faq"` i dwoma elementami `accordion-item` (nagłówki: Godziny oraz Kontakt).
4. Na starcie pierwszy panel ma być rozwinięty (`show`), drugi zwinięty (przycisk z klasą `collapsed`).
5. Na obu panelach `accordion-collapse` ustaw `data-bs-parent="#faq"`. W stopce zostaw autora.

## Przykład

Od razu widać treść sekcji Godziny. Klik w nagłówek Kontakt chowa godziny i pokazuje adres; ponowne kliknięcie w Godziny odwraca sytuację. Oba panele nie powinny zostać otwarte jednocześnie.
