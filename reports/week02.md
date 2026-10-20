# 1. Johdanto
SNMP on verkkolaitteiden valvontaan ja hallintaan käytettävä protokolla. SNMP mahdollistaa esimerkiksi laitteiden kuten reitittimien, kytkinten tai palvelimien tilan seurannan.

# 2. Asennus
```bash
root@web1:/# apt update
apt install snmp snmpd -y
Hit:1 http://security.ubuntu.com/ubuntu noble-security InRelease
Hit:2 http://archive.ubuntu.com/ubuntu noble InRelease
Hit:3 http://archive.ubuntu.com/ubuntu noble-updates InRelease
Hit:4 http://archive.ubuntu.com/ubuntu noble-backports InRelease
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
19 packages can be upgraded. Run 'apt list --upgradable' to see them.
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
snmp is already the newest version (5.9.4+dfsg-1.1ubuntu3.2).
snmpd is already the newest version (5.9.4+dfsg-1.1ubuntu3.2).
0 upgraded, 0 newly installed, 0 to remove and 19 not upgraded.
root@web1:/# service snmpd status
 * snmpd is not running

root@web1:/# nano /etc/snmp/snmpd.conf
root@web1:/# service snmpd restart
 * Restarting SNMP Services snmpd                                                                                                                                                                         [ OK ]
root@web1:/# ps aux | grep snmpd
Debian-+     175  0.0  0.0  20240  8040 ?        S    15:02   0:00 /usr/sbin/snmpd -LSwd -Lf /dev/null -u Debian-snmp -g Debian-snmp -I -smux mteTrigger mteTriggerConf -p /run/snmpd.pid
root         177  0.0  0.0   3536  1832 pts/1    S+   15:04   0:00 grep --color=auto snmpd
```

