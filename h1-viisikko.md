## h1 Viisikko

**x) Lue ja tiivistä. (Tässä x-alakohdassa ei tarvitse tehdä testejä tietokoneella, vain lukeminen tai kuunteleminen ja tiivistelmä riittää. Tiivistämiseen riittää muutama ranskalainen viiva. Ei siis vaadita pitkää eikä essee-muotoista tiivistelmää. Lisää kuhunkin jokin oma kysymys tai huomio.)**

Karvinen 2025: Install Salt on Debian 13 Trixie

- Salt on konfiguraationhallintatyökalu, jonka asennusta käydään läpi yllä olevassa jutussa
- Salt ei ole saatavilla Debian standard -"arkistossa" (repository) joten tarvitaan uusi apt-paketin arkisto.
- Tekstissä puhuttiin myös julkisesta PGP avaimesta. Tästä olen kuullut ja lukenut aikaisemmalla tietoturvakurssilla. 


Karvinen 2023: Run Salt Command Locally

- Salt-komentoja voi suorittaa paikallisesti. Tulokset tulevat heti nähtäville.
- Tämä helpottaa harjoittelua ja testausta.
- Tärkeimmät toiminnot ovat pkg, file, service, user ja cmd.
- Saltia käytetäään yleensä suuren määrän orjatietokoneiden hallintaan
- Mikä "foo" on?

Karvinen 2018: Salt Quickstart – Salt Stack Master and Slave on Ubuntu Linux

- Saltilla pystyy hallitsemaan tuhansia tietokoneita. Orjien vativat olla palomuurin takana tai jopa tuntemattomassa osoitteessa.
- Jokaisessa verkossa on yksi isäntä ja jokaisella orjalla pitää olla eri ID.
- Isäntä antaa komentoja ja orjat pystyvät toteuttamaan niitä. esim. sudo salt '*' cmd.run 'whoami'
- Millä komennolla pystyy käskyttämääna vain yhtä orjaa ja millä komenolla kaikkia?


Karvinen 2006: Raportin kirjoittaminen

- Raportin pitää olla täsmällinen ja sitä pitää kirjoittaa samalla kun teet Linux-ympäristössä töitä.
- Raportti pitää olla toistettavissa
- Raportissa pitää kertoa kaikki onnistumiset, epäonnistumiset, mitä laitetta käytit, milloin käytit ja mitä klikkasit. Raportti kannattaa kirjoittaa menneessä aikamuodossa.
- Jotta raporttia olisi helpompi lukea, väliotsikoita kannattaa käyttää.
- Lähteisiin viittaaminen on tärkeää.
- Helpottiaisko raportin lukemista tärkeimpien avainsanojen **lihavointi** tai *kursivointi*?

**a) Asenna Debian 13-Trixie virtuaalikoneeseen. (Poikkeuksellisesti tätä alakohtaa ei tarvitse raportoida, jos siinä ei ole mitään ongelmia. Mutta jos on ongelmia, sitten täsmällinen raportti, jotta voidaan ratkoa niitä yhdessä.)**

Asnnus sujui hyvin. Ei virheitä. Hyvät ohjeet sivulla https://terokarvinen.com/2021/install-debian-on-virtualbox/


**b) Asenna Salt (salt-minion) Linuxille (uuteen virtuaalikoneeseesi).**

Aloin asentamaan salt-minionia uuteen virtuaalikoneeseeni Haaga-Helian Pasilan kampuksella 21.10.2025 klo 16:20. Käytin tähän Atkinsin toimiston verkkoyhteyttä. Koneenani toimi Lenovon V14 Gen 4 kannettava tietokone. Käytin tässä tehtävässä apunani Tero karvisen ohjetta **Install Salt on Debian 13 Trixie** https://terokarvinen.com/install-salt-on-debian-13-trixie/

