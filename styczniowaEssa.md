1. Niezbędna pojemność bazy danych
Założenia:
Szacowana liczba użytkowników: 10,000 aktywnych użytkowników.
Szacowana liczba właścicieli sklepów: 500.
Szacowana liczba produktów na sklep: Średnio 200 produktów.
Szacowana liczba transakcji na użytkownika: 100 transakcji rocznie.
Obliczenia:
Tabela użytkowników (User):

Rozmiar jednego rekordu:
username: 20 znaków = 20 B
passwordHash: 64 B
salt: 16 B
Zakupione produkty: średnio 100 produktów rocznie → powiązanie z historią transakcji.
Razem: ~100 B.
10,000 użytkowników → 10,000 × 100 B = 1 MB.
Tabela właścicieli sklepów (Owner):

Rozmiar jednego rekordu:
username: 20 B
passwordHash: 64 B
salt: 16 B
Razem: ~100 B.
500 właścicieli → 500 × 100 B = 0.05 MB.
Tabela sklepów (Shop):

Rozmiar jednego rekordu:
shopName: 50 B
Lista produktów: średnio 200 produktów × 50 B = 10 KB.
Razem: ~10 KB.
500 sklepów → 500 × 10 KB = 5 MB.
Tabela produktów (Product):

Rozmiar jednego rekordu:
name: 20 B
price: 8 B
count: 4 B
description: średnio 200 B
Razem: ~232 B.
500 sklepów × 200 produktów = 100,000 produktów.
100,000 × 232 B = 23.2 MB.
Tabela transakcji (Transaction):

Rozmiar jednego rekordu:
transactionId: 16 B
userId: 8 B
productId: 8 B
date: 8 B
Razem: ~40 B.
10,000 użytkowników × 100 transakcji = 1,000,000 transakcji.
1,000,000 × 40 B = 40 MB.
Łączna pojemność bazy danych:
Użytkownicy: 1 MB.
Właściciele sklepów: 0.05 MB.
Sklepy: 5 MB.
Produkty: 23.2 MB.
Transakcje: 40 MB.
Razem: ~69 MB (przy uwzględnieniu indeksów i zapasowej przestrzeni: ~100 MB).
2. Plan wdrożenia
Etapy wdrożenia:
Przygotowanie środowiska:
Utworzenie środowiska produkcyjnego w AWS.
Konfiguracja bazy danych DynamoDB.
Migracja danych:
Import testowych danych.
Weryfikacja integralności danych.
Testy przedwdrożeniowe:
Testy wydajnościowe przy obciążeniu 1,000 równoczesnych użytkowników.
Testy regresji.
Soft launch:
Uruchomienie dla ograniczonej grupy użytkowników (beta testy).
Pełne wdrożenie:
Publiczne udostępnienie aplikacji.
Monitoring i optymalizacja:
Użycie narzędzi monitorujących (np. AWS CloudWatch).
3. Koncepcja organizacji szkoleń użytkowników
Cele szkoleń:
Nauka korzystania z systemu.
Zwiększenie efektywności użytkowników.
Redukcja liczby błędów użytkownika.
Forma szkoleń:
Instrukcje online: Dokumentacja i filmy instruktażowe.
Warsztaty stacjonarne: Dla właścicieli sklepów.
Webinary: Interaktywne sesje Q&A.
Materiały samouczkowe: Dostosowane do różnych grup użytkowników.
4. Koncepcja wsparcia technicznego
Model wsparcia:
Obsługa zgłoszeń:
System zgłoszeń w aplikacji.
Średni czas odpowiedzi: 24 godziny.
Kanały kontaktu:
E-mail: 24/7.
Telefon: 9:00-17:00 (dni robocze).
Zapewnienie ciągłości działania:
Redundancja serwerów w AWS.
Regularne kopie zapasowe (co 12 godzin).
SLA: 99.9% dostępności.
Usuwanie błędów:
Krytyczne: Naprawa w ciągu 24 godzin.
Średnie: Naprawa w ciągu 5 dni roboczych.
Niskie: Naprawa w kolejnym cyklu aktualizacji.
5. Główne punkty umów
Zakres usług:
Dostarczenie aplikacji i wsparcia technicznego.
Zapewnienie ciągłości działania.
SLA (Service Level Agreement):
99.9% dostępności.
Maksymalny czas reakcji: 24 godziny.
Prawa użytkownika:
Dostęp do aktualizacji.
Zachowanie poufności danych.
Prawa dostawcy:
Prawo do wyłączenia usługi w przypadku naruszeń regulaminu.
Cennik i płatności:
Koszty licencji, subskrypcji i wsparcia technicznego.
Polityka gwarancji:
Gwarancja poprawnego działania systemu przez 12 miesięcy.
6. Sposób pomiaru satysfakcji klienta
Metody pomiaru:
Ankiety po wdrożeniu:
Ocena funkcjonalności, łatwości obsługi, wydajności.
Net Promoter Score (NPS):
Pytanie: "Jak prawdopodobne jest, że polecisz naszą aplikację?"
Analiza wskaźników:
Czas odpowiedzi na zgłoszenia.
Liczba otwartych zgłoszeń technicznych.
Monitorowanie interakcji:
Czas spędzony w aplikacji.
Liczba porzuceń koszyka.
Wywiady z kluczowymi użytkownikami:
Szczegółowa analiza potrzeb właścicieli sklepów.






