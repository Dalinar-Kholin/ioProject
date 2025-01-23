Kacper Osadowski
Marceli Buczek

### **1. Niezbędna pojemność bazy danych**

#### **Założenia:**
- **Szacowana liczba użytkowników:** 10,000 aktywnych użytkowników.
- **Szacowana liczba właścicieli sklepów:** 500.
- **Szacowana liczba produktów na sklep:** Średnio 200 produktów.
- **Szacowana liczba transakcji na użytkownika:** 100 transakcji rocznie.

#### **Obliczenia:**

1. **Tabela użytkowników (User):**
   - Rozmiar jednego rekordu:
     - `username`: 20 znaków = 20 B
     - `passwordHash`: 64 B
     - `salt`: 16 B
     - Zakupione produkty: średnio 100 produktów rocznie → powiązanie z historią transakcji.
     - **Razem:** ~100 B.
   - 10,000 użytkowników → 10,000 × 100 B = **1 MB.**

2. **Tabela właścicieli sklepów (Owner):**
   - Rozmiar jednego rekordu:
     - `username`: 20 B
     - `passwordHash`: 64 B
     - `salt`: 16 B
     - **Razem:** ~100 B.
   - 500 właścicieli → 500 × 100 B = **0.05 MB.**

3. **Tabela sklepów (Shop):**
   - Rozmiar jednego rekordu:
     - `shopName`: 50 B
     - Lista produktów: średnio 200 produktów × 50 B = 10 KB.
     - **Razem:** ~10 KB.
   - 500 sklepów → 500 × 10 KB = **5 MB.**

4. **Tabela produktów (Product):**
   - Rozmiar jednego rekordu:
     - `name`: 20 B
     - `price`: 8 B
     - `count`: 4 B
     - `description`: średnio 200 B
     - **Razem:** ~232 B.
   - 500 sklepów × 200 produktów = 100,000 produktów.
   - 100,000 × 232 B = **23.2 MB.**

5. **Tabela transakcji (Transaction):**
   - Rozmiar jednego rekordu:
     - `transactionId`: 16 B
     - `userId`: 8 B
     - `productId`: 8 B
     - `date`: 8 B
     - **Razem:** ~40 B.
   - 10,000 użytkowników × 100 transakcji = 1,000,000 transakcji.
   - 1,000,000 × 40 B = **40 MB.**

#### **Łączna pojemność bazy danych:**
- Użytkownicy: 1 MB.
- Właściciele sklepów: 0.05 MB.
- Sklepy: 5 MB.
- Produkty: 23.2 MB.
- Transakcje: 40 MB.
- **Razem:** ~69 MB (przy uwzględnieniu indeksów i zapasowej przestrzeni: ~100 MB).

---

### **2. Plan wdrożenia**

#### **Etapy wdrożenia:**
1. **Przygotowanie środowiska:**
   - Utworzenie środowiska produkcyjnego w AWS.
   - Konfiguracja bazy danych DynamoDB.
2. **Migracja danych:**
   - Import testowych danych.
   - Weryfikacja integralności danych.
3. **Testy przedwdrożeniowe:**
   - Testy wydajnościowe przy obciążeniu 1,000 równoczesnych użytkowników.
   - Testy regresji.
4. **Soft launch:**
   - Uruchomienie dla ograniczonej grupy użytkowników (beta testy).
5. **Pełne wdrożenie:**
   - Publiczne udostępnienie aplikacji.
6. **Monitoring i optymalizacja:**
   - Użycie narzędzi monitorujących (np. AWS CloudWatch).

---

### **3. Koncepcja organizacji szkoleń użytkowników**

#### **Cele szkoleń:**
- Nauka korzystania z systemu.
- Zwiększenie efektywności użytkowników.
- Redukcja liczby błędów użytkownika.

#### **Forma szkoleń:**
- **Instrukcje online:** Dokumentacja i filmy instruktażowe.
- **Warsztaty stacjonarne:** Dla właścicieli sklepów.
- **Webinary:** Interaktywne sesje Q&A.
- **Materiały samouczkowe:** Dostosowane do różnych grup użytkowników.

---

### **4. Koncepcja wsparcia technicznego**

#### **Model wsparcia:**
1. **Obsługa zgłoszeń:**
   - System zgłoszeń w aplikacji.
   - Średni czas odpowiedzi: 24 godziny.
2. **Kanały kontaktu:**
   - E-mail: 24/7.
   - Telefon: 9:00-17:00 (dni robocze).
3. **Zapewnienie ciągłości działania:**
   - Redundancja serwerów w AWS.
   - Regularne kopie zapasowe (co 12 godzin).
   - SLA: 99.9% dostępności.

#### **Usuwanie błędów:**
- **Krytyczne:** Naprawa w ciągu 24 godzin.
- **Średnie:** Naprawa w ciągu 5 dni roboczych.
- **Niskie:** Naprawa w kolejnym cyklu aktualizacji.

---

### **5. Główne punkty umów**

1. **Zakres usług:**
   - Dostarczenie aplikacji i wsparcia technicznego.
   - Zapewnienie ciągłości działania.
2. **SLA (Service Level Agreement):**
   - 99.9% dostępności.
   - Maksymalny czas reakcji: 24 godziny.
3. **Prawa użytkownika:**
   - Dostęp do aktualizacji.
   - Zachowanie poufności danych.
4. **Prawa dostawcy:**
   - Prawo do wyłączenia usługi w przypadku naruszeń regulaminu.
5. **Cennik i płatności:**
   - Koszty licencji, subskrypcji i wsparcia technicznego.
6. **Polityka gwarancji:**
   - Gwarancja poprawnego działania systemu przez 12 miesięcy.

---

### **6. Sposób pomiaru satysfakcji klienta**

#### **Metody pomiaru:**
1. **Ankiety po wdrożeniu:**
   - Ocena funkcjonalności, łatwości obsługi, wydajności.
2. **Net Promoter Score (NPS):**
   - Pytanie: "Jak prawdopodobne jest, że polecisz naszą aplikację?"
3. **Analiza wskaźników:**
   - Czas odpowiedzi na zgłoszenia.
   - Liczba otwartych zgłoszeń technicznych.
4. **Monitorowanie interakcji:**
   - Czas spędzony w aplikacji.
   - Liczba porzuceń koszyka.
5. **Wywiady z kluczowymi użytkownikami:**
   - Szczegółowa analiza potrzeb właścicieli sklepów.
