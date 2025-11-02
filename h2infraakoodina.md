<h1>h2 Infraa koodina</h1>
<h2>Lue ja tiivistä.</h2>
<h3>Karvinen 2014: Hello Salt Infra-as-Code [2]</h3>

- ensin asennetaan salt

- luodaan oma moduuli halutulle ohjelmalle (mkdir)

- /srv/salt/ -kansio jaetaan kaikille orjille

- lisätään hello -moduulissa sijaitsevaan init.sls -tiedostoon sisältöä

- Ajetaan salt-komento

- Tutkitaan lopputulosta, tässä tapauksessa uusi tiedosto on tehty

- Varmistetaan ls-komennolla, että Salt on toiminut oikein

- Kun komennon ajaa uudelleen, järjestelmä ilmoittaa ettei muutoksia ole tarvetta tehdä.


<h3>Salt contributors: Salt overview [3]</h3>

Rules of YAML ja YAML simple structure


- YAMLin tehtävä on kääntää YAML-tietorakenne Pythoniksi Saltia varten

- YAML on monien Saltissa käytettyjen tiedostojen oletusrenderöijä

- Data on jäsennelty avain: arvo -pareiksi

- Avain: arvo -parien merkitsemineen käytetään kaksoispistettä ja yhtä välilyöntiä

- Avainten arvot voivat olla eri rakenteissa

- Kaikissa kirjainkoko on tärkeä

- Ei saa käyttää Tab, vaan välilyöntejä

- Kommentit alkavat #



- Rakenne koostuu kolmesta peruselementtityypistä

- Scalars: Arvo voi olla numero, merkkijono tai totuusarvo ('vegetables: peas')

