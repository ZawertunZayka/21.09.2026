# Teoria: komponenty Bootstrapa z JS

Na [`02_komponenty`](../02_komponenty/) pasek nawigacji był **zawsze** rozwinięty (`navbar-expand`), bez hamburgera. Dropdown, modal i karuzela tam nie wchodziły — wymagają skryptu Bootstrapa.

W tym dziale podpinasz **gotowy plik JavaScript** z CDN. To **nie** są zajęcia z przedmiotu JavaScript: nie piszesz `addEventListener`, nie wołasz `new bootstrap.Modal()`. Klikanie obsługuje Bootstrap, a Ty w HTML ustawiasz **klasy** i atrybuty **`data-bs-*`**.

Nadal pracujesz na Bootstrap **5.3.3** z jsDelivr. Siatka z działu 01 oraz `.btn` i `.card` z działu 02 zostają bez zmian.

---

## 1. Skrypt (bundle)

Arkusz CSS w `<head>` podłączasz tak jak w dziale 01. **Skrypt wstaw na końcu `body`**, tuż przed zamknięciem `</body>`:

```html
<script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/js/bootstrap.bundle.min.js"></script>
```

Plik **`bundle`** zawiera JavaScript Bootstrapa **oraz Popper**. Dropdown bez Poppera nie ustawi listy we właściwym miejscu przy przycisku. Nie myl go z `bootstrap.min.js`, który **nie** ma Poppera w środku.

Gdy w pracowni nie ma sieci, nauczyciel podaje plik obok strony. Na arkuszu egzaminacyjnym zwykle wystarczy CDN.

**Po co to jest.** Hamburger, collapse, dropdown, modal, accordion i zakładki reagują na klik dopiero wtedy, gdy przeglądarka załaduje ten skrypt. Same klasy CSS nie wystarczą — bez `bundle.min.js` przycisk hamburgera nic nie zrobi.

**Typowa pomyłka.** Wstawienie skryptu w `<head>` albo użycie `bootstrap.min.js` zamiast `bundle.min.js`. W pierwszym przypadku strona czasem „działa”, ale to zły nawyk; w drugim dropdown często się rozjeżdża.

---

## 2. `data-bs-toggle` i `data-bs-target`

Bootstrap 5 łączy przyciski z ukrytymi blokami przez atrybuty `data-bs-*`:

| Atrybut | Znaczenie |
| ------- | --------- |
| `data-bs-toggle` | Określa **rodzaj** zachowania: `collapse`, `dropdown`, `modal`, `tab`, `offcanvas` itd. |
| `data-bs-target` | Wskazuje **element docelowy** po `id` (np. `#menu`, `#okno`) — musi się zgadzać z `id` w HTML. |
| `data-bs-dismiss` | Zamyka komponent (modal, offcanvas, alert) po kliknięciu w krzyżyk lub przycisk „Anuluj”. |

Przycisk i cel muszą tworzyć parę: `data-bs-target="#menu"` na przycisku wymaga `id="menu"` na rozwijanym bloku. Literówka w `id` albo brak `#` w atrybucie sprawia, że klik nic nie robi — bez błędu w konsoli, który od razu by wskazał problem.

**Po co to jest.** Dzięki tym atrybutom nie piszesz własnego JS: Bootstrap nasłuchuje kliknięć i dopina klasy (`show`, `active`) we właściwym momencie.

**Typowa pomyłka.** Różne `id` na celu i w `data-bs-target`, albo zapomnienie `data-bs-toggle` przy samym `data-bs-target`. Oba przypadki wyglądają jak „zepsuty przycisk”.

---

## 3. Hamburger (`navbar` + collapse)

Na wąskim oknie linki w pasku chowasz w zwijanym bloku; zostaje przycisk z ikoną (hamburger). Od progu **`md` (768 px)** pasek znów pokazuje linki w jednym rzędzie.

