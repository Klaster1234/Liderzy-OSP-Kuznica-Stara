# Prompt do Lovable — OSP Kuźnica Stara

Poniższy prompt skopiuj i wklej do Lovable jako instrukcję wygenerowania strony. Załącz również pliki `hero-osp-kuznica.png` i `logotypy-ue.jpg` z tego folderu.

---

## PROMPT START

Stwórz nowoczesną, responsywną, jednostronicową (single-page) stronę internetową dla **Ochotniczej Straży Pożarnej (OSP) w Kuźnicy Starej**. Strona ma być platformą do pozyskiwania darowizn na sprzęt ratowniczy, angażowania lokalnej społeczności i informowania o działaniach jednostki.

Projekt jest dofinansowany z Funduszy Europejskich — **obowiązkowe** jest umieszczenie logotypów UE i hashtagów w stopce.

Użyj React + TypeScript + Tailwind CSS + shadcn/ui + Lucide React icons.

---

### KIERUNEK ESTETYCZNY: "HEROIC CIVIC"

Styl: kinematograficzny, monumentalny, ale ciepły i wspólnotowy. Strona ma wyglądać jak profesjonalny film dokumentalny o bohaterach codzienności — nie jak korporacyjna landing page. Dramatyczne kontrasty światła (ogień vs. ciemność), głębia, tekstury. Każda sekcja powinna budzić emocje: dumę, zaufanie i chęć działania.

**KOLORYSTYKA (CSS variables):**
```
--fire-red: #C41E3A        /* główny akcent — nagłówki, ikony, hover */
--deep-red: #8B1425        /* ciemniejszy wariant czerwieni */
--navy: #0F1B2D            /* ciemne tła, footer, overlay */
--navy-light: #1B2A4A      /* karty na ciemnym tle */
--signal-yellow: #FFD700   /* przyciski CTA — "Wspieram", hover glow */
--signal-amber: #FFA500    /* secondary CTA, paski postępu */
--smoke-white: #F7F5F3     /* tło sekcji jasnych — ciepły odcień, nie zimny biały */
--ash-gray: #E8E4E0        /* bordery, dividers */
--ember-glow: #FF6B35      /* subtelne akcenty, gradient z czerwienią */
--text-dark: #1A1A1A       /* tekst na jasnym tle */
--text-light: #F0EDE8      /* tekst na ciemnym tle */
```

**TYPOGRAFIA (Google Fonts):**
- **Nagłówki:** `Barlow Condensed` (700, 800) — mocny, zwięzły, militarno-przemysłowy charakter, uppercase z letter-spacing: 0.05em
- **Podtytuły / akcenty:** `Barlow Semi Condensed` (500, 600)
- **Body text:** `Source Sans 3` (400, 600) — czytelny, profesjonalny, cieplejszy niż Inter
- Hero H1: 56-72px (mobile: 36-44px), sekcja H2: 36-48px, body: 17px, line-height: 1.7

**EFEKTY I TEKSTURY:**
- Subtelna tekstura noise/grain overlay (opacity: 0.03) na ciemnych sekcjach — dodaje głębi
- Gradient mesh na Hero: radialny gradient od ember-glow do transparentnego (symulacja łuny ognia)
- Kafelki z efektem glassmorphism na ciemnym tle (backdrop-blur, border 1px white/10%)
- Cienie: duże, rozproszone cienie (shadow-2xl) na kartach — efekt unoszenia się
- Sekcje naprzemiennie: ciemna (navy) → jasna (smoke-white) → ciemna → jasna

**ANIMACJE (Intersection Observer, CSS transitions):**
- Staggered fade-in-up na kartach (każda z opóźnieniem 100ms)
- Licznik w Hero: count-up animation od 0 do docelowej kwoty (2s, ease-out)
- Paski postępu: animacja wypełniania od 0% do wartości docelowej (1.5s, ease-out) gdy wchodzą w viewport
- Przyciski CTA: hover → box-shadow glow (signal-yellow z blur 20px), scale(1.03)
- Header: zmiana tła z transparent na navy po scrollu 100px (transition 300ms)
- Sekcje: fade-in z translate Y 40px → 0 (duration 700ms, ease-out)

---

### NAWIGACJA (Sticky Header)

- Transparent na starcie, zmienia się na `navy` (solid) po scrollu 100px
- Po lewej: ikona Flame (Lucide, kolor fire-red) + tekst **"OSP Kuźnica Stara"** (Barlow Condensed, uppercase, biały)
- Po prawej: menu nawigacyjne (linki: Start, Wspieram Nas, O Nas, Aktualności, Galeria, Kontakt)
  - Linki: `text-light`, hover → `signal-yellow`, transition 200ms
  - Po kliknięciu: smooth scroll do odpowiedniej sekcji
