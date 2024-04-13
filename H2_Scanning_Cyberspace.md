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
## Lyon 2009: Nmap Network Scanning: Chapter 15. Nmap Reference Guide:
### [Port Scanning Basics](https://nmap.org/book/man-port-scanning-basics.html) (opettele, mitä tarkoittavat: open, closed, filtered; muuten vain silmäily)
- `open` tarkoittaa sitä, että sovellus hyväksyy aktiivisesti TCP yhteyksiä, UDP datagrammeja tai SCTP yhteyksiä
- `closed` tarkoittaa sitä, että portti on saavutettavissa, mutta mikään sovellus ei kuuntele sitä
- `filtered` tarkoittaa sitä, että nmap ei pysty määrittelemään onko portti auki, koska pakettien suodatus estää sitä pääsemästä porttiin
- `unfiltered` tarkoittaa sitä, että portti on saavutettavissa, mutta nmap ei pysty määrittelemään onko portti `open` vai `closed`. Vain ACK skannaus luokittelee portteja tähän
- `open filtered` Nmap laittaa portin tähän tilaan, kun se ei pysty määrittelemään onko portti `open` vai `filtered`. Tämä tapahtuu skannauksissa joissa `open` portti ei anna vastausta
- `closed filtered` Nmap laittaa portin tähän tilaan, kun se ei pysty määrittelemään onko portti `closed` vai `filtered`. Tämä tapahtuu vain `IP ID` idle skannauksissa
 
### [Port Scanning Techniques](https://nmap.org/book/man-port-scanning-techniques.html) (opettele, mitä ovat: -sS -sT -sU; muuten vain silmäily) 
- `-sS` (TCP SYN scan) 
	- suosituin, nopea, huomaamaton ja vaivihkainen
	- ei koskaan suorita TCP yhteyksiä loppuun
	- puoliavoin skannaus, sillä se vastaa SYN/ACK paketteihin resetin (RST)
- `-sT` (TCP connect scan) 
	- muodostaa TCP yhteyden samaan tapaan kuinn esim. nettiselain
	- jättää selkeät jäljet kohteen lokeihin
	- SYN skannaus parempi, jos se on mahdollinen
- `-sU` (UDP scans)
	- hitaampi ja vaikeampi kuin TCP
	- ICMP saavuttamattomuusvirheen palautuessa, portti on suljettu
	- avatut ja suodatetut portit lähettävät harvoin vastauksen

 ## [KKO 2003:36](https://finlex.fi/fi/oikeus/kko/kko/2003/20030036). Alaikäinen tuomittiin Osuuspankkikeskuksen porttiskannaamisesta, korkeimman oikeuden ratkaisu. 

 ## Vapaavalintainen läpikävely [0xdf](https://0xdf.gitlab.io/) tai [ippsec](https://www.youtube.com/channel/UCa6eh7gCkpPo5XXUDfygQQA/videos) (Kannattaa valita helppo; esim "Base Points: Easy")

