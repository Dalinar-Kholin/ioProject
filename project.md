w czym piszemy // dla nas
- golang + goGin + gorillaWebSocket - bibliioteka backend
- dynamoDb - baza danych 
- hosting na AWS 
- typescript + react


1. scenariusze przeypadków użyci
   1. logowanie
   2. wyszukiwanie produktu
   3. dodawanie produktu
   4. dodawanie sklepu :) 
   5. sprawdzanie zamówień
   6. dodawanie zamówień
2. Widoki:

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
	- narzekanie że trudno inwestowac
6. Zgodność z tablicą koncepcyjną:\\
   Po przeanalizowaniu wykonanych prac i porównaniu ich z wizją z tablicy koncepcyjnej
   oraz specyfikacji wymagań, możemy stwierdzić, że otrzymane wyniki są zadowalające.
   Aktualnie nie przewidujemy większych zmian względem tego, co zostało opisane w tablicy
   koncepcyjnej, ani specyfikacji wymagań.

 
