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
 - A yritti murtaa Osuuspankkikeskus-OPK osuuskunnan tietojärjestelmään 23.11.1998.
 - Porttiskannauksessa A käytti erityistä tietokoneohjelmaa skannatakseen verkon kaikki osoitteet.
 - Skannaus ei läpäissyt osuuskunnan tietojärjestelmän palomuuria.
 - Käräjäoikeus hylkäsi syytteen ja korvausvaatimukset, koska ei ollut selvää, kuka oli ottanut yhteyden tietojärjestelmään.
 - Hovioikeus kuitenkin katsoi, että A oli yrittänyt tietomurtoa ja määräsi hänet maksamaan vahingonkorvauksia.
 - Korkein oikeus vahvisti hovioikeuden päätöksen, todeten että A oli yrittänyt tunkeutua tietojärjestelmään ja velvoitti hänet korvaamaan aiheuttamansa vahingon kokonaisuudessaan.
 - A:n tekemä porttiskannaus täytti tietomurron yrityksen tunnusmerkistön.
 - Vaikka A ei tiennyt skannanneensa osuuskunnan verkon, hän on syyllistynyt tietomurron yritykseen.
 - A:lle ei sovitella vahingonkorvauksia, koska hän ymmärsi teon vakavuuden ja sen aiheuttaman vahingonvaaran.
 - Korkein oikeus vahvisti hovioikeuden päätöksen, eikä muuttanut tuomiota.


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
- `--server-ip=192.168.66.1` määrritää serverin ip-osoitteen
- `--netmask=255.255.255.0` määrittää verkkomaskin
- `--lower-ip=192.168.66.2` ja `--upper-ip=192.168.66.254` määrittää välin, jolla on vapaita ip-osoitteita
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
`ifconfig` komennolla sain selville mikä Kali koneen ip-osoite on.  
![2024-04-13_17-32](https://github.com/Veliquu/Tunkeutumistestaus_2024/assets/92360351/ce8782f2-9201-44fb-8eae-a3dad92fc9ca)  

Kuvassa nähdään, että Kalilla on verkkoportissa `eth1` ip-osoitteena `192.168.66.4`. Täten oletin `192.168.66.2` olevan Metasploitaplen ip-osoite ja laitoin sen verkkoselaimeen.  
![2024-04-13_17-39](https://github.com/Veliquu/Tunkeutumistestaus_2024/assets/92360351/c8278403-291f-456e-ba65-0026cac03352)

Wiresharkilla huomasimme, että db_nmap lähettää ARP kyselyn jokaiseen `dhcp` serverin ip-osoitteeseen ja jonka `192.168.66.2` kuittaa.  
![2024-04-13_17-42](https://github.com/Veliquu/Tunkeutumistestaus_2024/assets/92360351/0d256bb9-39ee-4ff5-9b03-8b7129ea8220)

En löytänyt vastausta, mikä 192.168.66.1 dhcp serverin yhteys ICMP protokollalla Kali linuxiin on ja miksi vastauksena on `Destination unreachable`  


## e) Porttiskannaa Metasploitable huolellisesti (db_nmap -A -p0-). Analysoi tulos. Kerro myös ammatillinen mielipiteesi (uusi, vanha, tavallinen, erikoinen), jos jokin herättää ajatuksia. Seuraa liikennettä snifferillä.

Ajoin komennon `db_nmap -A -p0- 192.168.66.2` skannatakseni Metasploitablen.  

<details>
<summary>Output</summary>
<pre>
msf6 > db_nmap -A -p0- 192.168.66.2
[*] Nmap: Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-04-13 23:08 EEST
[*] Nmap: 'mass_dns: warning: Unable to determine any DNS servers. Reverse DNS is disabled. Try using --system-dns or specify valid servers with --dns-servers'
[*] Nmap: Nmap scan report for 192.168.66.2
[*] Nmap: Host is up (0.00013s latency).
[*] Nmap: Not shown: 65506 closed tcp ports (conn-refused)
[*] Nmap: PORT      STATE SERVICE     VERSION
[*] Nmap: 21/tcp    open  ftp         vsftpd 2.3.4
[*] Nmap: | ftp-syst:
[*] Nmap: |   STAT:
[*] Nmap: | FTP server status:
[*] Nmap: |      Connected to 192.168.66.4
[*] Nmap: |      Logged in as ftp
[*] Nmap: |      TYPE: ASCII
[*] Nmap: |      No session bandwidth limit
[*] Nmap: |      Session timeout in seconds is 300
[*] Nmap: |      Control connection is plain text
[*] Nmap: |      Data connections will be plain text
[*] Nmap: |      vsFTPd 2.3.4 - secure, fast, stable
[*] Nmap: |_End of status
[*] Nmap: |_ftp-anon: Anonymous FTP login allowed (FTP code 230)
[*] Nmap: 22/tcp    open  ssh         OpenSSH 4.7p1 Debian 8ubuntu1 (protocol 2.0)
[*] Nmap: | ssh-hostkey:
[*] Nmap: |   1024 60:0f:cf:e1:c0:5f:6a:74:d6:90:24:fa:c4:d5:6c:cd (DSA)
[*] Nmap: |_  2048 56:56:24:0f:21:1d:de:a7:2b:ae:61:b1:24:3d:e8:f3 (RSA)
[*] Nmap: 23/tcp    open  telnet      Linux telnetd
[*] Nmap: 25/tcp    open  smtp        Postfix smtpd
[*] Nmap: | ssl-cert: Subject: commonName=ubuntu804-base.localdomain/organizationName=OCOSA/stateOrProvinceName=There is no such thing outside US/countryName=XX
[*] Nmap: | Not valid before: 2010-03-17T14:07:45
[*] Nmap: |_Not valid after:  2010-04-16T14:07:45
[*] Nmap: |_smtp-commands: metasploitable.localdomain, PIPELINING, SIZE 10240000, VRFY, ETRN, STARTTLS, ENHANCEDSTATUSCODES, 8BITMIME, DSN
[*] Nmap: |_ssl-date: 2024-04-13T15:11:14+00:00; -4h59m44s from scanner time.
[*] Nmap: | sslv2:
[*] Nmap: |   SSLv2 supported
[*] Nmap: |   ciphers:
[*] Nmap: |     SSL2_RC2_128_CBC_EXPORT40_WITH_MD5
[*] Nmap: |     SSL2_RC4_128_WITH_MD5
[*] Nmap: |     SSL2_RC2_128_CBC_WITH_MD5
[*] Nmap: |     SSL2_DES_64_CBC_WITH_MD5
[*] Nmap: |     SSL2_RC4_128_EXPORT40_WITH_MD5
[*] Nmap: |_    SSL2_DES_192_EDE3_CBC_WITH_MD5
[*] Nmap: 53/tcp    open  domain      ISC BIND 9.4.2
[*] Nmap: | dns-nsid:
[*] Nmap: |_  bind.version: 9.4.2
[*] Nmap: 80/tcp    open  http        Apache httpd 2.2.8 ((Ubuntu) DAV/2)
[*] Nmap: |_http-server-header: Apache/2.2.8 (Ubuntu) DAV/2
[*] Nmap: |_http-title: Metasploitable2 - Linux
[*] Nmap: 111/tcp   open  rpcbind     2 (RPC #100000)
[*] Nmap: | rpcinfo:
[*] Nmap: |   program version    port/proto  service
[*] Nmap: |   100000  2            111/tcp   rpcbind
[*] Nmap: |   100000  2            111/udp   rpcbind
[*] Nmap: |   100003  2,3,4       2049/tcp   nfs
[*] Nmap: |   100003  2,3,4       2049/udp   nfs
[*] Nmap: |   100005  1,2,3      59346/udp   mountd
[*] Nmap: |   100005  1,2,3      59467/tcp   mountd
[*] Nmap: |   100021  1,3,4      40213/tcp   nlockmgr
[*] Nmap: |   100021  1,3,4      52465/udp   nlockmgr
[*] Nmap: |   100024  1          40473/tcp   status
[*] Nmap: |_  100024  1          59964/udp   status
[*] Nmap: 139/tcp   open  netbios-ssn Samba smbd 3.X - 4.X (workgroup: WORKGROUP)
[*] Nmap: 445/tcp   open  netbios-ssn Samba smbd 3.0.20-Debian (workgroup: WORKGROUP)
[*] Nmap: 512/tcp   open  exec        netkit-rsh rexecd
[*] Nmap: 513/tcp   open  login       OpenBSD or Solaris rlogind
[*] Nmap: 514/tcp   open  shell       Netkit rshd
[*] Nmap: 1099/tcp  open  java-rmi    GNU Classpath grmiregistry
[*] Nmap: 1524/tcp  open  bindshell   Metasploitable root shell
[*] Nmap: 2049/tcp  open  nfs         2-4 (RPC #100003)
[*] Nmap: 2121/tcp  open  ftp         ProFTPD 1.3.1
[*] Nmap: 3306/tcp  open  mysql       MySQL 5.0.51a-3ubuntu5
[*] Nmap: | mysql-info:
[*] Nmap: |   Protocol: 10
[*] Nmap: |   Version: 5.0.51a-3ubuntu5
[*] Nmap: |   Thread ID: 11
[*] Nmap: |   Capabilities flags: 43564
[*] Nmap: |   Some Capabilities: SwitchToSSLAfterHandshake, LongColumnFlag, Support41Auth, SupportsTransactions, Speaks41ProtocolNew, SupportsCompression, ConnectWithDatabase
[*] Nmap: |   Status: Autocommit
[*] Nmap: |_  Salt: O~OO~MEOA835Psq]];O\
[*] Nmap: 3632/tcp  open  distccd     distccd v1 ((GNU) 4.2.4 (Ubuntu 4.2.4-1ubuntu4))
[*] Nmap: 5432/tcp  open  postgresql  PostgreSQL DB 8.3.0 - 8.3.7
[*] Nmap: |_ssl-date: 2024-04-13T15:11:14+00:00; -4h59m45s from scanner time.
[*] Nmap: | ssl-cert: Subject: commonName=ubuntu804-base.localdomain/organizationName=OCOSA/stateOrProvinceName=There is no such thing outside US/countryName=XX
[*] Nmap: | Not valid before: 2010-03-17T14:07:45
[*] Nmap: |_Not valid after:  2010-04-16T14:07:45
[*] Nmap: 5900/tcp  open  vnc         VNC (protocol 3.3)
[*] Nmap: | vnc-info:
[*] Nmap: |   Protocol version: 3.3
[*] Nmap: |   Security types:
[*] Nmap: |_    VNC Authentication (2)
[*] Nmap: 6000/tcp  open  X11         (access denied)
[*] Nmap: 6667/tcp  open  irc         UnrealIRCd
[*] Nmap: 6697/tcp  open  irc         UnrealIRCd (Admin email admin@Metasploitable.LAN)
[*] Nmap: 8009/tcp  open  ajp13       Apache Jserv (Protocol v1.3)
[*] Nmap: |_ajp-methods: Failed to get a valid response for the OPTION request
[*] Nmap: 8180/tcp  open  http        Apache Tomcat/Coyote JSP engine 1.1
[*] Nmap: |_http-title: Apache Tomcat/5.5
[*] Nmap: |_http-server-header: Apache-Coyote/1.1
[*] Nmap: |_http-favicon: Apache Tomcat
[*] Nmap: 8787/tcp  open  drb         Ruby DRb RMI (Ruby 1.8; path /usr/lib/ruby/1.8/drb)
[*] Nmap: 35696/tcp open  java-rmi    GNU Classpath grmiregistry
[*] Nmap: 40213/tcp open  nlockmgr    1-4 (RPC #100021)
[*] Nmap: 40473/tcp open  status      1 (RPC #100024)
[*] Nmap: 59467/tcp open  mountd      1-3 (RPC #100005)
[*] Nmap: Service Info: Hosts:  metasploitable.localdomain, irc.Metasploitable.LAN; OSs: Unix, Linux; CPE: cpe:/o:linux:linux_kernel
[*] Nmap: Host script results:
[*] Nmap: |_smb2-time: Protocol negotiation failed (SMB2)
[*] Nmap: | smb-security-mode:
[*] Nmap: |   account_used: <blank>
[*] Nmap: |   authentication_level: user
[*] Nmap: |   challenge_response: supported
[*] Nmap: |_  message_signing: disabled (dangerous, but default)
[*] Nmap: |_nbstat: NetBIOS name: METASPLOITABLE, NetBIOS user: <unknown>, NetBIOS MAC: <unknown> (unknown)
[*] Nmap: | smb-os-discovery:
[*] Nmap: |   OS: Unix (Samba 3.0.20-Debian)
[*] Nmap: |   Computer name: metasploitable
[*] Nmap: |   NetBIOS computer name:
[*] Nmap: |   Domain name: localdomain
[*] Nmap: |   FQDN: metasploitable.localdomain
[*] Nmap: |_  System time: 2024-04-13T11:11:04-04:00
[*] Nmap: |_clock-skew: mean: -3h59m44s, deviation: 1h59m59s, median: -4h59m45s
[*] Nmap: Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
[*] Nmap: Nmap done: 1 IP address (1 host up) scanned in 138.10 seconds

</pre>
</details>

Useita portteja on auki, sekä Apache, mysql ja vsftpd versiot vaikuttavat olevan vanhoja.  
Ftp-palvelimelle näyttäisi pystyvän kirjautumaan anonyymisti. 
```bash
[*] Nmap: |_ftp-anon: Anonymous FTP login allowed (FTP code 230)
```
Yleisesti vaikuttaisi siltä, että monet palvelut ovat vanhoja versioita mikä tekee niistä haavoittuvaisia. 

## f) Tallenna portiskannauksen tulos tiedostoon käyttäen nmap:n omaa tallennusta (nmap -oA foo).
Tallensim `nmap`in tuloksen nmapin työkalulla, käyttäen komentoa:
```bash
msf6 > nmap -oA /home/nmaptulokset 192.168.66.2
```
![2024-04-13_23-21](https://github.com/Veliquu/Tunkeutumistestaus_2024/assets/92360351/a1d3e251-a56c-495d-9d22-9eb85558ae84)

Tämän jälkeen tarkistin, että luotu tiedosto löytyy.
![2024-04-13_23-22](https://github.com/Veliquu/Tunkeutumistestaus_2024/assets/92360351/77f4c107-dcbd-43fd-b6ca-2b86ed144760)

Täällä näemme, että tiedosto on luotu.
  
## g) Tallenna shell-sessio tekstitiedostoon script-työkalulla (script -fa log001.txt)

Ajoin tehtävänannon ohjeen mukaan `script -fa log001.txt`  
![2024-04-13_23-27](https://github.com/Veliquu/Tunkeutumistestaus_2024/assets/92360351/9e7a23b5-cc03-4b6f-be46-b346fd8d55af)

Tämän jälkeen tarkistin, että tiedosto on tallennettu.  
![2024-04-13_23-29](https://github.com/Veliquu/Tunkeutumistestaus_2024/assets/92360351/1eb0037e-4b99-4b1a-9f7c-2679baf3bdfc)

Täällä näemme, että `log001.txt` tiedosto on luotu.

## 
h) Etsi kaikki maininnat jostain osoitteesta, palvelusta tai vastaavasta kaikista tallennetuista tuloksista ja lokeista (grep -ir tero).

Etsinn kaikki maininnat Apachesta komennollq;
```bash
$ grep -ir apache
```
Grepin jälkeen on `-ir`.
- `-i` meinaa sitä, että grep ohittaa kirjainkoostumukset kuvioissa ja syöttö tiedoissa, jotta vain kirjaimet, jotka eroavat vain kirjainkoon mukaan, vastaavat toisiaan
- `-r` (recursive) tekee sen, että grep lukee kaikki tiedostot jokaisesta hakemistosta rekursiivisesti.

<details>
<summary>Output</summary>
<pre>
─$ grep -ir apache
.msf4/store/modules_metadata.json:    "description": "This module plays a video on an AppleTV device. Note that\n        AppleTV can be somewhat picky about the server that hosts the video.\n        Tested servers include default IIS, default Apache, and Ruby's WEBrick.\n        For WEBrick, the default MIME list may need to be updated, depending on\n        what media file is to be played. Python SimpleHTTPServer is not\n        recommended. Also, if you're playing a video, the URL must be an IP\n        address. Some AppleTV devices are actually password-protected; in that\n        case please set the PASSWORD datastore option. For password\n        brute forcing, please see the module auxiliary/scanner/http/appletv_login.",
.msf4/store/modules_metadata.json:      "URL-http://tomcat.apache.org/"
.msf4/store/modules_metadata.json:    "name": "Apache Tomcat AJP File Read",
.msf4/store/modules_metadata.json:    "description": "When using the Apache JServ Protocol (AJP), care must be taken when trusting incoming connections to Apache\n          Tomcat. Tomcat treats AJP connections as having higher trust than, for example, a similar HTTP connection.\n          If such connections are available to an attacker, they can be exploited in ways that may be surprising.\n\n          In Apache Tomcat 9.0.0.M1 to 9.0.0.30, 8.5.0 to 8.5.50 and 7.0.0 to 7.0.99, Tomcat shipped with an AJP\n          Connector enabled by default that listened on all configured IP addresses. It was expected (and recommended\n          in the security guide) that this Connector would be disabled if not required. This vulnerability report\n          identified a mechanism that allowed: - returning arbitrary files from anywhere in the web application -\n          processing any file in the web application as a JSP. Further, if the web application allowed file upload\n          and stored those files within the web application (or the attacker was able to control the content of the\n          web application by some other means) then this, along with the ability to process a file as a JSP, made\n          remote code execution possible.\n\n          It is important to note that mitigation is only required if an AJP port is accessible to untrusted users.\n          Users wishing to take a defence-in-depth approach and block the vector that permits returning arbitrary files\n          and execution as JSP may upgrade to Apache Tomcat 9.0.31, 8.5.51 or 7.0.100 or later. A number of changes were\n          made to the default AJP Connector configuration in 9.0.31 to harden the default configuration.\n          It is likely that users upgrading to 9.0.31, 8.5.51 or 7.0.100 or later will need to make small changes\n          to their configurations.",
.msf4/store/modules_metadata.json:    "description": "This module tests whether a directory traversal vulnerability is present\n        in versions of Apache Tomcat 4.1.0 - 4.1.37, 5.5.0 - 5.5.26 and 6.0.0\n        - 6.0.16 under specific and non-default installations. The connector must have\n        allowLinking set to true and URIEncoding set to UTF-8. Furthermore, the\n        vulnerability actually occurs within Java and not Tomcat; the server must\n        use Java versions prior to Sun 1.4.2_19, 1.5.0_17, 6u11 - or prior IBM Java\n        5.0 SR9, 1.4.2 SR13, SE 6 SR4 releases. This module has only been tested against\n        RedHat 9 running Tomcat 6.0.16 and Sun JRE 1.5.0-05. You may wish to change\n        FILE (hosts,sensitive files), MAXDIRS and RPORT depending on your environment.",
.msf4/store/modules_metadata.json:      "URL-http://tomcat.apache.org/",
.msf4/store/modules_metadata.json:      "URL-http://tomcat.apache.org/",
.msf4/store/modules_metadata.json:    "description": "This module uses John the Ripper or Hashcat to identify weak passwords that have been\n        acquired from various web applications.\n        Atlassian uses PBKDF2-HMAC-SHA1 which is 12001 in hashcat.\n        PHPass uses phpass which is 400 in hashcat.\n        Mediawiki is MD5 based and is 3711 in hashcat.\n        Apache Superset, some Flask and Werkzeug apps is pbkdf2-sha256 and is 10900 in hashcat",
.msf4/store/modules_metadata.json:  "auxiliary_dos/http/apache_commons_fileupload_dos": {
.msf4/store/modules_metadata.json:    "name": "Apache Commons FileUpload and Apache Tomcat DoS",
.msf4/store/modules_metadata.json:    "fullname": "auxiliary/dos/http/apache_commons_fileupload_dos",
.msf4/store/modules_metadata.json:    "description": "This module triggers an infinite loop in Apache Commons FileUpload 1.0\n        through 1.3 via a specially crafted Content-Type header.\n        Apache Tomcat 7 and Apache Tomcat 8 use a copy of FileUpload to handle\n        mime-multipart requests, therefore, Apache Tomcat 7.0.0 through 7.0.50\n        and 8.0.0-RC1 through 8.0.1 are affected by this issue. Tomcat 6 also\n        uses Commons FileUpload as part of the Manager application.",
.msf4/store/modules_metadata.json:      "URL-https://tomcat.apache.org/security-8.html",
.msf4/store/modules_metadata.json:      "URL-https://tomcat.apache.org/security-7.html"
.msf4/store/modules_metadata.json:    "path": "/modules/auxiliary/dos/http/apache_commons_fileupload_dos.rb",
.msf4/store/modules_metadata.json:    "ref_name": "dos/http/apache_commons_fileupload_dos",
.msf4/store/modules_metadata.json:  "auxiliary_dos/http/apache_mod_isapi": {
.msf4/store/modules_metadata.json:    "name": "Apache mod_isapi Dangling Pointer",
.msf4/store/modules_metadata.json:    "fullname": "auxiliary/dos/http/apache_mod_isapi",
.msf4/store/modules_metadata.json:    "description": "This module triggers a use-after-free vulnerability in the Apache\n        Software Foundation mod_isapi extension for versions 2.2.14 and earlier.\n        In order to reach the vulnerable code, the target server must have an\n        ISAPI module installed and configured.\n\n        By making a request that terminates abnormally (either an aborted TCP\n        connection or an unsatisfied chunked request), mod_isapi will unload the\n        ISAPI extension. Later, if another request comes for that ISAPI module,\n        previously obtained pointers will be used resulting in an access\n        violation or potentially arbitrary code execution.\n\n        Although arbitrary code execution is theoretically possible, a\n        real-world method of invoking this consequence has not been proven. In\n        order to do so, one would need to find a situation where a particular\n        ISAPI module loads at an image base address that can be re-allocated by\n        a remote attacker.\n\n        Limited success was encountered using two separate ISAPI modules. In\n        this scenario, a second ISAPI module was loaded into the same memory\n        area as the previously unloaded module.",
.msf4/store/modules_metadata.json:      "URL-https://bz.apache.org/bugzilla/show_bug.cgi?id=48509",
.msf4/store/modules_metadata.json:      "URL-https://web.archive.org/web/20100715032229/http://www.gossamer-threads.com/lists/apache/cvs/381537",
.msf4/store/modules_metadata.json:    "path": "/modules/auxiliary/dos/http/apache_mod_isapi.rb",
.msf4/store/modules_metadata.json:    "ref_name": "dos/http/apache_mod_isapi",
.msf4/store/modules_metadata.json:  "auxiliary_dos/http/apache_range_dos": {
.msf4/store/modules_metadata.json:    "name": "Apache Range Header DoS (Apache Killer)",
.msf4/store/modules_metadata.json:    "fullname": "auxiliary/dos/http/apache_range_dos",
.msf4/store/modules_metadata.json:    "description": "The byterange filter in the Apache HTTP Server 2.0.x through 2.0.64, and 2.2.x\n        through 2.2.19 allows remote attackers to cause a denial of service (memory and\n        CPU consumption) via a Range header that expresses multiple overlapping ranges,\n        exploit called \"Apache Killer\"",
.msf4/store/modules_metadata.json:    "path": "/modules/auxiliary/dos/http/apache_range_dos.rb",
.msf4/store/modules_metadata.json:    "ref_name": "dos/http/apache_range_dos",
.msf4/store/modules_metadata.json:  "auxiliary_dos/http/apache_tomcat_transfer_encoding": {
.msf4/store/modules_metadata.json:    "name": "Apache Tomcat Transfer-Encoding Information Disclosure and DoS",
.msf4/store/modules_metadata.json:    "fullname": "auxiliary/dos/http/apache_tomcat_transfer_encoding",
.msf4/store/modules_metadata.json:    "description": "Apache Tomcat 5.5.0 through 5.5.29, 6.0.0 through 6.0.27, and 7.0.0 beta does not\n        properly handle an invalid Transfer-Encoding header, which allows remote attackers\n        to cause a denial of service (application outage) or obtain sensitive information\n        via a crafted header that interferes with \"recycling of a buffer.\"",
.msf4/store/modules_metadata.json:    "path": "/modules/auxiliary/dos/http/apache_tomcat_transfer_encoding.rb",
.msf4/store/modules_metadata.json:    "ref_name": "dos/http/apache_tomcat_transfer_encoding",
.msf4/store/modules_metadata.json:    "name": "LibreOffice 6.03 /Apache OpenOffice 4.1.5 Malicious ODT File Generator",
.msf4/store/modules_metadata.json:  "auxiliary_gather/apache_rave_creds": {
.msf4/store/modules_metadata.json:    "name": "Apache Rave User Information Disclosure",
.msf4/store/modules_metadata.json:    "fullname": "auxiliary/gather/apache_rave_creds",
.msf4/store/modules_metadata.json:    "description": "This module exploits an information disclosure in Apache Rave 0.20 and prior. The\n        vulnerability exists in the RPC API, which allows any authenticated user to\n        disclose information about all the users, including their password hashes. In order\n        to authenticate, the user can provide his own credentials. Also the default users\n        installed with Apache Rave 0.20 will be tried automatically. This module has been\n        successfully tested on Apache Rave 0.20.",
.msf4/store/modules_metadata.json:    "path": "/modules/auxiliary/gather/apache_rave_creds.rb",
.msf4/store/modules_metadata.json:    "ref_name": "gather/apache_rave_creds",
.msf4/store/modules_metadata.json:  "auxiliary_gather/apache_superset_cookie_sig_priv_esc": {
.msf4/store/modules_metadata.json:    "name": "Apache Superset Signed Cookie Priv Esc",
.msf4/store/modules_metadata.json:    "fullname": "auxiliary/gather/apache_superset_cookie_sig_priv_esc",
.msf4/store/modules_metadata.json:    "description": "Apache Superset versions <= 2.0.0 utilize Flask with a known default secret key which is used to sign HTTP cookies.\n          These cookies can therefore be forged. If a user is able to login to the site, they can decode the cookie, set their user_id to that\n          of an administrator, and re-sign the cookie. This valid cookie can then be used to login as the targeted user and retrieve database\n          credentials saved in Apache Superset.",
.msf4/store/modules_metadata.json:      "URL-https://vulcan.io/blog/cve-2023-27524-in-apache-superset-what-you-need-to-know/",
.msf4/store/modules_metadata.json:      "URL-https://www.horizon3.ai/cve-2023-27524-insecure-default-configuration-in-apache-superset-leads-to-remote-code-execution/",
.msf4/store/modules_metadata.json:    "path": "/modules/auxiliary/gather/apache_superset_cookie_sig_priv_esc.rb",
.msf4/store/modules_metadata.json:    "ref_name": "gather/apache_superset_cookie_sig_priv_esc",
.msf4/store/modules_metadata.json:        "exploit/linux/http/apache_superset_cookie_sig_rce"
.msf4/store/modules_metadata.json:  "auxiliary_gather/cve_2021_27850_apache_tapestry_hmac_key": {
.msf4/store/modules_metadata.json:    "name": "Apache Tapestry HMAC secret key leak",
.msf4/store/modules_metadata.json:    "fullname": "auxiliary/gather/cve_2021_27850_apache_tapestry_hmac_key",
.msf4/store/modules_metadata.json:    "description": "This exploit finds the HMAC secret key used in Java serialization by Apache Tapestry. This key\n          is located in the file AppModule.class by default and looks like the standard representation of UUID in hex digits (hd) :\n          6hd-4hd-4hd-4hd-12hd\n          If the HMAC key has been changed to look differently, this module won't find the key because it tries to download the file\n          and then uses a specific regex to find the key.",
.msf4/store/modules_metadata.json:    "path": "/modules/auxiliary/gather/cve_2021_27850_apache_tapestry_hmac_key.rb",
.msf4/store/modules_metadata.json:    "ref_name": "gather/cve_2021_27850_apache_tapestry_hmac_key",
.msf4/store/modules_metadata.json:    "description": "This module request a copy of the remote SSL certificate and creates a local\n          (self.signed) version using the information from the remote version. The module\n          then Outputs (PEM|DER) format private key / certificate and a combined version\n          for use in Apache or other Metasploit modules requiring SSLCert Inputs for private\n          key / CA cert have been provided for those with DigiNotar certs hanging about!",
.msf4/store/modules_metadata.json:    "name": "Apache ZooKeeper Information Disclosure",
.msf4/store/modules_metadata.json:    "description": "Apache ZooKeeper server service runs on TCP 2181 and by default, it is accessible without any authentication. This module targets Apache ZooKeeper service instances to extract information about the system environment, and service statistics.",
.msf4/store/modules_metadata.json:      "URL-https://zooKeeper.apache.org/doc/current/zookeeperAdmin.html"
.msf4/store/modules_metadata.json:      "URL-https://wiki.apache.org/couchdb/HTTP_database_API"
.msf4/store/modules_metadata.json:  "auxiliary_scanner/http/apache_activemq_source_disclosure": {
.msf4/store/modules_metadata.json:    "name": "Apache ActiveMQ JSP Files Source Disclosure",
.msf4/store/modules_metadata.json:    "fullname": "auxiliary/scanner/http/apache_activemq_source_disclosure",
.msf4/store/modules_metadata.json:    "description": "This module exploits a source code disclosure in Apache ActiveMQ. The\n        vulnerability is due to the Jetty's ResourceHandler handling of specially crafted\n        URI's starting with //. It has been tested successfully on Apache ActiveMQ 5.3.1\n        over Windows 2003 SP2 and Ubuntu 10.04.",
.msf4/store/modules_metadata.json:      "URL-https://issues.apache.org/jira/browse/AMQ-2700"
.msf4/store/modules_metadata.json:    "path": "/modules/auxiliary/scanner/http/apache_activemq_source_disclosure.rb",
.msf4/store/modules_metadata.json:    "ref_name": "scanner/http/apache_activemq_source_disclosure",
.msf4/store/modules_metadata.json:  "auxiliary_scanner/http/apache_activemq_traversal": {
.msf4/store/modules_metadata.json:    "name": "Apache ActiveMQ Directory Traversal",
.msf4/store/modules_metadata.json:    "fullname": "auxiliary/scanner/http/apache_activemq_traversal",
.msf4/store/modules_metadata.json:    "description": "This module exploits a directory traversal vulnerability in Apache ActiveMQ\n        5.3.1 and 5.3.2 on Windows systems. The vulnerability exists in the Jetty's\n        ResourceHandler installed with the affected versions. This module has been tested\n        successfully on ActiveMQ 5.3.1 and 5.3.2 over Windows 2003 SP2.",
.msf4/store/modules_metadata.json:      "URL-https://issues.apache.org/jira/browse/amq-2788"
.msf4/store/modules_metadata.json:    "path": "/modules/auxiliary/scanner/http/apache_activemq_traversal.rb",
.msf4/store/modules_metadata.json:    "ref_name": "scanner/http/apache_activemq_traversal",
.msf4/store/modules_metadata.json:  "auxiliary_scanner/http/apache_flink_jobmanager_traversal": {
.msf4/store/modules_metadata.json:    "name": "Apache Flink JobManager Traversal",
.msf4/store/modules_metadata.json:    "fullname": "auxiliary/scanner/http/apache_flink_jobmanager_traversal",
.msf4/store/modules_metadata.json:    "description": "This module exploits an unauthenticated directory traversal vulnerability\n          in Apache Flink versions 1.11.0 <= 1.11.2. The JobManager REST API fails\n          to validate user-supplied log file paths, allowing retrieval of arbitrary\n          files with the privileges of the web server user.\n\n          This module has been tested successfully on Apache Flink version 1.11.2\n          on Ubuntu 18.04.4.",
.msf4/store/modules_metadata.json:    "path": "/modules/auxiliary/scanner/http/apache_flink_jobmanager_traversal.rb",
.msf4/store/modules_metadata.json:    "ref_name": "scanner/http/apache_flink_jobmanager_traversal",
.msf4/store/modules_metadata.json:  "auxiliary_scanner/http/apache_mod_cgi_bash_env": {
.msf4/store/modules_metadata.json:    "name": "Apache mod_cgi Bash Environment Variable Injection (Shellshock) Scanner",
.msf4/store/modules_metadata.json:    "fullname": "auxiliary/scanner/http/apache_mod_cgi_bash_env",
.msf4/store/modules_metadata.json:    "description": "This module scans for the Shellshock vulnerability, a flaw in how the Bash shell\n        handles external environment variables. This module targets CGI scripts in the\n        Apache web server by setting the HTTP_USER_AGENT environment variable to a\n        malicious function definition.\n\n        PROTIP: Use exploit/multi/handler with a PAYLOAD appropriate to your\n        CMD, set ExitOnSession false, run -j, and then run this module to create\n        sessions on vulnerable hosts.\n\n        Note that this is not the recommended method for obtaining shells.\n        If you require sessions, please use the apache_mod_cgi_bash_env_exec\n        exploit module instead.",
.msf4/store/modules_metadata.json:    "path": "/modules/auxiliary/scanner/http/apache_mod_cgi_bash_env.rb",
.msf4/store/modules_metadata.json:    "ref_name": "scanner/http/apache_mod_cgi_bash_env",
.msf4/store/modules_metadata.json:  "auxiliary_scanner/http/apache_nifi_login": {
.msf4/store/modules_metadata.json:    "name": "Apache NiFi Login Scanner",
.msf4/store/modules_metadata.json:    "fullname": "auxiliary/scanner/http/apache_nifi_login",
.msf4/store/modules_metadata.json:    "description": "This module attempts to take login details for Apache NiFi websites\n          and identify if they are valid or not.\n\n          Tested against NiFi major releases 1.14.0 - 1.21.0, and 1.13.0\n          Also works against NiFi <= 1.13.0, but the module needs to be adjusted:\n          set SSL false\n          set rport 8080",
.msf4/store/modules_metadata.json:    "path": "/modules/auxiliary/scanner/http/apache_nifi_login.rb",
.msf4/store/modules_metadata.json:    "ref_name": "scanner/http/apache_nifi_login",
.msf4/store/modules_metadata.json:  "auxiliary_scanner/http/apache_nifi_version": {
.msf4/store/modules_metadata.json:    "name": "Apache NiFi Version Scanner",
.msf4/store/modules_metadata.json:    "fullname": "auxiliary/scanner/http/apache_nifi_version",
.msf4/store/modules_metadata.json:    "description": "This module identifies Apache NiFi websites and reports their version number.\n\n          Tested against NiFi major releases 1.14.0 - 1.21.0, and 1.11.0-1.13.0\n          Also works against NiFi <= 1.13.0, but the module needs to be adjusted:\n          set SSL false\n          set rport 8080",
.msf4/store/modules_metadata.json:    "path": "/modules/auxiliary/scanner/http/apache_nifi_version.rb",
.msf4/store/modules_metadata.json:    "ref_name": "scanner/http/apache_nifi_version",
.msf4/store/modules_metadata.json:  "auxiliary_scanner/http/apache_normalize_path": {
.msf4/store/modules_metadata.json:    "name": "Apache 2.4.49/2.4.50 Traversal RCE scanner",
.msf4/store/modules_metadata.json:    "fullname": "auxiliary/scanner/http/apache_normalize_path",
.msf4/store/modules_metadata.json:    "description": "This module scans for an unauthenticated RCE vulnerability which exists in Apache version 2.4.49 (CVE-2021-41773).\n          If files outside of the document root are not protected by ‘require all denied’ and CGI has been explicitly enabled,\n          it can be used to execute arbitrary commands (Remote Command Execution).\n          This vulnerability has been reintroduced in Apache 2.4.50 fix (CVE-2021-42013).",
.msf4/store/modules_metadata.json:      "URL-https://httpd.apache.org/security/vulnerabilities_24.html",
.msf4/store/modules_metadata.json:      "URL-https://github.com/projectdiscovery/nuclei-templates/blob/master/vulnerabilities/apache/apache-httpd-rce.yaml",
.msf4/store/modules_metadata.json:    "path": "/modules/auxiliary/scanner/http/apache_normalize_path.rb",
.msf4/store/modules_metadata.json:    "ref_name": "scanner/http/apache_normalize_path",
.msf4/store/modules_metadata.json:  "auxiliary_scanner/http/apache_optionsbleed": {
.msf4/store/modules_metadata.json:    "name": "Apache Optionsbleed Scanner",
.msf4/store/modules_metadata.json:    "fullname": "auxiliary/scanner/http/apache_optionsbleed",
.msf4/store/modules_metadata.json:    "description": "This module scans for the Apache optionsbleed vulnerability where the Allow\n        response header returned from an OPTIONS request may bleed memory if the\n        server has a .htaccess file with an invalid Limit method defined.",
.msf4/store/modules_metadata.json:      "URL-https://blog.fuzzing-project.org/60-Optionsbleed-HTTP-OPTIONS-method-can-leak-Apaches-server-memory.html"
.msf4/store/modules_metadata.json:    "path": "/modules/auxiliary/scanner/http/apache_optionsbleed.rb",
.msf4/store/modules_metadata.json:    "ref_name": "scanner/http/apache_optionsbleed",
.msf4/store/modules_metadata.json:  "auxiliary_scanner/http/apache_userdir_enum": {
.msf4/store/modules_metadata.json:    "name": "Apache \"mod_userdir\" User Enumeration",
.msf4/store/modules_metadata.json:    "fullname": "auxiliary/scanner/http/apache_userdir_enum",
.msf4/store/modules_metadata.json:    "description": "Apache with the UserDir directive enabled generates different error\n      codes when a username exists and there is no public_html directory and when the username\n      does not exist, which could allow remote attackers to determine valid usernames on the\n      server.",
.msf4/store/modules_metadata.json:    "path": "/modules/auxiliary/scanner/http/apache_userdir_enum.rb",
.msf4/store/modules_metadata.json:    "ref_name": "scanner/http/apache_userdir_enum",
.msf4/store/modules_metadata.json:    "name": "Apache Axis2 v1.4.1 Local File Inclusion",
.msf4/store/modules_metadata.json:    "description": "This module exploits an Apache Axis2 v1.4.1 local file inclusion (LFI) vulnerability.\n        By loading a local XML file which contains a cleartext username and password, attackers can trivially\n        recover authentication credentials to Axis services.",
.msf4/store/modules_metadata.json:    "name": "Apache Axis2 Brute Force Utility",
.msf4/store/modules_metadata.json:    "description": "This module attempts to login to an Apache Axis2 instance using\n        username and password combinations indicated by the USER_FILE,\n        PASS_FILE, and USERPASS_FILE options. It has been verified to\n        work on at least versions 1.4.1 and 1.6.2.",
.msf4/store/modules_metadata.json:    "description": "Versions of Apache Log4j2 impacted by CVE-2021-44228 which allow JNDI features used in configuration,\n        log messages, and parameters, do not protect against attacker controlled LDAP and other JNDI related endpoints.\n\n        This module will scan an HTTP end point for the Log4Shell vulnerability by injecting a format message that will\n        trigger an LDAP connection to Metasploit. This module is a generic scanner and is only capable of identifying\n        instances that are vulnerable via one of the pre-determined HTTP request injection points. These points include\n        HTTP headers and the HTTP request path.\n\n        Known impacted software includes Apache Struts 2, VMWare VCenter, Apache James, Apache Solr, Apache Druid,\n        Apache JSPWiki, Apache OFBiz.",
.msf4/store/modules_metadata.json:      "URL-https://logging.apache.org/log4j/2.x/security.html"
.msf4/store/modules_metadata.json:    "name": "Apache HTTPD mod_negotiation Filename Bruter",
.msf4/store/modules_metadata.json:    "name": "Apache HTTPD mod_negotiation Scanner",
.msf4/store/modules_metadata.json:    "name": "Apache Reverse Proxy Bypass Vulnerability Scanner",
.msf4/store/modules_metadata.json:    "description": "Scan for poorly configured reverse proxy servers.\n        By default, this module attempts to force the server to make\n        a request with an invalid domain name. Then, if the bypass\n        is successful, the server will look it up and of course fail,\n        then responding with a status code 502. A baseline status code\n        is always established and if that baseline matches your test\n        status code, the injection attempt does not occur.\n        \"set VERBOSE true\" if you are paranoid and want to catch potential\n        false negatives. Works best against Apache and mod_rewrite",
.msf4/store/modules_metadata.json:    "name": "Apache Tomcat User Enumeration",
.msf4/store/modules_metadata.json:    "description": "This module enumerates Apache Tomcat's usernames via malformed requests to\n        j_security_check, which can be found in the web administration package. It should\n        work against Tomcat servers 4.1.0 - 4.1.39, 5.5.0 - 5.5.27, and 6.0.0 - 6.0.18.\n        Newer versions no longer have the \"admin\" package by default. The 'admin' package\n        is no longer provided for Tomcat 6 and later versions.",
.msf4/store/modules_metadata.json:      "URL-https://tomcat.apache.org/",
.msf4/store/modules_metadata.json:    "description": "This module exploits the WANGKONGBAO CNS-1000 and 1100 UTM appliances aka\n        Network Security Platform. This directory traversal vulnerability is interesting\n        because the apache server is running as root, this means we can grab anything we\n        want! For instance, the /etc/shadow and /etc/passwd files for the special\n        kfc:$1$SlSyHd1a$PFZomnVnzaaj3Ei2v1ByC0:15488:0:99999:7::: user",
.msf4/store/modules_metadata.json:    "name": "Apache RocketMQ Version Scanner",
.msf4/store/modules_metadata.json:    "description": "Version scanner for the Apache RocketMQ product.",
.msf4/store/modules_metadata.json:      "URL-https://github.com/apache/rocketmq"
.msf4/store/modules_metadata.json:  "auxiliary_scanner/ssh/apache_karaf_command_execution": {
.msf4/store/modules_metadata.json:    "name": "Apache Karaf Default Credentials Command Execution",
.msf4/store/modules_metadata.json:    "fullname": "auxiliary/scanner/ssh/apache_karaf_command_execution",
.msf4/store/modules_metadata.json:    "description": "This module exploits a default misconfiguration flaw on Apache Karaf versions 2.x-4.x.\n        The 'karaf' user has a known default password, which can be used to login to the\n        SSH service, and execute operating system commands from remote.",
.msf4/store/modules_metadata.json:    "path": "/modules/auxiliary/scanner/ssh/apache_karaf_command_execution.rb",
.msf4/store/modules_metadata.json:    "ref_name": "scanner/ssh/apache_karaf_command_execution",
.msf4/store/modules_metadata.json:    "name": "Apache Karaf Login Utility",
.msf4/store/modules_metadata.json:    "description": "This module attempts to log into Apache Karaf's SSH. If the TRYDEFAULTCRED option is\n        set, then it will also try the default 'karaf' credential.",
.msf4/store/modules_metadata.json:  "exploit_linux/http/apache_airflow_dag_rce": {
.msf4/store/modules_metadata.json:    "name": "Apache Airflow 1.10.10 - Example DAG Remote Code Execution",
.msf4/store/modules_metadata.json:    "fullname": "exploit/linux/http/apache_airflow_dag_rce",
.msf4/store/modules_metadata.json:    "description": "This module exploits an unauthenticated command injection vulnerability\n          by combining two critical vulnerabilities in Apache Airflow 1.10.10.\n          The first, CVE-2020-11978, is an authenticated command injection vulnerability\n          found in one of Airflow's example DAGs, \"example_trigger_target_dag\", which\n          allows any authenticated user to run arbitrary OS commands as the user\n          running Airflow Worker/Scheduler. The second, CVE-2020-13927, is a default\n          setting of Airflow 1.10.10 that allows unauthenticated access to Airflow's\n          Experimental REST API to perform malicious actions such as creating the\n          vulnerable DAG above. The two CVEs taken together allow vulnerable DAG creation\n          and command injection, leading to unauthenticated remote code execution.",
.msf4/store/modules_metadata.json:      "URL-https://lists.apache.org/thread/cn57zwylxsnzjyjztwqxpmly0x9q5ljx",
.msf4/store/modules_metadata.json:      "URL-https://lists.apache.org/thread/mq1bpqf3ztg1nhyc5qbrjobfrzttwx1d"
.msf4/store/modules_metadata.json:    "path": "/modules/exploits/linux/http/apache_airflow_dag_rce.rb",
.msf4/store/modules_metadata.json:    "ref_name": "linux/http/apache_airflow_dag_rce",
.msf4/store/modules_metadata.json:  "exploit_linux/http/apache_continuum_cmd_exec": {
.msf4/store/modules_metadata.json:    "name": "Apache Continuum Arbitrary Command Execution",
.msf4/store/modules_metadata.json:    "fullname": "exploit/linux/http/apache_continuum_cmd_exec",
.msf4/store/modules_metadata.json:    "description": "This module exploits a command injection in Apache Continuum <= 1.4.2.\n        By injecting a command into the installation.varValue POST parameter to\n        /continuum/saveInstallation.action, a shell can be spawned.",
.msf4/store/modules_metadata.json:      "Apache Continuum <= 1.4.2"
.msf4/store/modules_metadata.json:    "path": "/modules/exploits/linux/http/apache_continuum_cmd_exec.rb",
.msf4/store/modules_metadata.json:    "ref_name": "linux/http/apache_continuum_cmd_exec",
.msf4/store/modules_metadata.json:  "exploit_linux/http/apache_couchdb_cmd_exec": {
.msf4/store/modules_metadata.json:    "name": "Apache CouchDB Arbitrary Command Execution",
.msf4/store/modules_metadata.json:    "fullname": "exploit/linux/http/apache_couchdb_cmd_exec",
.msf4/store/modules_metadata.json:    "description": "CouchDB administrative users can configure the database server via HTTP(S).\n        Some of the configuration options include paths for operating system-level binaries that are subsequently launched by CouchDB.\n        This allows an admin user in Apache CouchDB before 1.7.0 and 2.x before 2.1.1 to execute arbitrary shell commands as the CouchDB user,\n        including downloading and executing scripts from the public internet.",
.msf4/store/modules_metadata.json:      "URL-https://lists.apache.org/thread.html/6c405bf3f8358e6314076be9f48c89a2e0ddf00539906291ebdf0c67@%3Cdev.couchdb.apache.org%3E"
.msf4/store/modules_metadata.json:      "Apache CouchDB version 1.x",
.msf4/store/modules_metadata.json:      "Apache CouchDB version 2.x"
.msf4/store/modules_metadata.json:    "path": "/modules/exploits/linux/http/apache_couchdb_cmd_exec.rb",
.msf4/store/modules_metadata.json:    "ref_name": "linux/http/apache_couchdb_cmd_exec",
.msf4/store/modules_metadata.json:  "exploit_linux/http/apache_druid_js_rce": {
.msf4/store/modules_metadata.json:    "name": "Apache Druid 0.20.0 Remote Command Execution",
.msf4/store/modules_metadata.json:    "fullname": "exploit/linux/http/apache_druid_js_rce",
.msf4/store/modules_metadata.json:    "description": "Apache Druid includes the ability to execute user-provided JavaScript code embedded in\n          various types of requests; however, that feature is disabled by default.\n\n          In Druid versions prior to `0.20.1`, an authenticated user can send a specially-crafted request\n          that both enables the JavaScript code-execution feature and executes the supplied code all\n          at once, allowing for code execution on the server with the privileges of the Druid Server process.\n          More critically, authentication is not enabled in Apache Druid by default.\n\n          Tested on the following Apache Druid versions:\n\n          * 0.15.1\n          * 0.16.0-iap8\n          * 0.17.1\n          * 0.18.0-iap3\n          * 0.19.0-iap7\n          * 0.20.0-iap4.1\n          * 0.20.0\n          * 0.21.0-iap3",
.msf4/store/modules_metadata.json:      "URL-https://lists.apache.org/thread.html/rfda8a3aa6ac06a80c5cbfdeae0fc85f88a5984e32ea05e6dda46f866%40%3Cdev.druid.apache.org%3E",
.msf4/store/modules_metadata.json:    "path": "/modules/exploits/linux/http/apache_druid_js_rce.rb",
.msf4/store/modules_metadata.json:    "ref_name": "linux/http/apache_druid_js_rce",
.msf4/store/modules_metadata.json:  "exploit_linux/http/apache_nifi_h2_rce": {
.msf4/store/modules_metadata.json:    "name": "Apache NiFi H2 Connection String Remote Code Execution",
.msf4/store/modules_metadata.json:    "fullname": "exploit/linux/http/apache_nifi_h2_rce",
.msf4/store/modules_metadata.json:    "description": "The DBCPConnectionPool and HikariCPConnectionPool Controller Services in\n          Apache NiFi 0.0.2 through 1.21.0 allow an authenticated and authorized user\n          to configure a Database URL with the H2 driver that enables custom code execution.\n\n          This exploit will result in several shells (5-7).\n          Successfully tested against Apache nifi 1.17.0 through 1.21.0.",
.msf4/store/modules_metadata.json:      "URL-https://lists.apache.org/thread/7b82l4f5blmpkfcynf3y6z4x1vqo59h8",
.msf4/store/modules_metadata.json:      "URL-https://issues.apache.org/jira/browse/NIFI-11653",
.msf4/store/modules_metadata.json:      "URL-https://nifi.apache.org/security.html#1.22.0"
.msf4/store/modules_metadata.json:    "path": "/modules/exploits/linux/http/apache_nifi_h2_rce.rb",
.msf4/store/modules_metadata.json:    "ref_name": "linux/http/apache_nifi_h2_rce",
.msf4/store/modules_metadata.json:  "exploit_linux/http/apache_ofbiz_deserialization": {
.msf4/store/modules_metadata.json:    "name": "Apache OFBiz XML-RPC Java Deserialization",
.msf4/store/modules_metadata.json:    "fullname": "exploit/linux/http/apache_ofbiz_deserialization",
.msf4/store/modules_metadata.json:    "description": "This module exploits a Java deserialization vulnerability in Apache\n          OFBiz's unauthenticated XML-RPC endpoint /webtools/control/xmlrpc for\n          versions prior to 17.12.04.",
.msf4/store/modules_metadata.json:      "URL-https://securitylab.github.com/advisories/GHSL-2020-069-apache_ofbiz",
.msf4/store/modules_metadata.json:      "URL-https://ofbiz.apache.org/release-notes-17.12.04.html",
.msf4/store/modules_metadata.json:      "URL-https://issues.apache.org/jira/browse/OFBIZ-11716"
.msf4/store/modules_metadata.json:    "path": "/modules/exploits/linux/http/apache_ofbiz_deserialization.rb",
.msf4/store/modules_metadata.json:    "ref_name": "linux/http/apache_ofbiz_deserialization",
.msf4/store/modules_metadata.json:  "exploit_linux/http/apache_ofbiz_deserialization_soap": {
.msf4/store/modules_metadata.json:    "name": "Apache OFBiz SOAP Java Deserialization",
.msf4/store/modules_metadata.json:    "fullname": "exploit/linux/http/apache_ofbiz_deserialization_soap",
.msf4/store/modules_metadata.json:    "description": "This module exploits a Java deserialization vulnerability in Apache\n          OFBiz's unauthenticated SOAP endpoint /webtools/control/SOAPService for\n          versions prior to 17.12.06.",
.msf4/store/modules_metadata.json:      "URL-https://issues.apache.org/jira/browse/OFBIZ-12167"
.msf4/store/modules_metadata.json:    "path": "/modules/exploits/linux/http/apache_ofbiz_deserialization_soap.rb",
.msf4/store/modules_metadata.json:    "ref_name": "linux/http/apache_ofbiz_deserialization_soap",
.msf4/store/modules_metadata.json:  "exploit_linux/http/apache_spark_rce_cve_2022_33891": {
.msf4/store/modules_metadata.json:    "name": "Apache Spark Unauthenticated Command Injection RCE",
.msf4/store/modules_metadata.json:    "fullname": "exploit/linux/http/apache_spark_rce_cve_2022_33891",
.msf4/store/modules_metadata.json:    "description": "This module exploits an unauthenticated command injection vulnerability in Apache Spark.\n          Successful exploitation results in remote code execution under the context of the Spark application user.\n\n          The command injection occurs because Spark checks the group membership of the user passed\n          in the ?doAs parameter by using a raw Linux command.\n\n          It is triggered by a non-default setting called spark.acls.enable.\n          This configuration setting spark.acls.enable should be set true in the Spark configuration to make the application vulnerable for this attack.\n\n          Apache Spark versions 3.0.3 and earlier, versions 3.1.1 to 3.1.2, and versions 3.2.0 to 3.2.1 are affected by this vulnerability.",
.msf4/store/modules_metadata.json:      "URL-https://lists.apache.org/thread/p847l3kopoo5bjtmxrcwk21xp6tjxqlc",
.msf4/store/modules_metadata.json:    "path": "/modules/exploits/linux/http/apache_spark_rce_cve_2022_33891.rb",
.msf4/store/modules_metadata.json:    "ref_name": "linux/http/apache_spark_rce_cve_2022_33891",
.msf4/store/modules_metadata.json:  "exploit_linux/http/apache_superset_cookie_sig_rce": {
.msf4/store/modules_metadata.json:    "name": "Apache Superset Signed Cookie RCE",
.msf4/store/modules_metadata.json:    "fullname": "exploit/linux/http/apache_superset_cookie_sig_rce",
.msf4/store/modules_metadata.json:    "description": "Apache Superset versions <= 2.0.0 utilize Flask with a known default secret key which is used to sign HTTP cookies.\n          These cookies can therefore be forged. If a user is able to login to the site, they can decode the cookie, set their user_id to that\n          of an administrator, and re-sign the cookie. This valid cookie can then be used to login as the targeted user. From there the\n          Superset database is mounted, and credentials are pulled. A dashboard is then created. Lastly a pickled python payload can be\n          set for that dashboard within Superset's database which will trigger the RCE.\n\n          An attempt to clean up ALL of the dashboard key values and reset them to their previous values happens during the cleanup phase.",
.msf4/store/modules_metadata.json:      "URL-https://vulcan.io/blog/cve-2023-27524-in-apache-superset-what-you-need-to-know/",
.msf4/store/modules_metadata.json:      "URL-https://www.horizon3.ai/cve-2023-27524-insecure-default-configuration-in-apache-superset-leads-to-remote-code-execution/",
.msf4/store/modules_metadata.json:      "URL-https://www.horizon3.ai/apache-superset-part-ii-rce-credential-harvesting-and-more/",
.msf4/store/modules_metadata.json:    "path": "/modules/exploits/linux/http/apache_superset_cookie_sig_rce.rb",
.msf4/store/modules_metadata.json:    "ref_name": "linux/http/apache_superset_cookie_sig_rce",
.msf4/store/modules_metadata.json:        "auxiliary/gather/apache_superset_cookie_sig_priv_esc"
.msf4/store/modules_metadata.json:    "description": "This module exploits a directory traversal vulnerability in ATutor on an Apache/PHP\n          setup with display_errors set to On, which can be used to allow us to upload a malicious\n          ZIP file. On the web application, a blacklist verification is performed before extraction,\n          however it is not sufficient to prevent exploitation.\n\n          You are required to login to the target to reach the vulnerability, however this can be\n          done as a student account and remote registration is enabled by default.\n\n          Just in case remote registration isn't enabled, this module uses 2 vulnerabilities\n          in order to bypass the authentication:\n\n          1. confirm.php Authentication Bypass Type Juggling vulnerability\n          2. password_reminder.php Remote Password Reset TOCTOU vulnerability",
.msf4/store/modules_metadata.json:    "description": "Cisco Prime Infrastructure (CPI) contains two basic flaws that when exploited allow\n        an unauthenticated attacker to achieve remote code execution. The first flaw is a file\n        upload vulnerability that allows the attacker to upload and execute files as the Apache\n        Tomcat user; the second is a privilege escalation to root by bypassing execution restrictions\n        in a SUID binary.\n\n        This module exploits these vulnerabilities to achieve unauthenticated remote code execution\n        as root on the CPI default installation.\n\n        This module has been tested with CPI 3.2.0.0.258 and 3.4.0.0.348. Earlier and later versions\n        might also be affected, although 3.4.0.0.348 is the latest at the time of writing.\n        The file upload vulnerability should have been fixed in versions 3.4.1 and 3.3.1 Update 02.",
.msf4/store/modules_metadata.json:    "description": "This module exploits a vulnerability found in Cisco Prime Infrastructure. The issue is that\n        the TarArchive Java class the HA Health Monitor component uses does not check for any\n        directory traversals while unpacking a Tar file, which can be abused by a remote user to\n        leverage the UploadServlet class to upload a JSP payload to the Apache Tomcat's web apps\n        directory, and gain arbitrary remote code execution. Note that authentication is not\n        required to exploit this vulnerability.",
.msf4/store/modules_metadata.json:    "description": "This module exploits multiple vulnerabilities in EyesOfNetwork version 5.1, 5.2\n        and 5.3 in order to execute arbitrary commands as root.\n\n        This module takes advantage of a command injection vulnerability in the\n        `target` parameter of the AutoDiscovery functionality within the EON web\n        interface in order to write an Nmap NSE script containing the payload to\n        disk. It then starts an Nmap scan to activate the payload. This results in\n        privilege escalation because the`apache` user can execute Nmap as root.\n\n        Valid credentials for a user with administrative privileges are required.\n        However, this module can bypass authentication via various methods, depending on\n        the EON version. EON 5.3 is vulnerable to a hardcoded API key and two SQL\n        injection exploits. EON 5.1 and 5.2 can only be exploited via SQL injection.\n        This module has been successfully tested on EyesOfNetwork 5.1, 5.2 and 5.3.",
.msf4/store/modules_metadata.json:      "URL-https://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-common/SecureMode.html"
.msf4/store/modules_metadata.json:    "description": "This module exploits an unauthenticated command injection vulnerability\n          in Klog Server versions 2.4.1 and prior.\n\n          The `authenticate.php` file uses the `user` HTTP POST parameter in a call\n          to the `shell_exec()` PHP function without appropriate input validation,\n          allowing arbitrary command execution as the apache user.\n\n          The sudo configuration permits the apache user to execute any command\n          as root without providing a password, resulting in privileged command\n          execution as root.\n\n          This module has been successfully tested on Klog Server version 2.4.1\n          virtual appliance.",
.msf4/store/modules_metadata.json:    "description": "This module exploits a command injection vulnerability in Mida\n          Solutions eFramework version 2.9.0 and prior.\n\n          The `ajaxreq.php` file allows unauthenticated users to inject\n          arbitrary commands in the `PARAM` parameter to be executed as\n          the apache user. The sudo configuration permits the apache user\n          to execute any command as root without providing a password,\n          resulting in privileged command execution as root.\n\n          This module has been successfully tested on Mida Solutions\n          eFramework-C7-2.9.0 virtual appliance.",
.msf4/store/modules_metadata.json:    "description": "This module exploits CVE-2021-25296, CVE-2021-25297, and CVE-2021-25298, which are\n          OS command injection vulnerabilities in the windowswmi, switch, and cloud-vm\n          configuration wizards that allow an authenticated user to perform remote code\n          execution on Nagios XI versions 5.5.6 to 5.7.5 as the apache user.\n\n          Valid credentials for a Nagios XI user are required. This module has\n          been successfully tested against official NagiosXI OVAs from 5.5.6-5.7.5.",
.msf4/store/modules_metadata.json:    "description": "This module exploits CVE-2020-5791, an OS command injection vulnerability in\n          `admin/mibs.php` that enables an authenticated user with admin privileges to achieve\n          remote code execution as either the `apache` user or the `www-data` user on NagiosXI\n          version 5.6.0 to 5.7.3 inclusive (exact user depends on the version of NagiosXI\n          installed as well as the OS its installed on).\n\n          Valid credentials for a Nagios XI admin user are required. This module has\n          been successfully tested against Nagios XI 5.7.3 running on CentOS 7.",
.msf4/store/modules_metadata.json:    "description": "This module exploits a command injection vulnerability (CVE-2020-35578) in the `/admin/monitoringplugins.php`\n          page of Nagios XI versions prior to 5.8.0 when uploading plugins. Successful exploitation allows\n          an authenticated admin user to achieve remote code execution as the `apache` user by uploading\n          a malicious plugin.\n\n          Valid credentials for a Nagios XI admin user are required. This module has\n          been successfully tested against Nagios versions XI 5.3.0 and 5.7.5, both\n          running on CentOS 7.",
.msf4/store/modules_metadata.json:    "description": "This module exploits an OS command injection vulnerability in\n          includes/components/nxti/index.php that enables an authenticated user\n          with admin privileges to achieve remote code execution as the `apache`\n          user. The module uploads a simple PHP shell via includes/components/nxti/index.php\n          to includes/components/autodiscovery/jobs/<php_shell> and then\n          executes the payload as the `apache` user via an HTTP GET request to\n          includes/components/autodiscovery/jobs/<php_shell>?<php_param>=<cmd>\n\n          Valid credentials for a Nagios XI admin user are required. This module has\n          been successfully tested against Nagios XI 5.7.3 running on CentOS 7.",
.msf4/store/modules_metadata.json:    "description": "This module abuses two flaws - a metacharacter injection vulnerability in the\n        HTTP management server of RedHat 6.2 systems running the Piranha\n        LVS cluster service and GUI (rpm packages: piranha and piranha-gui).\n        The vulnerability allows an authenticated attacker to execute arbitrary\n        commands as the Apache user account (nobody) within the\n        /piranha/secure/passwd.php3 script. The package installs with a default\n        user and password of piranha:q which was exploited in the wild.",
.msf4/store/modules_metadata.json:    "description": "This module exploits multiple vulnerabilities in rConfig version 3.9\n          in order to execute arbitrary commands.\n          This module takes advantage of a command injection vulnerability in the\n          `path` parameter of the ajax archive file functionality within the rConfig web\n          interface in order to execute the payload.\n          Valid credentials for a user with administrative privileges are required.\n          However, this module can bypass authentication via SQLI.\n          This module has been successfully tested on Rconfig 3.9.3 and 3.9.4.\n          The steps are:\n          1. SQLi on /commands.inc.php allows us to add an administrative user.\n          2. An authenticated session is established with the newly added user\n          3. Command Injection on /lib/ajaxHandlers/ajaxArchiveFiles.php allows us to\n          execute the payload.\n          4. Remove the added admin user.\n          Tips : once you get a shell, look at the CVE-2019-19585.\n          You will probably get root because rConfig install script add Apache user to\n          sudoers with nopasswd ;-)",
.msf4/store/modules_metadata.json:    "name": "Apache Spark Unauthenticated Command Execution",
.msf4/store/modules_metadata.json:    "description": "This module exploits an unauthenticated command execution vulnerability in Apache Spark with standalone cluster mode through REST API.\n          It uses the function CreateSubmissionRequest to submit a malious java class and trigger it.",
.msf4/store/modules_metadata.json:    "description": "This module exploits a vulnerability found in Symantec Web Gateway's HTTP\n        service.  By injecting PHP code in the access log, it is possible to load it\n        with a directory traversal flaw, which allows remote code execution under the\n        context of 'apache'. Please note that it may take up to several minutes to\n        retrieve access_log, which is about the amount of time required to see a shell\n        back.",
.msf4/store/modules_metadata.json:    "description": "This module exploits multiple vulnerabilities together in order to achive a remote code execution.\n          Unauthenticated users can execute a terminal command under the context of the root user.\n\n          The specific flaw exists within the LogSettingHandler class of administrator interface software.\n          When parsing the mount_device parameter, the process does not properly validate a user-supplied string\n          before using it to execute a system call. An attacker can leverage this vulnerability to execute code in\n          the context of root. But authentication is required to exploit this vulnerability.\n\n          Another specific flaw exist within the proxy service, which listens on port 8080 by default. Unauthenticated users\n          can exploit this vulnerability in order to communicate with internal services in the product.\n\n          Last but not least a flaw exists within the Apache Solr application, which is installed within the product.\n          When parsing the file parameter, the process does not properly validate a user-supplied path prior to using it in file operations.\n          An attacker can leverage this vulnerability to disclose information in the context of the IWSS user.\n\n          Due to combination of these vulnerabilities, unauthenticated users can execute a terminal command under the context of the root user.\n\n          Version perior to 6.5 SP2 Patch 4 (Build 1901) are affected.",
.msf4/store/modules_metadata.json:    "description": "This module exploits an unauthenticated log file upload within the\n          log_upload_wsgi.py file of VMWare View Planner 4.6 prior to 4.6\n          Security Patch 1.\n\n          Successful exploitation will result in RCE as the apache user inside\n          the appacheServer Docker container.",
.msf4/store/modules_metadata.json:    "description": "VMWare Aria Operations for Networks (vRealize Network Insight) is vulnerable to command injection\n          when accepting user input through the Apache Thrift RPC interface. This vulnerability allows a\n          remote unauthenticated attacker to execute arbitrary commands on the underlying operating system\n          as the root user. The RPC interface is protected by a reverse proxy which can be bypassed.\n          VMware has evaluated the severity of this issue to be in the Critical severity range with a\n          maximum CVSSv3 base score of 9.8. A malicious actor can get remote code execution in the\n          context of 'root' on the appliance.\n          VMWare 6.x version are vulnerable.\n\n          This module exploits the vulnerability to upload and execute payloads gaining root privileges.\n          Successfully tested against version 6.8.0.",
.msf4/store/modules_metadata.json:    "description": "Version 6.1.12 and earlier of Kloxo contain two setuid root binaries such as\n        lxsuexec and lxrestart, allow local privilege escalation to root from uid 48,\n        Apache by default on CentOS 5.8, the operating system supported by Kloxo.\n        This module has been tested successfully with Kloxo 6.1.12 and 6.1.6.",
.msf4/store/modules_metadata.json:    "name": "Apache Tomcat on RedHat Based Systems Insecure Temp Config Privilege Escalation",
.msf4/store/modules_metadata.json:    "description": "This module exploits a vulnerability in RedHat based systems where\n          improper file permissions are applied to /usr/lib/tmpfiles.d/tomcat.conf\n          for Apache Tomcat versions before 7.0.54-8.  This may also work against\n\n          The configuration files in tmpfiles.d are used by systemd-tmpfiles to manage\n          temporary files including their creation.\n\n          With this weak permission, we're able to inject commands into systemd-tmpfiles\n          service to write a cron job to execute our payload.\n\n          systemd-tmpfiles is executed by default on boot on RedHat-based systems\n          through systemd-tmpfiles-setup.service. Depending on the system in use,\n          the execution of systemd-tmpfiles could also be triggered by other\n          services, cronjobs, startup scripts etc.\n\n          This module was tested against Tomcat 7.0.54-3 on Fedora 21.",
.msf4/store/modules_metadata.json:    "name": "Apache Tomcat on Ubuntu Log Init Privilege Escalation",
.msf4/store/modules_metadata.json:    "name": "Apache Storm Nimbus getTopologyHistory Unauthenticated Command Execution",
.msf4/store/modules_metadata.json:    "description": "This module exploits an unauthenticated command injection vulnerability within the Nimbus service component of Apache Storm.\n          The getTopologyHistory RPC method method takes a single argument which is the name of a user which is\n          concatenated into a string that is executed by bash. In order for the vulnerability to be exploitable, there\n          must have been at least one topology submitted to the server. The topology may be active or inactive, but at\n          least one must be present. Successful exploitation results in remote code execution as the user running Apache Storm.\n\n          This vulnerability was patched in versions 2.1.1, 2.2.1 and 1.2.4. This exploit was tested on version 2.2.0\n          which is affected.",
.msf4/store/modules_metadata.json:      "URL-https://securitylab.github.com/advisories/GHSL-2021-085-apache-storm/"
.msf4/store/modules_metadata.json:  "exploit_linux/smtp/apache_james_exec": {
.msf4/store/modules_metadata.json:    "name": "Apache James Server 2.3.2 Insecure User Creation Arbitrary File Write",
.msf4/store/modules_metadata.json:    "fullname": "exploit/linux/smtp/apache_james_exec",
.msf4/store/modules_metadata.json:    "description": "This module exploits a vulnerability that exists due to a lack of input\n        validation when creating a user. Messages for a given user are stored\n        in a directory partially defined by the username. By creating a user\n        with a directory traversal payload as the username, commands can be\n        written to a given directory. To use this module with the cron\n        exploitation method, run the exploit using the given payload, host, and\n        port. After running the exploit, the payload will be executed within 60\n        seconds. Due to differences in how cron may run in certain Linux\n        operating systems such as Ubuntu, it may be preferable to set the\n        target to Bash Completion as the cron method may not work. If the target\n        is set to Bash completion, start a listener using the given payload,\n        host, and port before running the exploit. After running the exploit,\n        the payload will be executed when a user logs into the system. For this\n        exploitation method, bash completion must be enabled to gain code\n        execution. This exploitation method will leave an Apache James mail\n        object artifact in the /etc/bash_completion.d directory and the\n        malicious user account.",
.msf4/store/modules_metadata.json:      "URL-https://www.exploit-db.com/docs/english/40123-exploiting-apache-james-server-2.3.2.pdf"
.msf4/store/modules_metadata.json:    "path": "/modules/exploits/linux/smtp/apache_james_exec.rb",
.msf4/store/modules_metadata.json:    "ref_name": "linux/smtp/apache_james_exec",
.msf4/store/modules_metadata.json:    "description": "This is a generic arbitrary file overwrite technique, which typically results in remote\n          command execution. This targets a simple yet widespread vulnerability that has been\n          seen affecting a variety of popular products including HP, Amazon, Apache, Cisco, etc.\n          The idea is that often archive extraction libraries have no mitigations against\n          directory traversal attacks. If an application uses it, there is a risk when opening an\n          archive that is maliciously modified, and result in the embedded payload to be written\n          to an arbitrary location (such as a web root), and result in remote code execution.",
.msf4/store/modules_metadata.json:  "exploit_multi/http/apache_activemq_upload_jsp": {
.msf4/store/modules_metadata.json:    "fullname": "exploit/multi/http/apache_activemq_upload_jsp",
.msf4/store/modules_metadata.json:    "description": "The Fileserver web application in Apache ActiveMQ 5.x before 5.14.0\n        allows remote attackers to upload and execute arbitrary files via an\n        HTTP PUT followed by an HTTP MOVE request.",
.msf4/store/modules_metadata.json:      "URL-http://activemq.apache.org/security-advisories.data/CVE-2016-3088-announcement.txt"
.msf4/store/modules_metadata.json:    "path": "/modules/exploits/multi/http/apache_activemq_upload_jsp.rb",
.msf4/store/modules_metadata.json:    "ref_name": "multi/http/apache_activemq_upload_jsp",
.msf4/store/modules_metadata.json:  "exploit_multi/http/apache_apisix_api_default_token_rce": {
.msf4/store/modules_metadata.json:    "fullname": "exploit/multi/http/apache_apisix_api_default_token_rce",
.msf4/store/modules_metadata.json:    "description": "Apache APISIX has a default, built-in API token edd1c9f034335f136f87ad84b625c8f1 that can be used to access\n          all of the admin API, which leads to remote LUA code execution through the script parameter added in the 2.x\n          version. This module also leverages another vulnerability to bypass the IP restriction plugin.",
.msf4/store/modules_metadata.json:      "URL-https://github.com/apache/apisix/pull/2244",
.msf4/store/modules_metadata.json:    "path": "/modules/exploits/multi/http/apache_apisix_api_default_token_rce.rb",
.msf4/store/modules_metadata.json:    "ref_name": "multi/http/apache_apisix_api_default_token_rce",
.msf4/store/modules_metadata.json:  "exploit_multi/http/apache_commons_text4shell": {
.msf4/store/modules_metadata.json:    "name": "Apache Commons Text RCE",
.msf4/store/modules_metadata.json:    "fullname": "exploit/multi/http/apache_commons_text4shell",
.msf4/store/modules_metadata.json:    "description": "This exploit takes advantage of the StringSubstitutor interpolator class,\n          which is included in the Commons Text library. A default interpolator\n          allows for string lookups that can lead to Remote Code Execution. This\n          is due to a logic flaw that makes the “script”, “dns” and “url” lookup\n          keys interpolated by default, as opposed to what it should be, according\n          to the documentation of the StringLookupFactory class. Those keys allow\n          an attacker to execute arbitrary code via lookups primarily using the\n          \"script\" key.\n\n          In order to exploit the vulnerabilities, the following requirements must\n          be met:\n\n          Run a version of Apache Commons Text from version 1.5 to 1.9\n          Use the StringSubstitutor interpolator\n          Target should run JDK < 15",
.msf4/store/modules_metadata.json:    "path": "/modules/exploits/multi/http/apache_commons_text4shell.rb",
.msf4/store/modules_metadata.json:    "ref_name": "multi/http/apache_commons_text4shell",
.msf4/store/modules_metadata.json:  "exploit_multi/http/apache_couchdb_erlang_rce": {
.msf4/store/modules_metadata.json:    "name": "Apache Couchdb Erlang RCE",
.msf4/store/modules_metadata.json:    "fullname": "exploit/multi/http/apache_couchdb_erlang_rce",
.msf4/store/modules_metadata.json:    "description": "In Apache CouchDB prior to 3.2.2, an attacker can access an improperly secured default installation without\n          authenticating and gain admin privileges.",
.msf4/store/modules_metadata.json:    "path": "/modules/exploits/multi/http/apache_couchdb_erlang_rce.rb",
.msf4/store/modules_metadata.json:    "ref_name": "multi/http/apache_couchdb_erlang_rce",
.msf4/store/modules_metadata.json:  "exploit_multi/http/apache_druid_cve_2023_25194": {
.msf4/store/modules_metadata.json:    "name": "Apache Druid JNDI Injection RCE",
.msf4/store/modules_metadata.json:    "fullname": "exploit/multi/http/apache_druid_cve_2023_25194",
.msf4/store/modules_metadata.json:    "description": "This module is designed to exploit the JNDI injection vulnerability\n        in Druid. The vulnerability specifically affects the indexer/v1/sampler\n        interface of Druid, enabling an attacker to execute arbitrary commands\n        on the targeted server.\n\n        The vulnerability is found in Apache Kafka clients versions ranging from\n        2.3.0 to 3.3.2. If an attacker can manipulate the sasl.jaas.config\n        property of any of the connector's Kafka clients to com.sun.security.auth.module.JndiLoginModule,\n        it allows the server to establish a connection with the attacker's LDAP server\n        and deserialize the LDAP response. This provides the attacker with the capability\n        to execute java deserialization gadget chains on the Kafka connect server,\n        potentially leading to unrestricted deserialization of untrusted data or even\n        remote code execution (RCE) if there are relevant gadgets in the classpath.\n\n        To facilitate the exploitation process, this module will initiate an LDAP server\n        that the target server needs to connect to in order to carry out the attack.",
.msf4/store/modules_metadata.json:      "URL-https://lists.apache.org/thread/vy1c7fqcdqvq5grcqp6q5jyyb302khyz"
.msf4/store/modules_metadata.json:    "path": "/modules/exploits/multi/http/apache_druid_cve_2023_25194.rb",
.msf4/store/modules_metadata.json:    "ref_name": "multi/http/apache_druid_cve_2023_25194",
.msf4/store/modules_metadata.json:  "exploit_multi/http/apache_flink_jar_upload_exec": {
.msf4/store/modules_metadata.json:    "name": "Apache Flink JAR Upload Java Code Execution",
.msf4/store/modules_metadata.json:    "fullname": "exploit/multi/http/apache_flink_jar_upload_exec",
.msf4/store/modules_metadata.json:    "description": "This module uses job functionality in Apache Flink dashboard web\n          interface to upload and execute a JAR file, leading to remote\n          execution of arbitrary Java code as the web server user.\n\n          This module has been tested successfully on Apache Flink versions:\n          1.9.3 on Ubuntu 18.04.4;\n          1.11.2 on Ubuntu 18.04.4;\n          1.9.3 on Windows 10; and\n          1.11.2 on Windows 10.",
.msf4/store/modules_metadata.json:      "URL-https://github.com/biggerwing/apache-flink-unauthorized-upload-rce-",
.msf4/store/modules_metadata.json:      "URL-https://nsfocusglobal.com/advisory-apache-flink-remote-code-execution-vulnerability/"
.msf4/store/modules_metadata.json:    "path": "/modules/exploits/multi/http/apache_flink_jar_upload_exec.rb",
.msf4/store/modules_metadata.json:    "ref_name": "multi/http/apache_flink_jar_upload_exec",
.msf4/store/modules_metadata.json:  "exploit_multi/http/apache_jetspeed_file_upload": {
.msf4/store/modules_metadata.json:    "name": "Apache Jetspeed Arbitrary File Upload",
.msf4/store/modules_metadata.json:    "fullname": "exploit/multi/http/apache_jetspeed_file_upload",
.msf4/store/modules_metadata.json:    "description": "This module exploits the unsecured User Manager REST API and a ZIP file\n        path traversal in Apache Jetspeed-2, version 2.3.0 and unknown earlier\n        versions, to upload and execute a shell.\n\n        Note: this exploit will create, use, and then delete a new admin user.\n\n        Warning: in testing, exploiting the file upload clobbered the web\n        interface beyond repair. No workaround has been found yet. Use this\n        module at your own risk. No check will be implemented.",
.msf4/store/modules_metadata.json:      "URL-http://haxx.ml/post/140552592371/remote-code-execution-in-apache-jetspeed-230-and",
.msf4/store/modules_metadata.json:      "URL-https://portals.apache.org/jetspeed-2/security-reports.html#CVE-2016-0709",
.msf4/store/modules_metadata.json:      "URL-https://portals.apache.org/jetspeed-2/security-reports.html#CVE-2016-0710"
.msf4/store/modules_metadata.json:      "Apache Jetspeed <= 2.3.0 (Linux)",
.msf4/store/modules_metadata.json:      "Apache Jetspeed <= 2.3.0 (Windows)"
.msf4/store/modules_metadata.json:    "path": "/modules/exploits/multi/http/apache_jetspeed_file_upload.rb",
.msf4/store/modules_metadata.json:    "ref_name": "multi/http/apache_jetspeed_file_upload",
.msf4/store/modules_metadata.json:  "exploit_multi/http/apache_mod_cgi_bash_env_exec": {
.msf4/store/modules_metadata.json:    "name": "Apache mod_cgi Bash Environment Variable Code Injection (Shellshock)",
.msf4/store/modules_metadata.json:    "fullname": "exploit/multi/http/apache_mod_cgi_bash_env_exec",
.msf4/store/modules_metadata.json:    "description": "This module exploits the Shellshock vulnerability, a flaw in how the Bash shell\n        handles external environment variables. This module targets CGI scripts in the\n        Apache web server by setting the HTTP_USER_AGENT environment variable to a\n        malicious function definition.",
.msf4/store/modules_metadata.json:    "path": "/modules/exploits/multi/http/apache_mod_cgi_bash_env_exec.rb",
.msf4/store/modules_metadata.json:    "ref_name": "multi/http/apache_mod_cgi_bash_env_exec",
.msf4/store/modules_metadata.json:  "exploit_multi/http/apache_nifi_processor_rce": {
.msf4/store/modules_metadata.json:    "name": "Apache NiFi API Remote Code Execution",
.msf4/store/modules_metadata.json:    "fullname": "exploit/multi/http/apache_nifi_processor_rce",
.msf4/store/modules_metadata.json:      "URL-https://nifi.apache.org/",
.msf4/store/modules_metadata.json:      "URL-https://github.com/apache/nifi",
.msf4/store/modules_metadata.json:      "URL-https://nifi.apache.org/docs/nifi-docs/components/org.apache.nifi/nifi-standard-nar/1.12.1/org.apache.nifi.processors.standard.ExecuteProcess/index.html"
.msf4/store/modules_metadata.json:    "path": "/modules/exploits/multi/http/apache_nifi_processor_rce.rb",
.msf4/store/modules_metadata.json:    "ref_name": "multi/http/apache_nifi_processor_rce",
.msf4/store/modules_metadata.json:  "exploit_multi/http/apache_normalize_path_rce": {
.msf4/store/modules_metadata.json:    "name": "Apache 2.4.49/2.4.50 Traversal RCE",
.msf4/store/modules_metadata.json:    "fullname": "exploit/multi/http/apache_normalize_path_rce",
.msf4/store/modules_metadata.json:    "description": "This module exploit an unauthenticated RCE vulnerability which exists in Apache version 2.4.49 (CVE-2021-41773).\n          If files outside of the document root are not protected by ‘require all denied’ and CGI has been explicitly enabled,\n          it can be used to execute arbitrary commands (Remote Command Execution).\n          This vulnerability has been reintroduced in Apache 2.4.50 fix (CVE-2021-42013).",
.msf4/store/modules_metadata.json:      "URL-https://httpd.apache.org/security/vulnerabilities_24.html",
.msf4/store/modules_metadata.json:      "URL-https://github.com/projectdiscovery/nuclei-templates/blob/master/vulnerabilities/apache/apache-httpd-rce.yaml",
.msf4/store/modules_metadata.json:    "path": "/modules/exploits/multi/http/apache_normalize_path_rce.rb",
.msf4/store/modules_metadata.json:    "ref_name": "multi/http/apache_normalize_path_rce",
.msf4/store/modules_metadata.json:  "exploit_multi/http/apache_rocketmq_update_config": {
.msf4/store/modules_metadata.json:    "name": "Apache RocketMQ update config RCE",
.msf4/store/modules_metadata.json:    "fullname": "exploit/multi/http/apache_rocketmq_update_config",
.msf4/store/modules_metadata.json:    "path": "/modules/exploits/multi/http/apache_rocketmq_update_config.rb",
.msf4/store/modules_metadata.json:    "ref_name": "multi/http/apache_rocketmq_update_config",
.msf4/store/modules_metadata.json:  "exploit_multi/http/apache_roller_ognl_injection": {
.msf4/store/modules_metadata.json:    "name": "Apache Roller OGNL Injection",
.msf4/store/modules_metadata.json:    "fullname": "exploit/multi/http/apache_roller_ognl_injection",
.msf4/store/modules_metadata.json:    "description": "This module exploits an OGNL injection vulnerability in Apache Roller < 5.0.2. The\n        vulnerability is due to an OGNL injection on the UIAction controller because of an\n        insecure usage of the ActionSupport.getText method. This module has been tested\n        successfully on Apache Roller 5.0.1 on Ubuntu 10.04.",
.msf4/store/modules_metadata.json:      "URL-http://security.coverity.com/advisory/2013/Oct/remote-code-execution-in-apache-roller-via-ognl-injection.html"
.msf4/store/modules_metadata.json:      "Apache Roller 5.0.1"
.msf4/store/modules_metadata.json:    "path": "/modules/exploits/multi/http/apache_roller_ognl_injection.rb",
.msf4/store/modules_metadata.json:    "ref_name": "multi/http/apache_roller_ognl_injection",
.msf4/store/modules_metadata.json:    "description": "DCNM exposes a file upload servlet (FileUploadServlet) at /fm/fileUpload.\n        An authenticated user can abuse this servlet to upload a WAR to the Apache Tomcat webapps\n        directory and achieve remote code execution as root.\n        This module exploits two other vulnerabilities, CVE-2019-1619 for authentication bypass on\n        versions 10.4(2) and below, and CVE-2019-1622 (information disclosure) to obtain the correct\n        directory for the WAR file upload.\n        This module was tested on the DCNM Linux virtual appliance 10.4(2), 11.0(1) and 11.1(1), and should\n        work on a few versions below 10.4(2). Only version 11.0(1) requires authentication to exploit\n        (see References to understand why).",
.msf4/store/modules_metadata.json:    "description": "Versions of Apache Log4j2 impacted by CVE-2021-44228 which allow JNDI features used in configuration,\n        log messages, and parameters, do not protect against attacker controlled LDAP and other JNDI related endpoints.\n\n        This module will exploit an HTTP end point with the Log4Shell vulnerability by injecting a format message that\n        will trigger an LDAP connection to Metasploit and load a payload.\n\n        The Automatic target delivers a Java payload using remote class loading. This requires Metasploit to run an HTTP\n        server in addition to the LDAP server that the target can connect to. The targeted application must have the\n        trusted code base option enabled for this technique to work.\n\n        The non-Automatic targets deliver a payload via a serialized Java object. This does not require Metasploit to\n        run an HTTP server and instead leverages the LDAP server to deliver the serialized object. The target\n        application in this case must be compatible with the user-specified JAVA_GADGET_CHAIN option.",
.msf4/store/modules_metadata.json:    "description": "This exploits an unauthenticated remote code execution vulnerability\n          that affects Zoho ManageEngine AdSelfService Plus versions 6210 and\n          below (CVE-2022-47966). Due to a dependency to an outdated library\n          (Apache Santuario version 1.4.1), it is possible to execute arbitrary\n          code by providing a crafted `samlResponse` XML to the ADSelfService Plus\n          SAML endpoint. Note that the target is only vulnerable if it has been\n          configured with SAML-based SSO at least once in the past, regardless of\n          the current SAML-based SSO status.",
.msf4/store/modules_metadata.json:    "description": "This exploits an unauthenticated remote code execution vulnerability\n          that affects Zoho ManageEngine ServiceDesk Plus versions 14003 and\n          below (CVE-2022-47966). Due to a dependency to an outdated library\n          (Apache Santuario version 1.4.1), it is possible to execute arbitrary\n          code by providing a crafted `samlResponse` XML to the ServiceDesk Plus\n          SAML endpoint. Note that the target is only vulnerable if it has been\n          configured with SAML-based SSO at least once in the past, regardless of\n          the current SAML-based SSO status.",
.msf4/store/modules_metadata.json:    "description": "Openfire is an XMPP server licensed under the Open Source Apache License.\n          Openfire's administrative console, a web-based application, was found to be vulnerable to a path traversal attack\n          via the setup environment. This permitted an unauthenticated user to use the unauthenticated Openfire Setup Environment\n          in an already configured Openfire environment to access restricted pages in the Openfire Admin Console reserved for\n          administrative users.\n          This module will use the vulnerability to create a new admin user that will be used to upload a Openfire management plugin\n          weaponised with java native payload that triggers an RCE.\n          This vulnerability affects all versions of Openfire that have been released since April 2015, starting with version 3.10.0.\n          The problem has been patched in Openfire release 4.7.5 and 4.6.8, and further improvements will be included in the\n          first version on the 4.8 branch, which is version 4.8.0.",
.msf4/store/modules_metadata.json:    "name": "Apache Shiro v1.2.4 Cookie RememberME Deserial RCE",
.msf4/store/modules_metadata.json:    "description": "This vulnerability allows remote attackers to execute arbitrary code on vulnerable\n          installations of Apache Shiro v1.2.4. Note that other versions of Apache Shiro may\n          also be exploitable if the encryption key used by Shiro to encrypt rememberMe\n          cookies is known.",
.msf4/store/modules_metadata.json:    "name": "Apache Solr Remote Code Execution via Velocity Template",
.msf4/store/modules_metadata.json:    "description": "This module exploits a vulnerability in Apache Solr <= 8.3.0 which allows remote code execution via a custom\n          Velocity template. Currently, this module only supports Solr basic authentication.\n\n          From the Tenable advisory:\n          An attacker could target a vulnerable Apache Solr instance by first identifying a list\n          of Solr core names. Once the core names have been identified, an attacker can send a specially crafted\n          HTTP POST request to the Config API to toggle the params resource loader value for the Velocity Response\n          Writer in the solrconfig.xml file to true. Enabling this parameter would allow an attacker to use the Velocity\n          template parameter in a specially crafted Solr request, leading to RCE.",
.msf4/store/modules_metadata.json:      "URL-https://www.tenable.com/blog/apache-solr-vulnerable-to-remote-code-execution-zero-day-vulnerability",
.msf4/store/modules_metadata.json:      "URL-https://github.com/AleWong/Apache-Solr-RCE-via-Velocity-template"
.msf4/store/modules_metadata.json:    "description": "This module exploits a vulnerability found in Dell SonicWALL Scrutinizer. The methodDetail\n        parameter in exporters.php allows an attacker to write arbitrary files to the file system\n        with an SQL Injection attack, and gain remote code execution under the context of SYSTEM\n        for Windows, or as Apache for Linux.\n\n        Authentication is required to exploit this vulnerability, but this module uses\n        the default admin:admin credential.",
.msf4/store/modules_metadata.json:    "description": "Spring Framework versions 5.3.0 to 5.3.17, 5.2.0 to 5.2.19, and older versions when running on JDK 9 or above\n          and specifically packaged as a traditional WAR and deployed in a standalone Tomcat instance are vulnerable\n          to remote code execution due to an unsafe data binding used to populate an object from request parameters\n          to set a Tomcat specific ClassLoader. By crafting a request to the application and referencing the\n          org.apache.catalina.valves.AccessLogValve class through the classLoader with parameters such as the following:\n          class.module.classLoader.resources.context.parent.pipeline.first.suffix=.jsp, an unauthenticated attacker can\n          gain remote code execution.",
.msf4/store/modules_metadata.json:    "name": "Apache Struts 2 Struts 1 Plugin Showcase OGNL Code Execution",
.msf4/store/modules_metadata.json:      "URL-https://cwiki.apache.org/confluence/display/WW/S2-048"
.msf4/store/modules_metadata.json:    "name": "Apache Struts Jakarta Multipart Parser OGNL Injection",
.msf4/store/modules_metadata.json:    "description": "This module exploits a remote code execution vulnerability in Apache Struts\n        version 2.3.5 - 2.3.31, and 2.5 - 2.5.10. Remote Code Execution can be performed\n        via http Content-Type header.\n\n        Native payloads will be converted to executables and dropped in the\n        server's temp dir. If this fails, try a cmd/* payload, which won't\n        have to write to the disk.",
.msf4/store/modules_metadata.json:      "URL-https://cwiki.apache.org/confluence/display/WW/S2-045"
.msf4/store/modules_metadata.json:    "name": "Apache Struts 2 Forced Multi OGNL Evaluation",
.msf4/store/modules_metadata.json:    "description": "The Apache Struts framework, when forced, performs double evaluation of attributes' values assigned to certain tags\n          attributes such as id. It is therefore possible to pass in a value to Struts that will be evaluated again when a\n          tag's attributes are rendered. With a carefully crafted request, this can lead to Remote Code Execution (RCE).\n\n          This vulnerability is application dependant. A server side template must make an affected use of request data to\n          render an HTML tag attribute.",
.msf4/store/modules_metadata.json:      "URL-https://cwiki.apache.org/confluence/display/WW/S2-059",
.msf4/store/modules_metadata.json:      "URL-https://cwiki.apache.org/confluence/display/WW/S2-061",
.msf4/store/modules_metadata.json:    "name": "Apache Struts 2 Namespace Redirect OGNL Injection",
.msf4/store/modules_metadata.json:    "description": "This module exploits a remote code execution vulnerability in Apache Struts\n        version 2.3 - 2.3.4, and 2.5 - 2.5.16. Remote Code Execution can be performed\n        via an endpoint that makes use of a redirect action.\n\n        Note that this exploit is dependant on the version of Tomcat running on\n        the target.  Versions of Tomcat starting with 7.0.88 currently don't\n        support payloads larger than ~7.5kb.  Windows Meterpreter sessions on\n        Tomcat >=7.0.88 are currently not supported.\n\n        Native payloads will be converted to executables and dropped in the\n        server's temp dir. If this fails, try a cmd/* payload, which won't\n        have to write to the disk.",
.msf4/store/modules_metadata.json:      "URL-https://lgtm.com/blog/apache_struts_CVE-2018-11776",
.msf4/store/modules_metadata.json:      "URL-https://cwiki.apache.org/confluence/display/WW/S2-057",
.msf4/store/modules_metadata.json:    "name": "Apache Struts 2 REST Plugin XStream RCE",
.msf4/store/modules_metadata.json:    "description": "Apache Struts versions 2.1.2 - 2.3.33 and Struts 2.5 - Struts 2.5.12,\n        using the REST plugin, are vulnerable to a Java deserialization attack\n        in the XStream library.",
.msf4/store/modules_metadata.json:      "URL-https://struts.apache.org/docs/s2-052.html",
.msf4/store/modules_metadata.json:      "URL-https://lgtm.com/blog/apache_struts_CVE-2017-9805_announcement",
.msf4/store/modules_metadata.json:    "name": "Apache Struts Remote Command Execution",
.msf4/store/modules_metadata.json:    "description": "This module exploits a remote command execution vulnerability in\n        Apache Struts versions < 2.2.0. This issue is caused by a failure to properly\n        handle unicode characters in OGNL extensive expressions passed to the web server.\n\n          By sending a specially crafted request to the Struts application it is possible to\n        bypass the \"#\" restriction on ParameterInterceptors by using OGNL context variables.\n        Bypassing this restriction allows for the execution of arbitrary Java code.",
.msf4/store/modules_metadata.json:    "name": "Apache Struts ClassLoader Manipulation Remote Code Execution",
.msf4/store/modules_metadata.json:    "description": "This module exploits a remote command execution vulnerability in Apache Struts versions\n        1.x (<= 1.3.10) and 2.x (< 2.3.16.2). In Struts 1.x the problem is related with\n        the ActionForm bean population mechanism while in case of Struts 2.x the vulnerability is due\n        to the ParametersInterceptor. Both allow access to 'class' parameter that is directly\n        mapped to getClass() method and allows ClassLoader manipulation. As a result, this can\n        allow remote attackers to execute arbitrary Java code via crafted parameters.",
.msf4/store/modules_metadata.json:      "URL-http://struts.apache.org/release/2.3.x/docs/s2-020.html",
.msf4/store/modules_metadata.json:    "name": "Apache Struts Remote Command Execution",
.msf4/store/modules_metadata.json:    "description": "This module exploits a remote command execution vulnerability in\n          Apache Struts versions < 2.2.1.1. This issue is caused because the\n          ExceptionDelegator interprets parameter values as OGNL expressions\n          during certain exception handling for mismatched data types of properties,\n          which allows remote attackers to execute arbitrary Java code via a\n          crafted parameter.",
.msf4/store/modules_metadata.json:    "name": "Apache Struts ParametersInterceptor Remote Code Execution",
.msf4/store/modules_metadata.json:    "description": "This module exploits a remote command execution vulnerability in Apache Struts\n        versions < 2.3.1.2. This issue is caused because the ParametersInterceptor allows\n        for the use of parentheses which in turn allows it to interpret parameter values as\n        OGNL expressions during certain exception handling for mismatched data types of\n        properties which allows remote attackers to execute arbitrary Java code via a\n        crafted parameter.",
.msf4/store/modules_metadata.json:      "URL-https://cwiki.apache.org/confluence/display/WW/S2-009"
.msf4/store/modules_metadata.json:    "name": "Apache Struts 2 DefaultActionMapper Prefixes OGNL Code Execution",
.msf4/store/modules_metadata.json:      "URL-http://struts.apache.org/release/2.3.x/docs/s2-016.html"
.msf4/store/modules_metadata.json:    "name": "Apache Struts 2 Developer Mode OGNL Execution",
.msf4/store/modules_metadata.json:    "description": "This module exploits a remote command execution vulnerability in Apache\n        Struts 2. The problem exists on applications running in developer mode,\n        where the DebuggingInterceptor allows evaluation and execution of OGNL\n        expressions, which allows remote attackers to execute arbitrary Java\n        code. This module has been tested successfully on Struts 2.3.16, Tomcat\n        7 and Ubuntu 10.04.",
.msf4/store/modules_metadata.json:      "URL-https://www.sec-consult.com/fxdata/seccons/prod/temedia/advisories_txt/20120104-0_Apache_Struts2_Multiple_Critical_Vulnerabilities.txt"
.msf4/store/modules_metadata.json:    "name": "Apache Struts Dynamic Method Invocation Remote Code Execution",
.msf4/store/modules_metadata.json:    "description": "This module exploits a remote command execution vulnerability in Apache Struts\n        version between 2.3.20 and 2.3.28 (except 2.3.20.2 and 2.3.24.2). Remote Code\n        Execution can be performed via method: prefix when Dynamic Method Invocation\n        is enabled.",
.msf4/store/modules_metadata.json:    "name": "Apache Struts REST Plugin With Dynamic Method Invocation Remote Code Execution",
.msf4/store/modules_metadata.json:    "description": "This module exploits a remote command execution vulnerability in Apache Struts\n        version between 2.3.20 and 2.3.28 (except 2.3.20.2 and 2.3.24.2). Remote Code\n        Execution can be performed when using REST Plugin with ! operator when\n        Dynamic Method Invocation is enabled.",
.msf4/store/modules_metadata.json:    "name": "Apache Struts includeParams Remote Code Execution",
.msf4/store/modules_metadata.json:    "description": "This module exploits a remote command execution vulnerability in Apache Struts\n        versions < 2.3.14.2. A specifically crafted request parameter can be used to inject\n        arbitrary OGNL code into the stack bypassing Struts and OGNL library protections.\n        When targeting an action which requires interaction through GET, the payload should\n        be split, taking into account the URI limits. In this case, if the rendered JSP has\n        more than one point of injection, it could result in payload corruption. This should\n        happen only when the payload is larger than the URI length.",
.msf4/store/modules_metadata.json:      "URL-https://cwiki.apache.org/confluence/display/WW/S2-014",
.msf4/store/modules_metadata.json:      "URL-http://struts.apache.org/development/2.x/docs/s2-013.html"
.msf4/store/modules_metadata.json:    "description": "This module uses a PUT request bypass to upload a jsp shell to a vulnerable Apache Tomcat configuration.",
.msf4/store/modules_metadata.json:      "URL-https://bz.apache.org/bugzilla/show_bug.cgi?id=61542",
.msf4/store/modules_metadata.json:    "name": "Apache Tomcat Manager Application Deployer Authenticated Code Execution",
.msf4/store/modules_metadata.json:    "description": "This module can be used to execute a payload on Apache Tomcat servers that\n        have an exposed \"manager\" application. The payload is uploaded as a WAR archive\n        containing a jsp application using a PUT request.\n\n        The manager application can also be abused using /manager/html/upload, but that\n        method is not implemented in this module.\n\n        NOTE: The compatible payload sets vary based on the selected target. For\n        example, you must select the Windows target to use native Windows payloads.",
.msf4/store/modules_metadata.json:      "URL-http://tomcat.apache.org/tomcat-5.5-doc/manager-howto.html"
.msf4/store/modules_metadata.json:    "name": "Apache Tomcat Manager Authenticated Upload Code Execution",
.msf4/store/modules_metadata.json:    "description": "This module can be used to execute a payload on Apache Tomcat servers that\n        have an exposed \"manager\" application. The payload is uploaded as a WAR archive\n        containing a jsp application using a POST request against the /manager/html/upload\n        component.\n\n        NOTE: The compatible payload sets vary based on the selected target. For\n        example, you must select the Windows target to use native Windows payloads.",
.msf4/store/modules_metadata.json:      "URL-http://tomcat.apache.org/tomcat-5.5-doc/manager-howto.html"
.msf4/store/modules_metadata.json:  "exploit_multi/misc/apache_activemq_rce_cve_2023_46604": {
.msf4/store/modules_metadata.json:    "name": "Apache ActiveMQ Unauthenticated Remote Code Execution",
.msf4/store/modules_metadata.json:    "fullname": "exploit/multi/misc/apache_activemq_rce_cve_2023_46604",
.msf4/store/modules_metadata.json:    "description": "This module exploits a deserialization vulnerability in the OpenWire transport unmarshaller in Apache\n          ActiveMQ. Affected versions include 5.18.0 through to 5.18.2, 5.17.0 through to 5.17.5, 5.16.0 through to\n          5.16.6, and all versions before 5.15.16.",
.msf4/store/modules_metadata.json:      "URL-https://exp10it.cn/2023/10/apache-activemq-%E7%89%88%E6%9C%AC-5.18.3-rce-%E5%88%86%E6%9E%90/",
.msf4/store/modules_metadata.json:      "URL-https://activemq.apache.org/security-advisories.data/CVE-2023-46604-announcement.txt"
.msf4/store/modules_metadata.json:    "path": "/modules/exploits/multi/misc/apache_activemq_rce_cve_2023_46604.rb",
.msf4/store/modules_metadata.json:    "ref_name": "multi/misc/apache_activemq_rce_cve_2023_46604",
.msf4/store/modules_metadata.json:    "name": "Apache OpenOffice Text Document Malicious Macro Execution",
.msf4/store/modules_metadata.json:    "description": "This module generates an Apache OpenOffice Text Document with a malicious macro in it.\n        To exploit successfully, the targeted user must adjust the security level in Macro\n        Security to either Medium or Low. If set to Medium, a prompt is presented to the user\n        to enable or disable the macro. If set to Low, the macro can automatically run without\n        any warning.\n\n        The module also works against LibreOffice.",
.msf4/store/modules_metadata.json:      "Apache OpenOffice on Windows (PSH)",
.msf4/store/modules_metadata.json:      "Apache OpenOffice on Linux/OSX (Python)"
.msf4/store/modules_metadata.json:    "description": "This module exploits the ContentKeeper Web Appliance. Versions prior\n        to 125.10 are affected. This module exploits a combination of weaknesses\n        to enable remote command execution as the Apache user. By setting\n        SkipEscalation to false, this module will attempt to setuid the bash shell.",
.msf4/store/modules_metadata.json:      "URL-http://spamassassin.apache.org/advisories/cve-2006-2447.txt"
.msf4/store/modules_metadata.json:    "description": "This module exploits an arbitrary file upload in the sample PHP upload\n        handler for blueimp's jQuery File Upload widget in versions <= 9.22.0.\n\n        Due to a default configuration in Apache 2.3.9+, the widget's .htaccess\n        file may be disabled, enabling exploitation of this vulnerability.\n\n        This vulnerability has been exploited in the wild since at least 2015\n        and was publicly disclosed to the vendor in 2018. It has been present\n        since the .htaccess change in Apache 2.3.9.\n\n        This module provides a generic exploit against the jQuery widget.",
.msf4/store/modules_metadata.json:      "URL-https://httpd.apache.org/docs/current/mod/core.html#allowoverride"
.msf4/store/modules_metadata.json:    "description": "This module exploits a vulnerability in MoinMoin 1.9.5. The vulnerability\n        exists on the manage of the twikidraw actions, where a traversal path can be used\n        in order to upload arbitrary files. Exploitation is achieved on Apached/mod_wsgi\n        configurations by overwriting moin.wsgi, which allows to execute arbitrary python\n        code, as exploited in the wild on July, 2012. This module is \"ManualRanking,\" and\n        the user is warned to use this module at his own risk since it will overwrite the\n        moin.wsgi file, required for the correct working of the MoinMoin wiki. While the\n        exploit will try to restore the attacked application at post exploitation, successful\n        restoration cannot be guaranteed.",
.msf4/store/modules_metadata.json:    "description": "This module exploits a vulnerability found in Project Pier.  The application's\n        uploading tool does not require any authentication, which allows a malicious user\n        to upload an arbitrary file onto the web server, and then cause remote code\n        execution by simply requesting it. This module is known to work against Apache\n        servers due to the way it handles an extension name, but the vulnerability may\n        not be exploitable on others.",
.msf4/store/modules_metadata.json:    "description": "This module exploits a PHP code injection in SPIP. The vulnerability exists in the\n        connect parameter and allows an unauthenticated user to execute arbitrary commands\n        with web user privileges. Branches 2.0, 2.1 and 3 are concerned. Vulnerable versions\n        are <2.0.21, <2.1.16 and < 3.0.3, but this module works only against branch 2.0 and\n        has been tested successfully with SPIP 2.0.11 and SPIP 2.0.20 with Apache on Ubuntu\n        and Fedora linux distributions.",
.msf4/store/modules_metadata.json:    "description": "This module exploits a command injection vulnerability in WordPress\n        version 4.6 with Exim as an MTA via a spoofed Host header to PHPMailer,\n        a mail-sending library that is bundled with WordPress.\n\n        A valid WordPress username is required to exploit the vulnerability.\n        Additionally, due to the altered Host header, exploitation is limited to\n        the default virtual host, assuming the header isn't mangled in transit.\n\n        If the target is running Apache 2.2.32 or 2.4.24 and later, the server\n        may have HttpProtocolOptions set to Strict, preventing a Host header\n        containing parens from passing through, making exploitation unlikely.",
.msf4/store/modules_metadata.json:      "URL-https://httpd.apache.org/docs/2.4/mod/core.html#httpprotocoloptions"
.msf4/store/modules_metadata.json:  "exploit_windows/http/apache_activemq_traversal_upload": {
.msf4/store/modules_metadata.json:    "name": "Apache ActiveMQ 5.x-5.11.1 Directory Traversal Shell Upload",
.msf4/store/modules_metadata.json:    "fullname": "exploit/windows/http/apache_activemq_traversal_upload",
.msf4/store/modules_metadata.json:    "description": "This module exploits a directory traversal vulnerability (CVE-2015-1830) in Apache\n          ActiveMQ 5.x before 5.11.2 for Windows.\n\n          The module tries to upload a JSP payload to the /admin directory via the traversal\n          path /fileserver/..\\admin\\ using an HTTP PUT request with the default ActiveMQ\n          credentials admin:admin (or other credentials provided by the user). It then issues\n          an HTTP GET request to /admin/<payload>.jsp on the target in order to trigger the\n          payload and obtain a shell.",
.msf4/store/modules_metadata.json:      "URL-https://activemq.apache.org/security-advisories.data/CVE-2015-1830-announcement.txt"
.msf4/store/modules_metadata.json:    "path": "/modules/exploits/windows/http/apache_activemq_traversal_upload.rb",
.msf4/store/modules_metadata.json:    "ref_name": "windows/http/apache_activemq_traversal_upload",
.msf4/store/modules_metadata.json:  "exploit_windows/http/apache_chunked": {
.msf4/store/modules_metadata.json:    "name": "Apache Win32 Chunked Encoding",
.msf4/store/modules_metadata.json:    "fullname": "exploit/windows/http/apache_chunked",
.msf4/store/modules_metadata.json:    "description": "This module exploits the chunked transfer integer wrap\n        vulnerability in Apache version 1.2.x to 1.3.24. This\n        particular module has been tested with all versions of the\n        official Win32 build between 1.3.9 and 1.3.24. Additionally,\n        it should work against most co-branded and bundled versions\n        of Apache (Oracle 8i, 9i, IBM HTTPD, etc).\n\n        You will need to use the Check() functionality to determine\n        the exact target version prior to launching the exploit. The\n        version of Apache bundled with Oracle 8.1.7 will not\n        automatically restart, so if you use the wrong target value,\n        the server will crash.",
.msf4/store/modules_metadata.json:      "Apache.org Build 1.3.9->1.3.19",
.msf4/store/modules_metadata.json:      "Apache.org Build 1.3.22->1.3.24",
.msf4/store/modules_metadata.json:      "Apache.org Build 1.3.19->1.3.24",
.msf4/store/modules_metadata.json:      "Apache.org Build 1.3.22",
.msf4/store/modules_metadata.json:      "Apache.org Build 1.3.17->1.3.24 (Windows 2000)",
.msf4/store/modules_metadata.json:      "Apache.org Build 1.3.17->1.3.24 (Windows NT)",
.msf4/store/modules_metadata.json:      "Oracle 8.1.7 Apache 1.3.12",
.msf4/store/modules_metadata.json:      "Oracle 9.1.0 Apache 1.3.12",
.msf4/store/modules_metadata.json:      "Oracle 9.2.0 Apache 1.3.22",
.msf4/store/modules_metadata.json:    "path": "/modules/exploits/windows/http/apache_chunked.rb",
.msf4/store/modules_metadata.json:    "ref_name": "windows/http/apache_chunked",
.msf4/store/modules_metadata.json:  "exploit_windows/http/apache_mod_rewrite_ldap": {
.msf4/store/modules_metadata.json:    "name": "Apache Module mod_rewrite LDAP Protocol Buffer Overflow",
.msf4/store/modules_metadata.json:    "fullname": "exploit/windows/http/apache_mod_rewrite_ldap",
.msf4/store/modules_metadata.json:    "description": "This module exploits the mod_rewrite LDAP protocol scheme handling\n        flaw discovered by Mark Dowd, which produces an off-by-one overflow.\n        Apache versions 1.3.29-36, 2.0.47-58, and 2.2.1-2 are vulnerable.\n        This module requires REWRITEPATH to be set accurately. In addition,\n        the target must have 'RewriteEngine on' configured, with a specific\n        'RewriteRule' condition enabled to allow for exploitation.\n\n        The flaw affects multiple platforms, however this module currently\n        only supports Windows based installations.",
.msf4/store/modules_metadata.json:    "path": "/modules/exploits/windows/http/apache_mod_rewrite_ldap.rb",
.msf4/store/modules_metadata.json:    "ref_name": "windows/http/apache_mod_rewrite_ldap",
.msf4/store/modules_metadata.json:  "exploit_windows/http/apache_modjk_overflow": {
.msf4/store/modules_metadata.json:    "name": "Apache mod_jk 1.2.20 Buffer Overflow",
.msf4/store/modules_metadata.json:    "fullname": "exploit/windows/http/apache_modjk_overflow",
.msf4/store/modules_metadata.json:      "mod_jk 1.2.20 (Apache 1.3.x/2.0.x/2.2.x) (any win32 OS/language)"
.msf4/store/modules_metadata.json:    "path": "/modules/exploits/windows/http/apache_modjk_overflow.rb",
.msf4/store/modules_metadata.json:    "ref_name": "windows/http/apache_modjk_overflow",
.msf4/store/modules_metadata.json:  "exploit_windows/http/apache_tika_jp2_jscript": {
.msf4/store/modules_metadata.json:    "name": "Apache Tika Header Command Injection",
.msf4/store/modules_metadata.json:    "fullname": "exploit/windows/http/apache_tika_jp2_jscript",
.msf4/store/modules_metadata.json:    "description": "This module exploits a command injection vulnerability in Apache\n        Tika 1.15 - 1.17 on Windows.  A file with the image/jp2 content-type is\n        used to bypass magic bytes checking.  When OCR is specified in the\n        request, parameters can be passed to change the parameters passed\n        at command line to allow for arbitrary JScript to execute. A\n        JScript stub is passed to execute arbitrary code. This module was\n        verified against version 1.15 - 1.17 on Windows 2012.\n        While the CVE and finding show more versions vulnerable, during\n        testing it was determined only > 1.14 was exploitable due to\n        jp2 support being added.",
.msf4/store/modules_metadata.json:      "URL-https://rhinosecuritylabs.com/application-security/exploiting-cve-2018-1335-apache-tika/",
.msf4/store/modules_metadata.json:      "URL-https://lists.apache.org/thread.html/b3ed4432380af767effd4c6f27665cc7b2686acccbefeb9f55851dca@%3Cdev.tika.apache.org%3E",
.msf4/store/modules_metadata.json:    "path": "/modules/exploits/windows/http/apache_tika_jp2_jscript.rb",
.msf4/store/modules_metadata.json:    "ref_name": "windows/http/apache_tika_jp2_jscript",
.msf4/store/modules_metadata.json:      "Windows Apache 2.2 - WebLogic module version 1.0.1136334",
.msf4/store/modules_metadata.json:      "Windows Apache 2.2 - WebLogic module version 1.0.1150354"
.msf4/store/modules_metadata.json:    "name": "Oracle Weblogic Apache Connector POST Request Buffer Overflow",
.msf4/store/modules_metadata.json:    "description": "This module exploits a stack based buffer overflow in the BEA\n        Weblogic Apache plugin.\n\n        The connector fails to properly handle specially crafted HTTP POST\n        requests, resulting a buffer overflow due to the insecure usage\n        of sprintf.  Currently, this module works over Windows systems without DEP,\n        and has been tested with Windows 2000 / XP.\n\n        In addition, the Weblogic Apache plugin version is fingerprinted with a POST\n        request containing a specially crafted Transfer-Encoding header.",
.msf4/store/modules_metadata.json:      "BEA WebLogic 8.1 SP6 - mod_wl_20.so / Apache 2.0 / Windows [XP/2000]",
.msf4/store/modules_metadata.json:      "BEA WebLogic 8.1 SP5 - mod_wl_20.so / Apache 2.0 / Windows [XP/2000]",
.msf4/store/modules_metadata.json:      "BEA WebLogic 8.1 SP4 - mod_wl_20.so / Apache 2.0 / Windows [XP/2000]"
.msf4/store/modules_metadata.json:    "description": "This module exploits a stack based buffer overflow in the BEA\n        Weblogic Apache plugin.  This vulnerability exists in the\n        error reporting for unknown Transfer-Encoding headers.\n        You may have to run this twice due to timing issues with handlers.",
.msf4/store/modules_metadata.json:      "Windows Apache 2.2 version Universal"
.msf4/store/modules_metadata.json:    "description": "This module exploits an unauthenticated SQLi in Cayin xPost <=2.5.  The\n          wayfinder_meeting_input.jsp file's wayfinder_seqid parameter can be injected\n          with a blind SQLi.  Since this app bundles MySQL and apache Tomcat the\n          environment is pretty static and therefore the default settings should\n          work.  Results in SYSTEM level access.\n          Only the java/jsp_shell_reverse_tcp and java/jsp_shell_bind_tcp payloads\n          seem to be valid.",
.msf4/store/modules_metadata.json:    "description": "This exploits an unauthenticated remote code execution vulnerability\n          that affects Zoho ManageEngine Endpoint Central and MSP versions 10.1.2228.10\n          and below (CVE-2022-47966). Due to a dependency to an outdated library\n          (Apache Santuario version 1.4.1), it is possible to execute arbitrary\n          code by providing a crafted `samlResponse` XML to the Endpoint Central\n          SAML endpoint. Note that the target is only vulnerable if it is\n          configured with SAML-based SSO , and the service should be active.",
.msf4/store/modules_metadata.json:  "exploit_windows/http/php_apache_request_headers_bof": {
.msf4/store/modules_metadata.json:    "name": "PHP apache_request_headers Function Buffer Overflow",
.msf4/store/modules_metadata.json:    "fullname": "exploit/windows/http/php_apache_request_headers_bof",
.msf4/store/modules_metadata.json:    "description": "This module exploits a stack based buffer overflow in the CGI version of PHP\n        5.4.x before 5.4.3. The vulnerability is due to the insecure handling of the\n        HTTP headers.\n\n          This module has been tested against the thread safe version of PHP 5.4.2,\n        from \"windows.php.net\", running with Apache 2.2.22 from \"apachelounge.com\".",
.msf4/store/modules_metadata.json:    "path": "/modules/exploits/windows/http/php_apache_request_headers_bof.rb",
.msf4/store/modules_metadata.json:    "ref_name": "windows/http/php_apache_request_headers_bof",
.msf4/store/modules_metadata.json:    "name": "Apache Tomcat CGIServlet enableCmdLineArguments Vulnerability",
.msf4/store/modules_metadata.json:    "description": "This module exploits a vulnerability in Apache Tomcat's CGIServlet component. When the\n        enableCmdLineArguments setting is set to true, a remote user can abuse this to execute\n        system commands, and gain remote code execution.",
.msf4/store/modules_metadata.json:      "URL-https://wwws.nightwatchcybersecurity.com/2019/04/30/remote-code-execution-rce-in-cgi-servlet-apache-tomcat-on-windows-cve-2019-0232/",
.msf4/store/modules_metadata.json:      "URL-https://blog.trendmicro.com/trendlabs-security-intelligence/uncovering-cve-2019-0232-a-remote-code-execution-vulnerability-in-apache-tomcat/"
.msf4/store/modules_metadata.json:      "Apache Tomcat 9.0 or prior for Windows"
.msf4/store/modules_metadata.json:    "description": "This module exploits a vulnerability in IBM's WebSphere Application Server. An unsafe deserialization\n        call of unauthenticated Java objects exists to the Apache Commons Collections (ACC) library, which allows\n        remote arbitrary code execution. Authentication is not required in order to exploit this vulnerability.",
.msf4/store/modules_metadata.json:    "description": "Spawn a shell on the established connection to\n        the webserver.  Unfortunately, this payload\n        can leave conspicuous evil-looking entries in the\n        apache error logs, so it is probably a good idea\n        to use a bind or reverse shell unless firewalls\n        prevent them from working.  The issue this\n        payload takes advantage of (CLOEXEC flag not set\n        on sockets) appears to have been patched on the\n        Ubuntu version of Apache and may not work on\n        other Debian-based distributions.  Only tested on\n        Apache but it might work on other web servers\n        that leak file descriptors to child processes.",
.msf4/store/modules_metadata.json:  "post_linux/gather/apache_nifi_credentials": {
.msf4/store/modules_metadata.json:    "name": "Apache NiFi Credentials Gather",
.msf4/store/modules_metadata.json:    "fullname": "post/linux/gather/apache_nifi_credentials",
.msf4/store/modules_metadata.json:    "description": "This module will grab Apache NiFi credentials from various files on Linux.",
.msf4/store/modules_metadata.json:      "URL-https://nifi.apache.org/docs/nifi-docs/html/administration-guide.html#nifi_sensitive_props_key"
.msf4/store/modules_metadata.json:    "path": "/modules/post/linux/gather/apache_nifi_credentials.rb",
.msf4/store/modules_metadata.json:    "ref_name": "linux/gather/apache_nifi_credentials",
.msf4/store/modules_metadata.json:    "description": "This module collects configuration files found on commonly installed\n          applications and services, such as Apache, MySQL, Samba, Sendmail, etc.\n          If a config file is found in its default path, the module will assume\n          that is the file we want.",
.msf4/store/modules_metadata.json:    "name": "Windows Gather Apache Tomcat Enumeration",
.msf4/store/modules_metadata.json:    "description": "This module will collect information from a Windows-based Apache Tomcat. You will get\n          information such as: The installation path, Tomcat version, port, web applications,\n          users, passwords, roles, etc.",
grep: .msf4/bootsnap_cache/bootsnap/load-path-cache: binary file matches
.cache/zcompdump:'apache2ctl' '_apachectl'
.cache/zcompdump:'apachectl' '_apachectl'
.cache/zcompdump:            _ansible _ant _antiword _apachectl _apm \
grep: .cache/mozilla/firefox/djprqdvp.default-esr/cache2/entries/CBA1EFBC2FDD9E976567D15BC9A93EFBD27B8BC8: binary file matches
grep: .cache/mozilla/firefox/djprqdvp.default-esr/cache2/entries/5CD931CB7762F2EA8AAEA3FB6FCE90BC89EBBDF4: binary file matches

</pre>
</details>

![2024-04-13_23-55](https://github.com/Veliquu/Tunkeutumistestaus_2024/assets/92360351/62f4804a-c4c1-4a92-a66d-a3323caa8ee3)

Tekstiä tulee paljon ja kaikki apacheen liittyvät maininnat näyttävät olevan json metadataa.

## i) Anna esimerkit nmap ajonaikaisista toiminnosta. (man nmap: runtime interaction)

En saanut mistään kuvaa, koska nmap skannaus oli niin nopea, että en kerennyt painamaan mitään.

- v/V Nostaa/laskee tarkkuustasoa, eli kuinka paljon tietoa skannauksen aikana skannauksesta näkyy
- d/D Nostaa/laskee vianmääritystason tasoa
- p/P Kytkee päälle/pois pakettien jäljityksen
- ? Tulostaa ajoajan vuorovaikutusohjeiden näytön

## Lähteet
Antti Halonen [https://github.com/therealhalonen/penetration_testing/blob/master/h1/report.md](https://github.com/therealhalonen/penetration_testing/blob/master/h1/report.md)  
db_nmap [https://gist.github.com/fabionoth/ba46407d9cd03144150225715697c47f](https://gist.github.com/fabionoth/ba46407d9cd03144150225715697c47f)  
Kali linux [https://www.kali.org/get-kali/#kali-platforms](https://www.kali.org/get-kali/#kali-platforms)  
man grep [https://man7.org/linux/man-pages/man1/grep.1.html](https://man7.org/linux/man-pages/man1/grep.1.html)  
man nmap [https://linux.die.net/man/1/nmap](https://linux.die.net/man/1/nmap)  
Metasploitable [https://sourceforge.net/projects/metasploitable/](https://sourceforge.net/projects/metasploitable/)  
Tero Karvinen [https://terokarvinen.com/2024/eettinen-hakkerointi-2024/](https://terokarvinen.com/2024/eettinen-hakkerointi-2024/)  
