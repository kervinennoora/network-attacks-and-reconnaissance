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

## Lähteet

Karvinen, T. 2025. Verkkoon tunkeutuminen ja tiedustelu. Saatavilla: https://terokarvinen.com/verkkoon-tunkeutuminen-ja-tiedustelu.

Karvinen, T. 2025 h2 - Lempiväri: Violetti. Saatavilla: https://terokarvinen.com/verkkoon-tunkeutuminen-ja-tiedustelu/#h2-lempivari-violetti

Bianco, D. 2013. Pyramid of pain. Saatavilla: https://detect-respond.blogspot.com/2013/03/the-pyramid-of-pain.html.

Hitchins, E. et al. 2011. Cyber Kill Chain. Saatavilla: https://detect-respond.blogspot.com/2013/03/the-pyramid-of-pain.html.

Caltagirone, S et al. 2013. Diamond Model. Saatavilla: https://detect-respond.blogspot.com/2013/03/the-pyramid-of-pain.html.

MITRE. s.a. ATT&CK. Saatavilla: https://attack.mitre.org/.