```html
<nav class="navbar navbar-expand-md navbar-dark tlo-nav">
  <div class="container">
    <a class="navbar-brand" href="index.html">Pracownia 12</a>
    <button
      class="navbar-toggler"
      type="button"
      data-bs-toggle="collapse"
      data-bs-target="#menu"
      aria-controls="menu"
      aria-expanded="false"
      aria-label="Przełącz menu"
    >
      <span class="navbar-toggler-icon"></span>
    </button>
    <div class="collapse navbar-collapse" id="menu">
      <div class="navbar-nav">
        <a class="nav-link" href="index.html">Start</a>
        <a class="nav-link" href="info.html">Info</a>
      </div>
    </div>
  </div>
</nav>
```

| Klasa / atrybut | Rola |
| --------------- | ---- |
| `navbar-expand-md` | Menu zwija się **poniżej** progu `md`; to nie to samo co `navbar-expand` z działu 02 (tam pasek jest zawsze rozwinięty). |
| `navbar-toggler` | Przycisk hamburgera widoczny na wąskim oknie. |
| `navbar-toggler-icon` | Trzy kreski; przy `navbar-dark` ikona jest jasna. |
| `collapse navbar-collapse` | Blok linków, który na wąsko jest schowany do pierwszego kliku. |
| `id="menu"` | Cel dla `data-bs-target` na przycisku togglera. |

Klasa `.tlo-nav` w `style.css` nadaje granatowy kolor szkoły — tak jak w dziale 02. Sprawdź efekt: zwęż okno, kliknij ikonę hamburgera.

**Po co to jest.** Użytkownik na telefonie widzi krótki pasek z logo i ikoną, a pełne menu dopiero po tapnięciu. Na tablecie i laptopie nie musi klikać — linki są od razu.

**Typowa pomyłka.** Zostawienie `navbar-expand` bez `-md` (menu nigdy się nie chowa) albo brak `navbar-toggler`. Inna pułapka: `data-bs-target="#menu"` przy `id="nav"` — hamburger nie trafi w blok linków.

---

## 4. Collapse (pokaż / ukryj treść)

Ten sam mechanizm co przy hamburgerze, tylko stosujesz go do zwykłego akapitu lub sekcji pod przyciskiem w treści strony.

```html
<button
  class="btn btn-primary"
  type="button"
  data-bs-toggle="collapse"
  data-bs-target="#opis"
  aria-expanded="false"
  aria-controls="opis"
>
  Pokaż opis
</button>
<div class="collapse" id="opis">
  <p class="mt-3">Sala 12 — zajęcia HTML i CSS.</p>
</div>
```

Klasa `collapse` **ukrywa** blok na starcie. Po kliknięciu Bootstrap dopina klasę `show` i treść się rozwija; kolejny klik znowu ją chowa.

**Po co to jest.** Możesz schować długi regulamin lub opis, żeby strona na pierwszy rzut oka była krótsza, a szczegóły pokazać na żądanie.

**Typowa pomyłka.** Brak klasy `collapse` na docelowym `div` (treść widać cały czas) albo brak `type="button"` na przycisku w formularzu — wtedy przycisk mógłby wysłać formularz zamiast rozwijać blok.

---

## 5. Dropdown

Przycisk rozwija listę pozycji pod spodem. Lista musi leżeć **wewnątrz** owijki `.dropdown`.

```html
<div class="dropdown">
  <button
    class="btn btn-primary dropdown-toggle"
    type="button"
    data-bs-toggle="dropdown"
    aria-expanded="false"
  >
    Sale
  </button>
  <ul class="dropdown-menu">
    <li><a class="dropdown-item" href="#s12">Sala 12</a></li>
    <li><a class="dropdown-item" href="#s4">Sala 4</a></li>
  </ul>
</div>
```

Klasa `dropdown-toggle` dodaje małą strzałkę przy etykiecie przycisku. W navbarze możesz użyć `nav-item dropdown` i `nav-link dropdown-toggle` — to wariant na witrynie wielostronicową; w zadaniach z `main` wystarczy przycisk w `.dropdown`.

**Po co to jest.** Kilka opcji (sale, działy, audycje) mieści się pod jednym przyciskiem zamiast zajmować cały wiersz linków.

**Typowa pomyłka.** `ul.dropdown-menu` poza `.dropdown` albo brak `dropdown-toggle` / `data-bs-toggle="dropdown"`. Bez `bundle.min.js` (Popper) menu może pojawić się w złym miejscu na stronie.

