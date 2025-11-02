<h1>h2 Infraa koodina</h1>


tiivistelmät


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
Lisäsin /srv/salt/hellopkg/init.sls -tiedostoon sisältöä(kuva).
<img width="574" height="66" alt="image" src="https://github.com/user-attachments/assets/9b0ea6a5-3077-45d3-b6df-ce42fdb0ebdb" />
<br>
Ajoin komennon 'sudo salt-call --local state.apply hellopkg' ja vastaus oli seuraava:
<br>
<img width="632" height="342" alt="image" src="https://github.com/user-attachments/assets/fb2591a0-3cb1-4cfc-a7a9-3428ee007c93" />
<br>
Curl-työkalu oli jo asennettu.
<br>



<h2>Tee sls-tiedosto, joka käyttää vähintään kahta eri tilafunktiota näistä: package, file, service, user. Tarkista eri ohjelmalla, että lopputulos on oikea. Osoita useammalla ajolla, että sls-tiedostosi on idempotentti.</h2>







<h2>Lähteet</h2>

Karvinen 2025 asdsdfsdf Linkki: asdasdasdasd [1]
