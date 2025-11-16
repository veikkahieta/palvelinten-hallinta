<h1>h4 Pkg-file-service</h1>

<h2>Tiivistelmä</h2>

- Asennetaan ohjelmisto, korvataan konfiguraatiotiedosto ja käynnistetään uudelleen

- Masterissa tila (sshd.sls) ja konfiguraatiotiedoston kopio (sshd_config)

- Luodaan SSH-tila

- sshd_config -tiedostoon puokataan portiksi 8888

- Käytetään orjille tilaa $ sudo salt '*' state.apply sshd

- Testataan



<h2>a) SSHouto. Lisää uusi portti, jossa SSHd kuuntelee.</h2>

Kirjauduin minion-koneelle komennolla 'vagrant ssh t002'. Avasin SSH:n konfiguraatiotiedoston 'sudoedit /etc/ssh/sshd_config'. Lisäsin listaan käytettäviksi porteiksi 22 (oma yhteyteni) ja 8888. <br>
<img width="558" height="34" alt="image" src="https://github.com/user-attachments/assets/dc255e72-2af3-4b18-927f-9454e3c5f891" /> <br>
<img width="634" height="124" alt="image" src="https://github.com/user-attachments/assets/00a60cc2-1c16-4449-a073-76e72361e94f" /> <br>

Käytin komentoa 'sudo service ssh restart' uudelleenkäynnistämiseen, sillä vagrantfilessa pakettini on trusty, eli upstart-init-järjestelmällä. <br>
<img width="364" height="60" alt="image" src="https://github.com/user-attachments/assets/7c305014-0ccc-4156-90c7-46be1428ac4b" /> <br>

Testasin yhteyden komennolla 'nc -vz localhost 8888'. <br>
<img width="444" height="36" alt="image" src="https://github.com/user-attachments/assets/483d53d0-af54-4cb0-8653-9a59f280b606" /> <br>

Poistin portin 8888 konfiguraatiotiedostosta ja käynnistin uudelleen:<br>
<img width="392" height="68" alt="image" src="https://github.com/user-attachments/assets/5afdc8e1-1f8b-46ec-be17-db0fbc761c58" /> <br>
<img width="550" height="42" alt="image" src="https://github.com/user-attachments/assets/319b0144-0aa7-4c31-a1ba-511b7218353c" /> <br>

Siirryin t001-koneelle (master). Loin hakemiston /srv/salt/sshdemon ja vaihdoin siihen luomaan tiedoston ssh_dem_donf. Lisäsin tiedostoon Port 22 ja Port 8888. <br>
<img width="458" height="50" alt="image" src="https://github.com/user-attachments/assets/724cd9f1-184c-4fad-8c36-786ad7cfdac2" /> <br>

Loin tiedoston init.sls komennolla 'sudoedit init.sls' ja lisäsin siihen sisältöä: <br>
<img width="578" height="282" alt="image" src="https://github.com/user-attachments/assets/73f19d9f-b1f3-433b-9c6e-56a0acdec5c2" /> <br>

Ajoin komennon 'sudo salt '*' state.sls sshdemon' (state.sls siksi, koska käytössä on aiemmin mainittu Trusty64): <br>
<img width="526" height="150" alt="image" src="https://github.com/user-attachments/assets/6d4e1e9c-7172-4258-9729-ca1dfd38c8d2" /> <br>

Testasin vielä t002-koneella: <br>
<img width="456" height="76" alt="image" src="https://github.com/user-attachments/assets/eb5b4544-40a7-474d-9209-0681bb7a26b7" /> <br>

<h2>Lähteet</h2>


Karvinen Tero 2025, Palvelinten hallinta, Linkki: https://terokarvinen.com/palvelinten-hallinta/#alustava-aikataulu <br>

Karvinen Tero 2018, Pkg-File-Service - Control Daemons with Salt - Change SSH Server Port, Linkki: https://terokarvinen.com/2018/04/03/pkg-file-service-control-daemons-with-salt-change-ssh-server-port/?fromSearch=karvinen%20salt%20ssh <br>

Harjula Satu 2025, h4 Pkg-File-Service, Linkki: https://github.com/satuharjula/Palvelinten-hallinta/blob/main/h4%20Pkg-File-Service.md <br>

Tavio Aapo 2025, H4 Pkg-file-service, Linkki: https://aapotavio.com/configuration-management-systems/h4-pkg-file-service/ <br>

wpscholar, vagrant-cheat-sheet, Linkki: https://gist.github.com/wpscholar/a49594e2e2b918f4d0c4 <br>









