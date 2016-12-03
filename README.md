HOJ-harjoitustyö, osa I, syksy 2016
SUMMAUSPALVELU SOKETEILLA

Työn tarkoituksena on harjoitella TCP- ja UDP-sokettien sekä säikeiden käyttöä Javalla. Työn voi tehdä 2–3 hengen ryhmissä. Ryhmien välillä on lupa keskustella työn ratkaisuun liittyvistä ongelmista periaatteellisella tasolla, mutta kaikenlainen koodin välittäminen on tiukasti kielletty. Myös ryhmäkoko 4 on mahdollinen, jos toteuttaa itse palvelimen Y. Työn voi tehdä myös muulla kielellä kuin Javalla, mutta tuolloin tulee itse toteuttaa Y.

Ryhmien kokoonpano tulee ilmoittaa ohjaajalle viimeistään 13.11.2016 (sampsa.rauti@utu.fi).
Tehtävänä on tehdä sovellus X, joka tarjoaa lukujen summauspalvelua erikseen määritellyn palvelimen Y käyttöön. Palvelin Y on valmiiksi toteutettu ja sen yhteyteen on määritelty protokolla, jonka avulla summauspalvelua tarjoava sovellus X voi ottaa siihen yhteyttä. Protokolla toimii seuraavasti:

1. Sovellus X ottaa yhteyttä UDP-protokollalla palvelimen Y porttiin 3126 välittäen yhden UDP-paketin, joka sisältää TCP-portin numeron, johon palvelimen Y halutaan ottavan yhteyttä ja jota sovellus X kuuntelee.

2. Palvelin Y ottaa yhteyden ilmaistuun porttiin z koneessa, josta UDP-pyyntö tuli 1...5 sekunnin kuluessa pyynnön lähettämisestä. Jos sovellus X ei saa tällaista TCP-pohjaista yhteydenottoa ko. ajan puitteissa, tulee sen lähettää edellisen kohdan UDP-viesti uudestaan. Viiden epäonnistuneen yrityskerran jälkeen sovelluksen X tulee lopettaa itsensä.

3. Kun TCP-yhteys on muodostunut X:n ja Y:n välille, keskustelu niiden välillä tapahtuu jatkossa oliovirtaa (ObjectInputStream / ObjectOutputStream) käyttäen. Kyseisessä virrassa välitetään vain kokonaislukuja. Ensin palvelin Y ilmoittaa X:lle kokonaisluvun t väliltä 2...10. Jos tällaista lukua ei tule 5 sekunnin kuluessa, tulee X:n lopettaa itsensä hallitusti välitettyään ensin luvun -1 palvelimelle Y.

4. Sovellus X vastaa lähettämällä takaisin t kappaletta kokonaislukuja P1, P2,..., Pt, jotka ovat sellaisten porttien numeroita, joissa sovelluksen X hallinnoimat summauspalvelijat toimivat.

5. Saatuaan tietää porttinumerot P1, P2,…, Pt, palvelin Y työllistää kyseisiä summauspalvelijoita välittämällä niille oliovirran yli kokonaislukuja. Välitettävien lukujen määrää ei tiedetä etukäteen. Palvelin Y välittää kullekin summauspalvelijalle lukusarjan, jonka viimeinen luku on nolla. Kun summauspalvelija vastaanottaa luvun nolla, sen tulee lopettaa itsensä ja sulkea yhteys palvelimeen Y. Summauspalvelijat eivät välitä mitään tietoa suoraan palvelimelle Y, vaan ne kartuttavat välitettyjen lukujen summaa ja lukumäärää sovelluksen X “osoittamaan” paikkaan. X osoittaa kullekin summauspalvelijalle “lokerot”, jonne ne voivat kerätä ko. tietoja.

6. Samalla kun palvelin Y työllistää summauspalvelijoita, se voi kysyä sovellukselta X kolmenlaista tietoa: (1) mikä on tähän mennessä välitettyjen lukujen kokonaissumma, (2) mille summauspalvelijalle välitettyjen lukujen summa on suurin ja (3) mikä on tähän mennessä kaikille summauspalvelimille välitettyjen lukujen kokonaismäärä. Edelliset utelut palvelin Y tekee välittämällä X:lle niiden välisen oliovirran yli kokonaisluvun 1, 2 tai 3 (vastaavasti). Sovelluksen X tulee vastata takaisin sen hetkisen tilanteen mukaisella kokonaisluvulla. Jos sovellus X saa tässä utelutilassa palvelimelta Y jonkin muun numeron kuin 1, 2, 3 tai 0 (selitys seuraavassa kohdassa), niin sen tulee vastata takaisin luvulla −1.

7. Palvelin Y voi suorittaa edellisiä kyselyitä useita ja osa summauspalvelijoista voi kysymyssarjan aikana päättyä (koska Y on välittänyt niille nollan). Kun palvelin Y päättää lopettaa X:n tarjoaman palvelun käytön, se välittää X:lle luvun nolla. Sen seurauksena sovelluksen X tulee sulkea TCP-yhteys palvelimeen Y, lopettaa mahdollisesti kesken olevat summauspalvelijat ja lopulta itse sovelluksen X suorituksen. Jos uteluissa on yli minuutin tauko, tulee X:n sulkea itsensä hallitusti.

Palvelin Y on saatavilla testauskäyttöä varten kurssin Moodle-sivulta.

Palauttaminen:
Työ palautetaan esittelemällä sen rakennetta (koodia) ja toimintaa ohjaajalle. Työn koodit (hyvin kommentoituina) tulee palauttaa kurssin Moodle-sivulla hyvissä ajoin ennen palaveria (DL 4.12).
Sovi erikseen palautusaika (sampsa.rauti@utu.fi) hyvissä ajoin siten, että palaveri pidetään välillä 5.12–16.12. Aikaa palauttamispalaveriin varataan 30 min.
