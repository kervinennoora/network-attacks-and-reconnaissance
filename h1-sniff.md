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

## Lähteet
Karvinen, T. 2025. Verkkoon tunkeutuminen ja tiedustelu - Network Attacks and Reconnaissence. Saatavila: https://terokarvinen.com/verkkoon-tunkeutuminen-ja-tiedustelu/.

Karvinen, T. 2025. h1 - Sniff. Saatavilla: https://terokarvinen.com/verkkoon-tunkeutuminen-ja-tiedustelu/#h1-sniff.

Karvinen, T. 2025. Wireshark - Getting Started. Saatavilla: https://terokarvinen.com/wireshark-getting-started/.

Karvinen, T. 2025. Network Interface Names on Linux. Saatavilla: https://terokarvinen.com/network-interface-linux/.