- List: Arvoluettelo, jokainen arvo omalla rivillään ja kaksi välilyöntiä sekä viiva
('vegetables:
   - peas
   - carrots')

- Dictionaries: Kokoelma arvomäärityksiä ja luetteloita 
('  drink: sparkling water
  entree:
    - steak
    - mashed potatoes')
 
Lists and dictionaries - YAML


- YAML-rakenteet on järjestetty lohkoihin

- Sisennyksellä asetetaan konteksti, ominaisuudet ja lista on sisennettävä vähintään yhdellä välilyönnillä mutta kaksi on vakio

- Kokoelma, joka on lista tai dictionary lohkosarja osoittaa jokaisen kohdan viivalla ja välilyönnillä.
 

<h3>Salt contributors: The top file [4]</h3>

- Useimmat infrat koostuvat koneryhmistä, joissa jokainen kone suorittaa samanlaista roolia kuin muut

- Järjestelmänvalvojan täytyy voida luoda rooleja näille ryhmille

- Rooleina esim. osoittaa, että kaikissa koneissa on Apache asennettuna ja että Apache on aina käynnissä

- Top file on tiedosto, joka sisältää ryhmien ja sovellettavien roolien välisen määrityksen

- Top-tiedoston nimi on oletuksena top.sls, koska se sijaitsee aina tilatiedostoja sisältävän hierarkian ylimpänä. Hierarkiaa kutsutaan tilapuuksi (state tree).


- Top-tiedostoilla on kolme komponenttia

- Environment: Tilatiedostoja järjestelmien konfiguroimiseksi sisältävä tilapuuhakemisto (state tree directory)

- Target: Ryhmä, joille asetetaan joukko tiloja

- State files: Lista tilatiedostoista, joita kohteeseen sovelletaan.

- Jokainen tilatiedosto kauvaa yhden tai useamman tilan, jotka konfiguroidaan ja ajetaan kohteessa

- Komponentit ovat sisäkkäin, ympäristöt (environment) sisältävät kohteita (target) ja kohteet sisältävät tiloja (states).



<br>
<h2>Hei infrakoodi! Kokeile paikallisesti (esim 'sudo salt-call --local') infraa koodina. Kirjota sls-tiedosto, joka tekee esimerkkitiedoston /tmp/ -kansioon.</h2>
Loin esimerk.sls -tiedoston ja lisäsin siihen sisältöä (kuva).
<img width="802" height="454" alt="image" src="https://github.com/user-attachments/assets/53738ddb-f5b4-41d7-961b-d9d703aa7b97" />
<br>
Ajoin 'sudo salt-call --local state.apply esimerk' -komennon, ja tuli virheilmoitus (kuva).
<img width="800" height="428" alt="image" src="https://github.com/user-attachments/assets/2010dfea-c2f0-4132-a848-aa8c32db8aec" />
<br>
Tajusin sisennyksen menneen rivi kerrallaan ylhäältäpäin 0 välilyöntiä, 2, 4 ja 6. Korjasin viimeiselle riville kuuden tilalle kahdeksan välilyöntiä, ajoin Salt-komennon uudelleen ja komento toimi.
<img width="666" height="412" alt="image" src="https://github.com/user-attachments/assets/e6fbf05c-04db-4ccd-94ec-0ef2032838d7" />

<br>
Tarkistin tuloksen vielä cat-komennolla:
<img width="454" height="42" alt="image" src="https://github.com/user-attachments/assets/a00bb607-584c-466d-b7b0-8f13c5ef68ce" />
<br>
Tajusin jälkeenpäin siirtää /srv/salt/esimerk.sls -tiedoston omaan alikansioonsa, kuten vinkeissä luki. Käytin komentoa 'sudo mv /srv/salt/esimerk.sls /srv/salt/esimerkki/esimerk.sls'. [1]
<h2>Toppping. Tee top-file, niin että kaikki omat tilasi ajetaan kerralla komennolla 'sudo salt-call --local state.apply'.</h2>

<br>
<br>
Loin tiedoston /srv/salt/top.sls komennolla 'sudo nano /srv/salt/top.sls' ja lisäsin sinne sisältöä (kuva).
<img width="540" height="92" alt="image" src="https://github.com/user-attachments/assets/1fb9e3b0-2081-4244-90eb-741aadb2b5b4" />
<br>
Ajoin salt-komennon 'sudo salt-call --local state.apply' ja sain halutun tuloksen.
<img width="632" height="340" alt="image" src="https://github.com/user-attachments/assets/fe20b8ed-d957-4732-82c8-6aa99e3541fc" />
<br>
Tarkistin vielä cat-komennolla.
<img width="418" height="40" alt="image" src="https://github.com/user-attachments/assets/710d8476-121a-4404-b5c6-2a39f442eb08" />

<br>
<br>
<h2>Viisikko tiedostossa. Tee erilliset esimerkit kustakin viidestä tärkeimmästä tilafunktiosta pkg, file, service, user, cmd. Kirjoita esimerkit omiksi tiloikseen /srv/salt/ alle, esim /srv/salt/hellopkg/init.sls.</h2>
<br>
<br>
Loin kaikille tiloille omat hakemistot komennolla 'sudo mkdir -p /srv/salt/{hellopkg,hellofile,helloservice,hellouser,hellocmd}'. Tarkistin tree-komennolla, että kaikki on oikein.
<img width="356" height="376" alt="image" src="https://github.com/user-attachments/assets/98f66f1d-e33b-424c-aee5-bb54134e07b0" />
<br>
<h3>pkg</h3>
Lisäsin /srv/salt/hellopkg/init.sls -tiedostoon sisältöä(kuva).
<img width="574" height="66" alt="image" src="https://github.com/user-attachments/assets/9b0ea6a5-3077-45d3-b6df-ce42fdb0ebdb" />
<br>
Ajoin komennon 'sudo salt-call --local state.apply hellopkg' ja vastaus oli seuraava:
<br>
<img width="632" height="342" alt="image" src="https://github.com/user-attachments/assets/fb2591a0-3cb1-4cfc-a7a9-3428ee007c93" />
<br>
Curl-työkalu oli jo asennettu.
<br>
<h3>file</h3>

Lisäsin /srv/salt/hellofile/init.sls -tiedostoon sisältöä (kuva).
<img width="614" height="114" alt="image" src="https://github.com/user-attachments/assets/197e69cc-e38e-481b-944d-98377e4e97c9" />

Ajoin komennon 'sudo salt-call --local state.apply hellofile' ja vastaus oli seuraava:
<img width="660" height="392" alt="image" src="https://github.com/user-attachments/assets/933e0aa4-1322-4ba3-aa11-fdf9c43d6d3a" />

Tarkistin tuloksen cat-komennolla 'cat /tmp/hellofile.txt':
<img width="424" height="34" alt="image" src="https://github.com/user-attachments/assets/a4354848-6964-45ef-b127-927da5333deb" />

<h3>service</h3>

Loin tiedoston /srv/salt/helloservice/init.sls ja lisäsin siihen sisältöä:
<img width="620" height="98" alt="image" src="https://github.com/user-attachments/assets/ee5858ec-7029-4f20-a70f-3ce76711dd73" />

Ajoin komennon 'sudo salt-call --local state.apply helloservice' ja tulos oli seuraava:
<img width="688" height="338" alt="image" src="https://github.com/user-attachments/assets/74f9e409-ba3f-4cd6-ad12-975d7a3782aa" />

Tämä tarkisti, että lähes jokaisesta Linuxista löytyvä cron-palvelu on käynnissä. Komento myös käynnistäisi palvelun, mikäli se ei olisi jo käynnissä. 'enable: True' varmistaa automaattisen käynnistymisen bootissa.

Varmistin vielä toimivuuden komennolla 'sudo systemctl status cron':
<img width="804" height="78" alt="image" src="https://github.com/user-attachments/assets/8f3bbf1c-a048-499a-96e8-aee4916f41fd" />

<h3>user</h3>
Loin tiedoston /srv/salt/hellouser/init.sls ja lisäsin siihen sisältöä:
<img width="608" height="116" alt="image" src="https://github.com/user-attachments/assets/c8d44f3a-b781-4689-845d-f866842b1e01" />

Ajoin salt-komennon 'sudo salt-call --local state.apply hellouser' ja vastaus oli seuraava:
<img width="646" height="630" alt="image" src="https://github.com/user-attachments/assets/a27ef650-1460-4930-8a09-c6e1f0368e64" />

Salt siis loi käyttäjän nimeltä "hello".


<h3>cmd</h3>

Loin /srv/salt/hellocmd/init.sls -tiedoston ja lisäsin siihen seuraavaa sisältöä:
<img width="596" height="110" alt="image" src="https://github.com/user-attachments/assets/fada7749-d10a-439a-84cf-ab88f9d68787" />

Ajoin salt-komennon 'sudo salt-call --local state.apply hellocmd' ja vastaus oli seuraava:
<img width="630" height="492" alt="image" src="https://github.com/user-attachments/assets/d35366e8-0df5-4ec3-9312-b20b9f954b66" />

Testasin vielä cat-komennolla:
<img width="424" height="36" alt="image" src="https://github.com/user-attachments/assets/41748299-9e5d-4f83-9d8c-1bd517cd8e1e" />

Salt suoritti onnistuneesti yksinkertaisen komennon.


<h2>Tee sls-tiedosto, joka käyttää vähintään kahta eri tilafunktiota näistä: package, file, service, user. Tarkista eri ohjelmalla, että lopputulos on oikea. Osoita useammalla ajolla, että sls-tiedostosi on idempotentti.</h2>

Loin uuden .sls-tiedoston, ja lisäsin siihen sisältöä:
<img width="542" height="34" alt="image" src="https://github.com/user-attachments/assets/5d140f87-be71-4c70-8c0b-a6392b7277e7" />
<img width="574" height="244" alt="image" src="https://github.com/user-attachments/assets/02dde3d5-a0de-4a01-8a86-78b9881cc48e" />

Muokkasin top.sls-tiedoston sisältöä komennolla 'sudo nano /srv/salt/top.sls'.
Lisäsin seuraavan sisällön top-tiedostoon:
<img width="560" height="96" alt="image" src="https://github.com/user-attachments/assets/2fa2bafc-16ab-4dd9-926c-8be9fa96fdf2" />

Ajoin salt-komennon 'sudo salt-call --local state.apply':
<img width="624" height="548" alt="image" src="https://github.com/user-attachments/assets/96c5cf3c-27c3-4f35-b95a-9c3b4171eec2" />

Tarkistin lopputuloksen cat-komennolla, sekä 'curl --version' -komennolla:
<img width="636" height="226" alt="image" src="https://github.com/user-attachments/assets/0f38629f-f048-49d1-8542-407ca4d49286" />

Ajoin salt-komennon uudelleen testatakseni idempotenssin:
<img width="664" height="494" alt="image" src="https://github.com/user-attachments/assets/be24fc81-2ea3-4260-bb5c-9512a1f2798a" />

Tila on idempotentti.



<h2>Lähteet</h2>

Karvinen, Tero 2025: Palvelinten Hallinta. Linkki: https://terokarvinen.com/palvelinten-hallinta/#alustava-aikataulu [1]
<br>Karvinen, Tero 2024: Hello Salt Infra-as-Code. Linkki: https://terokarvinen.com/2024/hello-salt-infra-as-code/ [2]
<br>Salt contributors 2021: Salt overview - Salt user guide. Linkki: https://docs.saltproject.io/salt/user-guide/en/latest/topics/overview.html#rules-of-yaml [3]
<br>Salt contributors 2025: The Top File. Linkki: https://docs.saltproject.io/en/latest/ref/states/top.html [4]
