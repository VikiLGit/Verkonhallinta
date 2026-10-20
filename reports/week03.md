# 1. Johdanto

Prometheus on monitorointi- ja hälytysjärjestelmä, jonka toiminta perustuu ensisijaisesti metriikan keräämiseen pull modelilla. Tekee siis säännöllisessti http-pull pyyntöjä.

# 2. Node Exporterin käyttöönotto

```bash
root@web1:/# curl -s http://localhost:9100/metrics | egrep '^(node_cpu_seconds_total|node_memory_MemTotal_bytes|node_filesystem_size_bytes)'
node_cpu_seconds_total{cpu="0",mode="idle"} 61898.12
node_cpu_seconds_total{cpu="0",mode="iowait"} 162.74
node_cpu_seconds_total{cpu="0",mode="irq"} 0
node_cpu_seconds_total{cpu="0",mode="nice"} 0
node_cpu_seconds_total{cpu="0",mode="softirq"} 540.31
node_cpu_seconds_total{cpu="0",mode="steal"} 0
node_cpu_seconds_total{cpu="0",mode="system"} 101.15
node_cpu_seconds_total{cpu="0",mode="user"} 139.29
node_cpu_seconds_total{cpu="1",mode="idle"} 62199.66
node_cpu_seconds_total{cpu="1",mode="iowait"} 30.4
node_cpu_seconds_total{cpu="1",mode="irq"} 0
node_cpu_seconds_total{cpu="1",mode="nice"} 0
node_cpu_seconds_total{cpu="1",mode="softirq"} 100.66
node_cpu_seconds_total{cpu="1",mode="steal"} 0
node_cpu_seconds_total{cpu="1",mode="system"} 44.87
node_cpu_seconds_total{cpu="1",mode="user"} 74.32
node_cpu_seconds_total{cpu="10",mode="idle"} 62009.1
node_cpu_seconds_total{cpu="10",mode="iowait"} 52.04
node_cpu_seconds_total{cpu="10",mode="irq"} 0
node_cpu_seconds_total{cpu="10",mode="nice"} 3.62
node_cpu_seconds_total{cpu="10",mode="softirq"} 1.92
node_cpu_seconds_total{cpu="10",mode="steal"} 0
node_cpu_seconds_total{cpu="10",mode="system"} 101.69
node_cpu_seconds_total{cpu="10",mode="user"} 138.67
node_cpu_seconds_total{cpu="11",mode="idle"} 62243.27
node_cpu_seconds_total{cpu="11",mode="iowait"} 4.83
node_cpu_seconds_total{cpu="11",mode="irq"} 0
node_cpu_seconds_total{cpu="11",mode="nice"} 1.82
node_cpu_seconds_total{cpu="11",mode="softirq"} 1.42
node_cpu_seconds_total{cpu="11",mode="steal"} 0
node_cpu_seconds_total{cpu="11",mode="system"} 41.09
node_cpu_seconds_total{cpu="11",mode="user"} 62.92
node_cpu_seconds_total{cpu="12",mode="idle"} 62034.11
node_cpu_seconds_total{cpu="12",mode="iowait"} 34.24
node_cpu_seconds_total{cpu="12",mode="irq"} 0
node_cpu_seconds_total{cpu="12",mode="nice"} 0
node_cpu_seconds_total{cpu="12",mode="softirq"} 2.17
node_cpu_seconds_total{cpu="12",mode="steal"} 0
node_cpu_seconds_total{cpu="12",mode="system"} 100.4
node_cpu_seconds_total{cpu="12",mode="user"} 138.44
node_cpu_seconds_total{cpu="13",mode="idle"} 62234.17
node_cpu_seconds_total{cpu="13",mode="iowait"} 5.52
node_cpu_seconds_total{cpu="13",mode="irq"} 0
node_cpu_seconds_total{cpu="13",mode="nice"} 0.08
node_cpu_seconds_total{cpu="13",mode="softirq"} 1.68
node_cpu_seconds_total{cpu="13",mode="steal"} 0
node_cpu_seconds_total{cpu="13",mode="system"} 46.07
node_cpu_seconds_total{cpu="13",mode="user"} 66.92
node_cpu_seconds_total{cpu="14",mode="idle"} 62029.59
node_cpu_seconds_total{cpu="14",mode="iowait"} 36.89
node_cpu_seconds_total{cpu="14",mode="irq"} 0
node_cpu_seconds_total{cpu="14",mode="nice"} 0
node_cpu_seconds_total{cpu="14",mode="softirq"} 2.72
node_cpu_seconds_total{cpu="14",mode="steal"} 0
node_cpu_seconds_total{cpu="14",mode="system"} 96.07
node_cpu_seconds_total{cpu="14",mode="user"} 150.1
node_cpu_seconds_total{cpu="15",mode="idle"} 62238.49
node_cpu_seconds_total{cpu="15",mode="iowait"} 5.75
node_cpu_seconds_total{cpu="15",mode="irq"} 0
node_cpu_seconds_total{cpu="15",mode="nice"} 0
node_cpu_seconds_total{cpu="15",mode="softirq"} 2.93
node_cpu_seconds_total{cpu="15",mode="steal"} 0
node_cpu_seconds_total{cpu="15",mode="system"} 44.18
node_cpu_seconds_total{cpu="15",mode="user"} 69.32
node_cpu_seconds_total{cpu="2",mode="idle"} 61871.52
node_cpu_seconds_total{cpu="2",mode="iowait"} 180.69
node_cpu_seconds_total{cpu="2",mode="irq"} 0
node_cpu_seconds_total{cpu="2",mode="nice"} 0
node_cpu_seconds_total{cpu="2",mode="softirq"} 38.3
node_cpu_seconds_total{cpu="2",mode="steal"} 0
node_cpu_seconds_total{cpu="2",mode="system"} 101.72
node_cpu_seconds_total{cpu="2",mode="user"} 149.16
node_cpu_seconds_total{cpu="3",mode="idle"} 62173.49
node_cpu_seconds_total{cpu="3",mode="iowait"} 42.73
node_cpu_seconds_total{cpu="3",mode="irq"} 0
node_cpu_seconds_total{cpu="3",mode="nice"} 0
node_cpu_seconds_total{cpu="3",mode="softirq"} 15.31
node_cpu_seconds_total{cpu="3",mode="steal"} 0
node_cpu_seconds_total{cpu="3",mode="system"} 46.96
node_cpu_seconds_total{cpu="3",mode="user"} 91
node_cpu_seconds_total{cpu="4",mode="idle"} 61943.54
node_cpu_seconds_total{cpu="4",mode="iowait"} 123.64
node_cpu_seconds_total{cpu="4",mode="irq"} 0
node_cpu_seconds_total{cpu="4",mode="nice"} 0
node_cpu_seconds_total{cpu="4",mode="softirq"} 3.62
node_cpu_seconds_total{cpu="4",mode="steal"} 0
node_cpu_seconds_total{cpu="4",mode="system"} 97.54
node_cpu_seconds_total{cpu="4",mode="user"} 147
node_cpu_seconds_total{cpu="5",mode="idle"} 62236.77
node_cpu_seconds_total{cpu="5",mode="iowait"} 11.84
node_cpu_seconds_total{cpu="5",mode="irq"} 0
node_cpu_seconds_total{cpu="5",mode="nice"} 0
node_cpu_seconds_total{cpu="5",mode="softirq"} 4.57
node_cpu_seconds_total{cpu="5",mode="steal"} 0
node_cpu_seconds_total{cpu="5",mode="system"} 40.56
node_cpu_seconds_total{cpu="5",mode="user"} 72.33
node_cpu_seconds_total{cpu="6",mode="idle"} 61981.37
node_cpu_seconds_total{cpu="6",mode="iowait"} 91.7
node_cpu_seconds_total{cpu="6",mode="irq"} 0
node_cpu_seconds_total{cpu="6",mode="nice"} 0.04
node_cpu_seconds_total{cpu="6",mode="softirq"} 2.53
node_cpu_seconds_total{cpu="6",mode="steal"} 0
node_cpu_seconds_total{cpu="6",mode="system"} 98.56
node_cpu_seconds_total{cpu="6",mode="user"} 143.35
node_cpu_seconds_total{cpu="7",mode="idle"} 62222.6
node_cpu_seconds_total{cpu="7",mode="iowait"} 8.78
node_cpu_seconds_total{cpu="7",mode="irq"} 0
node_cpu_seconds_total{cpu="7",mode="nice"} 0.04
node_cpu_seconds_total{cpu="7",mode="softirq"} 2.62
node_cpu_seconds_total{cpu="7",mode="steal"} 0
node_cpu_seconds_total{cpu="7",mode="system"} 44.46
node_cpu_seconds_total{cpu="7",mode="user"} 81.97
node_cpu_seconds_total{cpu="8",mode="idle"} 61999.47
node_cpu_seconds_total{cpu="8",mode="iowait"} 70.48
node_cpu_seconds_total{cpu="8",mode="irq"} 0
node_cpu_seconds_total{cpu="8",mode="nice"} 0.75
node_cpu_seconds_total{cpu="8",mode="softirq"} 2.58
node_cpu_seconds_total{cpu="8",mode="steal"} 0
node_cpu_seconds_total{cpu="8",mode="system"} 99.4
node_cpu_seconds_total{cpu="8",mode="user"} 141.91
node_cpu_seconds_total{cpu="9",mode="idle"} 62240.17
node_cpu_seconds_total{cpu="9",mode="iowait"} 6.12
node_cpu_seconds_total{cpu="9",mode="irq"} 0
node_cpu_seconds_total{cpu="9",mode="nice"} 2.55
node_cpu_seconds_total{cpu="9",mode="softirq"} 1.77
node_cpu_seconds_total{cpu="9",mode="steal"} 0
node_cpu_seconds_total{cpu="9",mode="system"} 42.88
node_cpu_seconds_total{cpu="9",mode="user"} 65.52
node_filesystem_size_bytes{device="/dev/sdd",device_error="",fstype="ext4",mountpoint="/configs"} 1.081101176832e+12
node_filesystem_size_bytes{device="/dev/sdd",device_error="",fstype="ext4",mountpoint="/etc/hostname"} 1.081101176832e+12
node_filesystem_size_bytes{device="/dev/sdd",device_error="",fstype="ext4",mountpoint="/etc/hosts"} 1.081101176832e+12
node_filesystem_size_bytes{device="/dev/sdd",device_error="",fstype="ext4",mountpoint="/etc/resolv.conf"} 1.081101176832e+12
node_filesystem_size_bytes{device="/dev/sdd",device_error="",fstype="ext4",mountpoint="/student-bootstrap"} 1.081101176832e+12
node_memory_MemTotal_bytes 1.6613269504e+10
```


