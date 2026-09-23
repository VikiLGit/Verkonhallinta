# 1. Johdanto
Ympäristön tarkoitus on toimia harjouitus ympäristönä meille jotka täällä näitä tehtäviä tehään joka jokseenkin vastaa oikeaa yritysverkkoa.
# 2. Verkkokaavio
<img width="364" height="756" alt="image" src="https://github.com/user-attachments/assets/6457dd87-ebaa-4a70-a448-a0a195f7088b" />



# 3. Laiteluettelo
| Laite | Tarkoitus |
|---------|---------|
| r1 | reititin joka yhdistää käyttäjäverkon r2:n|
| r2 | yhdistää r1 ja r3 reitittimet ja palvelinverkon ja hallintoverkon kai|
| r3 | yhdistää toimipisteen verkon r2 reitittimeen ja siten muualle |
| client1 | käyttäjäkone|
| attacker | kone jolla voidaan esimerkiksi kuormittaa verkkoa|
| web1 | verkkopalvelin|
| db1 | tietokantapalvelin |
| branch-client | toimipisteen käyttäjäkone|
| ansible | palvelin jota käytetään verkon ja palvelinten konfigurointiin|
| prometheus | palvelin jolla monitorodaan verkkoa ja palvelimia|
| grafana | palvelin jolla voidaan visualisoida monitoroinnista kerättyä dataa|
| zabbix | verkon ja palvelimien valvontajärjestelmä|

# 4. IP-suunnitelma
| Verkko | Tarkoitus | Yhdyskäytävä |
|---------|---------|---------|
| 10.10.10.0/24 | User Network | r1 10.10.10.1 |
| 10.10.20.0/24 | Server Network | r2 10.10.20.1 |
| 10.10.30.0/24 | Branch office Network | r3 10.10.30.1 |
| 10.10.99.0/24 | Management Network | r2y 10.10.99.1 |
| 10.255.12.0/30 | r1-r2 | ? |
| 10.255.23.0/30 | r2-r3 | ? |


# 5. Reitityksen analyysi
```text
root@client1:/# ip addr
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host
       valid_lft forever preferred_lft forever
2: eth0@if67: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP group default
    link/ether 02:66:ed:00:f0:e0 brd ff:ff:ff:ff:ff:ff link-netnsid 0
    inet 172.20.20.9/24 brd 172.20.20.255 scope global eth0
       valid_lft forever preferred_lft forever
71: eth1@if72: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 9500 qdisc noqueue state UP group default
    link/ether aa:c1:ab:15:3d:fd brd ff:ff:ff:ff:ff:ff link-netnsid 1
    altname clab-o-05031180f95d8850
    inet 10.10.10.101/24 scope global eth1
       valid_lft forever preferred_lft forever
    inet6 fe80::a8c1:abff:fe15:3dfd/64 scope link
       valid_lft forever preferred_lft forever
root@client1:/# ip route
default via 10.10.10.1 dev eth1
10.10.10.0/24 dev eth1 proto kernel scope link src 10.10.10.101
172.20.20.0/24 dev eth0 proto kernel scope link src 172.20.20.9
root@client1:/# ping -c 4 10.10.20.101
PING 10.10.20.101 (10.10.20.101) 56(84) bytes of data.
64 bytes from 10.10.20.101: icmp_seq=1 ttl=62 time=0.157 ms
64 bytes from 10.10.20.101: icmp_seq=2 ttl=62 time=0.060 ms
64 bytes from 10.10.20.101: icmp_seq=3 ttl=62 time=0.063 ms
64 bytes from 10.10.20.101: icmp_seq=4 ttl=62 time=0.116 ms

--- 10.10.20.101 ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3064ms
rtt min/avg/max/mdev = 0.060/0.099/0.157/0.040 ms
root@client1:/# ping -c 4 10.10.30.101
PING 10.10.30.101 (10.10.30.101) 56(84) bytes of data.
64 bytes from 10.10.30.101: icmp_seq=1 ttl=61 time=0.217 ms
64 bytes from 10.10.30.101: icmp_seq=2 ttl=61 time=0.146 ms
64 bytes from 10.10.30.101: icmp_seq=3 ttl=61 time=0.184 ms
64 bytes from 10.10.30.101: icmp_seq=4 ttl=61 time=0.087 ms

--- 10.10.30.101 ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3071ms
rtt min/avg/max/mdev = 0.087/0.158/0.217/0.048 ms
root@client1:/# traceroute 10.10.30.101
traceroute to 10.10.30.101 (10.10.30.101), 30 hops max, 60 byte packets
 1  10.10.10.1 (10.10.10.1)  0.390 ms  0.283 ms  0.272 ms
 2  10.255.12.2 (10.255.12.2)  0.264 ms  0.241 ms  0.231 ms
 3  10.255.23.2 (10.255.23.2)  0.219 ms  0.171 ms  0.156 ms
 4  10.10.30.101 (10.10.30.101)  0.143 ms  0.119 ms  0.102 ms
```
# 6. Yhteenveto
eniten aikaa käytin varmaankin laite luetteloon mutta se johtui vain siitä että olin pihalla noin niinku kuvainnollisesti.
tämä tehtävä sai minut ymmärtämää että dokumentaatio on erittäin tärkeä sillä ilman sitä on kaikki tuskaa! ja opin myös etten halua ikinä tehdä dokumentaatiota millekkään!
it-alan ammattilaista dokumentaatio auttaisi nopeuttamalla työtä siinä missä ilman dokumentaatiota täytyisi hänen ensin tutkiskella verkkoa ja pohtia että miksi kukaan olisi tälläisen verkon rakentanut niin hän voisi dokumentaation avulla nähdä ja ymmärtää nopeammin ja hyvä dokumentaatio saattaa jopa selittää että miksi ne päätökset jotka on tehty on tehty tai jotai.
