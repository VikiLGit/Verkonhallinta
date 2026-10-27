
# Johdanto

Tietoturva verkonhallinnan näkökulmasta.
Verkkoliikenteen analysoinnilla voidaan tunnistaa käytössä olevia palveluita, havaita poikkeavaa toimintaa ja arvioida verkon turvallisuutta.

Tässä tehtävässä kaapataan ja analysoidaan verkkoliikennettä tcpdump- ja Wireshark-työkaluilla, suoritetaan porttiskannauksia Nmapilla ja tutkitaan Linux-palvelimen lokitietoja.

# Kaappaus

Keräsimme verkkoliikenteen tcpdump työkalulla jolla kirjoitimme eth1 verkkoliitännän verkkoliikenteen web1.pcap nimiseen tiedostoon.

# Porttiskannaus

Skannaus tuli IP-osoitteesta 10.10.10.200.
<img width="1648" height="639" alt="kuva5" src="./images/kuva5.png" />


# Wireshark

Havaintoja liikenteestä.

skannaus tuli IP-osoitteesta 10.10.10.200. - aa:c1:ab:ff:7d:d9
Testattuja portteja: mm. 443, 995, 25, 8080, 1025, 8888, 111, 113, 23, 5900, 22, 53, 554 ja 987 muuta.
<img width="625" height="347" alt="image" src="https://github.com/user-attachments/assets/f4d470e0-efd6-4e90-8a83-1e2f0325f349" />
Nmap 172.20.20.12
<img width="485" height="182" alt="image" src="https://github.com/user-attachments/assets/07e106eb-4a4a-4a20-bbf0-d56abcddef2d" />

Palvelin: 
<img width="796" height="97" alt="image" src="https://github.com/user-attachments/assets/61983811-ed06-444f-b8df-760325527885" />

Ei DNS liikennettä.
Ei HTTP liikennettä.

# Loki-analyysi

Tutkitut lokit ja löydökset.
/var/log/bootstrap.log
Löytyi paljon dpkg:n varoituksia.
<img width="608" height="545" alt="image" src="https://github.com/user-attachments/assets/7be205f2-eef5-4576-8ff8-69309a789b2d" />

Journalctl ei palauttanut merkintöjä.

# Turvallisuusarvio
Portti skannausten tulokset viittaavat, että Portteja suodatetaan. 
Verkossa 172.20.20.12 - 998 tcp porttia suljettu. Portti 22 ssh ja Portti 9100 Jetdirect.
<img width="562" height="277" alt="image" src="https://github.com/user-attachments/assets/d3f5ffe9-8778-4653-8af5-35fe02d64519" />

Ympäristö toimii hyvin ja vaikuttaa turvalliselta ulkoisia verkkoja kohtaan. 
Verkossa 172.20.20.12 - on hyvä tarkastaa portin 9100 tarpeellisuus, saavutettavuus ja käyttötarkoitus.

/var/log/bootstrap.log-tiedostosta löytyi paljon dpkg:n varoituksia. Niiden syyt tulisi selvittää, jotta mahdolliset ohjelmistojen asennukseen tai järjestelmän toimintaan liittyvät ongelmat voidaan korjata. Lisäksi lokituksen toimivuus tulisi varmistaa.

# Yhteenveto
Opitut asiat.
Opimme kaappaamaan ja analysoimaan verkkoliikennettä sekä käyttämään Nmapia porttien tilan selvittämiseen. Opimme myös erottamaan avoimet, suljetut ja suodatetut portit toisistaan.

Lisäksi, että verkkoliikenne ja järjestelmälokit täydentävät toisiaan tietoturvan arvioinnissa. Jatkuvan monitoroinnin avulla voi havaita epäilyttäviä yhteydenottoja ja tunnistaa mahdollisia hyökkäyksiä aikaisessa vaiheessa.

