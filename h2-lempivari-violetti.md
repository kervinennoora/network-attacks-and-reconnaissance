# h2 - Lempiväri: violetti
## x) Lue ja vastaa kysymyksiin

### Bianco 2013
Pyramid of Pain osoittaa, että jotkin hyökkäyksen tunnusmerkit aiheuttavat hyökkääjille enemmän haittaa kuin toiset.
Tämä johtuu siitä, että kun tietyt tunnusmerkit estetään, niiden menetys on hyökkääjälle kivuliaampi kuin toisten.

### Caltagirone et al 2013
Diamond malli kuvaa hyökkääjän toimintaa tapahtumina, jotka yhdistetään aktiviteettiketjuiksi hyökkäysprosessin analysoimiseksi.
Näitä ketjuja voidaan ryhmitellä ja hyödyntää torjuntastrategioiden suunnittelussa.
## a) Apache log

Aloitetaan lataamalla Apache Kali-koneelle käyttäen koemntoja ``sudo apt-get update`` ja ``sudo apt-get install apache2``.

![image](https://github.com/user-attachments/assets/a2bf39d2-b26d-49c1-a4a2-925421b621f5)

Käynnistetään Apache komennolla ``sudo systemctl start apache2``.

Surffataan oletuswebbisivua komennolla ``curl http://localhost``.

![image](https://github.com/user-attachments/assets/f9f57d47-4a0a-4de3-ac3b-3f8a9e6bf86c)

Tutkitaan ja tulkitaan tämä Apachen lokista. Ensin siirrytään kansioon */var/log/apache2/*, käyttäen komentoa ``cd /var/log/apache2/``. Tämän jälkeen katsotaan logia komennolla ``cat access.log``.

![image](https://github.com/user-attachments/assets/5ad26a46-e45d-44ea-abf1-37b22f34aff4)

Tutkitaan curlauksen lokiriviä tarkemmin.

![image](https://github.com/user-attachments/assets/60ff47ef-397f-414a-a0ae-22651c4d0d1e)

Lokista ilmenee heti alkuun päivämäärä ja aika. Tämän perässä on IPv6 osoite. Seuraavana siitä ilmenee HTTP GET -pyyntö juuripolkuun. Lisäksi siinä on statuskoodi 200 joka tarkoittaa sitä, että pyyntö on onnistunut ja palvelin vastasi. kohta "-" tarkoittaa, että pyyntö tehtiin suoraan. Ja viimeisenä meille selviää, että pyyntö tehtiin curlin avulla ja curlista on käytössä versio 8.12.1.

## b) Nmapped

Seuraavaksi porttiskannataan oletuswebbisivua portista 80. Ensin kuitenkin varmistetaan ettei kone ole yhteydessä internettiin. 

![image](https://github.com/user-attachments/assets/efbe84f6-1f30-4d71-8098-d772a5a68ccf)

Kun kone ei ole yhteydessä internettiin, voidaan skannata portti 80 komennolla ``sudo nmap -A localhost``.

![image](https://github.com/user-attachments/assets/10be4e70-9041-43fc-a81d-3e30c1c743d3)

Skannauksesta selviää, että kohteena on *localhost* jonka IP-osoite on 127.0.0.1.  Skannauksessa ei näy 999 muuta suljettua porttia ainoastaan portti 80 on skannattu. Portista 80 löytyy Apache httpd 2.4.63 palvelu. Lisäksi Ilmoitetaan HTTP-otsikko "Apache2 Debian Default Page: It works" eli oletussivun otsikko. Lopuksi selviää järjestelmätiedot eli; Linux OS, tarkemmin LInux 5.0-6.2 ja että kyseessä on paikallinen skannaus (Network Distance: 0 hops).

## c) Skriptit

![image](https://github.com/user-attachments/assets/2113a65e-34a1-4fbc-bde4-b6096ec7fefc)

Sieltä löytyy skirptit *_http-server-header:* ja *_http-tittle*.

## d) Jäljet lokissa

Etsitään webbipalvelimen lokeista jäljet porttiskannauksesta komennolla ``grep "Nmap Scripting Engine" /var/log/apache2/access.log``.

![image](https://github.com/user-attachments/assets/f6e23126-e5ee-4e58-99d6-64f086b1f6f7)

Nmap kirjoitetaan isolla alkukirjaimella. Kuintekin HTTPS-osoitteessa se kirjoitetaan kokonaan pienellä  (https://nmap.org/book/nse.html). Komennolla ``grep -i "nmap" /var/log/apache2/access.log`` löytää porttiskannauksen isommastakin lokista. 

## e) Wire Sharking


Aloitetaan avaamalla Wireshark.

![image](https://github.com/user-attachments/assets/bd7c5f8f-edb8-4dcb-87dc-2c84dec8a740)

Valitaan loopback adapteri ja siepataan verkkoliikennettä. Terminaalissa käytin komentoa ``nmap -A localhot``. Tallennetaan siepatut paketit .pcap tiedostona. 

![image](https://github.com/user-attachments/assets/8edff3a7-7a6f-4e12-aa17-c44a9265a67d)

Tutkitaan siepattuja paketteja tarkemmin. Etsitään kohdat joissa lukee nmap käyttäen filtteriä ``tcp.port == 80 || tcp contains "nmap"``.

![image](https://github.com/user-attachments/assets/30ebdd8d-739b-4b4c-834e-464dcf22a408

Filtterin avulla näemme ainoastaan portin 80 liikenteen. Paketti 55 on TCP pyyntö joka varmistaa onko portti 80 auki. Lähde ja kohde ovat samassa osoitteessa eli kyseessä paikallinen liikenne. Paketin pituus on 58 tavua.

Paketti 56 on myös paikallisen liikenteen paketti. Paketissa Apache kertoo, että portti 80 on auki. Tämän paketin pituus on 54 tavua. 


## f) Net Grep

Tarkistetaan onko ngrep asennettu Kali-koneelle. 

![image](https://github.com/user-attachments/assets/99613585-d200-4c73-b94d-a326ac99d323)

Se olikin jo valmiiksi asennettuna joten voimme kaapata liikennettä komennolla ``sudo ngrep -d lo -i nmap"

![image](https://github.com/user-attachments/assets/a9bc8d4a-d135-4094-9ab0-2e3979043e39)

Jos ymmärsin tehtävänannon oikein tässä kaappauksessa näkyy kaikki missä mainitaan nmap. 


## g) Agentti

Kokeilin tehtävää seuraavalla monsteri komennolla jonka löysin internetin syöveristä ``nmap -p 80 --script http-title --script-args http.useragent="Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/120.0.0.0 Safari/537.36" localhost``.

![image](https://github.com/user-attachments/assets/dc8f9507-6bff-47db-afcb-7db788dd3a50)


## h) Pienemmät jäljet

Aloitetaan skannaamalla portti silloin kun kone ei ole yhteydessä internettiin komennolla ``nmap -A localhots``. Tämän jälkeen tutkitaan lokia.

![image](https://github.com/user-attachments/assets/fe1d0cf0-e128-41e6-89fa-55481b73dfdc)

Lokista puuttuu kohta *Nmap Scripting Engine*.

Seuraavakis tutkitaan siepattu verkkoliikenne.

![image](https://github.com/user-attachments/assets/9ee741c5-91ce-4b14-b10a-3543d6b63300)

Sieppauksessa näkyy ainoastaan TCP ja HTTP protokollien liikennettä, verrattuuna aiempaan missä oli monia protokollia.

## i) Hieman vaikeampi: LoWeR ChEcK

Valitettavasti aikataulutus syistä en kerkeä tehtä tätä tehtävää ennen 24h palautusrajaa. Lisään sen kuiten myöhemmin tähän dokumenttiin. 

## Lähteet

Karvinen, T. 2025. Verkkoon tunkeutuminen ja tiedustelu. Saatavilla: https://terokarvinen.com/verkkoon-tunkeutuminen-ja-tiedustelu.

Karvinen, T. 2025 h2 - Lempiväri: Violetti. Saatavilla: https://terokarvinen.com/verkkoon-tunkeutuminen-ja-tiedustelu/#h2-lempivari-violetti

Bianco, D. 2013. Pyramid of pain. Saatavilla: https://detect-respond.blogspot.com/2013/03/the-pyramid-of-pain.html.

Hitchins, E. et al. 2011. Cyber Kill Chain. Saatavilla: https://detect-respond.blogspot.com/2013/03/the-pyramid-of-pain.html.

Caltagirone, S et al. 2013. Diamond Model. Saatavilla: https://detect-respond.blogspot.com/2013/03/the-pyramid-of-pain.html.

MITRE. s.a. ATT&CK. Saatavilla: https://attack.mitre.org/.

Alagos, M. 2023. Cange your user agent in web pentests and bug bounties. Saatavilla: https://mrtalagoz.medium.com/change-your-user-agent-in-web-pentests-bug-bounties-dont-be-a-plain-jane-98b442a0c601.
