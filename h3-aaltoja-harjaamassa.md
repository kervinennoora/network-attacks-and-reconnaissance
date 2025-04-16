# h3 - Aaltoja harjaamassa

## x) Lue ja tiivistä

### Hubacek 2019

- Ennen radioliikenteen kaappaamista kannattaa varmistaa onko tajuus oikea.
- Tutkiessa kaapattuja aaltoja, ei kannata kuunnella suoraan aallon korkeimmalta kohdalta.
- Tämän jälkeen videossa kaapataan aaltoja 433 MHz taajuudelta, samalla kun painetaan kaukosäätimen nappia.
- Kun kaappaus on tallennettu, se analysoidaan. Ensin täytyy vaihtaa oikea modulaatio.
- Kannattaa myös tarkistaa onko yhden bitin pituus melkein sama kuin arvioita bitin pituus.
- Videon lopussa näytetään kaapatut aallot myös Hexinä.

### Cornelius 2022

- Artikkelissa analysoidaan sääasemaa.
- Ekana käytössä oli rtl_433 työkalu, joka tulkitsi signaalin Nexus-TH protokollaksi.
- Tarkempaan analyysiin käytettiin Universal Radio Hacker (URH) -ohjelmaa.
- Analyysin perusteella on mahdoollisuus rakentaa oma sensori esim. Arduinolla ja 433 MHz -lähettimellä.
- 433 MHz sääsensorin signaalin voi purkaa ja jäljitellä ilman virallista dokumentaatiota käyttäen ohjelmistoradiota ja avoimia työkaluja.

## a) WebSDR

![image](https://github.com/user-attachments/assets/eb026cbe-f2a1-43e6-acdc-ec39bfb930f1)

Tätä tehtävää varten kuuntelin radiota joka sijaitsee Cornwall, Englannissa. Kuunellessa käytin CW modulaatiota ja taajuus oli 10489751.37 kHz. Jos tulkitsen kuvaa oikein, aallon pituus on 0.09 kHz. 

## b) rtl_433

![image](https://github.com/user-attachments/assets/e90f91cd-5ba0-4ade-984b-de4a3ffc6629)

Asennetaan rtl_433 merbanan ohjeilla. Ensin päivitin koneen komennolla ``sudo apt-get update`` ja tämän jälkeen asensin ohjelman komennolla ``sudo apt-get install rtl-433``. Lopuksi kokeilaan, onnistuiko asennus.

![image](https://github.com/user-attachments/assets/f007ad06-0106-40ef-877d-4828e5cf6a59)

Rtl_433 vastasi takaisin.

## c) Automaattinen analyysi

Ladataan analysoitava paketti.

![image](https://github.com/user-attachments/assets/413038e2-cdf2-433e-99be-e9dae00f8812)

Siirryin Downloads kansioon jonka jälkeen avasin näytteen komennolla ``rtl_433 -r Converted_433.92M_2000k.cs8``.

![image](https://github.com/user-attachments/assets/784e96c8-1537-4fc9-b7c0-f34da30162c0)

Näytteessä toistuu modelit *Nexa-Security*, *Proove-Security* ja *KlikAanKlikUit-Switch*. Osassa näytteistä ei ole id-numeroa, osassa toistuu sama *8785315*. Molempien security modelien state on off ja nw tulevat kanavalta 3. Nexan house koodi on *8785315* eli sama kuin id-numero. 


## d) Too complex 16?

Ladataan näyte tehtävänannosta.

![image](https://github.com/user-attachments/assets/bfda70bb-ac76-4362-989e-2916e808ea35)

## e) Ultimate

### f) Yleiskuva

### g) Bittistä

## Lähteet

Karvinen. T. 2025. Verkkoon tunkeutuminen ja tiedustelu. Saatavilla: https://terokarvinen.com/verkkoon-tunkeutuminen-ja-tiedustelu/.

Karvinen, T. 2025. h3 - Aaltoja harjaamassa. Saatavilla: https://terokarvinen.com/verkkoon-tunkeutuminen-ja-tiedustelu/#h3-aaltoja-harjaamassa.

Hubacek. 2019. Universal Radio Hacker SDR Tutorial on 433 MHz radio plugs. 3:19-7:40. Saatavilla: https://www.youtube.com/watch?v=sbqMqb6FVMY&t=199s.

Cornelius. 2022. Decode 433.92 MHz weather station data https://www.onetransistor.eu/2022/01/decode-433mhz-ask-signal.html
