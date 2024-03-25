# Tcpdump
Aloitin asentamalla wiresharkin tietokoneelle komennolla:
```bash
[jesse@archlinux ~]$ yay -S tcpdump
```
Tämän jälkeen sieppasin 10 pakettia. F5 painammalla githubin profiilin sivulla saan näkymään liikennettä oman koneen ja githubin välillä.
![tcpdump](https://github.com/Veliquu/Tunkeutumistestaus_2024/assets/92360351/99faa32b-91c8-47d2-b18d-35cd040c731b)
Rivien alusta näemme aikaleimat kaapatuille paketeille.  
Tämän jälkeen näemme pakettien protokollat. Tässä tapauksessa jokaisella paketilla on `IP` mikä tarkoittaa sitä, että ne ovat `ipv4` prootokollia. Mikäli jokin paketti näyttäisi `IP6` olisi nämä `ipv6` protokollia.
Seuraavaksi näemme Lähde osoitteen, jota seuraa kohde.
```bash
esim 10:23:05.391105 IP archlinux.36020 > lb-140-82-121-3-fra.github.com.https: Flags [P.], seq 865:904, ack 1, win 3573, options [nop,nop,TS val 2787728731 ecr 3099635735], length 39
```
Tämän jälkeen näemme mitä paketteja lähetetään.  
esimimerkiksi githubiin lähetetyissä paketeissa:  
Esinmmäisen paketin Flags `[P.]` on `Push Aknowledgement` paketti.  
Tähän github vastaa `[.]` joka on `Aknowledgement` paketti.  
Nämä näyttävät meille sen, että koneelta lähtee pyyntö githubiin ja koska verkko on toiminnassa saamme vastauksen githubilta.
Tämän jälkeen näkyy sekvenssi numero joka on muodossa `ensimmäinen:viimeinen`  
esim.  
Ensimmäisen paketin sekvenssi numero on `865:904`. Ensimmäinen paketti sai kaksi vastausta joista ensimmäisen tunnistin numero on `865` ja toisen `904`  
Viimeisenä näkyy payload datan pituus.
Sekvenssi numerot eivät nyt ole täysin itsellä muistissa mitä ne kertoo.

Lähteet;  
[https://terokarvinen.com/2024/eettinen-hakkerointi-2024/]  
[https://linuxize.com/post/tcpdump-command-in-linux/] 
