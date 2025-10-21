## h1 Viisikko

**x) Lue ja tiivistä. (Tässä x-alakohdassa ei tarvitse tehdä testejä tietokoneella, vain lukeminen tai kuunteleminen ja tiivistelmä riittää. Tiivistämiseen riittää muutama ranskalainen viiva. Ei siis vaadita pitkää eikä essee-muotoista tiivistelmää. Lisää kuhunkin jokin oma kysymys tai huomio.)**

Karvinen 2025: Install Salt on Debian 13 Trixie

- Salt on konfiguraationhallintatyökalu jonka asennusta käydään läpi yllä olevassa jutussa
- Salt ei ole saatavilla Debian standard -"arkistossa" (repository) joten tarvitaan uusi apt-paketin arkisto.
- Tekstissä puhuttiin myös julkisesta PGP avaimesta. Tästä olen kuullut ja lukenut aikaisemmalla tietoturvakurssilla. 


Karvinen 2023: Run Salt Command Locally

Karvinen 2018: Salt Quickstart – Salt Stack Master and Slave on Ubuntu Linux


Karvinen 2006: Raportin kirjoittaminen


**a) Asenna Debian 13-Trixie virtuaalikoneeseen. (Poikkeuksellisesti tätä alakohtaa ei tarvitse raportoida, jos siinä ei ole mitään ongelmia. Mutta jos on ongelmia, sitten täsmällinen raportti, jotta voidaan ratkoa niitä yhdessä.)**

Asnnus sujui hyvin. Ei virheitä. Hyvät ohjeet sivulla https://terokarvinen.com/2021/install-debian-on-virtualbox/


**b) Asenna Salt (salt-minion) Linuxille (uuteen virtuaalikoneeseesi).**

Aloin asentamaan salt-minionia uuteen virtuaalikoneeseeni Haaga-Helian Pasilan kampuksella 21.10.2025 klo 16:20. Käytin tähän Atkinsin toimiston verkkoyhteyttä. Koneenani toimi Lenovon V14 Gen 4 kannettava tietokone. Käytin tässä tehtävässä apunani Tero karvisen ohjetta **Install Salt on Debian 13 Trixie** https://terokarvinen.com/install-salt-on-debian-13-trixie/

Aloitin asentamisen käynnistämällä Oracle VirtualBox Managerin ja sekä käynnistin Debian virtuaalikoneeni. Kirjauduin sisään omilla tunnuksillani ja avasin terminal-ikkunan. Syötin ensin komennon *sudo apt-get update* jonka jälkeen syötin *sudo apt-get install wget*. Ei mennyt montaakaan sekuntia ja wget oli asennettu. Tämän jälkeen loin uuden hakemiston nimeltä "saltrepo" komennolla *mkdir saltrepo/* jonka jälkeen siirryin kyseiseen hakemistoon komennolla *cd saltrepo/*. Seuraavaksi latasin kaksi tiedostoa komennoilla 
*wget https://packages.broadcom.com/artifactory/api/security/keypair/SaltProjectKey/public*
ja
*wget https://github.com/saltstack/salt-install-guide/releases/latest/download/salt.sources*
Tämän jälkeen tarkistelin kyseisiä public ja salt.sources tiedostoja komennoilla
*less public* 
ja
*less salt.sources*
Molemmisa tuli ohjeiden kaltainen tulos. 
Seuraavaksi kopioin "public" tiedoston kohteeseen /etc/apt/keyrings/salt-archive-keyring.pgp sekä "salt.sources" tiedoston kohteeseen /etc/apt/sources.list.d/

*sudo cp public /etc/apt/keyrings/salt-archive-keyring.pgp*
*sudo cp salt.sources /etc/apt/sources.list.d/*

Sitten olikin aika asentaa Salt. Ajoin komennot *sudo apt-get update* sekä *sudo apt-get install salt-minion salt-master*. Asennus sujui onnistuneesti ja testasin tämän ajamalla komennon *salt --version*. Vastaukseksi tuli **salt 3007.8 (Chlorine)**. 
Loin myös tiedoston komennolla *sudo salt-call --local state.single file.managed /tmp/ollil* ja tämä toimi myös. 
Testasin tämän komennolla *ls /tmp/ollil*. 

Asennus sujui onnistuneesti eikä ongelmia tai virheilmoituksia tullut. 




**c) Viisi tärkeintä. Näytä Linuxissa esimerkit viidestä tärkeimmästä Saltin tilafunktiosta: pkg, file, service, user, cmd. Analysoi ja selitä tulokset.**


**d) Idempotentti. Anna esimerkki idempotenssista. Aja 'salt-call --local' komentoja, analysoi tulokset, selitä miten idempotenssi ilmenee**
