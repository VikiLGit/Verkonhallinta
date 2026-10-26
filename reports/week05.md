
# Johdanto

Tietoturva verkonhallinnan näkökulmasta.

# Kaappaus

Keräsimme verkkoliikenteen tcpdump työkalulla jolla kirjoitimme eth1 verkkoliitännän verkkoliikenteen web1.pcap nimiseen tiedostoon.

# Porttiskannaus

skannaus tuli IP-osoitteesta 10.10.10.200. - aa:c1:ab:ff:7d:d9

<img width="1648" height="639" alt="kuva5" src="./images/kuva5.png" />


# Wireshark

Havaintoja liikenteestä.

skannaus tuli IP-osoitteesta 10.10.10.200. - aa:c1:ab:ff:7d:d9
Testattuja portteja: mm. 443, 995, 25, 8080, 1025, 8888, 111, 113, 23, 5900, 22, 53, 554
Palvelin: 
<img width="625" height="347" alt="image" src="https://github.com/user-attachments/assets/f4d470e0-efd6-4e90-8a83-1e2f0325f349" />

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
<img width="562" height="277" alt="image" src="https://github.com/user-attachments/assets/d3f5ffe9-8778-4653-8af5-35fe02d64519" />

Parannusehdotukset.

# Yhteenveto

Opitut asiat.