- Skrajnie po prawej: przycisk CTA **"Wesprzyj nas"** — tło signal-yellow, tekst navy, font-weight 700, border-radius 8px, hover → glow
- Mobile: hamburger menu (ikona Menu z Lucide), drawer z ciemnym tłem (navy), linki w kolumnie

---

### SEKCJA 1: HERO (pełny viewport, min-height: 100vh)

**Tło:**
- Zdjęcie `hero-osp-kuznica.png` (załączone) — object-fit: cover, pełna szerokość i wysokość
- Overlay: gradient wielowarstwowy:
  - Warstwa 1: linear-gradient od `rgba(15,27,45,0.7)` do `rgba(15,27,45,0.4)` (góra do dołu)
  - Warstwa 2: radial-gradient od `rgba(255,107,53,0.15)` w lewym dolnym rogu (łuna ognia)
- Subtelny parallax scroll na zdjęciu (transform translateY przy scrollu — NIE używaj background-attachment: fixed, bo nie działa na iOS Safari)

**Treść (wycentrowana, max-width: 800px):**
- Mały tekst nad nagłówkiem: "OCHOTNICZA STRAŻ POŻARNA" — Barlow Condensed, 14px, uppercase, letter-spacing 0.2em, kolor signal-yellow, z linią dekoracyjną po obu stronach (border)
- **H1:** "Wspólnie chronimy to, co najważniejsze" — Barlow Condensed 800, 56-72px, uppercase, text-white, text-shadow duży
- **Podtytuł:** "Od pokoleń na straży bezpieczeństwa mieszkańców Kuźnicy Starej i okolic" — Source Sans 3, 20px, text-light, opacity 0.9
- **CTA:** Duży przycisk "Wesprzyj naszą jednostkę" — tło signal-yellow, tekst navy, padding 16px 40px, font-size 18px, Barlow Semi Condensed 700, border-radius 12px, hover: glow + scale
- Pod przyciskiem: mały tekst "Każda złotówka ratuje życie" — italic, opacity 0.7

**Licznik zbiórek (pod CTA, margin-top 48px):**
- Kontener z glassmorphism (backdrop-blur, bg white/10%, border white/20%, border-radius 16px, padding 24px)
- Tekst "Łącznie zebrano" — mały, uppercase
- Kwota: **"14 450 zł"** — Barlow Condensed 800, 48px, kolor signal-yellow, animacja count-up
- Tekst "z potrzebnych 83 000 zł" — mniejszy, opacity 0.8
- Pasek postępu: wysokość 8px, border-radius full, tło white/20%, wypełnienie gradient (signal-yellow → signal-amber), animacja szerokości

**Scroll indicator:** na dole sekcji — animowana strzałka w dół (ChevronDown, bounce animation)

---

### SEKCJA 2: WSPIERAM NAS (tło: smoke-white)

**Nagłówek sekcji:**
- Mały tekst nad H2: "ZBIÓRKI" — uppercase, letter-spacing, kolor fire-red, Barlow Condensed
- **H2:** "Pomóż nam ratować — każda złotówka się liczy" — Barlow Condensed 700, 40px, kolor text-dark
- Podtytuł: "Wybierz, na co chcesz przeznaczyć swoją darowiznę. Każda zbiórka ma jasno określony cel." — Source Sans 3, 18px, opacity 0.7

**Grid kafelków (2x2 na desktop, 1 kolumna na mobile):**

Każdy kafelek to karta z:
- Białe tło, border-radius 16px, shadow-2xl, padding 32px
- Górna część: ikona Lucide w kole (56px, tło fire-red/10%, ikona fire-red) + nazwa potrzeby (Barlow Semi Condensed 600, 22px)
- Środek: opis potrzeby (Source Sans 3, 16px, text-dark/70%)
- Dolna część:
  - Kwoty: "Zebrano: **8 200 zł** z 25 000 zł" — kwota zebrana w fire-red bold
  - Pasek postępu: wysokość 10px, border-radius full, tło ash-gray, wypełnienie gradient (fire-red → ember-glow), animacja on-scroll
  - Procent: badge w prawym górnym rogu (np. "33%")
- Przycisk: "Wspieram" — tło signal-yellow, tekst navy, pełna szerokość, border-radius 10px, hover: glow

