# Hacker Warmup
```Bash
Host: Arch Linux Lenovo 5 Pro
~$ lsb_release -a
LSB Version:	n/a
Distributor ID:	Arch
Description:	Arch Linux
Release:	rolling
Codename:	n/a
```

## x) Lue/katso ja tiivistä. (Tässä x-alakohdassa ei tarvitse tehdä testejä tietokoneella, vain lukeminen tai kuunteleminen ja tiivistelmä riittää. Tiivistämiseen riittää muutama ranskalainen viiva.)
### € Santos et al: The Art of Hacking (Video Collection): [..] [4.3 Surveying Essential Tools for Active Reconnaissance](https://www.oreilly.com/videos/the-art-of/9780135767849/9780135767849-SPTT_04_00/). Sisältää porttiskannauksen. 5 videota, yhteensä noin 20 min.
- Aktiivinen tiedustelu on toimintaa, jossa lähetetään informaatiota kohde verkkoon
- Aktiivinen tiedustelu jättää jälkiä logeihin
- Porttiskannaus on yksi yleisimpiä aktiivisen tiedutelun tekniikoista
- Porttiskannauksella pyritään selvittämään aukiolevia portteja kohdejärjestelmässä
- Hyökkääjä pyrkii päästä järjestelmään avoimien porttien kautta

### [Hutchins et al 2011: Intelligence-Driven Computer Network Defense Informed by Analysis of Adversary Campaigns and Intrusion Kill Chains](https://lockheedmartin.com/content/dam/lockheed-martin/rms/documents/cyber/LM-White-Paper-Intel-Driven-Defense.pdf), chapters Abstract, 3.2 Intrusion Kill Chain.
- Perinteiset puolustustyökalut keskittyvät haavoittuvuuksiin ja olettavat onnistuneen tunkeutumisen.
- Tietoon perustuvat puolustustekniikat luovat tiedustelupalauteloopin ja ähentävät tunkeutujien onnistumisen todennäköisyyttä.
- Hyökkäysketjussa pyritään saada pääsy kohteeseen ja toteuttaa hyökkäys toteuttamalla sarja vaiheita.
	- Tiedustelu: on kohteiden tutkimista ja tunnistamista eri lähteistä
	- Aseistaminen: yhdistää etäkäyttö-troijalaisen toimitettavassa olevaan hyötykuormaan.
	- Tomitus: ase lähetetään kohdistettuun ympäristöön
	- Hyödyntäminen: käynnistää hyökkääjän koodin
	- Asentaminen: mahdollistaa hyökkääjän ylläpitää pysyvyyttä ympäristön sisällä
	- Komento ja hallinta: luodaan C2-kanava, mikä antaa hyökkääjällepääsyn kohteeseen
	- Toiminnot tavoitteiden suhteen: hyökkääjä pyrkii saavuttamaan alkuperäisen tavoitteensa

## a) Ratkaise [Over The Wire: Bandit](https://overthewire.org/wargames/bandit/) kolme ensimmäistä tasoa (0-2).
Aloitin asentamalla ssh:n koneelleni
```bash
$ sudo pacman -S openssh
```
Seuraavaksi laitoin ssh demonin toimintaan
```bash
$ systemctl start sshd
```
Nyt pystyin aloittamaan tehtävien suorittamisen.  
  
### Level 0
Yhdistin itseni ssh yhteydellä hostiin. Host on `bandit.labs.overthewire.org` ja käyttäjä `bandit0`.  
Host on portissa `2220`, joka määritellään komennossa `-p 2220`.
```bash
$ ssh -p 2220 bandit0@bandit.labs.overthewire.org
```
Tämän jälkeen kirjauduin sisään (salasana on `bandit0`)  
Käytin komentoa `ls` saadakseni tietää tiedoston nimen, mikä sisältää salasanan.
```bash
$ ls
readme
```

Seuraavaksi sain level 1 salasanan komennolla `cat readme`
```bash
$ cat readme
NH2SXQwcBdpmTEzi3bvBHMM9H66vVXjL
```  
### Level 1
Kirjauduin level 1 tehtävään ssh:lla
```bash
$ ssh -p 2220 bandit1@bandit.labs.overthewire.org
```
Ja käytin saamaani salasanaa kirjautuakseni sisään.  
Käytin komentoa `ls` saadakseni tietää tiedoston nimen, mikä sisältää salasanan.
```bash
$ ls
-
```
Seuraavaksi hankin seuraavan salasanan komennolla `cat ./-`
```bash
$ cat ./-
rRGizSaX8Mk1RTb1CNQoXTcYZWU6lgzi
```
Tässä täytyi käyttää tiedostopolkua `./-`, koska `-` käytetään määrittelemään komentorivi vaihtoehtoja.  

