Historyjki użytkownika
1. przegląd produktów
	1. jako użytkownik
	2. chce oglądać produkty
	3. aby wybrać produkt do zakupu
2. budowa sklepu
	1. jako sprzedawca
	2. chcę skonfugurować sklep
	3. aby sprzedawać produkty
3. zwiększenie priorytetu
	1. jako sprzedawca
	2. chcę zwiększyć zaufanie klienta
	3. aby mógł przeglądać więcej zawartości

Wymagania Funkcjonalne:
- dodawanie sklepu - prosty interface pozwalający na szybkie stworzenie sklepu dostępnego dla użytkowników
- dodawanie produktów - możliwość dodawania produktów dla właściciela sklepu
- logowanie - możliwość zalogowania się użytkownika do systemu
- logowanie dla właściciela - możliwość logowania się do systemu dla właściciela sklepu
- wyszukiwanie produktu w sklepie - użytkownik może wyszukiwać produkty w sklepie
- zamówienia - użytkownik może sprawdzić zamówienia jakich dokonał

wymagania niefunkcjonalne
- bezpieczeństwo użytkownika - użytkownik musi pozostać anonimowy
- bezpieczeństwo sprzedawcy - sprzedawca również musi pozostać anonimowy
- dostępność - system musi obsługiwać zapytania przez 99,9% czasu miesiąca
- przejrzystość - użytkownik musi móc zrealizować główne funkcje w mniej niż  5 kroków
- zgodność z prawem - do sklepu mogą zostać dodane produkty legalne w rejonie w którym sklep określił jako swoje miejsce działalności :)

2 scenariusze przypadków użycia
1. logowanie lub rejestracja (niezalogowany uzytkownik)
	1. użytkownik wybiera "login" lub "register"
		1. po wybraniu "register"
			1. pojawia się formularz rejestracji
				użytkownik wypełnia
				- username (min 6 znaków - max 20 znaków)
				- password (min 7 znaków - max 20 znaków)
				- OTP - autoryzacja
				klika zarejestruj
				- w bazie danych pojawia się jego konto i może on się poprawnie logować do sklepu
		2. po wybraniu login
			- pojawia się formularz logowania
			- użytkownik wypełnia login
			- użytkownik wypełnia hasło
			- jeżeli dane są poprawne użytkownik ma dostęp do zasobów wpp. użykownik dostaje informacje że podane dane są niepoprawne
2. dodanie produktu (zalogowany właściciel sklepu)
	1. właściciel wybiera przycik dodaj produkt
	2. użytkownik wybiera czy chce dodać produkty z pliku JSON czy ręcznie
		1. tryb JSON
			użytkownik podaje plik json w którym znajduje się opis produktu zgodny z dokumentacją
		2. manualnie
			- użytkownik jest przekierowywany na formularz dodawania produktu do sklepu
			- użytkownik wypełnia nazwe produktu (min 3 max 20 znaków)
			- użytkownik wypełnia cene produktu (0 - 1_000_000_000)
			- użytkownik wypełnia ilość produktu (min 0 max 1_000_000_000)
			- użytkownik wypełnia opis produktu (min 0 max 1000 znaków)
			- użytkownik wypełnia dla jakich klientów jest produkt ( freeTier, lowTier, godTier)
		- system przeprawadza walidacje przesłanego produktu względem zgodności prawnej 
		- jeżeli walidacja się powiodła właściciel dostaje informacje o dodaniu produktu
		- produkt jest dostępny do przeglądania i zakupu
1. zakup produktu(zalogowany użytkownik)
	1. użytkownik wchodzi do sklepu
	2. użytkownik dodaje produkt do koszyka 
	3. użytkownik wybiera zakup produkt
	4. użytkownikowi pojawia się pole chatu ze sprzedwacą gdzie mogą wymieniać wiadomości(w celu uzgodnienia przesyłki)
	5. użytkownik płaci na wskazane konto
	6. sprzedawca dostaje informacje o zakupie
	7. zakup pojawia się w historii użytkownika
2. 

3. Widoki:
![[Pasted image 20241208213920.png]]
![[Pasted image 20241208213906.png]]
![[Pasted image 20241208213851.png]]
![[Pasted image 20241208213838.png]]
![[Pasted image 20241208213823.png]]
![[Pasted image 20241208213808.png]]