---

## 6. Modal (okno na wierzchu)

Modal to karta dialogowa na półprzezroczystym tle; reszta strony jest na chwilę „zablokowana” wizualnie.

```html
<button type="button" class="btn btn-primary" data-bs-toggle="modal" data-bs-target="#okno">
  Godziny
</button>

<div class="modal fade" id="okno" tabindex="-1">
  <div class="modal-dialog">
    <div class="modal-content">
      <div class="modal-header">
        <h2 class="modal-title">Godziny</h2>
        <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Zamknij"></button>
      </div>
      <div class="modal-body">
        <p>Poniedziałek–piątek, 8:00–16:00.</p>
      </div>
    </div>
  </div>
</div>
```

Struktura warstw: `modal` → `modal-dialog` → `modal-content` → `modal-header` / `modal-body`. Bez `modal-dialog` i `modal-content` okno nie wygląda jak wyśrodkowana karta na przyciemnieniu. Klasa `fade` daje krótką animację wejścia. Krzyżyk to `btn-close` z `data-bs-dismiss="modal"` — nie wstawiasz własnego tekstu „X”.

**Po co to jest.** Godziny otwarcia, krótki regulamin lub potwierdzenie możesz pokazać bez przeładowania strony i bez osobnej podstrony.

**Typowa pomyłka.** Płaski HTML: treść bezpośrednio w `div.modal` bez `dialog` i `content`. Druga pułapka: modal wstawiony **wewnątrz** wąskiej kolumny z `overflow: hidden` — wtedy cień i wyśrodkowanie mogą wyglądać źle; modal najlepiej trzymać tuż przed końcem `body`.

---

## 7. Accordion (składane sekcje)

Accordion to kilka paneli collapse w jednej owijce; zwykle **tylko jeden** panel jest otwarty naraz dzięki `data-bs-parent`.

```html
<div class="accordion" id="faq">
  <div class="accordion-item">
    <h2 class="accordion-header">
      <button
        class="accordion-button"
        type="button"
        data-bs-toggle="collapse"
        data-bs-target="#a1"
        aria-expanded="true"
        aria-controls="a1"
      >
        Godziny
      </button>
    </h2>
    <div id="a1" class="accordion-collapse collapse show" data-bs-parent="#faq">
      <div class="accordion-body">Poniedziałek–piątek, 8:00–16:00.</div>
    </div>
  </div>
  <div class="accordion-item">
    <h2 class="accordion-header">
      <button
        class="accordion-button collapsed"
        type="button"
        data-bs-toggle="collapse"
        data-bs-target="#a2"
        aria-expanded="false"
        aria-controls="a2"
      >
        Kontakt
      </button>
    </h2>
    <div id="a2" class="accordion-collapse collapse" data-bs-parent="#faq">
      <div class="accordion-body">Sala 12, piętro 1.</div>
    </div>
  </div>
</div>
```

Pierwszy panel: przycisk `accordion-button` (bez `collapsed`) i panel z klasami `collapse show`. Kolejne: `accordion-button collapsed` i panel tylko z `collapse` (bez `show`). Atrybut `data-bs-parent="#faq"` na panelach wskazuje wspólną owijkę — po otwarciu następnej sekcji Bootstrap zamyka poprzednią.

**Po co to jest.** FAQ, wypożyczenia i zwroty albo ramówka i kontakt mieszczą się w jednym kolumnowym bloku bez długiego scrollowania wszystkich tekstów naraz.

**Typowa pomyłka.** Brak `data-bs-parent` — wtedy oba panele mogą zostać otwarte i accordion traci sens. Zapomnienie `collapsed` / `show` na starcie sprawia, że wszystkie sekcje wyglądają jak zamknięte albo wszystkie otwarte.

---

## 8. Zakładki (`tab`)

Zakładki przełączają widoczne panele treści pod paskiem przycisków; strona się nie przeładowuje.