**4 kafelki:**
1. Ikona `Droplets` — **"Nowa motopompa"** — "Nasza aktualna motopompa ma ponad 15 lat. Nowy sprzęt to szybsza i pewniejsza pomoc." — cel: 25 000 zł — zebrano: 8 200 zł
2. Ikona `HardHat` — **"Umundurowanie bojowe"** — "Komplet umundurowania chroni życie strażaka. Potrzebujemy 5 nowych kompletów." — cel: 15 000 zł — zebrano: 4 100 zł
3. Ikona `Wrench` — **"Sprzęt ratowniczy"** — "Nożyce hydrauliczne i rozpieracze do wypadków drogowych — ratują życie w złotej godzinie." — cel: 35 000 zł — zebrano: 0 zł
4. Ikona `GraduationCap` — **"Szkolenia i kursy"** — "Regularne szkolenia podnoszą kompetencje ochotników i bezpieczeństwo akcji." — cel: 8 000 zł — zebrano: 2 150 zł

**Pod kafelkami — sekcja informacyjna (kontener z border-left 4px fire-red, bg fire-red/5%, padding 24px):**
- **Numer konta:** "Wpłaty na konto: XX XXXX XXXX XXXX XXXX XXXX XXXX" — monospace font, łatwy do skopiowania (przycisk kopiuj)
- **1,5% podatku:** "Możesz przekazać 1,5% podatku na naszą jednostkę. KRS: XXXXXXXXXX"
- **Transparentność:** "Każda darowizna jest rozliczana — publikujemy kwartalne raporty z wydatków."

---

### SEKCJA 3: O NAS (tło: navy, tekst: text-light)

Ta sekcja jest rozbudowana — składa się z trzech części: historia i misja, drużyna ze zdjęciami, oraz powody do wsparcia.

**CZĘŚĆ 1 — HISTORIA I MISJA (layout dwukolumnowy 60/40):**

**Lewa kolumna (60%):**
- Mały tekst: "NASZA HISTORIA" — uppercase, signal-yellow
- **H2:** "Kim jesteśmy" — Barlow Condensed 700, biały
- Tekst akapitowy (Source Sans 3, 17px, line-height 1.8, text-light):

  "Ochotnicza Straż Pożarna w Kuźnicy Starej to jednostka z wieloletnią tradycją służby na rzecz lokalnej społeczności. Nasi strażacy-ochotnicy to mieszkańcy, którzy w wolnym czasie poświęcają się ochronie życia, zdrowia i mienia — bez wynagrodzenia, z czystej pasji i poczucia odpowiedzialności."

  "Działamy na co dzień — gasimy pożary, pomagamy przy wypadkach drogowych, usuwamy skutki nawałnic i wichur, zabezpieczamy wydarzenia lokalne i wspieramy sąsiadów w potrzebie. Jesteśmy zawsze tam, gdzie nas potrzebują."

  "Nasza jednostka to nie tylko straż pożarna — to serce społeczności Kuźnicy Starej. Organizujemy szkolenia, angażujemy młodzież, dbamy o bezpieczeństwo i budujemy więzi między mieszkańcami."

- **Statystyki w rzędzie (3 kolumny):**
  - Duża liczba (Barlow Condensed 800, 48px, signal-yellow) + opis pod spodem (14px, text-light/70%)
  - "1952" — "Rok założenia"
  - "24" — "Aktywnych strażaków"
  - "87" — "Interwencji w 2025 r."
  - Statystyki z animacją count-up on-scroll

- Link do Facebooka: przycisk "Śledź nas na Facebooku" — ikona Facebook + tekst, outlined (border white/30%), hover: bg white/10% — link: https://www.facebook.com/p/Osp-Ku%C5%BAnica-Stara-100075858371987/?locale=pl_PL

**Prawa kolumna (40%):**
- Placeholder na zdjęcie drużyny — kontener z border-radius 16px, bg navy-light, border 2px dashed white/20%, ikona Camera (Lucide), tekst "Zdjęcie drużyny OSP"
- Obrót o -2deg (transform rotate) dla dynamiki, cień shadow-2xl
- Pod zdjęciem: podpis "Drużyna OSP Kuźnica Stara" — italic, 14px, text-light/50%

---

**CZĘŚĆ 2 — NASZA DRUŻYNA I DZIAŁANIA (podzsekcja, tło: navy-light, padding 60px 0):**

- Mały tekst: "NASZA SŁUŻBA" — uppercase, signal-yellow
- **H3:** "Codzienni bohaterowie Kuźnicy Starej" — Barlow Condensed 700, 32px, biały