3. projekt architektury

   aplikacja napisana zostanie w Golangu wraz z goGin jako server backend, do komunikacji real time użyty zostanie GorillaWebSocket

   do wyświetlania treści na stronie wykorzystamy bibliotekę React pozwalającą na tworzneie responsywnych stron http

   jako bazy danych skorzystamy z dynamoDb w celu zapewnienia elastyczności obiektów oraz szybkiej komunikajci ze zhostowanymi na aws aplikacjami

   schematy obiektów
   
   
{ //obiekt właściciela sklepu <br>
	_id: number<br>
	username: string<br>
	passwordHash: string<br>
	salt: binary<br>
	shopId: number<br>
}

{ // obiekt sklepu<br>
	_id: number<br>
	shopName: string<br>
	freeTierUsers: []User<br>
	lowTierUsers:  []User<br>
	godTierUsers: []User<br>
	products: []Product <br>
}

{ // product<br>
	_id: number<br>
	name: string<br>
	price: number<br>
	count: number<br>
	availability: Tier<br>
	description: string<br>
}

{ // user<br>
	_id: number<br>
	username: string<br>
	passwordHash: string<br>
	salt: binary<br>
	boughtProduct: {<br>
		shopId: number<br>
		date: number<br>
		products: []Products<br>
	}<br>
}<br>

4. główne zasady programowania/ kodowanaia dla ułomnych -- Kacper
   1. pisanie kodu powinno się odbywać z ogólnie przeyjętymi zasadami
   2. komentarze, nazwy zmiennych, kod powinny być pisane po angielsku - aby w razie sukcesu komercyjnego, można było rozszerzyć zespół nie zamykając się na poski rynek
   3. jako iż kod pisany jest w języku GoLang, powinien on spełniać szeroko przyjęte standardy tego języka takie jak
      1. nazewnictwo zmiennych, funkcji i klas prywatnych camelCase, exportowanych PascalCase - wymuszone przez sam język
      2. nazwy interfejsów powinien zaczynać się od I następnie sama nazwa interfacu z wielkiej litery np IGameEngine
      3. testy karzdej funkcji powinny znajdować się w tym samym katalogu co testowana metoda/klasa, oraz nazwa musi kończyć się na _test.go gameEngine_test.go
      4. nie ignorujemy błędów
      5. utrzymywanie prostych jednozadaniowych funkcji
      6. w przypadku pisannia kodu w którym możliwe jest użycie wzorców projektowych, należy ich użyć w celu zwiększenia elastyczności projektu w szczególności modele: abstract factory, builder, adapter, proxy, facade, flyweight, chain of Responsibility, observer
   4. korzystając z reacta, niedopuszczalne jest korzystanie z typów any, każdy typ musi być ściśle określony
   5. jeden plik jeden komponent, dla każdego komponentu, jego interface powinien być w tym samym pliku
   6. jeden katalog jedna użyteczność
   7. cały kod umieszczony będzie w prywatnym repozytorium github, z dostępem dla programistów, testerów oraz zarządu
   8. jak najmniejsze commity 
   9. mergowanie z opcją rebase 
   10. wiadomość commitu powinna być w języku angielskim i opisywać jakie nastąpiły zmiany
5. Identyfikacja i zasady zarządzania ryzykiem:
   - Niedotrzymanie terminu - Prawdopodobieństwo tego ryzyka jest
   dość spore. Jeżeli nie będziemy na bieżąco sprawdzać postępów lub źle rozplanujemy
   czas na wykonywanie danego etapu będziemy musieli się rozprawić z brakującym
   czasem. Aby uniknąć tego problemu należy monitorować postępy na bieżąco. Jeśli
   problem wystąpi pracownicy będą musieli zmierzyć się z nadgodzinami lub opóźnieniem
   w realizacji projektu.
   - Przeciążenie serwerów - Prawdopodobieństwo tego ryzyka na początku działania jest znikome. Z rozpoczęciem kampani reklamowej ryzyko się sporo zwiększy, 
   ale będziemy spodziewać się kiedy może to nastąpić i łatwo temu zapobiegniemy.
	- smerfy pod chatą
1. Zgodność z tablicą koncepcyjną:
   Po przeanalizowaniu wykonanych prac i porównaniu ich z wizją z tablicy koncepcyjnej oraz specyfikacji wymagań, możemy stwierdzić, że otrzymane wyniki są zadowalające. Aktualnie nie przewidujemy większych zmian względem tego, co zostało opisane w tablicy koncepcyjnej, ani specyfikacji wymagań.

 