```html
<ul class="nav nav-tabs" role="tablist">
  <li class="nav-item" role="presentation">
    <button
      class="nav-link active"
      id="tab-html"
      data-bs-toggle="tab"
      data-bs-target="#panel-html"
      type="button"
      role="tab"
    >
      HTML
    </button>
  </li>
  <li class="nav-item" role="presentation">
    <button
      class="nav-link"
      id="tab-css"
      data-bs-toggle="tab"
      data-bs-target="#panel-css"
      type="button"
      role="tab"
    >
      CSS
    </button>
  </li>
</ul>
<div class="tab-content">
  <div class="tab-pane fade show active" id="panel-html" role="tabpanel">
    <p class="mt-3">Znaczniki i atrybuty.</p>
  </div>
  <div class="tab-pane fade" id="panel-css" role="tabpanel">
    <p class="mt-3">Wygląd i układ.</p>
  </div>
</div>
```

Panel widoczny na start ma klasy `tab-pane fade show active`. Przycisk tej zakładki ma `nav-link active`. Każde `data-bs-target` na zakładce musi wskazywać `id` istniejącego panelu w `.tab-content`.

**Po co to jest.** Krótkie opisy w kilku kategoriach (HTML, CSS, JS) przełączasz jednym klikniem zamiast robić trzy osobne sekcje jedna pod drugą.

**Typowa pomyłka.** `active` tylko na przycisku, bez `show active` na panelu — albo odwrotnie. Niespójne `id` między `data-bs-target` a panelem daje pusty obszar po kliknięciu zakładki.

---

## 9. Extra: karuzela i offcanvas

**Karuzela** pokazuje jeden slajd naraz i przełącza go strzałkami. Owijka ma klasy `carousel slide` i unikalne `id` (np. `#galeria`). Slajdy leżą w `carousel-inner`; każdy slajd to `carousel-item`, pierwszy ma dodatkowo `active`. Strzałki używają `carousel-control-prev` / `carousel-control-next`, wskazują karuzelę przez `data-bs-target="#galeria"` oraz `data-bs-slide="prev"` lub `"next"`. Tła slajdów (klasy `.slajd` w zadaniu) są w `style.css` — nie wstawiasz własnych zdjęć, chyba że instrukcja każe inaczej.

**Offcanvas** to panel wysuwany z boku ekranu (np. z prawej: `offcanvas offcanvas-end`). Przycisk otwierający ma `data-bs-toggle="offcanvas"` i `data-bs-target` na `id` panelu. Zamknięcie: `btn-close` z `data-bs-dismiss="offcanvas"` w nagłówku panelu.

**Po co to jest.** Karuzela nadaje się do krótkiej galerii miejsc w bibliotece lub radiowęźle. Offcanvas zastępuje modal, gdy chcesz menu boczne z ramówką bez zasłaniania całej strony kartą na środku.

**Typowa pomyłka.** W karuzeli brak `active` na pierwszym slajdzie albo strzałki wskazujące inne `id` niż owijka karuzeli. W offcanvas brak `offcanvas-end` (panel wjedzie z niewłaściwej strony) albo panel bez `tabindex` gdy Bootstrap tego wymaga w szablonie zadania.

Tooltip i toast **pomijamy** w tym dziale: często wymagają jednej linijki `new bootstrap.Tooltip(...)` — to już materiał przedmiotu JavaScript.

---

## 10. Checklist

Przed oddaniem strony przejdź poniższe punkty — to szybka kontrola typowych wymagań działu 03.

- W `<head>` jest CSS Bootstrap 5.3.3, a **`bootstrap.bundle.min.js` stoi na końcu `body`**.
- Hamburger: `navbar-expand-md`, `navbar-toggler`, blok `collapse navbar-collapse` z tym samym `id`, co w `data-bs-target` przycisku.
- Nie dopisujesz własnego JavaScriptu ani nie kopiujesz jQuery — wystarczą `data-bs-*`.
- Modal: pełna drabina `modal` → `modal-dialog` → `modal-content` → `header` / `body`.
- Dropdown: struktura `dropdown` → przycisk z `dropdown-toggle` → `ul.dropdown-menu` z `dropdown-item`.
- `navbar-expand` **bez** `-md` z działu 02 to nie hamburger — menu na telefonie nadal będzie w pełnej szerokości.