# 3. Kerätyt tiedot
```bash
root@ansible:/# snmpwalk -v2c -c public web1 system
SNMPv2-MIB::sysDescr.0 = STRING: Linux web1 6.18.33.2-microsoft-standard-WSL2 #1 SMP PREEMPT_DYNAMIC Thu Jun 18 21:54:43 UTC 2026 x86_64
SNMPv2-MIB::sysObjectID.0 = OID: NET-SNMP-MIB::netSnmpAgentOIDs.10
DISMAN-EVENT-MIB::sysUpTimeInstance = Timeticks: (1062) 0:00:10.62
SNMPv2-MIB::sysContact.0 = STRING: Me <me@example.org>
SNMPv2-MIB::sysName.0 = STRING: web1
SNMPv2-MIB::sysLocation.0 = STRING: Sitting on the Dock of the Bay
SNMPv2-MIB::sysServices.0 = INTEGER: 72
SNMPv2-MIB::sysORLastChange.0 = Timeticks: (0) 0:00:00.00
SNMPv2-MIB::sysORID.1 = OID: SNMP-FRAMEWORK-MIB::snmpFrameworkMIBCompliance
SNMPv2-MIB::sysORID.2 = OID: SNMP-MPD-MIB::snmpMPDCompliance
SNMPv2-MIB::sysORID.3 = OID: SNMP-USER-BASED-SM-MIB::usmMIBCompliance
SNMPv2-MIB::sysORID.4 = OID: SNMPv2-MIB::snmpMIB
SNMPv2-MIB::sysORID.5 = OID: SNMP-VIEW-BASED-ACM-MIB::vacmBasicGroup
SNMPv2-MIB::sysORID.6 = OID: TCP-MIB::tcpMIB
SNMPv2-MIB::sysORID.7 = OID: UDP-MIB::udpMIB
SNMPv2-MIB::sysORID.8 = OID: IP-MIB::ip
SNMPv2-MIB::sysORID.9 = OID: SNMP-NOTIFICATION-MIB::snmpNotifyFullCompliance
SNMPv2-MIB::sysORID.10 = OID: NOTIFICATION-LOG-MIB::notificationLogMIB
SNMPv2-MIB::sysORDescr.1 = STRING: The SNMP Management Architecture MIB.
SNMPv2-MIB::sysORDescr.2 = STRING: The MIB for Message Processing and Dispatching.
SNMPv2-MIB::sysORDescr.3 = STRING: The management information definitions for the SNMP User-based Security Model.
SNMPv2-MIB::sysORDescr.4 = STRING: The MIB module for SNMPv2 entities
SNMPv2-MIB::sysORDescr.5 = STRING: View-based Access Control Model for SNMP.
SNMPv2-MIB::sysORDescr.6 = STRING: The MIB module for managing TCP implementations
SNMPv2-MIB::sysORDescr.7 = STRING: The MIB module for managing UDP implementations
SNMPv2-MIB::sysORDescr.8 = STRING: The MIB module for managing IP and ICMP implementations
SNMPv2-MIB::sysORDescr.9 = STRING: The MIB modules for managing SNMP Notification, plus filtering.
SNMPv2-MIB::sysORDescr.10 = STRING: The MIB module for logging SNMP Notifications.
SNMPv2-MIB::sysORUpTime.1 = Timeticks: (0) 0:00:00.00
SNMPv2-MIB::sysORUpTime.2 = Timeticks: (0) 0:00:00.00
SNMPv2-MIB::sysORUpTime.3 = Timeticks: (0) 0:00:00.00
SNMPv2-MIB::sysORUpTime.4 = Timeticks: (0) 0:00:00.00
SNMPv2-MIB::sysORUpTime.5 = Timeticks: (0) 0:00:00.00
SNMPv2-MIB::sysORUpTime.6 = Timeticks: (0) 0:00:00.00
SNMPv2-MIB::sysORUpTime.7 = Timeticks: (0) 0:00:00.00
SNMPv2-MIB::sysORUpTime.8 = Timeticks: (0) 0:00:00.00
SNMPv2-MIB::sysORUpTime.9 = Timeticks: (0) 0:00:00.00
SNMPv2-MIB::sysORUpTime.10 = Timeticks: (0) 0:00:00.00

root@ansible:/# snmpget -v2c -c public web1 sysName.0
SNMPv2-MIB::sysName.0 = STRING: web1
root@ansible:/# snmpget -v2c -c public web1 sysDescr.0
SNMPv2-MIB::sysDescr.0 = STRING: Linux web1 6.18.33.2-microsoft-standard-WSL2 #1 SMP PREEMPT_DYNAMIC Thu Jun 18 21:54:43 UTC 2026 x86_64
root@ansible:/# snmpget -v2c -c public web1 sysUpTime.0
DISMAN-EVENT-MIB::sysUpTimeInstance = Timeticks: (89302) 0:14:53.02
```

# 4. Verkkorajapinnat
```bash
root@ansible:/# snmpwalk -v2c -c public web1 ifDescr
IF-MIB::ifDescr.1 = STRING: lo
IF-MIB::ifDescr.2 = STRING: eth0
IF-MIB::ifDescr.80 = STRING: eth1
```
3 verkkorajapintaa
uskoisin että eth0 on verkko?

# 5. OID-analyysi
| OID | Tarkoitus |
|------|------|
| sysName.0 | laitteen nimi|
| sysDescr.0 | laitteen kuvaus|
| sysUpTime.0 | käynnissä olo aika|
| ifDescr | verkkokortin tai liitännän kuvaus|
| ifOperStatus | toiminnallinen tila|

| Laite | Nimi | Käyttöjärjestelmä | Uptime |
|---------|---------|---------|---------|
| web1 | web1 | linux | 5:26:43.19  |
| db1 | db1 | Linux | 0:20:34.68 |
| branch-client | branch-client | Linux |0:19:44.17 |

# 6. Pohdinta
SNMP mahdollistaa datan keräyksen, laitteiden hallinnan, ja etävalvonnan.
SNMP:n avulla voi kerätä lähes mitävain tietoa laitteesta.
SNMPv2c:n suurin ongelma on sen turvattomuus.
SNMPv3:a tulisi käyttää aina kun turvallisuudella on väliä.