### Level 2

Kirjauduin level 2 tehtävään ssh:lla ja käyttämällä edellisellä levelillä saamaani salasanaa.
```bash
$ ssh -p 2220 bandit2@bandit.labs.overthewire.org
```
Käyttämällä komentoa `ls` sain tiedoston nimen selville.
```bash
$ ls
spaces in this filename
```
Koska tiedoston nimi sisältää välilyöntejä, täytyy `cat` komennossa käyttää `''` tiedoston nimen ympärillä.
```bash
$ cat 'spaces in this filename'
aBZ0W5EmUfAf7kHTQeOwd8bauFJ2lAiG
```
Näin sain selville level 3 tehtävän salasanan.

## b) Asenna [WebGoat](https://terokarvinen.com/2020/install-webgoat-web-pentest-practice-target/) ja kokeile, että pääset kirjautumaan sisään.
Loitin päivittämällä järjestelmän.
```bash
$ sudo pacman -Syu
```
Kokeilin asentaa Javan ja hyödyllisiä työkaluja [ohjeen](https://terokarvinen.com/2020/install-webgoat-web-pentest-practice-target/) mukaan.
```bash
$ sudo pacman -S openjdk-17-jre ufw wget bash-completion
```
Sovellusta openjdk-17-jre ei kuitenkaan löytynyt. Ohje on kuitenkin Debianille tehty joten googletin mikä on saman paketin nimi Arch linuxilla ja se on `jdk17-openjdk`.  
Muuttamalla paketin nimen komennossa sain ohjelmat asennettua.
```bash
$ sudo pacman -S jdk17-openjdk ufw wget bash-completion
```
Tämän jälkeen aktivoin palomuurin.
```bash
$ sudo ufw enable
[sudo] password for jesse:
Firewall is active and enabled on system startup
```
Seuraavaksi asensin WebGoatin
```bash
$ sudo wget https://terokarvinen.com/2020/install-webgoat-web-pentest-practice-target/webgoat-server-8.0.0.M26.jar
```
Tämän jälkeen käynnistin WebGoatin.
```bash
$ java -jar webgoat-server-8.0.0.M26.jar
```
Seuraavaksi avasin web selaimessa `http://localhost:8080/WebGoat/`  
![WebGoat](https://github.com/Veliquu/Tunkeutumistestaus_2024/assets/92360351/753fef3b-470e-4468-abe3-d92260f77289)  
Täällä loin itselleni käyttäjän `Register new user` kohdasta ja kirjauduin sisään.  
![LoggedIn](https://github.com/Veliquu/Tunkeutumistestaus_2024/assets/92360351/e8516444-cfdc-4a08-8d2e-249ec716b796)  

## c) Ratkaise WebGoatista tehtävät "HTTP Basics" ja "Developer tools". Katso vinkit alta.
### HTTP Basics
Aluksi käydään läpi HTTP:n toimintaa.  
Clientti lähettää pyyntöjä serverille joihin se vastaa. Clientti voi lähettää `GET` tai `POST` pyyntöjä. GET pyynnöillä clientti pyytää tietoa serveriltä. Nämä GET pyynnöt voivat sisältää url parametreja, jotka näkee `ẁeb access` logeista.  
POST pyynnöillä clientti lähettää dataa serverille.  

Itse tehtävässä painoin F12 nähdäkseni selaimelle tulevat GET ja POST pyynnöt, jonka jälkeen annoin nimeni tehtävään.  
![HTTPBasics](https://github.com/Veliquu/Tunkeutumistestaus_2024/assets/92360351/800eca49-4da3-4298-b8e6-4ae91721e42e)  

Sain oikein, että kyseessä oli POST pyyntö, mutta jäi epäselväksi mikä on `Magic number` ja mistä sen löytää.  
![MagicNumber](https://github.com/Veliquu/Tunkeutumistestaus_2024/assets/92360351/7d02658d-c77d-439f-9e79-7d666d906cee)  

### Developer tools
Aluksi käytiin läpi developer toolia. Sen saa auki `F12`, `right click` ja `inspect`, `Ctrl` + `Shift` + `Ì` tai menemällä selaimen vasempaan yläkulmaan, avaamall sielta menu (kolme pistettä), sieltä kohtaan `More tools` ja sitten `Developer tools`.  
Seuraavaksi käytiin läpi developer tool välilehdet:  
  - Elements: HTML- ja CSS-lähdekoodit
  - Console: javascript-tulosteita
  - Sources: kaikki sivun luomiseen käytetyt tiedostot
  - Network: HTTP-pyynnöt ja vastaukset, jotka verkkosivusto on suorittanut.



Ensimmäisessä osiossa syötettiin consoleen javascript functio `webgoat.customjs.phoneHome()`. Tämä antoi vastauksen, josta ohjeen mukaan saatiin numero `-911982842`joka sypötettiin vastaus palkkiin.  
![JavaScript](https://github.com/Veliquu/Tunkeutumistestaus_2024/assets/92360351/3f0222e1-2b75-42c4-bb3b-270b652be710)

Seuraavassa osiossa lähetettiin HTTP pyyntö painamalla sivustolla olevaa `Go!` nappia. Seuraavaksi etsin oikean pyynnön `network`, joka sisälsi payloadissa `networkNum: 67.96952673626701`. Tämä oli oikea vastaus.  
![networkNum](https://github.com/Veliquu/Tunkeutumistestaus_2024/assets/92360351/3af0ff96-2ba2-48c5-9245-53499efa73c9)


## d) Ratkaise PortSwigger Labs: [Lab: SQL injection vulnerability in WHERE clause allowing retrieval of hidden data](https://portswigger.net/web-security/sql-injection/lab-retrieve-hidden-data). (Edellyttää ilmaista rekisteröitymistä. Tehtävän voi ratkaista pelkästään selaimen osoitekenttää muokkaamalla.)
Minulla oli vaikeuksia ymmärtää tätä tehtävää. Luin [tämän](https://portswigger.net/web-security/sql-injection), jotta sain ymmärryksen kuinka SQL injection hyökkäyksen voi tehdä selaimessa.  
Valitsin ensi kategorian isvustolta.  
![categories](https://github.com/Veliquu/Tunkeutumistestaus_2024/assets/92360351/c2b0cb22-fcbd-4a04-86dd-4746bddf4427)
 
Tämän jälkeen tarkastelin sivuston url:ää, joka näytti seuraavanlaiselta:  
```bash
https://0afa00bd03912d1b81879e8200dc004d.web-security-academy.net/filter?category=Gifts
```
Tämä sivu näytti minulle 3 tuotetta.  
![prducts3](https://github.com/Veliquu/Tunkeutumistestaus_2024/assets/92360351/03b5f8a6-3571-4b52-ab34-335cf7aceefb)
  
Tämän jälkeen lisäsin url:in perään `'+or+1=1--`.  Tämä muuttaa SQL lausetta niin, että se palauttaa kaikki tuotteet millä on kategoria `Gifts` ja `1=1`. Tämä palauttaa kaikki tuotteet sillä SQL:ssä `--` on kommentti, minkä takia `released = 1` ei ole enää kriteeri minkä mukaan tuloksia palautetaan.
```bash
SELECT * FROM products WHERE category = 'Gifts' OR 1=1--' AND released = 1
```
```bash
https://0afa00bd03912d1b81879e8200dc004d.web-security-academy.net/filter?category=Gifts'+or+1=1--
```
Tämä näytti minulle lisää tuetteita.  
![moreProducts](https://github.com/Veliquu/Tunkeutumistestaus_2024/assets/92360351/bade68de-b658-44f9-8e68-97fe98a682a2)

Tällä labsi tuli suoritettua.  
![solved](https://github.com/Veliquu/Tunkeutumistestaus_2024/assets/92360351/b4ff6772-e838-42ea-bbc8-a8d391ae8f7d)
  

## e) Asenna Linux virtuaalikoneeseen. Suosittelen joko [Kali](https://www.kali.org/) (viimeisin versio) tai [Debian 12-Bookworm](https://terokarvinen.com/2021/install-debian-on-virtualbox/).

Asensin Virtualboxin host koneelle.
```bash
$ sudo pacman -S virtualbox
```

Minulla oli olemassa oleva Debian ISO koneellani, mutta ISO-imagen saa ladattua [täältä](https://cdimage.debian.org/debian-cd/current-live/amd64/iso-hybrid/)
Seuraavaksi valitsin Virtualboxista `New` ja annoin virtuaalikoneelle nimeksi Debian.  
![image](https://github.com/Veliquu/Tunkeutumistestaus_2024/assets/92360351/5ebcc60a-2a08-47c4-ad28-cf0ba82d5339)
 
Sitten loin virtuaalikoneelle käyttäjän.  
![image](https://github.com/Veliquu/Tunkeutumistestaus_2024/assets/92360351/727c3448-29e2-4bf2-bb0b-c17d98ed1c45)
  
Seuraavaksi määrittelin virtuaalikoneen RAM muistin ja prosessorien ytimien määrän.  
![image](https://github.com/Veliquu/Tunkeutumistestaus_2024/assets/92360351/7361e5c1-762f-49f5-b356-8233c673a924)
  
Sittten määrittelin levyn koon virtuaalikoneelle.  
![image](https://github.com/Veliquu/Tunkeutumistestaus_2024/assets/92360351/f7bfa169-1cab-4cc1-9714-ce86ce9473da)
 
Viimeisenä tarkistin virtuaalikoneen tiedot ja hyväksyin sen luonnin.  
![image](https://github.com/Veliquu/Tunkeutumistestaus_2024/assets/92360351/637823b2-03a3-41d7-9a08-ce3b625657d4)
  

Käynnistin virtuaalikoneen. Ja ajoin Debianin asennuksen.
![image](https://github.com/Veliquu/Tunkeutumistestaus_2024/assets/92360351/b6d1be08-84ac-47ac-995d-87e8591288b2)
 
Debian on asennettu.  
![installed](https://github.com/Veliquu/Tunkeutumistestaus_2024/assets/92360351/5d9aa96c-85ff-4f8c-869b-da9eaff8a7e8)

Lopuksi ajoin vielä: 
```bash
$ sudo apt update && sudo apt upgrade
```
Näin varmistin kaiken olevan päivitettybä.  

## f) Porttiskannaa 1000 tavallisinta tcp-porttia omasta koneestasi (localhost). Analysoi tulokset.  
Asensin Debian virtuaalikoneelle `nmap`.
```bash
~$ sudo apt install nmap
```
Minkä jälkeen ajoin `nmap localhost`, mikä skannaa 1000 tavallisinta tcp-porttia.  
![localhost](https://github.com/Veliquu/Tunkeutumistestaus_2024/assets/92360351/831ed839-cc58-428c-86af-53c8dc27c40b)
  

Tuloksissas näkyy, että virtuaalikoneella on vain portti 631/tcp auki.    
Portti 631 on `ipp` verkkoportti.

Kokeilin myös host koneella.  
![HostLocalhost](https://github.com/Veliquu/Tunkeutumistestaus_2024/assets/92360351/b90964a8-d3cc-4056-912c-98cf19dce292)
 
Tämä näytti 3 porttia auki.  
  - Portti 22/tco on ssh:ta varten
  - Portti 8080/tcp on auki, koska WebGoat oli vielq tehtävää tehdessä auki.
  - Portti 9001/tcp, tästä en ole täysin varma, mutta [tämän](https://www.speedguide.net/port.php?port=9001) sivuston selityksen mukaan oletan tämän portin olevan auki, koska se toimii routerina virtuaali koneelle.

## g) Porttiskannaa kaikki koneesi (localhost) tcp-portit. Analysoi tulokset. (Edellisissä kohdissa mainittuja analyyseja ei tarvitse toistaa, voit vain viitata niihin ja keskittyä eroihin).
Debianilla ajoin komennon `nmap -p0- localhost`. `-p0-` skannaa kaikki portit lähtien portista 0, koska se voi jostain ihmeen syystä olla välillä käytössä.   
![allPorts](https://github.com/Veliquu/Tunkeutumistestaus_2024/assets/92360351/2f4eb5df-87b1-482d-b9fa-93c398a9a7db)

Debianilla ei ollut muita portteja auki, kuin samat mitkä edellisessä kohdassa näkyi.  
  
Host koneella ajoin saman komennon.  
![HostAllPorts](https://github.com/Veliquu/Tunkeutumistestaus_2024/assets/92360351/6c9996be-3a82-418f-90a7-d4bf756e465a)
 
Host koneellakaan ei ollut muita portteja auki.

## h) Tee laaja porttiskanaus (nmap -A) omalle koneellesi (localhost), kaikki portit. Selitä, mitä -A tekee. Analysoi tulokset. (Edellisissä kohdissa mainittuja analyyseja ei tarvitse toistaa, voit vain viitata niihin ja keskittyä eroihin.).
Debianilla ajoin `sudo nmap -A -p0- localhost`  
![Ports-A](https://github.com/Veliquu/Tunkeutumistestaus_2024/assets/92360351/2c985c2c-3a24-460a-bdc4-a981b18f0d8a)

Uusia auki olevia portteja ei löytynyt, mutta komento sai selville järjestelmän pyörivän linux kernerillä, mutta distributiota se ei saanut selville.  

Ajoin saman komennon host koneella.  
![HostPorts-A](https://github.com/Veliquu/Tunkeutumistestaus_2024/assets/92360351/219091cf-5e1c-474a-90a1-ee50d9474623)
  
Tällä kertaa host koneella ei löytynyt kuin ssh portti avonaisena. Tämä johtuu siitä että sulkiessasni avoimia ikkunoita suljin WebGoatin samalla.  

-A lippu aktivoi neljä muuta lippua:
  - -sV, joka tunnistaa käynnissä olevia palveluita ja niiden versioita.
  - -O, joka tunnistaa käyttöjärjestelmän.
  - -sC, joka pyrkii havaitsemaan palvelun haavoittuvuuksia, haittaohjelmia, sekä kerää lisätietoja tietokannoista ja verkkopalveluista.
  - --traceroute, joka sisältää toisen käänteisen DNS-resoluutiokierroksen intermediate hosteille.
  
## i) Asenna demoni tai pari (esim Apache ja SSH). Vertaile, miten localhost:n laajan porttiskannauksen tulos eroaa.
Asensin Debianille ssh:n ja apachen. 
```bash
$ sudo apt install ssh apache2
```
Tämän jälkeen aktivoin molemmat järjestelmässä
```bash
$ sudo systemctl start ssh
$ sudo systemctl start apache2
```

Seuraavaksi ajoi `nmap -p0- localhost`  
![apache](https://github.com/Veliquu/Tunkeutumistestaus_2024/assets/92360351/869762b8-03c2-43d7-bd71-c1876d8853f9)

Portit 22/tcp ja 80/tcp ovat nytten avattu/
   - 22/tcp on ssh:n käytössä
   - 80/tcp on apachen käyttämä portti.

## j) Kokeile ja esittele jokin avointen lähteiden tiedusteluun sopiva weppisivu tai työkalu. Hyviä esimerkkejä löytyy [Bazzel: IntelTechniques: Tools](https://inteltechniques.com/tools/index.html) ja [Bellingcat: Resources](https://www.bellingcat.com/category/resources/), voit myös käyttää muuta itse valitsemaasi työkalua. Työkalua pitää siis myös kokeilla, pelkkä nimen mainitseminen ei riitä. Pidä esimerkit harmittomina, älä julkaise kenenkään henkilökohtaisia salaisuuksia raportissasi.
Kokeilin [namevine.com](https://namevine.com)ia. Tämä löytyi [Bazzel: IntelTechniques: Tools](https://inteltechniques.com/tools/index.html) usernames osiosta. Kokeilin tehtävässä käyttää käyttäjätunnusta, joka on ollut itsellä käytössä viimeksi 12 vuotiaana.  
Laitoin hakuun siis käyttäjän `Jouolio`joka on siis itsellä ollut käytössq vain Steamsissä.  
![namevine](https://github.com/Veliquu/Tunkeutumistestaus_2024/assets/92360351/6af4a321-a4a5-40b5-8035-2c5384982e6b)

Vaikka käyttäjätunnus on ollut itsellä vain Steamsissa käytössä niin namevine löytää, että nimi on käytössä muuallakin (Twitter, Facebook, Youtube yms). Sivusto antaa myös haetun nimen perusteella domain nimi ehdotuksia.

## Lähteet  
Debian: [https://cdimage.debian.org/debian-cd/current-live/amd64/iso-hybrid/](https://cdimage.debian.org/debian-cd/current-live/amd64/iso-hybrid/)  
nmap: [https://linux.die.net/man/1/nmap](https://linux.die.net/man/1/nmap)  
PortSwigger: [https://portswigger.net/web-security/sql-injection](https://portswigger.net/web-security/sql-injection)  
Speed Guide: [https://www.speedguide.net/port.php?port=9001](https://www.speedguide.net/port.php?port=9001)  
Tero Karvinen: [https://terokarvinen.com/2024/eettinen-hakkerointi-2024/](https://terokarvinen.com/2024/eettinen-hakkerointi-2024/)  
Tero Karvinen: [https://terokarvinen.com/2020/install-webgoat-web-pentest-practice-target/](https://terokarvinen.com/2020/install-webgoat-web-pentest-practice-target/)  





