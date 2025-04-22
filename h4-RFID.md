# h4 - RFID

## 1) Tarkastele käytössäsi olevia RFID tuotteita, mieti miten hyvin olet suojautunut RFID urkinnalta?

Itselläni on melkein päivittäin käytössä kulkukortti ja lähiluettavat kortit. Kulukortit ovat tuttuja myös työssäni, sillä niiden avulla pääsee vain henkilökunnalle tarkoitettuihin tiloihin. 
Periaatteessa se ei ole arkisessa käytössä, mutta talossamme asuu kaksi sirutettua kissaa. Kulkukortti ja lähiluettavat kortit ovat RFID-lompakossa, jonka avulla pyrin välttämään urkintaa. 
Työpaikan kulkukorttia en kuljeta mukanani ellei kyseessä ole työpäivä. Työpäivän aikana se on roikkumassa kaulastani eli mitään erityistä suojausta sille ei ole. 
Pyrin olemaan varovainen urkintaa vastaan ja koen onnistuneeni siinä hyvin, sillä tähän mennessä ei ole käynyt ilmi, että RFID tuotteitani olisi urkittu.

## 2) Tutustu APDU komentojen rakenteeseen (voit käyttää tekoälyä tutustumiseen)

APDU (Application Protocol Data Unit) on viestintäprotokolla, jota käytetään älykorttien ja lukijalaitteen välisessä kommunikoinnissa. APDU-protokolla on standardoitu ISO/IEC 7816-4 -standardiin.
PDU-komennot noudattavat tarkkoja binäärimuotoja, ja ne koostuvat lukijan komennosta (Command APDU) ja kortin vastauksesta (Response APDU).
**Lukijan komento** koostuu pakkolisista ja valinnaisista kentistä. Pakollisia kenttiä ovat komentoluokka, komento koodi, parametri 1 ja parametri 2. Valinnaisia ovat kentät jotka sisältävät dataa tai pituustietoja. 
Esimerkiksi lähetettävän datan pituus ja odotetun vastauksen enimmäis pituus.
**Kortin vastaus** koostuu datasta ja tilakoodista. Data on kortin palauttamaa tietoa ja tilakoodi kertoo onnistumisesta tai epäonnistumisesta. 

## 3) Tutki ja kerro minkä mielenkiintoisen RFID hakkerointi uutiset löysit. 

Löysin The Guardian lehdestä artikkelin brittiläisistä korkeakouluopiskelijoista, jotka skannasivat 

## Lähteet

Iso-Anttila, L. 2025. Kotiläksyt. Luettavissa: https://hhmoodle.haaga-helia.fi/course/view.php?id=42566&section=1#tabs-tree-start.

CardLogix Corporation. s.a. Application Protocol Data Unit (APDU). Luettavissa: https://www.cardlogix.com/glossary/apdu-application-protocol-data-unit-smart-card/. 

Grossman, W. 2013. Is UK college's RFID chip tracking of pupils an invasion of privacy? The Guardian. Luettavissa: https://www.theguardian.com/technology/2013/nov/19/college-rfid-chip-tracking-pupils-invasion-privacy.
