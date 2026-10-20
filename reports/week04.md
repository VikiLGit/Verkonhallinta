
# Johdanto

Infrastructure as Code on infran määrittämistä ja hallintaa koodin avulla.


# Inventory

Inventory sisältää laitteet (ansible, attacker, branch-client, cadvisor, client1, db1, grafana, prometheus, r1, r2, r3, web1, zabbix) ja ne on luokissa seuraavasti: reitittimet (r1, r2, r3), asiakaskoneet (client1, attacker, branch-client), palvelimet (web1, db1), monitorointikoneet (prometheus, grafana, zabbix, cadvisor), hallinta (ansible), käyttäjäverkko (client1, attacker), palvelinverkko (web1, db1), toimipiste (branch-client), verkkolaitteet (reitittimet), linux laitteet (asiakaskoneet, palvelimet, monitorointikoneet, hallinta), ubuntu laitteet (client1, web1, db1, branch-client), node exporter (reitittimet asiakaskoneet, palvelimet).

Ryhmät auttavat laitteiden hallinnassa.

# Esimerkkiplaybookit

Playbook tekee yhteys testin. 
Tuloksista voidaan päätellä, ettei monitorointikoneissa ja reitittimissä ole ssh yhteyttä.

Playbookeissa käytetään seuraavia moduuleja: apt, file, get_url, unarchive, copy, shell, uri, debug, ja service.
Muuttujia on käytetty esim. node exportterin version valitsemiseen ja lataus url:n täydentämiseen dynaamisesti. Muuttujia on käytetty myös esim. tulostuksessa inventory_hostname, joka palauttaa palvelimen nimen tai jotai emt.
Handelers-lohkoa käytetään käynnistämään snmpd uudelleen playbookin lopussa, silloin kun snmpd.conf tiedostoon kirjoitetaan. 
Node Exporter playbook ei kirjoita conf tiedostoon mitään ja se taitaa käynnistyä uudelleen jokatapauksessa aina kun tuo playbook ajetaan.



# Oma playbook


```yml
- name: Marko ja Polo
  hosts: web1
  become: true

  vars:
    web_package: apache2
    html_dest: /var/www/html/index.html

  tasks:

    - name: Update package cache
      apt:
        update_cache: yes

    - name: Install web server package
      apt:
        name: "{{ web_package }}"
        state: present

    - name: Configure web server
      copy:
        dest: "{{ html_dest }}"
        content: |
          <!DOCTYPE html>
          <html>
          <head>
              <title>Web1</title>
          </head>
          <body>
              <h1>{{ inventory_hostname }}</h1>
              <p>hei</p>
          </body>
          </html>

      notify: Restart web server

    - name: Enable web server
      #ai code alert wee woo wee woo    
      shell: apache2ctl start
      register: apache_start
      failed_when: 
        - apache_start.rc != 0
        - "'already running' not in apache_start.stderr"
      changed_when: "'starting' in apache_start.stdout or apache_start.rc == 0"

    - name: Verify web server
      uri:
        url: http://localhost
        status_code: 200
      register: web_check

    - name: Display verification
      debug:
        msg: "Web server running on {{ inventory_hostname }}"

  handlers:

    - name: Restart web server
      service:
        name: "{{ web_package }}"
        state: restarted



```
```bash
root@ansible:/ansible/playbooks# ansible-playbook -i ../inventory.ini install-webserver.yml

PLAY [Marko ja Polo] ********************************************************************************************************************************************************************************************

TASK [Update package cache] *************************************************************************************************************************************************************************************
ok: [web1]

TASK [Install web server package] *******************************************************************************************************************************************************************************
ok: [web1]

TASK [Configure web server] *************************************************************************************************************************************************************************************
ok: [web1]

TASK [Enable web server] ****************************************************************************************************************************************************************************************
changed: [web1]

TASK [Verify web server] ****************************************************************************************************************************************************************************************
ok: [web1]

TASK [Display verification] *************************************************************************************************************************************************************************************
ok: [web1] => {
    "msg": "Web server running on web1"
}

PLAY RECAP ******************************************************************************************************************************************************************************************************
web1                       : ok=6    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0

```

# Vertailu

client1
| Kerättävä tieto | saatu arvo |
|---------|---------:|
| käyttöjärjestelmä | Ubuntu |
| IP-osoite | 172.20.20.5, 10.10.10.101 |
| prosessorien määrä | 16 |
| muistin määrä | 15843 mb |

web1
| Kerättävä tieto | saatu arvo |
|---------|---------:|
| käyttöjärjestelmä | Ubuntu |
| IP-osoite | 172.20.20.2, 10.10.20.101 |
| prosessorien määrä | 16 |
| muistin määrä | 15843 mb |

branch-client
| Kerättävä tieto | saatu arvo |
|---------|---------:|
| käyttöjärjestelmä | Ubuntu |
| IP-osoite | 172.20.20.4, 10.10.30.101 |
| prosessorien määrä | 16 |
| muistin määrä | 15843 mb |

db1
| Kerättävä tieto | saatu arvo |
|---------|---------:|
| käyttöjärjestelmä | Ubuntu |
| IP-osoite | 10.10.20.102, 172.20.20.8 |
| prosessorien määrä | 16 |
| muistin määrä | 15843 mb |

client 1
| Kerättävä tieto | saatu arvo |
|---------|---------:|
| käyttöjärjestelmä | Ubuntu |
| IP-osoite | 172.20.20.3, 10.10.10.200 |
| prosessorien määrä | 16 |
| muistin määrä | 15843 mb |


# Yhteenveto

ansiblen avulla voi asentaa palveluita sun muita playbook:in avulla joka voi sisältää kyseisen palvelun kaikki konfiguraatiot. ansible nopeuttaa varmasti palveluiden asennusta etenkin jos ne täytyy asentaa samat jutut monelle palvelimelle. infrastructure as code menettely näin yleisemmin mahdollistaa palveluiden konfiguraatioiden version hallinnan sun muun sillä infra on määritelty koodilla joka voi olla esim githubissa. jos kunfiguroidaan vain yksi palveli ja se tehdään vain kerran eikä palveluita päivitetä ikinä niin ansible tyyppinen ratkaisu ei mielestäni ole käsin tehtyä parempi. 