Aloitin asentamisen käynnistämällä Oracle VirtualBox Managerin ja sekä käynnistin Debian virtuaalikoneeni. Kirjauduin sisään omilla tunnuksillani ja avasin terminal-ikkunan. Syötin ensin komennon 
```
sudo apt-get update
```
jonka jälkeen syötin 
```
sudo apt-get install wget
```
Ei mennyt montaakaan sekuntia ja wget oli asennettu. Tämän jälkeen loin uuden hakemiston nimeltä "saltrepo" komennolla 
```
mkdir saltrepo/ 
```
jonka jälkeen siirryin kyseiseen hakemistoon komennolla 
```
cd saltrepo/
```
Seuraavaksi latasin kaksi tiedostoa komennoilla 
```
wget https://packages.broadcom.com/artifactory/api/security/keypair/SaltProjectKey/public

wget https://github.com/saltstack/salt-install-guide/releases/latest/download/salt.sources
```
Tämän jälkeen tarkistelin kyseisiä public ja salt.sources tiedostoja komennoilla
```
less public 

less salt.sources
```
Molemmisa tuli ohjeiden kaltainen tulos. 
Seuraavaksi kopioin "public" tiedoston kohteeseen /etc/apt/keyrings/salt-archive-keyring.pgp sekä "salt.sources" tiedoston kohteeseen /etc/apt/sources.list.d/
```
sudo cp public /etc/apt/keyrings/salt-archive-keyring.pgp
sudo cp salt.sources /etc/apt/sources.list.d/
```
Sitten olikin aika asentaa Salt. Ajoin komennot 
```
sudo apt-get update
sudo apt-get install salt-minion salt-master
```
Asennus sujui onnistuneesti ja testasin tämän ajamalla komennon 
```
salt --version
```
Vastaukseksi tuli **salt 3007.8 (Chlorine)**. 
Loin myös tiedoston komennolla 
```
sudo salt-call --local state.single file.managed /tmp/ollil
```
ja tämä toimi myös. 
Testasin tämän komennolla ```ls /tmp/ollil``` 

Asennus sujui onnistuneesti eikä ongelmia tai virheilmoituksia tullut. 




**c) Viisi tärkeintä. Näytä Linuxissa esimerkit viidestä tärkeimmästä Saltin tilafunktiosta: pkg, file, service, user, cmd. Analysoi ja selitä tulokset.**

Aloitin tämän harjoituksen tekemisen Haaga-Helian Pasilan kampuksella 24.10.2025 klo 09:20. Käytin tähän Atkinsin toimiston verkkoyhteyttä. Koneenani toimi Lenovon V14 Gen 4 kannettava tietokone. Käytin tässä tehtävässä apunani Tero karvisen ohjetta **Run Salt Command Locally** https://terokarvinen.com/2021/salt-run-command-locally/

Ensin tarkistin alla olevalla komennolla, että minulla edelleen oli salt asennettuna
```
sudo salt-call --version
```
**pkg.installed**\
Aloitetaan pkg-funktion testaamisella
```
$ sudo salt-call --local -l info state.single pkg.installed tree
```
Selitykset tulostetuille termeille:\
ID: tree <-- Tämä on ohjelma joka asennettiin\
Function: pkg.installed <-- Funkitio jota suoritettiin\
Result: True <-- Mikä oli lopputulos. Tässä tapauksessa "True" eli ohjelman asennus onnistui.\
Comment: The following packages were installed/updated: tree <-- Tässä on vielä kommenttina mitä tapahtui. \
Started: 09:27:12.479924 <-- Koska asennus alkoi\
Duration: 11138.191 ms <-- kauanka asennus kesti\
Changes: tree: new: 2.2.1-1 <-- Muutokset mitä asennuksessa tapahtui. Tässä tapauksessa asennettiin tree versio 2.2.1-1.\
Summary for local\
Succeeded: 1 (changed=1)\
Failed: 0\
Tässä kohtaa kysyin ai:lta mitä tuo ylläoleva tarkoittaa: Installing pkg in salt minion. What does 
"Succeeded: 1 (changed=1) Failed: 0" mean? \
Succeeded: 1 kertoo että yksi tilantarkastus on onnistunut. 
Changed=1 kertoo että ”Succeeded”-tiloista yksi johti muutokseen minionin järjestelmässä. Pakettia ei oltu vielä asennettu minioniin. Salt latasi ja asensi paketin onnistuneesti, jolloin järjestelmän tila muuttui ”not installed” -tilasta ”installed”-tilaan.
Failed=0 kertoo että 0 tilaa epäonnistui. 