**Grid zdjęć z opisami (3 kolumny desktop, 1 mobile):**
Każda karta: border-radius 16px, overflow hidden, bg navy, shadow-xl

1. Placeholder zdjęcie (aspect-ratio 4/3) + podpis:
   - **"Akcje ratownicze"** — "Pożary, wypadki, nawałnice — jesteśmy na miejscu w kilka minut."
2. Placeholder zdjęcie + podpis:
   - **"Szkolenia i ćwiczenia"** — "Regularnie doskonalimy umiejętności, bo w akcji liczy się każda sekunda."
3. Placeholder zdjęcie + podpis:
   - **"Życie jednostki"** — "Wspólne prace, remonty remizy, spotkania — budujemy więzi."

Pod gridem: tekst zachęcający — "Chcesz zobaczyć więcej? Odwiedź nas na Facebooku!" z linkiem do profilu FB (https://www.facebook.com/p/Osp-Ku%C5%BAnica-Stara-100075858371987/?locale=pl_PL)

---

**CZĘŚĆ 3 — DLACZEGO WARTO NAS WSPIERAĆ? (na dole sekcji O Nas):**

3 karty w rzędzie, każda: glassmorphism (bg white/5%, backdrop-blur, border white/10%), padding 32px, text-center
1. Ikona `Shield` (signal-yellow, 40px) — **"Bezpieczeństwo Twojej okolicy"** — "Chronimy domy, lasy i drogi w promieniu 15 km."
2. Ikona `Users` (signal-yellow, 40px) — **"Ochotnicy z pasją"** — "Działamy społecznie, bez wynagrodzenia. Z miłości do ludzi."
3. Ikona `Heart` (signal-yellow, 40px) — **"100% na społeczność"** — "Każda złotówka zostaje w naszej gminie i wraca do mieszkańców."

---

### SEKCJA 4: AKTUALNOŚCI (tło: smoke-white)

- Mały tekst: "AKTUALNOŚCI" — uppercase, fire-red
- **H2:** "Co u nas słychać?" — Barlow Condensed 700
- Podtytuł: "Śledź nasze działania i dowiedz się, jak Twoje wsparcie zmienia naszą jednostkę."

**Grid 3 kolumny (1 na mobile):**

Każda karta:
- Białe tło, border-radius 16px, shadow-xl, overflow hidden
- Góra: placeholder na zdjęcie (aspect-ratio 16/9, szare tło z ikoną Image)
- Dół: padding 24px
  - Badge z datą: "12 marca 2026" — małe, bg fire-red/10%, text fire-red, border-radius full, font-size 12px
  - Tytuł: Barlow Semi Condensed 600, 20px — "Ćwiczenia z gaszenia pożarów"
  - Opis: 2 zdania, Source Sans 3, 15px, opacity 0.7
  - Link "Czytaj więcej →" — fire-red, hover: underline

**3 przykładowe wpisy:**
1. "Ćwiczenia z gaszenia pożarów — doskonalimy nasze umiejętności" — "Nasi ochotnicy wzięli udział w ćwiczeniach na poligonie. Trenowaliśmy gaszenie pożarów wewnętrznych i ewakuację."
2. "Nowy sprzęt dzięki Waszym darowiznom!" — "Dzięki Waszej hojności zakupiliśmy nowe węże strażackie i agregat prądotwórczy."
3. "Dzień Otwarty w naszej remizie" — "Zapraszamy rodziny z dziećmi na Dzień Otwarty. Pokazy sprzętu, jazda wozem i mnóstwo atrakcji."

Przycisk na dole: **"Zobacz wszystkie aktualności →"** — outlined (border fire-red, text fire-red, hover: bg fire-red text white)

---

### SEKCJA 5: GALERIA (tło: navy)

- Mały tekst: "GALERIA" — uppercase, signal-yellow
- **H2:** "Nasza służba w obiektywie" — Barlow Condensed 700, biały

**Masonry-style grid (3 kolumny desktop, 2 tablet, 1 mobile):**
- 6 placeholderów na zdjęcia z różnymi aspect-ratio (niektóre wyższe, niektóre szersze)
- Każde zdjęcie: border-radius 12px, hover → scale(1.03) + overlay z ikoną Maximize (Lucide) + podpis
- Placeholder: bg navy-light, border 1px dashed white/20%, ikona Camera centralna
- Efekt lightbox po kliknięciu (dialog/modal z powiększonym zdjęciem)

Podpisy placeholderów: "Akcja gaśnicza", "Szkolenie drużyny", "Przegląd sprzętu", "Dzień Otwarty", "Ćwiczenia", "Spotkanie z młodzieżą"

---

### SEKCJA 6: STREFA SPONSORA (tło: smoke-white)

- Mały tekst: "PARTNERZY" — uppercase, fire-red
- **H2:** "Dziękujemy naszym wspierającym" — Barlow Condensed 700

**Pasek z logotypami sponsorów:**
- Rząd 4-6 placeholderów (szare prostokąty 160x80px z tekstem "Logo sponsora")
- Grayscale domyślnie, hover → kolorowe (filter: grayscale(0))
- Automatyczne przesuwanie (marquee / CSS animation) lub statyczny grid

**CTA pod spodem:**
- Tekst: "Chcesz zostać sponsorem OSP Kuźnica Stara? Oferujemy promocję Twojej firmy na naszej stronie, w mediach społecznościowych i podczas lokalnych wydarzeń."
- Przycisk: **"Zostań sponsorem"** — outlined (border fire-red, text fire-red), hover → fill

---

### SEKCJA 7: KONTAKT (tło: navy)

- Mały tekst: "KONTAKT" — uppercase, signal-yellow
- **H2:** "Skontaktuj się z nami" — Barlow Condensed 700, biały

**Layout dwukolumnowy (50/50, na mobile: kolumna):**

**Lewa kolumna — formularz:**
- Kontener: bg navy-light, border-radius 16px, padding 32px
- Pola (shadcn/ui Input/Select): ciemne tło (bg white/5%), border white/10%, text white, placeholder white/40%
  - Imię i nazwisko (wymagane)
  - Email (wymagane)
  - Telefon (opcjonalne)
  - Temat — dropdown/select: "Chcę przekazać darowiznę", "Chcę dołączyć do OSP", "Propozycja sponsoringu", "Inne"
  - Wiadomość — textarea, min 4 rzędy
- Przycisk "Wyślij wiadomość" — tło signal-yellow, tekst navy, pełna szerokość, hover: glow

**Prawa kolumna — dane + mapa:**
- Ikona `MapPin` + Adres: "OSP Kuźnica Stara, ul. [adres], [kod pocztowy] Kuźnica Stara"
- Ikona `Phone` + Telefon: "+48 XXX XXX XXX"
- Ikona `Mail` + Email: "osp.kuznicastara@example.com"
- Ikona `Clock` + Godziny: "Remiza czynna: Pn-Pt 17:00-20:00, Sb 9:00-14:00"
- Ikona `Facebook` + Link: "Facebook OSP Kuźnica Stara" — link do: https://www.facebook.com/p/Osp-Ku%C5%BAnica-Stara-100075858371987/?locale=pl_PL
- Placeholder na mapę: prostokąt 100% width, aspect-ratio 4/3, bg navy-light, border-radius 12px, ikona Map centralna, tekst "Google Maps"
- Wyróżniony blok na dole: bg ember-glow/10%, border-left 4px signal-yellow, padding 16px — **"Chcesz dołączyć do naszej drużyny? Zapraszamy — każdy ochotnik jest na wagę złota!"**

---

### STOPKA (Footer)

**Część 1 — Belka logotypów UE (OBOWIĄZKOWA):**
- Pełna szerokość, **białe tło**, padding 24px 0
- Wycentrowany obrazek: plik `logotypy-ue.jpg` (załączony) — max-width 700px, auto height
- Pod obrazkiem tekst: **"Projekt dofinansowany ze środków Unii Europejskiej w ramach Funduszy Europejskich dla Rozwoju Społecznego"** — Source Sans 3, 13px, text-dark/60%, text-center
- Hashtagi: **#FunduszeUE #FunduszeEuropejskie** — font-weight 600, text-dark/80%

**Część 2 — Footer właściwy (tło: #0A1220 — ciemniejsze niż navy):**
- **3 kolumny na desktop:**
  1. Logo (ikona Flame + "OSP Kuźnica Stara") + krótki opis: "Ochotnicza Straż Pożarna w Kuźnicy Starej — chronimy to, co najważniejsze." + ikony social media: Facebook (link: https://www.facebook.com/p/Osp-Ku%C5%BAnica-Stara-100075858371987/?locale=pl_PL), Instagram — hover signal-yellow
  2. Nawigacja: linki do sekcji (Start, Wspieram Nas, O Nas, Aktualności, Galeria, Kontakt)
  3. Kontakt: adres, telefon, email
- Separator: border-top 1px white/10%
- Copyright: "© 2026 OSP Kuźnica Stara. Wszelkie prawa zastrzeżone." — text-center, 13px, opacity 0.5

---

### PANEL ADMINISTRACYJNY (dostępny pod /admin)

Stwórz pełny panel administracyjny dostępny po zalogowaniu pod adresem `/admin`. Panel ma pozwalać członkom OSP zarządzać całą treścią strony bez wiedzy technicznej.

**LOGOWANIE:**
- Strona logowania: prosty formularz (email + hasło) na tle navy z logo OSP
- Użyj Supabase Auth (email/password) — stwórz tabelę `profiles` z rolami (admin, editor)
- Utwórz pierwsze konto administratora przy seedowaniu bazy:
  - Email: **partycypacje@klaster.org.pl**
  - Hasło: **Adrian11**
  - Rola: admin
- Po zalogowaniu: redirect do dashboardu
- Przycisk "Przypomnij hasło" z resetem przez email
- Zabezpieczenie: wszystkie trasy `/admin/*` chronione — bez logowania redirect do `/admin/login`

**DASHBOARD (strona główna panelu):**
- Sidebar nawigacja (navy tło): Dashboard, Aktualności, Zbiórki, Galeria, Sponsorzy, Wiadomości, Wnioski, Ustawienia
- Header z: nazwą zalogowanego użytkownika, przyciskiem "Wyloguj", linkiem "Zobacz stronę" (otwiera stronę publiczną)
- Na dashboardzie karty podsumowujące (grid 2x2):
  1. **"Zebrano łącznie"** — kwota z sumą wszystkich aktywnych zbiórek, ikona TrendingUp, porównanie z poprzednim miesiącem (np. "+2 350 zł w tym miesiącu")
  2. **"Nieprzeczytane wiadomości"** — liczba, ikona Mail, kliknięcie przenosi do Wiadomości
  3. **"Aktywne zbiórki"** — liczba aktywnych zbiórek / łączna liczba, ikona Target
  4. **"Wnioski w toku"** — liczba wniosków ze statusem "w przygotowaniu" lub "złożony", ikona FileText
- Pod kartami: **wykres postępu zbiórek** (chart/bar chart) — słupkowy wykres pokazujący każdą aktywną zbiórkę: nazwa, kwota zebrana vs. cel, procent realizacji. Użyj Recharts lub prostych CSS barów.
- Pod wykresem: **ostatnia aktywność** — lista 5 ostatnich zdarzeń (np. "Nowa darowizna +500 zł na motopompę", "Nowa wiadomość od Jana Kowalskiego", "Opublikowano wpis: Ćwiczenia...")

**ZARZĄDZANIE AKTUALNOŚCIAMI:**
Tabela `posts` w Supabase: id, title, content (rich text), image_url, published_at, created_at, author_id
- Lista wpisów: tabela z kolumnami — Tytuł, Data, Status (opublikowany/szkic), Akcje (edytuj/usuń)
- Formularz dodawania/edycji:
  - Pole: Tytuł (input)
  - Pole: Treść (textarea z podstawowym formatowaniem — pogrubienie, lista, nagłówek)
  - Pole: Zdjęcie (upload do Supabase Storage, podgląd miniaturki)
  - Checkbox: "Opublikuj od razu" (domyślnie zaznaczony)
  - Przyciski: "Zapisz" / "Anuluj"
- Potwierdzenie przed usunięciem (dialog: "Czy na pewno chcesz usunąć ten wpis?")

**ZARZĄDZANIE ZBIÓRKAMI:**
Tabela `fundraisers` w Supabase: id, name, description, icon_name, goal_amount, collected_amount, is_active, created_at
Tabela `donations` w Supabase: id, fundraiser_id, amount, donor_name (opcjonalne), note, created_at, recorded_by

- **Lista zbiórek** z paskami postępu (wizualnie jak na stronie publicznej), procent realizacji, data utworzenia
- Edycja: zmiana nazwy, opisu, kwoty docelowej, statusu (aktywna/zakończona)
- Dodawanie nowej zbiórki: formularz z polami: Nazwa, Opis, Kwota docelowa, Ikona (dropdown z dostępnymi ikonami Lucide)
- Zakończenie zbiórki: przycisk "Zakończ" — zmienia status, zbiórka znika ze strony publicznej ale zostaje w historii
- Automatyczna suma: strona publiczna automatycznie sumuje `collected_amount` ze wszystkich aktywnych zbiórek

- **REJESTROWANIE WPŁAT (kluczowa funkcja):**
  - Przy każdej zbiórce przycisk "Dodaj wpłatę"
  - Formularz: Kwota (wymagane), Imię darczyńcy (opcjonalne — "Anonim" domyślnie), Notatka (opcjonalne, np. "przelew bankowy", "zbiórka podczas Dnia Otwartego")
  - Po dodaniu wpłaty: `collected_amount` w zbiórce aktualizuje się automatycznie (suma z tabeli `donations`)
  - Toast: "Dodano wpłatę: +500 zł"

- **HISTORIA WPŁAT (zakładka wewnątrz zbiórki):**
  - Lista wszystkich wpłat: data, kwota, darczyńca, notatka, kto zarejestrował
  - Sortowanie: od najnowszej
  - Filtrowanie: po dacie (od-do), po kwocie (min-max)
  - Możliwość usunięcia błędnej wpłaty (z potwierdzeniem i automatyczną aktualizacją sumy)

- **RAPORT ZBIÓRKI:**
  - Przycisk "Pobierz raport" przy każdej zbiórce — generuje podsumowanie w formacie do druku (HTML/PDF):
    - Nazwa zbiórki, cel, zebrano, procent
    - Lista wszystkich wpłat (data, kwota, darczyńca)
    - Suma końcowa
  - Przydatne do rozliczenia z darczyńcami i sprawozdań

**GALERIA ZDJĘĆ:**
Tabela `gallery` w Supabase: id, image_url, caption, sort_order, created_at
- Grid miniaturek z podpisami
- Upload: drag-and-drop lub przycisk "Dodaj zdjęcia" (multiple upload do Supabase Storage)
- Edycja podpisu: kliknij na podpis → inline edit
- Zmiana kolejności: drag-and-drop (aktualizacja sort_order)
- Usuwanie: ikona kosza z potwierdzeniem

**SPONSORZY:**
Tabela `sponsors` w Supabase: id, name, logo_url, website_url, sort_order, is_active
- Lista sponsorów z miniaturkami logotypów
- Dodawanie: upload logo + nazwa firmy + opcjonalny link do strony
- Zmiana kolejności: drag-and-drop
- Aktywacja/dezaktywacja: toggle switch

**WIADOMOŚCI (z formularza kontaktowego):**
Tabela `messages` w Supabase: id, name, email, phone, subject, message, is_read, created_at
- Lista wiadomości: najnowsze na górze, nieprzeczytane wyróżnione (bold + badge)
- Podgląd: kliknij → pełna treść wiadomości
- Oznacz jako przeczytane/nieprzeczytane
- Przycisk "Odpowiedz" — otwiera mailto: link z emailem nadawcy
- Badge w sidebarze: liczba nieprzeczytanych wiadomości

**WNIOSKI / GRANTY (moduł do pisania i śledzenia wniosków o dofinansowanie):**
Tabela `grants` w Supabase: id, title, organization, program_name, deadline, amount_requested, status, description, notes, attachments (JSON array of URLs), created_at, updated_at, author_id

To sekcja dla OSP do zarządzania wnioskami o dofinansowanie ze źródeł zewnętrznych (granty, dotacje, programy UE, samorząd, ministerstwo, fundacje).

- **Lista wniosków** — tabela z kolumnami:
  - Tytuł wniosku
  - Instytucja/program (np. "Fundusz Sprawiedliwości", "KSRG", "Urząd Gminy", "FE dla Rozwoju Społecznego")
  - Kwota wnioskowana
  - Termin składania (deadline) — z kolorowym oznaczeniem: zielony (>30 dni), żółty (7-30 dni), czerwony (<7 dni), szary (minął)
  - Status — badge z kolorem:
    - "Pomysł" (szary) — wstępny pomysł, jeszcze nie rozpoczęto prac
    - "W przygotowaniu" (żółty) — trwa pisanie wniosku
    - "Gotowy do złożenia" (niebieski) — wniosek gotowy, czeka na złożenie
    - "Złożony" (fioletowy) — wniosek złożony, czekamy na decyzję
    - "Przyznany" (zielony) — dofinansowanie przyznane!
    - "Odrzucony" (czerwony) — wniosek odrzucony
    - "W realizacji" (signal-yellow) — projekt w trakcie realizacji
  - Akcje: edytuj, usuń

- **Formularz wniosku** (dodawanie/edycja):
  - Tytuł wniosku (input, np. "Dofinansowanie zakupu motopompy")
  - Instytucja / program grantowy (input, np. "Fundusz Sprawiedliwości — Przeciwdziałanie przyczynom przestępczości")
  - Kwota wnioskowana (number input, w zł)
  - Termin składania (date picker)
  - Status (dropdown z powyższych opcji)
  - Opis / streszczenie wniosku (textarea, duże pole — min. 8 rzędów)
  - Notatki wewnętrzne (textarea — np. "Potrzebujemy jeszcze kosztorysu od dostawcy", "Skonsultować z gminą")
  - Załączniki — upload plików (PDF, DOCX, JPG) do Supabase Storage, lista z możliwością pobrania i usunięcia
  - Powiązana zbiórka — opcjonalny dropdown łączący wniosek z istniejącą zbiórką (jeśli wniosek dotyczy tego samego celu)
  - Przyciski: "Zapisz" / "Anuluj"

- **Widok szczegółowy wniosku:**
  - Wszystkie dane w czytelnym layoucie
  - Timeline/oś czasu zmian statusu (np. "12.03 — Pomysł → 15.03 — W przygotowaniu → 20.03 — Złożony")
  - Lista załączników z miniaturkami (PDF) lub ikonami
  - Sekcja notatek — chronologiczna, można dodawać kolejne notatki (jak komentarze)

- **Dashboard wniosków (widok kalendarza):**
  - Widok listy (domyślny) — z filtrami po statusie
  - Widok kalendarza — pokazuje deadliny na kalendarzu miesięcznym (kolorowe kropki wg statusu)
  - Nadchodzące terminy — wyróżniony blok na górze: "3 wnioski z terminem w ciągu 30 dni"

- **Powiadomienia:**
  - Na dashboardzie głównym: alert gdy deadline wniosku jest za <7 dni
  - Badge "Wnioski" w sidebarze z liczbą wniosków bliskich deadline'u

**USTAWIENIA:**
Tabela `settings` w Supabase: id, key, value (JSON)
- Dane kontaktowe: adres, telefon, email, godziny otwarcia (edytowalne pola)
- Social media: linki do Facebooka i Instagrama
- Numer konta bankowego (do sekcji Wspieram Nas)
- Numer KRS (1,5% podatku)
- Dane "O Nas": rok założenia, liczba strażaków, liczba interwencji (wyświetlane w statystykach)

**DESIGN PANELU:**
- Tło: smoke-white (#F7F5F3), sidebar: navy (#0F1B2D)
- Akcenty: fire-red na przyciskach usuwania/ważnych, signal-yellow na przyciskach zapisu
- Typografia: ta sama co na stronie publicznej (Barlow Condensed nagłówki, Source Sans 3 tekst)
- Komponenty: shadcn/ui (Table, Card, Input, Button, Dialog, Select, Tabs, Badge, Toast)
- Toast notifications: "Zapisano pomyślnie", "Usunięto", "Błąd — spróbuj ponownie"
- Responsywny: na mobile sidebar zamienia się w hamburger menu

---

### WYMOGI TECHNICZNE

- Pełna responsywność: mobile-first (360px → 768px → 1024px → 1440px)
- Mobile: hamburger menu, 1 kolumna, mniejsze fonty (H1: 36px, H2: 28px)
- Tablet: 2 kolumny w gridach
- Desktop: pełny layout
- Smooth scroll (scroll-behavior: smooth) na linkach nawigacyjnych
- Lazy loading na zdjęciach w galerii (loading="lazy")
- Intersection Observer na animacjach (fade-in, count-up, progress bars)
- Semantyczny HTML (header, nav, main, section, footer, article)
- WCAG AA: kontrast kolorów spełniony, aria-labels na przyciskach i linkach
- Meta tagi SEO: title "OSP Kuźnica Stara — Wspólnie chronimy to, co najważniejsze", description, og:image
- **Backend: Supabase** — baza danych (PostgreSQL), auth (email/password), storage (zdjęcia, logotypy), RLS (Row Level Security) na wszystkich tabelach
- Tabele: posts, fundraisers, donations, gallery, sponsors, messages, grants, settings, profiles
- Storage buckets: "images" (zdjęcia postów i galerii), "logos" (logotypy sponsorów), "attachments" (załączniki do wniosków)
- RLS: publiczny odczyt danych (SELECT), zapis/edycja/usuwanie tylko dla zalogowanych użytkowników z rolą admin/editor

### PLIKI DO ZAŁĄCZENIA

Podczas generowania projektu załącz te pliki:
1. **`hero-osp-kuznica.png`** — zdjęcie wozu strażackiego do sekcji Hero (tło)
2. **`logotypy-ue.jpg`** — belka logotypów UE do stopki (obowiązkowa)

---

## PROMPT END
