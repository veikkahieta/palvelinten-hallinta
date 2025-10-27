<h1>h1 Viisikko</h1>

<H2>Lue ja tiivistä:</H2>

<h3>Install Salt on Debian 13 Trixie</h3>

- Ensin ladataan wget
- Luodaan hakemisto
- Ladataan kaksi tarvittavaa tiedostoa
- Tutkitaan tiedostoja
- Luotetaan ja asennetaan
- Lopuksi testaus


<h3>Run Salt Command Locally</h3>

- Salt-komentoja voi ajaa paikallisesti
- Toimii myös Windowsissa
- Ladataan Salt Slave
- Testataan pkg, file, service, user ja cmd


<h3>Salt Quickstart – Salt Stack Master and Slave on Ubuntu Linux</h3>

- Saltin avulla voi hallita tuhansia tietokoneita
- Orjat voivat sijaita missä tahansa, ja niitä voi silti kontrolloida
- Ainoastaan master tarvitsee julkisen palvelimen ja tunnetun osoitteen
- Promptit: master=master$, slave=slave$
- Ladataan master sekä slave
- Hyväksytään orjan avain
- master$ sudo salt '*' cmd.run 'whoami'


<h3>Raportin kirjoittaminen</h3>

- Raportin kirjoittamisen ohjeet ovat pätevät jokaiseen teknisten testien toteutusympäristöön.

- Raporttia kirjoitetaan jatkuvasti samalla, kun testejä toteutetaan.

- Raportin tulee olla täsmällinen ja yksityiskohtainen.

- Raporttia voi hyödyntää pohjana ohjeita laatiessa.

- Myös ympäristön raportoiminen on tärkeää.

- Esimerkiksi kellonajan kertominen voi olla ratkaisevaa, mikäli myöhemmin ilmenee laajempia verkon laajuisia ongelmia.

- Raportoi kaikki odotetut ja odottamattomat tulokset ylös. Mahdolliset ongelmat on myös hyvä tiedostaa.

- Käytä väliotsikoita ja oikeanlaista kieltä.

- Loppuun voi kirjoittaa tiivistelmän.

- Kirjoita tekstisi itse ja käytä ainoastaan luvallisia kuvia.

<h2>Asensin Debian 13 trixien ongelmitta.</h2>


<h2>Asennetaan salt-minion:</h2>


Loin saltille oman hakemiston 'mkdir saltrepo/' ja vaihdoin direktiota 'cd saltrepo/'.

Seuraavana latasin kaksi tarvittavaa tiedostoa. 'wget https://packages.broadcom.com/artifactory/api/security/keypair/SaltProjectKey/public'
ja 'wget https://github.com/saltstack/salt-install-guide/releases/latest/download/salt.sources'.

Seuraavaksi ajoin komennon 'gpg --show-key --with-fingerprint public'.
<img width="796" height="166" alt="image" src="https://github.com/user-attachments/assets/d36c0053-88a3-47b4-9515-d3bd0d9815ab" />


Luotin ja latasin reporistoryn komennoilla 'sudo cp public /etc/apt/keyrings/salt-archive-keyring.pgp' ja 'sudo cp salt.sources /etc/apt/sources.list.d/'.
<img width="796" height="108" alt="image" src="https://github.com/user-attachments/assets/5436112c-57f7-4aa5-b575-08753175a831" />


Seuraavana latasin Saltin komennolla 'sudo apt-get update' ja 'sudo apt-get install salt-minion salt-master'. Vastaus oli "Unable to locate package ...".
<img width="776" height="122" alt="image" src="https://github.com/user-attachments/assets/cac5b930-1f36-429f-93b4-427dcb79c175" />

Tein prosessin uudelleen ja sain sen toimimaan.

Testasin Saltia komennolla 'salt --version'.
<img width="428" height="38" alt="image" src="https://github.com/user-attachments/assets/c9a39998-2ed3-4b08-b2df-198a1f0a92bf" />


<h2>Viisi tärkeintä. pkg, file, service, user, cmd.</h2>


pkg, eli pakettien hallinta voi poistaa, asentaa tai varmistaa että tietty paketti on asennettuna.

Loin tiedoston komennolla 'sudo salt-call --local state-single file.managed /tmp/helloveikka'.
Tämän jälkeen tarkistin että tiedosto on olemassa:
<img width="502" height="36" alt="image" src="https://github.com/user-attachments/assets/6ef5765e-afdc-4413-977d-fb47387907ff" />

file hallitsee tiedostoja. Loin tiedoston nimeltä "filetest.sls" komennolla 'sudo nano /srv/salt/filetest.sls'.
Onnistuin luomaan filellä tiedoston.
<img width="716" height="396" alt="image" src="https://github.com/user-attachments/assets/5e634d63-9046-4551-8a14-ead5377da14c" />


service.running varmistaa, että jokin palvelu on käynnissä ja toimii normaalisti.
Loin taas tiedoston, ja testasin sen toimivuuden komennolla 'sudo salt-call --local state.apply servicetest'.
<img width="760" height="360" alt="image" src="https://github.com/user-attachments/assets/35955c85-ae09-4171-92af-0a4fc54d3d61" />


Loin uudelleen tiedoston, jolla voin testata useria. Ajoin sitten komennon 'sudo salt-call --local state.apply usertest'.
user siis luo käyttäjän, jos sitä ei ole.
<img width="778" height="572" alt="image" src="https://github.com/user-attachments/assets/6c629c2a-a14d-43ef-8bba-0ca1e16bc253" />


cmd ajaa halutun komennon terminaalissa. Loin tiedoston cmdtest.sls komennolla 'sudo nano /srv/salt/cmdtest.sls'.
<img width="756" height="488" alt="image" src="https://github.com/user-attachments/assets/41d5a5ae-0f39-47e0-9c24-4e1ac99e68f3" />

<h2>Esimerkki idempotenssista:</h2>

Loin tiedoston '/srv/salt/idempotenssi.sls'. Lisäsin sisältöä tiedostoon '/tmp/terve.txt: file.managed: - contents "Moro, testi."'.
Ajoin komennon 'sudo salt-call --local state.apply idempotenssi'. Salt loi tiedoston.
<img width="770" height="470" alt="image" src="https://github.com/user-attachments/assets/8eb336b7-6488-4423-9fbb-41c42b9243ff" />
Ajoin saman komennon uudelleen:
<img width="776" height="338" alt="image" src="https://github.com/user-attachments/assets/dea17947-79ef-458a-b1e4-125f2bee3b41" />
Salt ei tehnyt mitään, sillä tiedosto oli jo halutussa tilassa.

Salt siis muuttaa järjestelmää, mikäli muutoksia tarvitaan.



<h2>Lähteet:</h2>
Karvinen, Tero 2025: Install Salt on Debian 13 Trixie. Linkki: https://terokarvinen.com/install-salt-on-debian-13-trixie/
Karvinen, Tero 2025: Palvelinten Hallinta. Linkki: https://terokarvinen.com/palvelinten-hallinta/#alustava-aikataulu
Karvinen, Tero 2023: Run Salt Command Locally. Linkki: https://terokarvinen.com/2021/salt-run-command-locally/
Karvinen, Tero 2018: Salt Quickstart - Salt Stack Master and Slave on Ubuntu Linux. Linkki: https://terokarvinen.com/2018/03/28/salt-quickstart-salt-stack-master-and-slave-on-ubuntu-linux/
Karvinen, Tero 2006: Raportin kirjoittaminen. Linkki: https://terokarvinen.com/2006/06/04/raportin-kirjoittaminen-4/



