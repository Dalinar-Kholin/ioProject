### 1. Przypadki testowe niższego rzędu dla wybranych funkcji:

#### Przypadek 1: Logowanie użytkownika
- **Opis przypadku użycia:** Użytkownik wypełnia formularz logowania.
- **Dane wejściowe:**
  - Login: `testUser`
  - Hasło: `securePass123`
- **Stan początkowy:**
  - Konto użytkownika istnieje w bazie danych:
    ```json
    {
      "username": "testUser",
      "passwordHash": "hashed_securePass123"
    }
    ```
- **Przebieg testu:**
  1. Użytkownik otwiera stronę logowania.
  2. Wprowadza login i hasło.
  3. System weryfikuje dane.
- **Oczekiwany wynik:** Użytkownik zostaje zalogowany, widzi stronę główną sklepu.
- **Stan końcowy:** Użytkownik jest zalogowany, sesja jest aktywna.

---

#### Przypadek 2: Dodanie produktu ręcznie przez właściciela sklepu
- **Opis przypadku użycia:** Właściciel wypełnia formularz dodania produktu.
- **Dane wejściowe:**
  - Nazwa produktu: `Gaming Chair`
  - Cena: `599.99`
  - Ilość: `50`
  - Opis: `Ergonomic gaming chair with RGB lights.`
  - Klienci: `lowTier`
- **Stan początkowy:**
  - Sklep istnieje, brak produktu w bazie danych.
- **Przebieg testu:**
  1. Właściciel otwiera formularz dodawania produktu.
  2. Wypełnia dane produktu i klika "Dodaj".
  3. System waliduje dane i zapisuje produkt w bazie.
- **Oczekiwany wynik:** Produkt jest widoczny w ofercie sklepu.
- **Stan końcowy:** Produkt zapisany w bazie, dostępny do zakupu.

---

#### Przypadek 3: Zakup produktu przez użytkownika
- **Opis przypadku użycia:** Użytkownik dodaje produkt do koszyka i dokonuje zakupu.
- **Dane wejściowe:**
  - Produkt: `Gaming Chair`
  - Ilość: `1`
  - Metoda płatności: `przelew`
- **Stan początkowy:**
  - Produkt dostępny w magazynie w ilości `50`.
  - Konto użytkownika istnieje w systemie.
- **Przebieg testu:**
  1. Użytkownik dodaje produkt do koszyka.
  2. Potwierdza zakup i przechodzi do płatności.
  3. System rejestruje płatność i aktualizuje stan magazynowy.
- **Oczekiwany wynik:** Użytkownik widzi zakup w historii zamówień, stan magazynowy zmniejszony o 1.
- **Stan końcowy:** Zakup zapisany w bazie, produkt w historii użytkownika.

---

### 2. Pomiar zgodności z normami ISO/IEC 9126 i ISO 25000

#### Wybrane cechy jakości:
- **Funkcjonalność:**
  - **Kryteria:** Pokrycie wszystkich przypadków użycia.
  - **Pomiar:** Testy funkcjonalne, weryfikacja wymagań zgodnie z przypadkami testowymi.
- **Niezawodność:**
  - **Kryteria:** System dostępny 99,9% czasu.
  - **Pomiar:** Symulacje przeciążeń serwera, monitoring czasu przestoju.
- **Użyteczność:**
  - **Kryteria:** Intuicyjność interfejsu.
  - **Pomiar:** Ankiety beta testerów, analiza ścieżek użytkownika.
- **Efektywność:**
  - **Kryteria:** Czas odpowiedzi poniżej 200 ms.
  - **Pomiar:** Testy wydajności przy 100, 500, i 1000 równoczesnych użytkownikach.
- **Przenośność:**
  - **Kryteria:** Działanie na różnych przeglądarkach.
  - **Pomiar:** Testy na Chrome, Firefox, Safari, Edge.

---

### 3. Plan beta testowania
- **Cele:**
  - Weryfikacja funkcjonalności systemu.
  - Identyfikacja problemów użyteczności.
  - Testy wydajności.
- **Zakres:**
  - Funkcje logowania, rejestracji, zakupów i zarządzania produktami.
- **Metody:**
  - Testy manualne przez grupę 20 testerów.
  - Testy automatyczne scenariuszy krytycznych.
- **Harmonogram:** 2 tygodnie testów.
- **Raportowanie:** Codzienne raporty błędów.

---

### 4. Plan zarządzania jakością oprogramowania
- **Zasady:**
  - Pełna zgodność z wymaganiami funkcjonalnymi i niefunkcjonalnymi.
  - Regularne przeglądy kodu.
  - Automatyczne testy regresji.
- **Narzędzia:**
  - GitHub (zarządzanie wersjami).
  - Jest, Cypress (testy React).
  - LoadRunner (testy wydajności).
- **KPI:**
  - 100% pokrycie testami krytycznych funkcji.
  - Mniej niż 1 krytyczny błąd w wersji beta.

---

### 5. Plan wykonania produktu
- **Etapy:**
  - Projektowanie: 2 tygodnie.
  - Programowanie: 6 tygodni.
  - Testy wewnętrzne: 2 tygodnie.
  - Beta testy: 2 tygodnie.
  - Wdrożenie: 1 tydzień.
- **Pracochłonność:**
  - Backend: 240 godzin.
  - Frontend: 160 godzin.
  - Testowanie: 80 godzin.
- **Harmonogram:** 3 miesiące.

---

### 6. Ocena zgodności z wizją systemu i specyfikacją wymagań
- **Stan:** System zgodny z wizją koncepcyjną i specyfikacją.
- **Ocena:** Wszystkie opisane przypadki użycia zostały zaimplementowane. System spełnia wymagania funkcjonalne i niefunkcjonalne.
