Prvi projekat iz sistemskog programiranja.
Radio tim 73 (Petar Stojanović, 19408)

Tekst zadatka:
Kreirati web server koji vrši binarizaciju slike (pretvaranje u crno-belu sliku pomoću praga). Svi
zahtevi serveru se šalju preko browser-a korišćenjem GET metode. U zahtevu se kao parametar
navodi naziv fajla, odnosno slike, kao i vrednost praga. Server prihvata zahtev, pretražuje root
folder za zahtevani fajl i vrši binarizaciju — svaki piksel čija je prosečna vrednost RGB kanala
ispod praga postaje crn (0, 0, 0), a iznad praga postaje beo (255, 255, 255). Ukoliko traženi fajl ne
postoji, vratiti grešku korisniku.
Primer poziva serveru: http://localhost:5050/foto.jpg?prag=128

Strategija upravljanja kešom: Ograničenje veličine

Kritične sekcije sam uočio pri logovanju podataka (rešeno korišnjenjem lock-a), praćenju broja aktivnih niti (rešeno pomoću lock-a) i pri pristupu cache memoriji (korišćen je ConcurrentDictionary za keš kao i za rečnik semafora za specifični unos u kešu. Ovaj drugi rečnik služi za rešavanje keš stampeda - blokira svaku sledeću nit koja pristupa istom ključu u kešu dok prva ne obradi podatak i upiše ga u keš)