# 3. Prometheus

<img width="1726" height="79" alt="kuva2" src="./images/kuva2.png" />

# 4. Dashboard

<img width="1487" height="1075" alt="kuva3" src="./images/kuva3.png" />

# 5. Kuormitustesti

<img width="1407" height="985" alt="kuva4" src="./images/kuva4.png" />

Cpu käyrä nousi vähäsen ja käväisi pikaisesti 9,8 % kohdilla.

Levytilan käyttö käyrästä näkee selvästi missä 500mb:n tiedosto on luotu ja missä kohtaa stress-ng on asennettu.

Ainoa liikahdus verkkoliikenteessä näyttäisi olevan stress-ng:n asennus.

# 6. SNMP vs Prometheus

| Ominaisuus | SNMP | Prometheus |
|------------|------|------------|
| Tiedonkeruu | Kyselypohjainen | Kyselypohjainen |
| Käyttöönotto | aika yksinkertainen | yksinkertainen |
| Mittarien määrä | Vähempi | Enempi|
| Visualisointi | Vähän kökkö | Laaja valikoima lukuisia eri graaffeja |
| Hälytysmahdollisuudet | Laitteet voivat lähettää hälytyksiä | Lähes mikä vain on mahdollista |
| Soveltuvuus pilviympäristöihin | Ei sovi pilviympäristöihin | Rakennettu juuri pilviympäristöjä ajatellen |

# 7. Yhteenveto
Prometheus käyttää promQL kieltä sen kyselyihin joka mahdollistaa erittäin kompleksitkin kyselyt, prometheus on erittäin skaalautuva.

Ylläpitäjille tärkeät mittarit voidaan jakaa kahteen eri kategoriaan infran terveys ja palvelun laatu. Infran puolella on laitteiden käyttöaste ja virheet, palvelun laadun puolella on pyyntömäärät, vasteaika, ja virheet.

Dashboardista näkyy cpu:n, muisti:n, ja tallennustila:n käyttö, sekä netin vastaannottoon ja lähetykseen käytetty kaistaleveys.

Tämän hetken dashboardista puuttuu palvelun laadun puolen mittarit eli lisäisin ne seuraavaksi.

Monitorointi tiedot auttaa vianetsinnässä sillä voit nähdä mikä-, miten-, ja milloin muuttui. 





