<h1>h3 Soitto kotiin</h1>

<h2>Lue ja tiivistä</h2>

<h3>Two machine virtual Network with Debian 11 Bullseye and Vagrant [1]</h3>


- Vagrant asentaa automaattisesti Virtualbox-koneet, automatisoi SSH-kirjautumisen

- Ei tarvita graafista käyttöliittymää

- Lataus Debianilla ja Ubuntulla helppo (sudo apt-get install vagrant virtualbox)

- Luodaan uusi hakemisto ja tallennetaan Vagrantfile sinne

- SSH-kirjautuminen vagrant ssh t001 (poistuminen vagrant@001$ exit)

- Molemmat hostit voivat yhdistää toisiinsa sekä verkkoon

- vagrant destroy tuhoaa virtuaalikoneet

- Uudet tyhjät koneet saa vagrant up

- "IP numbers not allowed" -> muutetaan vagrantfile-tiedostossa IP-osoite sallittuun alueeseen (ipcalc)




<h3>Salt quickstart [2]</h3>


- Orjat voivat olla missä tahansa ja silti hallittavissa

- Pääpalvelimella tarvitsee olla julkinen palvelin ja tunnettu osoite

- Yksi master, useita orjia

- masterin lataaminen sudo apt-get -y install salt-master ja hostname -I

- Jos masterissa palomuuri, tarvitaan reiät

- orjan lataaminen sudo apt-get -y install salt-minion

- Orjan pitää tietää masterin sijainti

- Jotta voi käyttää, tarvitaan orjan uudelleenkäynnistys (sudo systemctl restart salt-minion.service)

- master: sudo salt-key -A (hyväksytään orjan avain)



<h3>Infra as code ja top.sls - what slave runs what states [3]</h3>


- Tehdään uusi hakemisto sudo mkdir -p /srv/salt/hello, sudoedit /srv/salt/hello/init.sls

- Lisätään init-tiedostoon tiettyä sisältöä (file.managed…)

- Top-tiedosto määrittää mitkä toiminnot milläkin orjilla ajetaan

- Top-tiedoston ansiosta ei tarvitse erikseen ajaa jokaista orjaa yksinään


<h2>a)</h2>
Olen asentanut Vagrantin: <br>
<img width="372" height="32" alt="image" src="https://github.com/user-attachments/assets/3c0dd6aa-464d-438f-aca2-353fe93bf672" /> <br>

<h2>b)</h2>
Valitsin Vagrantille boxin Vagrantin dokumentaatiosta [4]. Valitsemani box oli centos. Käynnistin Vagrantin ja samalla se loi automaattisesti uuden virtuaalikoneen komennolla vagrant up. <br>
<img width="668" height="162" alt="image" src="https://github.com/user-attachments/assets/3aeee9ca-562b-4580-b350-c3f9b77ec3cd" /> <br>


Virtuaalikone näkyi myös VirtualBoxissa: <br>
<img width="252" height="60" alt="image" src="https://github.com/user-attachments/assets/70a0794d-831f-4cf4-a9a1-d7a2c2914f1a" /> <br>


Kopioin Vagrantfilen sisällön Teroin kotisivuilta [1], mutta vaihdoin sisällöstä boxin käyttämääni boxiin (centos). <br>
<img width="684" height="578" alt="image" src="https://github.com/user-attachments/assets/7de53d01-0195-4884-987c-a57182c9045d" /> <br>

Tämän jälkeen ajoin sudo-oikeuksilla 'sudo vagrant up'-komennon. Asennus alkoi erillisessä PowerShellissä, joka sammui asennuksen jälkeen automaattisesti. <br>
<img width="412" height="42" alt="image" src="https://github.com/user-attachments/assets/4a5ba047-cfec-4512-a4d4-bb85e35a8500" /> <br>

<h2>c)</h2>