**file.managed**\
Seuraavaksi vuorossa on tilafunktio file.
Ajoin komennon
```
sudo salt-call --local -l info state.single file.managed /tmp/ollil contents="Tässä testailen file tilafunktiota. Onnistuukohan?"
```
Tulostetut termit ja selitykset olivat samoja kuin pkg tilafunktiossa. Nyt loimme tiedoston.
Tarkistin vielä että tiedostoon tuli kyseinen teksinpätkä komennolla 
```
cd /tmp
cat ollil
```
*Tässä testailen file tilafunktiota. Onnistuukohan?* tulostui joten homma toimi. 

**service.running**\
Seuraavaksi testasin service-tilafunktiota. Tätä tilafunktiota käytetään usein daemonin automaattiseen uudelleenkäynnistykseen silloin kun asetuksia muutetaan. Ajoin komennon:
```
sudo salt-call --local -l info state.single service.running ufw enable=True
```
Tällä komennolla palomuurin pitäisi mennä päälle. 
Tuloksissa minulle pisti silmään:\
"Comment: The service is already running". Olinkin jo Debianin asennusvaiheessa laittanut palomuurin päälle joten tämä ei tehnytkään mitään eli ei tullut muutoksia. 

**user.present**\
Seuraavaksi oli vuorossa user-tilafunktio. User tilafunktion tehtävänä on luoda ja hallita käyttäjiä ja niiden asetuksia. (Salt project, https://docs.saltproject.io/en/3006/ref/states/all/salt.states.user.html). Ajoin komennon:
```
sudo salt-call --local -l info state.single user.present seppo
```
Comment: New user seppo created <-- kyseistä käyttäjää ei ollut olemassa joten uusi käyttäjä "seppo" luotiin. \
Gid: 1001 <-- kertoo ryhmän id tunnuksen.\
Groups: seppo <-- ryhmä johon käyttäjä "seppo" luotiin. \
Home: /home/seppo <-- kyseisen käyttäjän polku\
Name: Seppo <-- käyttäjän nimi\
Shell: /bin/sh <-- Kirjautumis-shell, oletusarvoisesti järjestelmän oletus-shell\
uid: 1001 <-- käyttäjän id\
Succeeded: 1 (changed=1)\
Failed: 0\
Yksi tilantarkastus onnistui ja yhteen tehtiin muutoksia, koska käyttäjää ei ollut alunperin olemassa. 

**cmd.run**\

Viimeisenä vuorossa oli cmd-tilafunktio. 
Cmd tilafunktio hallinnoi suoritettuja komentoja. Tämä tila voi määrätä komennon suoritettavaksi tietyissä olosuhteissa. (Salt project, https://docs.saltproject.io/en/3007/ref/states/all/salt.states.cmd.html). 
Päätin kokeilla seuraavaa komentoa:
```
sudo salt-call --local -l info state.single cmd.run 'touch /tmp/foo' creates="/tmp/foo"
```
ID: touch /tmp/foo <-- komento joka suoritetaan, jos ehdot täyttyvät\
Comment: command "touch /tmp/foo" run <--komento suoritettiin\
PID: 5783 <-- id joka annettiin kyseiselle prosessille. (Process ID)\
retcode: 0 <-- "Return code", jos prosessi on onnistunut, tähän tulee nolla. Kaikki muut numerot tarkoittavat että prosessi on epäonnistunut (Packet Coders, https://www.packetcoders.io/network-automation-and-the-linux-return-code/) \
Succeeded: 1 (changed=1)\
Failed: 0\
Yksi tilantarkastus onnistui ja yhteen tehtiin muutoksia. 



**d) Idempotentti. Anna esimerkki idempotenssista. Aja 'salt-call --local' komentoja, analysoi tulokset, selitä miten idempotenssi ilmenee**
