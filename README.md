# Palvelimet ja Palvelinohjelmat II - TODO Lista

## 🚀 Ympäristön Pystytys

- [x] Vagrant asennettu CachyOS:ään
- [x] VirtualBox moduulit ladattu
- [x] Vagrantfile luotu kahdelle palvelimelle
- [x] Molemmat virtuaalikoneet käynnissä ja toimivat
- [x] SSH-yhteydet molempiin koneisiin toimivat
- [x] Ansible asennettu isäntäkoneelle
- [X] Ansible inventory-tiedosto luotu
- [X] Ansible-yhteys virtuaalikoneisiin testattu

---

## ⭐ Arvosana +1: Tiedostonjakopalvelin ja Varmuuskopiointi

### Verkkoasetukset
- [x] Host-only verkko-adapterit (enp0s8) konfiguroitu
- [x] IP-osoitteet annettu (192.168.56.10 ja 192.168.56.11)
- [x] Verkkojen toimivuus testattu

### Samba-tiedostonjako
- [x] `sambajako` käyttäjäryhmä luotu server1:lle
- [x] Samba asennettu server1:lle
  - [x] **Ansible**: Samba-asennus playbook
- [X] Samba-jako konfiguroitu vain `sambajako`-ryhmälle
  - [x] **Ansible**: Samba-konfiguraatio template
- [X] Käyttäjiä lisätty `sambajako`-ryhmään
  - [x] **Ansible**: Käyttäjien luonti ja ryhmäjäsenyys
- [X] Samba-yhteys testattu isäntäkoneelta IP-osoitteen kautta
- [X] Symlinkit luotu käyttäjien kotihakemistoihin
  - [x] **Ansible**: Symlinkien luonti

### Varmuuskopiointi
- [x] rsync asennettu molemmille palvelimille
  - [x] **Ansible**: rsync-asennus
- [x] Varmuuskopiointiskripti luotu
  - [x] **Ansible**: Skriptin deployaus
- [x] Varmuuskopiointi server1 → server2 testattu
- [x] Cron-job varmuuskopioinnille (valinnainen)
  - [x] **Ansible**: Cron-konfiguraatio

### Palomuuri (UFW)
- [x] UFW asennettu ja aktivoitu server1:lle
  - [x] **Ansible**: UFW-asennus ja aktivointi
- [x] SSH-portti (22) avattu
  - [x] **Ansible**: UFW-säännöt
- [x] Samba-portit avattu (137, 138, 139, 445)
  - [x] **Ansible**: UFW Samba-säännöt
- [x] Muut portit estetty (default deny)
- [x] Palomuurin toiminta testattu

### Dokumentaatio
- [ ] Selvitetty Samban käyttämät portit
- [ ] Kirjoitettu selitys palomuurin toiminnasta yleisellä tasolla
- [ ] Dokumentoitu palomuurisäännöt

---

## ⭐ Arvosana +1: Web-host

### Nginx-asennus ja käyttäjähallinta
- [x] Nginx asennettu server1:lle
  - [x] **Ansible**: Nginx-asennus playbook
- [x] `developers` käyttäjäryhmä luotu
  - [x] **Ansible**: Ryhmän ja käyttäjien luonti
- [x] `webmaster` käyttäjä luotu ja lisätty `developers`-ryhmään
- [x] Käyttöoikeudet nginx-konfiguraatioille ja verkkosivuille
  - [x] **Ansible**: File permissions management

### Verkkosivut ja hakemistorakenne
- [x] Verkkosivuhakemisto luotu `/srv/` alle (esim. `/srv/www`)
  - [x] **Ansible**: Hakemistorakenteen luonti
- [x] Verkkosivut luotu tai kopioitu
  - [x] **Ansible**: Verkkosivujen deployaus template
- [x] Virhesivut luotu (404, 500, 301)
  - [x] **Ansible**: Error pages deployment

### SSL/TLS-sertifikaatit
- [x] Hakemistot sertifikaateille luotu (ei oletushakemisto)
  - [x] **Ansible**: SSL-hakemistojen luonti
- [x] Itse-allekirjoitettu SSL-sertifikaatti luotu
  - [x] **Ansible**: Self-signed certificate generation
- [x] Käyttöoikeudet sertifikaateille (principle of least privilege)
  - [x] **Ansible**: Certificate permissions
- [x] Yksityinen avain suojattu (ei developers-ryhmälle lukuoikeutta)

### Nginx-konfiguraatio
- [x] Nginx konfiguroidtu käyttämään `/srv/www` hakemistoa
  - [x] **Ansible**: Nginx site configuration template