Siirryin käyttämään t001-konetta. <br>
<img width="410" height="14" alt="image" src="https://github.com/user-attachments/assets/40bb9043-4860-4ca1-9eb2-be46eaf42598" /> <br>

Pingasin t002-koneeseen ja se onnistui. <br>
<img width="506" height="114" alt="image" src="https://github.com/user-attachments/assets/b4a0b99d-7805-49ab-bef3-09ecdcfb2457" /> <br>

Siirryin käyttämään konetta t002. <br>
<img width="412" height="50" alt="image" src="https://github.com/user-attachments/assets/9a5fd08a-046d-48bc-be08-7ed955ac2e6f" /> <br>

Pingasin t002-koneesta t001-koneeseen ja se onnistui. <br>
<img width="494" height="116" alt="image" src="https://github.com/user-attachments/assets/07213729-e668-4816-882c-01fa919ca00d" /> <br>


<h2>d)</h2>
Yritin alkaa asentamaan Saltia, mutta selvitin internetistä [5] että centos ei käytä samoja komentoja, kuin Debian-pohjaiset käyttöjärjestelmät. Päätin asentaa Debian-pohjaisen Ubuntun vaihtamalla vagrantfilen sisältöä. <br>
<img width="274" height="20" alt="image" src="https://github.com/user-attachments/assets/130a0dcd-106f-4200-80d6-7d638ac2e5d5" /> <br>

Asensin Salt-masterin t001-koneeseen komennoilla 'sudo apt-get update' ja 'sudo apt-get -y install salt-master'. <br>
<img width="546" height="46" alt="image" src="https://github.com/user-attachments/assets/9dddc884-2866-4d08-9b7c-23f96e5b02bb" /> <br>

Asensin salt-minionin t002-koneelle. <br>
<img width="438" height="38" alt="image" src="https://github.com/user-attachments/assets/63673739-5683-4312-b4aa-19c6a60072de" /> <br>

Muutin  /etc/salt/minion -tiedostoa ja lisäsin hostin IP-osoitteen ja annoin sille id:n.  <br>

Hyväksyin master-koneella keyn: <br>
<img width="432" height="96" alt="image" src="https://github.com/user-attachments/assets/388c4d54-dd64-40a4-86ca-acca4535362d" /> <br>
Pientä testiä:<br>
<img width="396" height="48" alt="image" src="https://github.com/user-attachments/assets/3c135155-ebc6-4fd8-95d0-e7c4c96e9226" /> <br>

<h2>e)</h2>
Testasin myös pkg- ja cmd-tiloja: <br>
<img width="556" height="334" alt="image" src="https://github.com/user-attachments/assets/525cde49-aae6-4407-aae7-21755c6c9774" /> <br>



<h2>Lähteet</h2>


Karvinen Tero 2021, Two Machine Virtual Network With Debian 11 Bullseye and Vagrant, Linkki: https://terokarvinen.com/2021/two-machine-virtual-network-with-debian-11-bullseye-and-vagrant/ [1] <br>


Karvinen Tero 2021, Salt Quickstart – Salt Stack Master and Slave on Ubuntu Linux, Linkki: https://terokarvinen.com/2018/salt-quickstart-salt-stack-master-and-slave-on-ubuntu-linux/ [2] <br>


Karvinen Tero 2023, Salt Vagrant - automatically provision one master and two slaves, Linkki: https://terokarvinen.com/2023/salt-vagrant/#infra-as-code---your-wishes-as-a-text-file [3] <br>


HashiCorp, Discover Vagrant Boxes, Linkki: https://portal.cloud.hashicorp.com/vagrant/discover [4] <br>
StackExhange 2019, How to install apt-get and dpkg, Linkki: https://unix.stackexchange.com/questions/555466/how-to-install-apt-get-and-dpkg [5] <br>

Karvinen Tero 2025, Palvelinten hallinta, Linkki: https://terokarvinen.com/palvelinten-hallinta/#alustava-aikataulu <br>

