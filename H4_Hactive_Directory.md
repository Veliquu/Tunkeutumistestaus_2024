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

# x) Lue/katso ja tiivistä. (Tässä x-alakohdassa ei tarvitse tehdä testejä tietokoneella, vain lukeminen tai kuunteleminen ja tiivistelmä riittää. Tiivistämiseen riittää muutama ranskalainen viiva kustakin artikkelista. Kannattaa lisätä myös jokin oma ajatus, idea, huomio tai kysymys.)
Luettiin [Hijacking DLLs in Windows](https://www.wietzebeukema.nl/blog/hijacking-dlls-in-windows)  

DLL-hyökkäysten yleiskatsaus:

- DLL-hyökkäysten määritelmä ja virheellinen käsitekäyttö, jossa usein sekoitetaan eri termejä.
- Hyökkääjien motiivit: suoritus, pysyvyys, privilegioiden kohotus.
- Erilaiset lähestymistavat DLL-hyökkäyksiin, kuten DLL:n korvaaminen, hakujärjestyksen kaappaaminen ja DLL:n uudelleenohjaaminen.
- Haasteet haavoittuvien suoritettavien löytämisessä, keskittyen heikkoihin variaatioihin oletus käyttäjäoikeuksien vuoksi.
- Esimerkki OceanLotus/APT32:sta, joka käytti laillista suoritettavaa yhdessä haitallisen DLL:n kanssa.
- Lähestymistapa suoritettavien tunnistamiseen ja testaamiseen.

Tunnistetut haavoittuvat suoritettavat:

- Keskitytty suoritettaviin tiedostoihin kohdekansiossa C:\Windows\System32.
- Käytetty Procmon-työkalua DLL-latausten seurantaan.
- Kopioitu luotettavia suoritettavia tiedostoja analysointia varten.
- Vahvistettu 287 haavoittuvaa suoritettavaa, joilla on kaappaamiskelpoisia DLL-tiedostoja.

Yhdistäminen UAC:n ohituksen kanssa:

- Tutkittu mahdollisuutta kohottaa käyttöoikeuksia UAC:n ohituksen avulla.
- Auto-kohotetut suoritettavat haavoittuvia DLL-hyökkäyksille.
- UAC:n ohitusmenetelmät ja hakemistojen jäljitelmät.

Ennaltaehkäisy ja havaitseminen:

- Ehdotettu ennaltaehkäisykeinoja, kuten absoluuttisten polkujen käyttöä ja DLL:ien varmistamista ennen niiden lataamista.
- Korostettu havainnoinnin tärkeyttä epätyypillisten DLL-latauspolkujen valvonnassa.

# a) Ratkaise Nikitan / WithSecuren Windows-haaste. Älä julkaise läpikävelyohjetta, myöskään itse kirjoittamaasi. (Update: Tämä on nyt siis kerrankin sellainen tehtävä, johon voi vastata vain "tehty").
Yritettiin tehdä. Olin sairaana kun tunnilla käyttiin näitä asioita ja itse opiskeluna en oikein ymmärtänyt näitä.