- [x] HTTP → HTTPS redirect konfiguroidtu
- [x] HTTPS konfiguroidtu SSL-sertifikaatilla
- [x] Virhesivut konfiguroidtu (404, 500, 301)
- [x] Nginx käynnistetty uudelleen
  - [x] **Ansible**: Nginx restart handler

### Testaus
- [ ] Verkkosivulle pääsy testattu HTTP:llä (pitäisi ohjautua HTTPS:ään)
- [ ] Verkkosivulle pääsy testattu HTTPS:llä
- [ ] Testattu isäntäkoneelta (esim. https://192.168.56.10)
- [ ] Virhesivut testattu (404, 500)

### Palomuuri
- [x] HTTP-portti (80) avattu UFW:ssä
  - [x] **Ansible**: UFW HTTP/HTTPS rules
- [x] HTTPS-portti (443) avattu UFW:ssä

### Dokumentaatio
- [ ] Selitetty käyttäjäryhmien merkitys tietoturvalle
- [ ] Selitetty sovellusten eristämisen merkitys
- [ ] Tutkittu HTTP-headerit tietoturvan kannalta:
  - [ ] Content-Security-Policy
  - [ ] X-Frame-Options
  - [ ] X-Content-Type-Options
  - [ ] Strict-Transport-Security (HSTS)
  - [ ] Referrer-Policy
- [ ] Dokumentoitu security headerit nginx-konfiguraatioon

---

## ⭐ Arvosana +1: DNS ja Containerit

### BIND9 DNS-palvelu
- [ ] BIND9 asennettu server1:lle
  - [ ] **Ansible**: BIND9 installation
- [ ] BIND9 konfiguroidtu `omalabra.local` domainille
  - [ ] **Ansible**: BIND9 zone configuration template
- [ ] A-record luotu: `www.omalabra.local` → server1 IP
  - [ ] **Ansible**: DNS records configuration
- [ ] BIND9 käynnistetty ja aktivoitu
  - [ ] **Ansible**: BIND9 service management
- [ ] DNS testattu server2:lta
- [ ] DNS testattu isäntäkoneelta
- [ ] UFW sääntö DNS:lle (portti 53)
  - [ ] **Ansible**: UFW DNS rule

### Docker-asennus
- [ ] Docker asennettu server1:lle
  - [ ] **Ansible**: Docker installation playbook
- [ ] Docker Compose asennettu
  - [ ] **Ansible**: Docker Compose installation
- [ ] Käyttäjä lisätty docker-ryhmään
  - [ ] **Ansible**: User docker group membership

### Docker Compose -verkkopalvelu
- [ ] Nginx-palvelu suljettu (konflikti Dockerin kanssa)
  - [ ] **Ansible**: Service stop and disable
- [ ] Docker Compose -tiedosto luotu
  - [ ] **Ansible**: Docker Compose file deployment
- [ ] Compose määrittelee nginx-containerin
- [ ] Containeriin mountattu `/srv/www` hakemisto
- [ ] Container käynnistetty (`docker compose up -d`)
- [ ] Verkkopalvelu testattu virtuaalikoneelta
- [ ] Verkkopalvelu testattu isäntäkoneelta

### Palomuuri ja Docker
- [ ] Tutkittu miten Docker käsittelee iptables/nftables sääntöjä
- [ ] Dokumentoitu Docker verkko-asetukset
- [ ] Tarvittavat UFW-säännöt Dockerille
  - [ ] **Ansible**: UFW Docker rules

### Dokumentaatio
- [ ] Selitetty Docker-arkkitehtuuri:
  - [ ] Containerit vs. virtuaalikoneet
  - [ ] Docker daemon
  - [ ] Docker images ja layers
  - [ ] Docker networking
- [ ] Dokumentoitu Docker ja palomuurin integraatio
- [ ] Selvitetty miksi Docker ohittaa UFW:n oletuksena

---

## ⭐ Arvosana +1: Docker Swarm

### Swarm-klusterin pystytys
- [ ] Docker Swarm alustettu server1:llä (manager)
  - [ ] **Ansible**: Docker Swarm init
- [ ] Server2 liitetty Swarm-klusteriin (worker)
  - [ ] **Ansible**: Join worker to swarm
- [ ] Swarm-tila tarkistettu (`docker node ls`)

### Docker Image ja palvelu
- [ ] Dockerfile luotu yksinkertaiselle nginx-palvelulle
  - [ ] **Ansible**: Dockerfile deployment
- [ ] Docker image builattu
  - [ ] **Ansible**: Docker image build task (valinnainen)
- [ ] Swarm service luotu
  - [ ] **Ansible**: Docker service deployment
- [ ] Service skaalattu useampaan replicaan

### Palomuuri Swarmille
- [ ] Dokumentoitu Swarm-portit:
  - [ ] 2377/tcp (cluster management)
  - [ ] 7946/tcp+udp (node communication)
  - [ ] 4789/udp (overlay network)
- [ ] UFW-säännöt Swarmille molemmilla palvelimilla
  - [ ] **Ansible**: UFW Swarm rules

### Testaus ja kuormantasaus
- [ ] Kyselyitä verkkosivulle useita kertoja
- [ ] Docker logs tutkittu (`docker service logs`)
- [ ] Dokumentoitu mihin nodeen kyselyt ohjautuvat
- [ ] Load balancing testattu
- [ ] Server2 sammutettu ja testattu klusterin toimivuus
- [ ] Dokumentoitu mitä tapahtui

### Dokumentaatio
- [ ] Pohdittu Swarmin hyödyt ja rajoitukset
- [ ] Verrattu Swarmia Kubernetesiin
- [ ] Pohdittu Swarm ja globaali skaalautuvuus
- [ ] Dokumentoitu high availability -ominaisuudet

---

## ⭐ Arvosana +1: Tietoturva

### Docker-tietoturva
- [ ] Tutkittu Docker-tietoturvaparhaita käytäntöjä
- [ ] Toteutettu tietoturvakonfiguraatioita:
  - [ ] Non-root käyttäjä containerissa
  - [ ] Read-only filesystem
  - [ ] Dropped capabilities
  - [ ] Resource limits (CPU, memory)
  - [ ] Security options (no-new-privileges, seccomp)
  - [ ] Network isolation
  - [ ] Secrets management
- [ ] **Ansible**: Security-hardened Docker Compose template

### Docker Image -tietoturva
- [ ] Minimoitu image-koko (alpine pohja?)
- [ ] Multi-stage build käytetty (jos soveltuu)
- [ ] Vulnerability scanning (Trivy, Docker Scout)
- [ ] Dokumentoitu löydetyt haavoittuvuudet ja korjaukset

### Dokumentaatio
- [ ] Listattu käytetyt tietoturvaparannukset
- [ ] Selitetty kunkin parannuksen vaikutus
- [ ] Dokumentoitu trade-offit (turvallisuus vs. käytettävyys)
- [ ] Benchmarkattu CIS Docker Benchmark vastaan (valinnainen)

---

## 🔧 Ansible Playbooks -rakenne

### Suunniteltu hakemistorakenne:
```
ansible/
├── inventory/
│   └── hosts.ini
├── group_vars/
│   └── all.yml
├── playbooks/
│   ├── 01-initial-setup.yml
│   ├── 02-samba-setup.yml
│   ├── 03-nginx-setup.yml
│   ├── 04-dns-setup.yml
│   ├── 05-docker-setup.yml
│   ├── 06-swarm-setup.yml
│   └── 07-security-hardening.yml
├── roles/
│   ├── common/
│   ├── samba/
│   ├── nginx/
│   ├── bind9/
│   ├── docker/
│   └── security/
└── templates/
    ├── smb.conf.j2
    ├── nginx-site.conf.j2
    ├── named.conf.j2
    └── docker-compose.yml.j2
```

### Ansible-tehtävät
- [ ] Ansible-hakemistorakenne luotu
- [ ] Inventory-tiedosto luotu
- [ ] Group variables määritelty
- [ ] Common-rooli: peruspakettien asennus, käyttäjät
- [ ] Samba-rooli täydellinen
- [ ] Nginx-rooli täydellinen
- [ ] BIND9-rooli täydellinen
- [ ] Docker-rooli täydellinen
- [ ] Security-rooli täydellinen
- [ ] Master playbook joka ajaa kaikki roolit

---

## 📝 Loppudokumentaatio

- [ ] README.md projektin juureen
- [ ] Arkkitehtuuridiagrammi
- [ ] Verkkokaavio
- [ ] Kuvakaappaukset testauksista
- [ ] Kaikki selvitykset kirjoitettu
- [ ] Ansible-dokumentaatio
- [ ] Troubleshooting-osio
- [ ] Lähteet ja referenssit

---

## 🎯 Yhteenveto

**Projektin tila:** Aloitettu - Vagrant ympäristö pystytetty

**Seuraavat askeleet:**
1. Käynnistä virtuaalikoneet ja testaa SSH-yhteydet
2. Asenna Ansible isäntäkoneelle
3. Luo Ansible inventory ja testaa yhteydet
4. Aloita Samba-tehtävästä

**Muistiinpanot:**
- IP-osoitteet: 192.168.56.10 (server1), 192.168.56.11 (server2)

