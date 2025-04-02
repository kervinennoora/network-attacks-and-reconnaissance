# h1 - Sniff

## x) Lue ja tiivistä
### Karvinen 2025
- Kyseisessä artikkelissa käydään läpi kuinka asennetaan Wireshark Linux pohjaiselle koneelle.
- Wiresharkilla voi kaapata liikennettä ja tarkastella tilastoja.
- Asennusosuuden jälkeen ohjeen mukaan voi sniffata liikennettä.
- Lopuksi artikkelissa on ohje sniffauspakettien asennukseen
### Karvinen 2025
- Artikkelissa käsitellään verkkoliittymiä ja niiden nimiä.
- Liittymän etuliite nykyaikaisissa Linuxjärjestelmissä:
    - en - Langallinen Ethernet
    - wl - WLAN, Langaton lähierkko, Wifi
    - lo - Loopback-sovitin
 
- Esimerkkejä yleisistä verkkoliittymistä:
    - wlp4s0 - Wifi-kortti
    - enp1s0 - Langallinen Ethernet-kortti
    - lo - Loopback-sovitin
    - enx738899738899 - Langallinen Ethernet-kortti. "x":n jälkeinen numero on kortin MAC-osoite.
 
- Omat verkkoliittymät voi tarkastaa komennoilla
    - ``ip a``
    - ``ip route``
## a) Linux

Ohitan tämän kohdan raportoinnin, sillä Linuxin asennus on minulle tuttua ja sitä tehdessä ei ilmestynyt ongelmia. 

## b) Ei voi kalastaa

Avattuani Kali koneen pingasin Googlea komennolla ``ping 8.8.8.8`` ja sain vastauksen. Irroitin virtuaalikoneen verkosta ja pingasin uudelleen. Tällä kertaa se ei onnistunut.

![image](https://github.com/user-attachments/assets/35df6320-0c89-4f61-988a-4b87ab997a2e)

## c) Wireshark

Asennetaan virtuaalikonelle Wireshark. Asennuksessa hyödynsin Karvisen artikkelia Wiresharkin asennuksesta.

Asennuksessa käytettiin komentoja ``sudo apt-get update`` ja ``sudo-apt get install wireshark`` . Avatakseni Wiresharkin käytin komentoja ``newgrp wireshark`` ja ``wireshark``.

![image](https://github.com/user-attachments/assets/a08b4e25-c81f-47a4-ae39-8a9abdbe1b28)

Testasin sniffausta pingaamalla Googleen.

![image](https://github.com/user-attachments/assets/ba9815fa-4bc6-4808-95b3-da50e99260e2)

## d) Oikeesti TCP/IP

Pingatessa verkkoliikennettä käytin komentoa ``wget https://example.com``.
Wireshark on mielstäni hyvä siitä syystä, että eri paketit ovat väri koodattuja.

![image](https://github.com/user-attachments/assets/aa920cfe-b1fa-40dd-9daa-74a2dca0e5de)

Sinisellä taustalla oleva DNS paketti on osa sovelluskerrosta. Vihreällä taustalla näkyy TCP, joka on osa "kuljetuskerrosta". Pinkkiä taustaa vasten löytyy ICMPv6 paketit, jotka ovat osa internet-kerrosta. Verkko/linkki-kerroksen paketit löytyivät valitessa yksi paketti tarkempaan tarkasteluun.

![image](https://github.com/user-attachments/assets/cc3798b4-96eb-441e-adc4-ee8bd3491832)

Kuvassa näkyy lähdeosoite ja kohdeosoite.

## e) Mitäs tuli surffailtua? 

Surfing-secure.pcapin avulla selvisi, että kaappauksissa on kaksi konetta. Silmään minulla pistää TCP, DNS, ICMP ja HTTP protokollat. Kaappaus oli noin 20 pakettia pitkä eli todella lyhyt. 

## g) Minkä merkkinen verkkokortti käyttäjällä on?

![image](https://github.com/user-attachments/assets/401ad5b8-e27b-41be-b7d5-7b087fd65501)

Kyseessä on Loopback-sovitin

## h) Millä weppipalvelimella käyttäjä on surffaillut?

Kaappauksesta ilmenee, että käyttäjä on vieraillut DNS-palvelimella.

![image](https://github.com/user-attachments/assets/c29a4b1b-97ee-4287-83e7-f2b922b6df44)

## i) Analyysi

Analysoitavat paketit:

![image](https://github.com/user-attachments/assets/3256cc62-65f8-492d-9825-c6174e0d106e)

**Kuvassa näkyy:**
- Rivillä yksi lähetetään broadcast pyyntöä.
- Rivillä kaksi vastataan pyyntöön.
ICMP liikenne:
- Rivillä kolme näkyy, että pingataan osoitteeseen 8.8.8.8
- Rivit 7,8 ja 9 viittaa siihen, että pingataan edelleen osoitteeseen 8.8.8.8
- Riveillä 4 ja 6 näkyy ICMPv6 paketteja, jotka yrittävät multicastilla ottaa yhteyttä muihin IPv6 verkossa oleviin paketteihin.


## Lähteet
Karvinen, T. 2025. Verkkoon tunkeutuminen ja tiedustelu - Network Attacks and Reconnaissence. Saatavila: https://terokarvinen.com/verkkoon-tunkeutuminen-ja-tiedustelu/.

Karvinen, T. 2025. h1 - Sniff. Saatavilla: https://terokarvinen.com/verkkoon-tunkeutuminen-ja-tiedustelu/#h1-sniff.

Karvinen, T. 2025. Wireshark - Getting Started. Saatavilla: https://terokarvinen.com/wireshark-getting-started/.

Karvinen, T. 2025. Network Interface Names on Linux. Saatavilla: https://terokarvinen.com/network-interface-linux/.
