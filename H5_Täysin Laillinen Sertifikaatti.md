Host 
Arch Linux, Lenovo Legion 5Pro
```bash
~ /  lsb_release -a
LSB Version:	n/a
Distributor ID:	Arch
Description:	Arch Linux
Release:	rolling
Codename:	n/a
```
Virtuaalikone: Kali linux
```bash
$ lsb_release -a
No LSB modules are available.
Distributor ID: Kali
Description:    Kali GNU/Linux Rolling
Release:        2024.1
Codename:       kali-rolling

```

# x) Lue/katso ja tiivistä. (Tässä x-alakohdassa ei tarvitse tehdä testejä tietokoneella, vain lukeminen tai kuunteleminen ja tiivistelmä riittää. Tiivistämiseen riittää muutama ranskalainen viiva kustakin artikkelista. Kannattaa lisätä myös jokin oma ajatus, idea, huomio tai kysymys.)
## OWASP 2021: OWASP Top 10:2021
### [A01:2021 – Broken Access Control](https://owasp.org/Top10/A01_2021-Broken_Access_Control/) (IDOR ja path traversal ovat osa tätä)
Tunnistettuja avainturvallisuusongelmia ovat herkkien tietojen paljastuminen, herkkien tietojen lisääminen lähetettyihin tietoihin ja Cross-Site Request Forgery.

Pääsyoikeuksien epäonnistuminen voi johtaa luvattomaan tietojen käyttöön, muokkaukseen tai tuhoamiseen. Haavoittuvuuksiin kuuluvat vähimmäisvaltuuksien periaatteen rikkominen, pääsynvalvonnan tarkistusten ohitus, epäsuojatut suorat objektiviittaukset ja etuoikeuden korottaminen. Ennaltaehkäisevät toimenpiteet sisältävät pääsynhallinnan toteuttamisen luotettavassa palvelinpuolen koodissa, kieltämällä pääsy oletusarvoisesti, pääsynvalvontamekanismien johdonmukaisen täytäntöönpanon ja mallipääsynvalvonnan, joka valvoo tietueiden omistajuutta.

Hyökkäyskuvaukset sisältävät esimerkkejä SQL-kutsuissa käytetyn varmistamattoman tiedon käytöstä, jonka avulla hyökkääjät voivat päästä käsiksi mihin tahansa käyttäjän tiliin, ja hallintasivujen luvattomasta pääsystä URL:n manipuloinnin kautta.

Ehkäisevät toimenpiteet, kuten datan syöttöjen varmistaminen, pääsynvalvonnan tiukka toteuttaminen ja privilegioiden rajoittaminen, voivat lieventää näitä riskejä.
### [A10:2021 – Server-Side Request Forgery (SSRF)](https://owasp.org/Top10/A10_2021-Server-Side_Request_Forgery_%28SSRF%29/)
SSRF-virheet ilmenevät aina, kun verkkosovellus noutaa etäresurssin validoimatta käyttäjän toimittamaa URL-osoitetta. Se mahdollistaa hyökkääjän houkutella sovellusta lähettämään muokatun pyynnön odottamattomaan kohteeseen, vaikka sitä suojaisivat palomuuri, VPN tai jokin muu verkkojen pääsyvalvontaluettelo (ACL).

Koska nykyaikaiset verkkosovellukset tarjoavat loppukäyttäjille käteviä ominaisuuksia, URL-osoitteen noutaminen on yleistä. Tuloksena SSRF:n esiintyvyys kasvaa. Lisäksi SSRF:n vakavuus kasvaa pilvipalvelujen ja arkkitehtuurin monimutkaisuuden vuoksi.

Kehittäjät voivat estää SSRF:n toteuttamalla seuraavat puolustusmekanismit tai osan niistä:

Verkkokerroksesta:
- Jaa etäresurssien käyttötoiminto erillisiin verkkoihin vähentääksesi SSRF:n vaikutusta.
- Käytä "kiellä oletusarvoisesti" palomuurisääntöjä tai verkkojen pääsyvalvontasääntöjä estääksesi kaiken muun paitsi välttämättömän intranet-liikenteen.
- Kirjaa kaikki hyväksytyt ja estetyt verkkovirrat palomuurilla (katso A09:2021-Turvallisuuslokien ja valvontavirheiden kohdat).

Sovelluskerroksesta:
- Puhdista ja validoikaa kaikki asiakkaan toimittamat syötteet.
- Pakota URL-skeema, portti ja kohde positiivisella sallittujen luettelolla.
- Älä lähetä raakoja vastauksia asiakkaille ja poista HTTP-uudelleenohjaukset.
- Ole tietoinen URL:n johdonmukaisuudesta välttääksesi hyökkäyksiä, kuten DNS-uudelleenohjausta ja "tarkista ajan kuluessa, käytä aikana" (TOCTOU) -kilpailuehtoja.

Lisätoimenpiteitä harkittavaksi sisältävät:
- Vältä turvallisuuteen liittyvien palvelujen käyttöönottoa etujärjestelmissä (esim. OpenID). Hallitse paikallista liikennettä näillä järjestelmillä (esim. localhost).

Hyökkäyskuvaukset, jotka liittyvät SSRF:ään, kattavat sisäisten palvelinten porttiskannauksen, herkkien tietojen paljastumisen, pilvipalvelujen metatietojen tallennuksen käytön ja sisäisten palvelujen kompromoinnin jatkohyökkäyksiä varten, kuten etäkoodin suoritus (RCE) tai palvelun estäminen (DoS).

## PortSwigget Academy:
### [Insecure direct object references (IDOR)](https://portswigger.net/web-security/access-control/idor)
Epävarmat suorat objektiviittaukset (IDOR) ilmenevät, kun sovellukset sallivat käyttäjien toimittaman syötteen suoran pääsyn kohteisiin. Nämä haavoittuvuudet, jotka ovat peräisin OWASP 2007 Top Ten -listalta, mahdollistavat hyökkääjien kiertää pääsynhallinnan. Esimerkiksi URL-osoitteita manipuloimalla hyökkääjät voivat päästä käsiksi muiden käyttäjien tietoihin tai staattisiin tiedostoihin tallennettuihin herkkiin resursseihin.
### 
