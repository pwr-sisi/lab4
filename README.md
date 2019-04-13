# SiSI - Lab 4

# Laboratorium 3. Baza danych

Do wykonania ćwiczeń z laboratorium potrzebujesz zainstalowanych aplikacji: VirtualBox i Vagrant. Obie aplikacje istnieją w wersjach dla systemów Linux, Windows, Mac.

Po pobraniu repozytorium uruchom maszynę vagranta: vagrant up. Gdy maszyna zakończy proces uruchamiania w wyświetlonym przez VirtualBox okinie maszyny wirtualnej zaloguj się na konto vagrant używając hasła vagrant.

W ramach ćwiczenia zapoznasz się z nierelacyjną bazą danych MongoDB. W maszynie zainstalowana została baza danych MongoDB, testowa baza danych oraz aplikacja Robo3T do zdalnej administracji.

## Łączenie się z bazą danych

1. Uruchom program Robo3T (sekcja Akcesoria).
2. Tylko przy pierwszym uruchomieniu: Zaakceptuj umowę licencyjną, nie musisz podawać swoich danych. Następnie w oknie *MongoDB Connections* utwórz (Create) nowe połączenie z bazą danych: adres serwera: localhost, port: 27017.
3. Po połączeniu z serwerem zobaczysz (pod nazwą połączenia) listę baz danych. Rozwiń bazę danych Samples, a w niej kolekcję samples_pokemon. Obejrzyj zawartość kolekcji w prawym panelu. Przy pomocy ikon w prawym górnym rogu panelu przełącz widok kolekcji na widok: tabeli (Table view), dokumentu (Document view) i drzewo (Tree view).
4.  Kliknij na wybranym dokumencie i z menu podręcznego wybierz Edit document. Obejrzyj i zmodyfikuj właściwości wybranego pokemona.
5. W czarnym polu powyżej panelu zmodyfikuj kod w następujący sposób:
   ```javascript
   db.getCollection('samples_pokemon').find({name:"Pikachu"})
   ```
   Naciśnij klawisz F5 i obejrzyj efekt. Zobacz jakie pola ma znaleziony dokument. Zmodyfikuj zapytanie i uruchom je ponownie:
   ```javascript
   db.getCollection('samples_pokemon').find({name:"Pikachu"},{_id:0,name:1,weight:1})
   ```
6. Kliknij dwukrotnie nazwę kolekcji `samples_pokemon` w lewym panelu aby przywrócić domyślny widok.  Kliknij prawym klawiszem dowolny dokument, z menu podręcznego wybierz *Edit document* aby zmodyfikować właściwości pokemona. Przed zapamiętaniem zmian kliknij przycisk *Validate*,
7. Kliknij prawym klawiszem myszy kolekcję `samples_pokemon`, z menu podręcznego wybierz *Insert document*. Wstaw nowy dokument z opisem własnego pokemona.

## Konsola

1. Uruchom terminal: menu / System Tools / LXTerminal
2. Uruchom program `mongo`
3. Wyświetl dostępne bazy danych, wybierz bazę danych Sample i wyświetl kolekcje w bazie danych:
   ```
   show dbs
   use Sample
   show collections
   ```
4. Wyświetl wszystkie dokumenty z kolekcji `samples_pokemon` oraz obejrzyj szczegółowe informacje o Pikachu:
    ```
    db.samples_pokemon.find()
    db.samples_pokemon.find({name:'Pikachu'})
    db.samples_pokemon.find({name:'Pikachu'}).pretty()
    ```