[https://0xdf.gitlab.io/2023/11/04/htb-topology.html](https://0xdf.gitlab.io/2023/11/04/htb-topology.html)  
- Käytettiin Nmapia avointen porttien (SSH 22, HTTP 80) tunnistamiseen.
- Tutkittiin yliopiston matematiikan verkkosivustoa virtuaalisten isäntien avulla ja löydettiin LaTeX-yhtälön generaattori osoitteessa `latex.topology.htb`.
- Käytettiin feroxbusteria ja ffufia alidomainien ja hakemistojen löytämiseen ja tunnistettiin `dev.topology.htb` ja `stats.topology.htb`.
- Löydettiin HTTP Basic Auth osoitteessa `dev.topology.htb` ja ohitettiin todennus käyttäen `admin:admin`-tunnuksia
- Hyödynnettiin LaTeX-injektiota osoitteessa `latex.topology.htb`
- Purettiin sensitiivitä tietoa ja paljastettiin Apache-konfiguraatiot
- Murrettiin vdaisleyn salasana: `vdaisley:calculus20`
- Saatiin tiivistetyt salasanat `.htpasswd`-tiedostosta
- Lähetettiin PHP-webshell LaTeX-injektion kautta osoitteessa `dev.topology.htb` ja päästiin shelliin vdaisleynä käyttäen murrettuja tunnuksia.
- Hyödynnettiin LaTeX-injektiota .plt-tiedostossa saadakseen pääkäyttäjän oikeudet
- Lisättiin komentoja `.plt`-tiedostoon cron-työn manipulointia varten

# a) Asenna Kali virtuaalikoneeseen
Latasin Kalin asennus ISO:n [Kalin verkkosivuilta](https://www.kali.org/get-kali/#kali-platforms).  
Loin Virtualboxissa uuden Virtuaalikoneen.  
![2024-04-13_14-46](https://github.com/Veliquu/Tunkeutumistestaus_2024/assets/92360351/7cf19f25-eccc-4ccf-b9c0-a9b05aafe047)  
  
Seuraavaksi määrittelin `RAM` muistin ja CPU ydinten määrän.  
![2024-04-13_14-48](https://github.com/Veliquu/Tunkeutumistestaus_2024/assets/92360351/69839879-db9f-4efd-a1e6-6486360f4ac5)
  
Tämän jälkeen määriteltiin levyn koko.  
![2024-04-13_14-49](https://github.com/Veliquu/Tunkeutumistestaus_2024/assets/92360351/f2476408-ecaa-46fd-8ab7-9ddb25d6359d)
  
Viimesienä varmistettiin, että kaikki valitsemat asetukset on oikein.  
![2024-04-13_14-49_1](https://github.com/Veliquu/Tunkeutumistestaus_2024/assets/92360351/54f40c4a-7679-456b-a792-11dc42cc9941)
  

Seuraavaksi käynnistin virtuaalikoneen ja valitsin `Graphical Instalaltion` ja ajettiin se.   
Kali asennettu:  
![2024-04-13_15-21](https://github.com/Veliquu/Tunkeutumistestaus_2024/assets/92360351/e5dd997d-4255-462f-b8a9-b7d6ddfc57e4)


## b) Asenna Metasploitable 2 virtuaalikoneeseen
Latasin Metasplotable2 paketin [Sourceforge: Metasploitable2](https://sourceforge.net/projects/metasploitable/).  
Latauksen jälkeen purin tiedoston valitsemaani kansioon.  
```bash
~/Downloads $ unzip metasploitable-linux-2.0.0.zip
```
Tämän jälkeen käytin [tätä](https://www.geeksforgeeks.org/how-to-install-metasploitable-2-in-virtualbox/) ohjetta asentaakseni Metasploitablen Virtualboxiin.  
Käytännössä asennus ei eronnut Kalin asennuksesta muuten, kuin virtuaali kovalevyn kohdalla valittiin olemassa oleva kovalevy ja haettiin unzipattu Metasploitable.  
Käynnistin Metasploitablen ja kirjauduin sisään default käyttäjätunnuksilla.
```bash
Default login: msfadmin
Default password: msfadmin
```
Metasploitable on toiminnassa.  
![2024-04-13_15-36](https://github.com/Veliquu/Tunkeutumistestaus_2024/assets/92360351/66e1aacd-a0f4-4869-90c7-79ac866d7051)

## c) Tee koneille virtuaaliverkko, jossa
### - Kalin ja Metasploitablen välillä on host-only network, niin että porttiskannatessa ym. koneet on eristetty intenetistä, mutta ne saavat yhteyden toisiinsa
### - Vapaaehtoisena lisänä: Kali saa yhteyden Internettiin, mutta sen voi laittaa pois päältä.
Aikaisemman kurssitoteutuksen [raportin](https://github.com/therealhalonen/penetration_testing/blob/master/h1/report.md) ohjeistuksella loin virtuaalisen `DHCP` serverin host koneelle.  
Terminaali komento, millä `DHCP` serveri luotiin:  
```bash
VBoxManage dhcpserver add --network=pentestNet --server-ip=192.168.66.1 --netmask=255.255.255.0 --lower-ip=192.168.66.2 --upper-ip=192.168.66.254 --enable
```
- `VBoxManage dhcpserver add` lisää serverin
- `--network=pentestNet` määrittää verkon nimen
- `--server-ip=192.168.66.1` määrritää serverin ip osoitteen
- `--netmask=255.255.255.0` määrittää verkkomaskin
- `--lower-ip=192.168.66.2` ja `--upper-ip=192.168.66.254` määrittää välin, jolla on vapaita ip osoitteita
- `--enable` jotta serveri on käynnissä
  
`DHCP` serverin luotua muokkasin Virtualboxin asetuksia virtuaalikoneille.
- Kali
	- Network Adabter 1: NAT = Pääsy Internetiin voidaan yksinkertaisesti estää katkaisemalla liitetty kaapeli  
  ![2024-04-13_16-04](https://github.com/Veliquu/Tunkeutumistestaus_2024/assets/92360351/a6819880-33b9-4c56-8c2a-6810a9f815fb)
  
	- Network Adabter 2: Internal Network  - pentestNet  
	![2024-04-13_16-07_1](https://github.com/Veliquu/Tunkeutumistestaus_2024/assets/92360351/b5d33dfc-247d-4e80-b661-3a0134e0420c)

- Metasploitable
	- Network Adabter 1: Internal Network - pentestNet  
	![2024-04-13_16-07](https://github.com/Veliquu/Tunkeutumistestaus_2024/assets/92360351/486177cc-d0f2-4680-bbd1-0ce9d56bf0b5)


Näillä asetuksilla kumpikin kone on `DHCP` serverissä, mutta vain Kali pääsee internettiin.

### Osoita eri komennoilla, että Internet-yhteys katkeaa: 'ping 1.1.1.1', 'ping www.google.com', 'curl www.google.com'
Metasploitablella kun pingataan `www.google.com` saadaan `unknown hos` viesti.  
![2024-04-13_16-13](https://github.com/Veliquu/Tunkeutumistestaus_2024/assets/92360351/4e2938cc-be84-4e45-a60a-bcb1c768df7d)

Kalilla saadaan ensin pingillä yhteys googleen, mutta kun irroitin `Network Adapter 1` virtualiboxissa niin pingi ei mene enään läpi.  
![2024-04-13_17-14](https://github.com/Veliquu/Tunkeutumistestaus_2024/assets/92360351/f6eef9c4-a5dd-4792-848d-d3fa3538ec18)

## d) Etsi Metasploitable porttiskannaamalla (db_nmap -sn). Tarkista selaimella, että löysit oikean IP:n - Metasploitablen weppipalvelimen etusivulla lukee Metasploitable. Katso, ettei skannauspaketteja vuoda Internetiin - kannattaa irrottaa koneet netistä skannatessa. Seuraa liikennettä snifferillä.
Käytin [tätä](https://gist.github.com/fabionoth/ba46407d9cd03144150225715697c47f) ohjeistusta `db_nmap` käytössä.  
Ensiksi käynnistettiin postgresql -palvelu ja metasploitin msfdb -skripti. Ja tämän jälkeen siirryttiin metasploit kehykseen.
```bash
kali ~# sudo systemctl start postgresql.service
kali ~# sudo msfdb init
kali ~# msfconsole 
```
Ajoin komennon `db_nmap -sn 192.168.66.*`, jossa ip on `DHCP` serverille määritelty ip-osoite avaruus (* meinaa sitä, että komento hakee kaikki ip-osoitteet verkon sisältä).  
![2024-04-13_17-31](https://github.com/Veliquu/Tunkeutumistestaus_2024/assets/92360351/edf0b281-b70c-4833-95a4-f3fb31a5221d)

Ylhäällä oli kaksi hostia `192.168.66.2` ja `192.168.66.4`.  
`ifconfig` komennolla sain selville mikä Kali koneen ip osoite on.  
![2024-04-13_17-32](https://github.com/Veliquu/Tunkeutumistestaus_2024/assets/92360351/ce8782f2-9201-44fb-8eae-a3dad92fc9ca)  

Kuvassa nähdään, että Kalilla on verkkoportissa `eth1` ip-osoitteena `192.168.66.4`. Täten oletin `192.168.66.2` olevan Metasploitaplen ip-osoite ja laitoin sen verkkoselaimeen.  
![2024-04-13_17-39](https://github.com/Veliquu/Tunkeutumistestaus_2024/assets/92360351/c8278403-291f-456e-ba65-0026cac03352)

Wiresharkilla huomasimme, että db_nmap lähettää ARP kyselyn jokaiseen `dhcp` serverin ip-osoitteeseen ja jonka `192.168.66.2` kuittaa.  
![2024-04-13_17-42](https://github.com/Veliquu/Tunkeutumistestaus_2024/assets/92360351/0d256bb9-39ee-4ff5-9b03-8b7129ea8220)


