# MTTPP-project

## Opis projekta

Ideja ovog projekta je testiranje i usporedba 5 web stranica za online prodaju kako reagiraju pod opterećenjem, većim brojem istovremenih korisnika. Odabrane stranice za testiranje su: Links, HGSpot, Protis, Mall.hr i Extreme Digital. Nakon testiranja, rezultati će se usporediti i utvrditi će se koja od testiranih stranica ima najbolje perfomanse. Testiranje će se odvijati pomoću Apache JMeter alata. To je alat koji nudi brojne mogućnosti testiranja, od simuliranja većeg broja korisnika do detaljnog korištenja i simulacije stvarnog korisnika.

## Test opterećenja

Test opterećenja je kreiranje modela po kojem će se simulirati veći broj korisnika koji istovremeno ili u vrlo kratkom roku pristupaju istoj stranici. U ovom testu će se razmatrati na koliko zahtjeva pojedina stranica može odgovoriti u jednoj minuti. Testiranje će se izvoditi simulacijom 500 korisnika koji šalju zahtjeve tijekom 10 sekundi.
Jednostavan način da se to ostavi je korištenjem JMeter alata. Postupak koji je potreban da se model napravi je slijedeći: 

1. U testnu grupu potrebno je dodati standardu konfiguraciju HTTP standarda u kojem se definira zajednička komponenta svih stranica, a to je HTTPS protokol.

![HTTP](https://user-images.githubusercontent.com/42654074/123707474-0e1f5700-d86a-11eb-8a2c-79201f2045fd.PNG)

2. Potrebno je napraviti _Thread Group_ za svaku web stranicu i u njima definirati broj simuliranih korisnika, vrijeme pokretanja te koliko će se puta simulirati. Uz to se mogu konfigurirati razne opcije. Kako je već napisano, broj korisnika je 500, vrijeme pokretanja je 10 sekundi i vrijeme ponavljana je jednom.

![Niti](https://user-images.githubusercontent.com/42654074/123707842-a9183100-d86a-11eb-805d-23c09d7a885e.PNG)

3. Još je potrebno dodati elemente _HTTP Request_, _View Result Tree_, _Graph Results_ svakoj grupi.

![Elementi](https://user-images.githubusercontent.com/42654074/123708164-3bb8d000-d86b-11eb-8b4e-9c4d12719cd1.png)

4. Nakon što se elementi dodaju svakoj grupi, potrebno je konfigurirati _HTTP Request_ jer se on razlikuje za svaku grupu. Kao primjer prikazati će se za prvu grupu. Ono što je potrebno napraviti je definirati ime servera kojem se pristupa, koja se metoda koristi i ako postoji dodati put na stranici kojoj se pristupa. Samo se osnovni dio web adrese stavlja u polje imena jer je to dio koji predstavlja IP adresu servera dok se sve ostale informacije stavljaju dodatno polje nakon definiranja tipa poziva. Ovdje će se koristiti samo _GET_ pozivi.

![HTTP_konf](https://user-images.githubusercontent.com/42654074/123708598-fea10d80-d86b-11eb-92f6-a2ff3e1f87b2.png)

5. Nakon što su se svi elementi definirali, potrebno je provesti testiranje. Nakon što testovi završe i sve niti zatvore, u elementu _View Results Tree_ mogu se vidjeti pojedini pozivi, njihov status i ako se pritisne na bilo koji mogu se vidjeti povratne informacije. Isto tako u elementu _Graph Results_ mogu se vidjeti vremena pristupa i ostale korisne informacije.

![Lista](https://user-images.githubusercontent.com/42654074/123709036-a61e4000-d86c-11eb-85e9-1ffc953be0a9.png)

![Graf](https://user-images.githubusercontent.com/42654074/123709176-e8478180-d86c-11eb-944f-1a5e96b23736.png)


## Analiza rezultata


### Prikaz grafova

1. __Links__

![Links](https://user-images.githubusercontent.com/42654074/123709465-699f1400-d86d-11eb-91f8-c354f5ff9687.png)

2. __HGSpot__

![Hgspot](https://user-images.githubusercontent.com/42654074/123709495-73c11280-d86d-11eb-9e66-4b7206c5201c.PNG)

3. __Protis__

![Protis](https://user-images.githubusercontent.com/42654074/123709514-7d4a7a80-d86d-11eb-864d-03dbbe6e916f.PNG)

4. __Extreme Digital__

![Extreme_Digital](https://user-images.githubusercontent.com/42654074/123709531-876c7900-d86d-11eb-9141-ce754e8a98f5.PNG)

5. __Mall.hr__

![Mall](https://user-images.githubusercontent.com/42654074/123709539-8b000000-d86d-11eb-829a-6039b13edf4a.PNG)

### Tablica rezultata

Web stranica | Propusnost | Devijacija
-------------|------------|-----------
Extreme Digital | 1472 / min | 54
Links | 467 / min | 12110
Mall.hr | 270 / min | 13781
Protis | 139 / min | 52473
HGSpot | 86 / min | 16361


## Analiza 

Propusnost je glavni pokazatelj koliko je stranica dobra, ondnoso server na kojem se nalazi. Iz tablice se može vidjeti da __Extreme Digital__ ima najveću propusnost, isto tako i najmanju devijaciju što je još jedan super pokazatalj. Na rezultate utječe puno toga na strani servera, ali isto tako i na strani korisnika. Lokacija, udaljenost između korisnika i servera, brzina interneta na svakoj strani, snazi računalnih komponenti, trenutnom opterećenju mreže i slično.

