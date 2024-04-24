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
## Karvinen 2023: [Find Hidden Web Directories - Fuzz URLs with ffuf](https://terokarvinen.com/2023/fuzz-urls-find-hidden-directories/)
- Web-palvelimet piilottavat salaisia hakemistoja, joita ei ole linkitetty mistään.
- 
## Karvinen 2022: [Cracking Passwords with Hashcat](https://terokarvinen.com/2022/cracking-passwords-with-hashcat/)
## Karvinen 2023: [Crack File Password With John](https://terokarvinen.com/2023/crack-file-password-with-john/)

# a) Asenna Hashcat ja testaa sen toiminta murtamalla esimerkkisalasana.
Avasain Kalin ja päivitin ensin järjestelmän.
```bash
$ sudo apt update && sudo apt upgrade
```
Tämän jälkeen asensin hashcatin.
```bash
$ sudo apt install hashcat 
```
Seuraavaksi loin kansion hashcatille.
```bash
$ mkdir hashcat  
```
Tutustuin hashcatin käyttöön [tältä](https://www.stationx.net/how-to-use-hashcat/) sivustolta.  
Täällä mainittiin, että hashcat tulee Kalilla valmiiksi sanalistojen kanssa ja ne löytyvät `/usr/share/wordlist/`. Kopion tämän kansion luomaani kansioon.  
![2024-04-22_18-24](https://github.com/Veliquu/Tunkeutumistestaus_2024/assets/92360351/f6cf14f3-51f5-4fa0-bde6-b517c42ecb12)

Tämä kansio sisälsi `rockyou.txt.gz` tiedoston, jonka purin `gzip -d rockyou.txt.gz`. Tämän jälkeen pystyin tarkastelemaan tekstitiedostoa.  
![2024-04-22_18-36](https://github.com/Veliquu/Tunkeutumistestaus_2024/assets/92360351/4259d4ff-3483-46d7-91f3-02890f427c37)

Seuraavaksi kokeilin murtaa esimerkkisalasanan Tero Karvisen [hashcat](https://terokarvinen.com/2022/cracking-passwords-with-hashcat/) artikkelin perusteella.  
```bash
$ hashid -m 6b1628b016dff46e6fa35684be6acc96
Analyzing '6b1628b016dff46e6fa35684be6acc96'
[+] MD2 
[+] MD5 [Hashcat Mode: 0]
[+] MD4 [Hashcat Mode: 900]
[+] Double MD5 [Hashcat Mode: 2600]
[+] LM [Hashcat Mode: 3000]
[+] RIPEMD-128 
[+] Haval-128 
[+] Tiger-128 
[+] Skein-256(128) 
[+] Skein-512(128) 
[+] Lotus Notes/Domino 5 [Hashcat Mode: 8600]
[+] Skype [Hashcat Mode: 23]
[+] Snefru-128 
[+] NTLM [Hashcat Mode: 1000]
[+] Domain Cached Credentials [Hashcat Mode: 1100]
[+] Domain Cached Credentials 2 [Hashcat Mode: 2100]
[+] DNSSEC(NSEC3) [Hashcat Mode: 8300]
[+] RAdmin v2.x [Hashcat Mode: 9900]
```
Karvisen artikkelissa mainitaan, että oikea hashcat parametri murtamiseen on yleensä kolmen ensimmäisen vaihtoehdon seassa.  
Artikkelissa kokeillaan murtamista MD5 parametrilla, käyttäen komentoa `hashcat -m 0 '6b1628b016dff46e6fa35684be6acc96' rockyou.txt -o solved`. Komennossa `-m 0` määrittelee parametrin jota käytetään, `'6b1628b016dff46e6fa35684be6acc96'` on se mitä halutaan murtaa ja `-o solved` tallentaa tuloksen tyhjään tiedostoon `solved`.  
Kokeilin tätä samaa itse.  
```bash
$ hashcat -m 0 '6b1628b016dff46e6fa35684be6acc96' rockyou.txt -o solved
hashcat (v6.2.6) starting

OpenCL API (OpenCL 3.0 PoCL 5.0+debian  Linux, None+Asserts, RELOC, SPIR, LLVM 16.0.6, SLEEF, DISTRO, POCL_DEBUG) - Platform #1 [The pocl project]
==================================================================================================================================================
* Device #1: cpu-sandybridge-AMD Ryzen 7 5800H with Radeon Graphics, 1439/2943 MB (512 MB allocatable), 4MCU

Minimum password length supported by kernel: 0
Maximum password length supported by kernel: 256

Hashes: 1 digests; 1 unique digests, 1 unique salts
Bitmaps: 16 bits, 65536 entries, 0x0000ffff mask, 262144 bytes, 5/13 rotates
Rules: 1

Optimizers applied:
* Zero-Byte
* Early-Skip
* Not-Salted
* Not-Iterated
* Single-Hash
* Single-Salt
* Raw-Hash

ATTENTION! Pure (unoptimized) backend kernels selected.
Pure kernels can crack longer passwords, but drastically reduce performance.
If you want to switch to optimized kernels, append -O to your commandline.
See the above message to find out about the exact limits.

Watchdog: Temperature abort trigger set to 90c

Host memory required for this attack: 0 MB

Dictionary cache built:
* Filename..: rockyou.txt
* Passwords.: 14344392
* Bytes.....: 139921507
* Keyspace..: 14344385
* Runtime...: 1 sec

                                                          
Session..........: hashcat
Status...........: Cracked
Hash.Mode........: 0 (MD5)
Hash.Target......: 6b1628b016dff46e6fa35684be6acc96
Time.Started.....: Mon Apr 22 18:46:08 2024 (0 secs)
Time.Estimated...: Mon Apr 22 18:46:08 2024 (0 secs)
Kernel.Feature...: Pure Kernel
Guess.Base.......: File (rockyou.txt)
Guess.Queue......: 1/1 (100.00%)
Speed.#1.........:    24672 H/s (0.05ms) @ Accel:256 Loops:1 Thr:1 Vec:8
Recovered........: 1/1 (100.00%) Digests (total), 1/1 (100.00%) Digests (new)
Progress.........: 1024/14344385 (0.01%)
Rejected.........: 0/1024 (0.00%)
Restore.Point....: 0/14344385 (0.00%)
Restore.Sub.#1...: Salt:0 Amplifier:0-1 Iteration:0-1
Candidate.Engine.: Device Generator
Candidates.#1....: 123456 -> bethany
Hardware.Mon.#1..: Util: 21%

Started: Mon Apr 22 18:45:47 2024
Stopped: Mon Apr 22 18:46:09 2024

```
Yläpuolella näkyy komento ja sen tulos.  
Murtaminen onnistui ja voimme tarkistaa tämän tarkistelemalla `solved` tiedostoa.
![2024-04-22_18-49](https://github.com/Veliquu/Tunkeutumistestaus_2024/assets/92360351/56ac3583-a3db-4394-a75e-7d55dd2acf6c)

# b) Salainen, mutta ei multa. Ratkaise dirfuzt-1 artikkelista Karvinen 2023: [Find Hidden Web Directories - Fuzz URLs with ffuf](https://terokarvinen.com/2023/fuzz-urls-find-hidden-directories/)
Aloitin tekemällä `dirfutz-0` artikkelin esimerkin mukaisesti. 
Latasin ja käynnistin `dirfutz-0`.
```bash
$ wget https://terokarvinen.com/2023/fuzz-urls-find-hidden-directories/dirfuzt-0
$ chmod u+x dirfuzt-0
$ ./dirfuzt-0
Learn more at TeroKarvinen.com
http://127.0.0.2:8000
```
Tarkistin, että toimii menemällä verkkoselaimessa osoitteeseen `http://127.0.0.2:8000`.  
![2024-04-22_19-15](https://github.com/Veliquu/Tunkeutumistestaus_2024/assets/92360351/05dd2ab3-aff5-4030-b674-851c6773dff2)
Seuraavaksi asennettiin fuff.  
```bash
$ wget https://github.com/ffuf/ffuf/releases/download/v2.0.0/ffuf_2.0.0_linux_amd64.tar.gz
$ tar -xf ffuf_2.0.0_linux_amd64.tar.gz
$ ./ffuf
```
Seuraavaksi asensin [Seclist](https://github.com/danielmiessler/SecLists/tree/master) sanalistat.
```bash
$ sudo apt -y install seclists
```
Tämän jälkeen ajoin fuffin komennolla `$ ./ffuf -w /usr/share/seclists/Discovery/Web-Content/common.txt  -u http://127.0.0.2:8000/FUZZ` 
- `./fuff` käynnistää fuffin
- `-w /usr/share/seclists/Discovery/Web-Content/common.txt` määrittää käytettävän sanalistan.
- `-u http://127.0.0.2:8000/FUZZ` on kohdeosoite

Aluksi tuli paljon tekstiä, joten lisäsin komennon perään `-ac`, joka määrittää automaattisesti suodattimet osumien perusteella.  
```bash
$ ./ffuf -w /usr/share/seclists/Discovery/Web-Content/common.txt -u http:

        /'___\  /'___\           /'___\       
       /\ \__/ /\ \__/  __  __  /\ \__/       
       \ \ ,__\\ \ ,__\/\ \/\ \ \ \ ,__\      
        \ \ \_/ \ \ \_/\ \ \_\ \ \ \ \_/      
         \ \_\   \ \_\  \ \____/  \ \_\       
          \/_/    \/_/   \/___/    \/_/       

       v2.0.0
________________________________________________

 :: Method           : GET
 :: URL              : http://127.0.0.2:8000/FUZZ
 :: Wordlist         : FUZZ: /usr/share/seclists/Discovery/Web-Content/comm
 :: Follow redirects : false
 :: Calibration      : true
 :: Timeout          : 10
 :: Threads          : 40
 :: Matcher          : Response status: 200,204,301,302,307,401,403,405,500
________________________________________________

[Status: 200, Size: 160, Words: 10, Lines: 11, Duration: 0ms]
    * FUZZ: admin

[Status: 301, Size: 64, Words: 3, Lines: 3, Duration: 0ms]
    * FUZZ: render/https://www.google.com

:: Progress: [4727/4727] :: Job [1/1] :: 0 req/sec :: Duration: [0:00:00] :
   ```
Löydettiin admin ja render, ja kokeiltiin selaimessa vielä `http://127.0.0.2:8000/admin`  
![2024-04-22_20-32](https://github.com/Veliquu/Tunkeutumistestaus_2024/assets/92360351/0daf1ba4-00cb-4818-87df-dc324fe7e1f6)  
Tässä välissä uudelleen käynnistin virtuaalikoneen ja latasin ja käynnistin `dirfutz-1`
```bash
$ wget https://terokarvinen.com/2023/fuzz-urls-find-hidden-directories/dirfuzt-1
$ chmod u+x dirfuzt-1
$ ./dirfuzt-1
Learn more at TeroKarvinen.com
http://127.0.0.2:8000
```
Tarkistin selaimesta, että toimii.  
![2024-04-22_20-45](https://github.com/Veliquu/Tunkeutumistestaus_2024/assets/92360351/f133929d-d51e-4acb-961f-5cf04a8619b3)  
Seuraavaksi ajoin saman komennon fuffilla:
```bash
$ ./ffuf -w /usr/share/seclists/Discovery/Web-Content/common.txt  -u http://127.0.0.2:8000/FUZZ -ac
```
Tämä antoi seuraavan tuloksen.
```bash
$ ./ffuf -w /usr/share/seclists/Discovery/Web-Content/common.txt  -u http://127.0.0.2:8000/FUZZ -ac

        /'___\  /'___\           /'___\       
       /\ \__/ /\ \__/  __  __  /\ \__/       
       \ \ ,__\\ \ ,__\/\ \/\ \ \ \ ,__\      
        \ \ \_/ \ \ \_/\ \ \_\ \ \ \ \_/      
         \ \_\   \ \_\  \ \____/  \ \_\       
          \/_/    \/_/   \/___/    \/_/       

       v2.0.0
________________________________________________

 :: Method           : GET
 :: URL              : http://127.0.0.2:8000/FUZZ
 :: Wordlist         : FUZZ: /usr/share/seclists/Discovery/Web-Content/common.txt
 :: Follow redirects : false
 :: Calibration      : true
 :: Timeout          : 10
 :: Threads          : 40
 :: Matcher          : Response status: 200,204,301,302,307,401,403,405,500
________________________________________________

:: Progress: [1/4727] :: Job [1/1] :: 0 req/sec :: Duration: [0:00:00] :: [Status: 200, Size: 178, Words: 6, Lines: 11, Duration: 1ms]
    * FUZZ: .git/HEAD

:: Progress: [41/4727] :: Job [1/1] :: 0 req/sec :: Duration: [0:00:00] ::[Status: 200, Size: 178, Words: 6, Lines: 11, Duration: 0ms]
    * FUZZ: .git/index

:: Progress: [41/4727] :: Job [1/1] :: 0 req/sec :: Duration: [0:00:00] ::[Status: 200, Size: 178, Words: 6, Lines: 11, Duration: 1ms]
    * FUZZ: .git/config

:: Progress: [41/4727] :: Job [1/1] :: 0 req/sec :: Duration: [0:00:00] ::[Status: 301, Size: 41, Words: 3, Lines: 3, Duration: 1ms]
    * FUZZ: .git

:: Progress: [41/4727] :: Job [1/1] :: 0 req/sec :: Duration: [0:00:00] ::[Status: 200, Size: 178, Words: 6, Lines: 11, Duration: 1ms]
    * FUZZ: .git/logs/

:: Progress: [41/4727] :: Job [1/1] :: 0 req/sec :: Duration: [0:00:00] ::[Status: 301, Size: 64, Words: 3, Lines: 3, Duration: 0ms]
    * FUZZ: render/https://www.google.com

:: Progress: [3536/4727] :: Job [1/1] :: 0 req/sec :: Duration: [0:00:00] :: Progress: [4394/4727] :: Job [1/1] :: 0 req/sec :: Duration: [0:00:00] [Status: 200, Size: 182, Words: 6, Lines: 11, Duration: 0ms]
    * FUZZ: wp-admin

:: Progress: [4595/4727] :: Job [1/1] :: 0 req/sec :: Duration: [0:00:00] :: Progress: [4727/4727] :: Job [1/1] :: 0 req/sec :: Duration: [0:00:00] :: Progress: [4727/4727] :: Job [1/1] :: 0 req/sec :: Duration: [0:00:00] :: Errors: 0 ::
```
Löydettiin wp-admin ja .git ja näitä kokeiltiin nettiselaimessa. `http://127.0.0.2:8000/wp-admin` ja `http://127.0.0.2:8000/.git`  
![2024-04-22_20-50](https://github.com/Veliquu/Tunkeutumistestaus_2024/assets/92360351/cf34156d-c494-4cf3-9adc-5482e61245ad)  
Ratkaisut löydettiin.


# c) Asenna John the Ripper ja testaa sen toiminta murtamalla jonkin esimerkkitiedoston salasana.
Aloitin asentamisen [tämän](https://terokarvinen.com/2023/crack-file-password-with-john/) artikkelin mukaan.  
Ensin päivittettiin järjestelmä: `sudo apt update && sudo apt upgrade` ja tämän jälkeen asennettiin artikkelin mukaan tarvittavat sovellukset.
```bash
sudo apt-get -y install micro bash-completion git build-essential libssl-dev zlib1g zlib1g-dev zlib-gst libbz2-1.0 libbz2-dev atool zip wget
```
Muuten kaikki asentui mutta yski errori tuli:
```bash
E: Unable to locate package zlib-gst
```
Googlettamalla en löytänyt paketille vastinetta Kalissa, eikä löytynyt muutenkaan selkää vastausta kyseiseen pakettiin liittyen Kalissa. Jatkoin eteenpäin.  
Seuraavaksi asennettiin John the Ripper.  
Ensin hain ladattiin se gitillä.
```bash
$ git clone --depth=1 https://github.com/openwall/john.git
```
Tämän jälkeen siirryin luotuun kansioon ja siellä `src`, jonka jälkeen ajoin `./configure` 
```bash
$ cd john/src/	
$ ./configure
```
![2024-04-23_18-48](https://github.com/Veliquu/Tunkeutumistestaus_2024/assets/92360351/779d5c97-3a3f-4826-b714-be3fc2c12130)  
Configurointi onnistui ja ajoin seuraavaksi `$ make -s clean && make -sj4` ohjeen mukaan.  
Tämän jälkeen siirryin hakemistoon `/john/run` ja ajoin John the Ripper ohjelman komennolla `./john`.   
![2024-04-23_19-01](https://github.com/Veliquu/Tunkeutumistestaus_2024/assets/92360351/56dde7d7-36e9-4197-a577-a622f17dd640)
Toimii.  
Seuraavaksi latasin artikkelissa käytetyn esimerkki salasanalla suojatun zip. tiedoston, jotta voi kokeilla murtaa sen.  
```bash
$ wget https://TeroKarvinen.com/2023/crack-file-password-with-john/tero.zip
```
Kokeilin purkaa zip tiedoston, mutta se haluaa salasanan.  
![2024-04-23_19-14](https://github.com/Veliquu/Tunkeutumistestaus_2024/assets/92360351/dd8cbe16-cdd5-4700-ad43-ee5ca0376744)  
Seuraavaksi kokeillaan purkaa salasanan tiivistelmä John the Ripperillä.
Ensikis 

# d) Fuffme. Asenna [Ffufme harjoitusmaali](https://terokarvinen.com/2023/fuffme-web-fuzzing-target-debian/) paikallisesti omalle koneellesi. Ratkaise tehtävät (kaikki paitsi ei "Content Discovery - Pipes")

## Basic Content Discovery

## Content Discovery With Recursion

## Content Discovery With File Extensions

## No 404 Status

## Param Mining

## Rate Limited

## Subdomains - Virtual Host Enumeration

# e) Tee msfvenom-työkalulla haittaohjelma, joka soittaa kotiin (reverse shell). Ota yhteys vastaan metasploitin multi/handler -työkalulla.

## Haittaohjelma ei saa olla automaattisesti leviävä. Msfvenom tekee tunnilla opetelluilla asetuksilla ohjelman, joka avaa reverse shellin, kun sen ajaa, mutta joka ei leviä eikä tee muutenkaan mitään itsestään.

## Raporttiin riittävät pelkät komennot haitakkeen tekemiseen, itse binääriä ei ole pakko laittaa verkkoon. Mikäli laitat binäärin verkkoon, pakkaa se salakirjoitettuun zip-pakettiin ja laita salasanaksi "infected". Latauslinkin yhteydessä on oltava selkeä varoitus siitä, että binääriä ei tule ajaa oikeilla koneilla. Salasanan voit halutessasi kertoa varoitusten yhteydessä.

# f) Asenna Windows virtuaalikoneeseen. Voi olla esimerkiksi Metasploitable 3 tai Microsoftin sivuilta saatava ilmainen kokeiluversio.

# g) Ota Windowsiin graafinen etähallintayhteys Linuxista. Käytä RDP:tä eli Remote Desktop Protocol.

# Lähteet
Sationx: [https://www.stationx.net/how-to-use-hashcat/](https://www.stationx.net/how-to-use-hashcat/)  
