<h1>h5 Toimiva versio</h1>
<h2>Tiivistelmät</h2>
<h3>What is Git?</h3>
- Gitin käyttöliittymä on melko samanlainen, kuin muissa VCS, mutta toimii eri tavoin

- Suurin ero datan käsittelytavassa

- Gitissä joka commit ottaa kuvan tiedostojen nykytilasta ja tallentaa

- Jos tiedostot eivät ole muuttuneet, Git ei tallenna uudelleen vaan linkittää edelliseen identtiseen tiedostoon

- Useimmat Gitin toiminnot vaativat vain paikallisia tiedostoja

- Git lukee historian paikallisesta tietokannasta

- VPN- tai verkkoyhteyden merkitys pienempi Gitillä, kuin muilla

- Git havaitsee tiedostojen tai hakemistojen muutokset, mikä auttaa vianselvityksessä

- Modified: Tiedostoa on muutettu, mutta ei commitattu tietokantaan

- Staged: Muokattu tiedosto on merkattu seuraavaan commit snapshotiin

- Committed: Tiedot on tallennettu turvallisesti paikalliseen tietokantaan

- index-tiedostossa lukee tiedot seuraavan commitin sisällöstä

-  Git-hakemistoon tallennetaan projektien metatiedot

<h3>'git add . && git commit; git pull && git push'</h3>
- git add . - lisää tiedostoja committiin, piste lisää kaikki muokatut tiedostot

- git commit - luo commitin

- git pull - Lataa varastosta uuusimman version

- git push - Lisää commitin varastoon

<h3>Varaston terokarvinen/suolax/ historia<h3>

1. Initial commit
2. Improve README.md
3. Add hello World module to create a temporary file
4. Add Makefile to apply hello state
5. Add state to install my favourite apps, currently just 'tree'
6. Add more favourite programs, and list instsalledf modules in top file
7. Clean up README.md
8. Improve usage instructions

<h2>a)</h2>

Loin Githubiin varaston selaimen kautta:<br>
<img width="1182" height="642" alt="image" src="https://github.com/user-attachments/assets/71963c57-10f3-40be-bc48-43eee45863c8" /><br>

<h2>b)</h2>
Clonasin varaston virtuaalikoneelle luomaani "snowman"-hakemistoon:<br>
<img width="780" height="252" alt="image" src="https://github.com/user-attachments/assets/1c2fbd4b-6d5a-43d2-ba19-a3e7bc391065" /><br>

Tein muutoksia README.md -tiedostoon. Muutokset näkyivät Githubissa:<br>
<img width="636" height="402" alt="image" src="https://github.com/user-attachments/assets/c42573a8-3d86-43fd-a4d9-5e90d9c07cba" /><br>
<img width="934" height="540" alt="image" src="https://github.com/user-attachments/assets/11fcf633-9fdd-44b8-841d-e3fabf67cc9e" /><br>
<img width="1346" height="190" alt="image" src="https://github.com/user-attachments/assets/cc1b5af6-6143-49a6-8a57-89e1d184a8bf" /><br>

SSH-avain oli jo aikaisemmin yhdistetty virtuaalikoneeseen: <br>
<img width="654" height="252" alt="image" src="https://github.com/user-attachments/assets/574412ac-23c5-4ba1-9040-db029b88eb7d" /><br>

<h2>c)</h2>
Lisäsin README.md -tiedostoon uutta sisältöä:<br>
<img width="526" height="134" alt="image" src="https://github.com/user-attachments/assets/edad69cd-543a-4cd4-b258-8263142e1b74" /><br>

Ajoin 'git reset --hard' -komennon ja haluttu teksti poistui READMEstä:<br>
<img width="602" height="126" alt="image" src="https://github.com/user-attachments/assets/2f2f281f-b36d-45e2-be5d-ad8bdaeea23d" /><br>

<h2>d)</h2>

Ajoin komennon 'git log --patch' ja sisältö oli seuraava:<br>
<img width="804" height="458" alt="image" src="https://github.com/user-attachments/assets/d70b0cb4-e99b-4e5f-b164-91f17ad3c457" /><br>

Github käyttäjään liitetty sähköpostini vaihtui kesken tehtävän tarkoituksellisesti.<br>
Tekemäni kaksi committia näkyivät lokissa. Kellonajat olivat oikeat ja lisäksi sähköpostit sekä nimi olivat virheettömiä.<br>

<h2>e)</h2>

Loin Githubiin Salt-kansion ja tein sinne snow.sls tiedoston, jonka sisällön kopioin Teron Githubista, joka oli tehtävän vinkeissä.<br>
<img width="360" height="266" alt="image" src="https://github.com/user-attachments/assets/94d5de81-4a93-48fa-b7b7-4a938ccd4ec7" /><br>

Ajoin 'sudo salt-call --local --file-root ./salt state.apply snow':<br>
<img width="952" height="484" alt="image" src="https://github.com/user-attachments/assets/a475c4a0-9b42-499a-8f4e-bb89da8f6caf" /><br>


<h2>Lähteet</h2>

Karvinen, Tero 2025: Palvelinten Hallinta. Linkki: https://terokarvinen.com/palvelinten-hallinta/#alustava-aikataulu

<br>Karvinen, Tero 2024: Hello Salt Infra-as-Code. Linkki: https://terokarvinen.com/2024/hello-salt-infra-as-code/

<br>Karvinen, Tero 2024: suolax. Linkki: https://github.com/terokarvinen/suolax

<br>Chacon and Straub 2014: Pro Git 2ed: 1.3 Getting Started - What is Git? Linkki: https://git-scm.com/book/en/v2/Getting-Started-What-is-Git%3F
