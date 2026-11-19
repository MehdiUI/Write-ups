# Wireshark: Traffic Analysis — Network Traffic Analysis (TryHackMe)

**Catégorie :** Blue Team / SOC / Network Security  
**Date de complétion :** 19/11/2026  
**Lien :** https://tryhackme.com/room/wiresharktrafficanalysis  
**Parcours :** [SOC Level 1](https://tryhackme.com/path/outline/soclevel1)

---

## 🎯 Objectif de la room

Troisième et dernier volet de la trilogie Wireshark, cette room marque le passage de **l'inspection de paquets** à la **détection d'anomalies et d'activités malveillantes** dans une capture réseau[reference:0]. L'objectif n'est plus seulement de filtrer ou de compter, mais de **corréler les informations dispersées dans les paquets** pour reconstruire une attaque : scan réseau, empoisonnement ARP, tunnélisation, fuite d'identifiants en clair, exploitation Log4j ou encore déchiffrement de TLS. La room couvre **onze tâches** avec des captures dédiées et un environnement en Split View.

---

## 🧠 Ce que j'ai appris

### Détection des scans Nmap

Un analyste SOC doit savoir **reconnaître la signature réseau** de chaque type de scan pour distinguer une reconnaissance légitime d'une activité suspecte[reference:2].

| Type de scan | Signature réseau | Filtre Wireshark clé |
|---|---|---|
| **TCP Connect** (`-sT`) | Handshake TCP complet (SYN → SYN/ACK → ACK), puis RST | `tcp.flags.syn == 1 && tcp.flags.ack == 0 && tcp.window_size > 1024` |
| **SYN scan** (`-sS`) | SYN → SYN/ACK → **RST** (pas de ACK final) | `tcp.flags == 2` (SYN seul) / `tcp.flags == 18` (SYN+ACK) |
| **UDP scan** (`-sU`) | Réponses **ICMP Port Unreachable** sur ports fermés | `icmp.type == 3 && icmp.code == 3` |

**Résultats de la capture :** **1000** scans TCP Connect, **1083** messages ICMP "Port Unreachable", et le port UDP **68** identifié comme ouvert dans la plage 55–70[reference:3].

### Empoisonnement ARP et interception HTTP (MITM)

ARP n'a **aucune authentification** : un attaquant peut répondre à la place de la passerelle pour s'insérer dans le flux (ARP Spoofing / MITM)[reference:4].

**Signaux de détection :**
- **Conflit ARP** : deux adresses MAC différentes revendiquent la même IP. Wireshark signale cela via `arp.duplicate-address-detected` / `arp.duplicate-address-frame`[reference:5].
- **Flood ARP** : une même MAC génère un volume anormal de requêtes ARP[reference:6].

**Conséquence pratique :** une fois le MITM en place, le trafic HTTP de la victime transite par l'attaquant — identifiants et données sensibles exposés en clair.

### Identification des hôtes : DHCP, NetBIOS, Kerberos

Pour **attribuer une activité à un hôte** au-delà de son IP, trois protocoles sont précieux[reference:7] :

- **DHCP** : `dhcp.option.hostname` révèle le nom d'hôte (ex. modèle de téléphone Galaxy), et `dhcp.option.requested_ip_address` associe un hôte à une IP demandée.
- **NetBIOS (NBNS)** : `nbns.name` + `nbns.flags.opcode == 5` isole les **enregistrements de nom** et permet de compter les tentatives d'enregistrement.
- **Kerberos** : `kerberos.CNameString` expose les **noms d'utilisateur** dans les tickets AS-REQ. Un `$` en suffixe indique un **compte machine** (ex. `xp1$`).

### Tunnélisation ICMP et DNS

Les attaquants cachent des données dans des protocoles légitimes pour contourner le périmètre[reference:8].

**ICMP tunneling :** les paquets ICMP avec un **payload anormalement gros** (`data.len > 64`) peuvent transporter un autre protocole. La capture révèle une bannière **OpenSSH** et des blocs d'échange de clés RSA encapsulés dans de l'ICMP Echo — signature d'un tunnel SSH[reference:9].

**DNS tunneling :** les requêtes DNS de tunnel se distinguent par des **sous-domaines très longs et encodés**, répétés vers un même domaine parent. Le filtre `dns.qry.name.len > 50` (ou `> 246` pour affiner) permet d'isoler le domaine suspect : **`dataexfil[.]com`**[reference:10].

### Analyse des protocoles en clair : FTP et HTTP

**FTP** : les identifiants et commandes circulent en clair. `ftp.response.code == 530` compte les **échecs d'authentification**, et une session acceptée permet de suivre les commandes `SIZE`, `STOR` et `RETR` pour reconstituer les transferts de fichiers.

**HTTP — User-Agent Analysis :** l'en-tête `User-Agent` est un **indicateur de compromission** sous-estimé. Dans la capture, **6 user-agents anormaux** ont été identifiés, dont :
- `Nmap Scripting Engine`
- `Wfuzz/2.4`
- `sqlmap/1.4#stable`
- une chaîne `${jndi:ldap://...}` — signature de **Log4Shell**
- `Mozlila/5.0` — une **faute de frappe subtile** dans "Mozilla" (packet 52)[reference:12]

**Log4j (Log4Shell)** : la phase d'attaque commence par un `POST` contenant `$` ou `==` dans le User-Agent (packet **444**). Le décodage base64 de la chaîne JNDI révèle l'IP de l'attaquant : **`62[.]210[.]130[.]250`**[reference:13].

### Déchiffrement TLS (HTTPS)

Avec une **clé de session TLS** (key log file), Wireshark peut déchiffrer le trafic HTTPS et révéler les flux **HTTP/2** sous-jacents. On passe alors des "blobs opaques" à une visibilité applicative complète : comptage des paquets HTTP/2, inspection des en-têtes (`:authority`) et recherche de contenu (flags, données sensibles) dans le trafic déchiffré[reference:14].

---

## 🛠️ Ce que j'ai manipulé

- **Nmap scans** : filtres `tcp.flags.syn`, `tcp.flags.ack`, `tcp.window_size`, `icmp.type == 3 && icmp.code == 3`, `udp.port in {55..70}` — comptage des **1000** scans TCP Connect et identification du port UDP **68** ouvert[reference:15].
- **ARP / MITM** : filtre `arp.duplicate-address-detected`, identification de la MAC attaquante (`00:0c:29:e2:18:b4`), comptage des requêtes ARP malveillantes et des paquets HTTP interceptés (`http && eth.dst == ATTACKER_MAC`).
- **HTTP credentials** : `http.request.method == "POST" && http.request.uri == "/userinfo.php" && frame contains "pass="` — extraction des paires login/mot de passe en clair.
- **DHCP / NetBIOS / Kerberos** : `dhcp.option.hostname contains "A30"`, `nbns.name contains "LIVALJM" && nbns.flags.opcode == 5`, `kerberos.CNameString == "u5"` et `kerberos.CNameString contains "$"`.
- **Tunnels ICMP/DNS** : `icmp && data.len > 64` (détection de SSH dans ICMP), `dns.qry.name.len > 50` (identification de `dataexfil[.]com`)[reference:19].
- **FTP** : `ftp.response.code == 530` (échecs de login), suivi de flux TCP pour lire la taille du fichier et les commandes de permission.
- **HTTP User-Agent** : extraction de `http.user_agent` en colonne, identification des **6 user-agents anormaux** (Nmap, sqlmap, Wfuzz, Log4Shell, Mozlila) et du packet **52** pour la faute de frappe[reference:21].
- **Log4Shell** : filtre `(http.user_agent contains "$") or (http.user_agent contains "==")` — packet **444**, décodage base64 de la commande JNDI → IP **`62[.]210[.]130[.]250`**[reference:22].
- **Déchiffrement TLS** : chargement du **key log file** dans Wireshark, passage aux flux **HTTP/2** déchiffrés et recherche du flag dans la session web[reference:23].

---

## 📌 Ce que ça m'apporte pour un SOC

- **Passage du filtre à l'investigation** : je ne me contente plus d'isoler des paquets — je **corrèle** les informations (scan → ARP poisoning → interception HTTP) pour reconstituer une chaîne d'attaque, exactement comme lors du triage d'une alerte réseau.
- **Détection multi-vecteurs** : je sais reconnaître les signatures de **scans Nmap**, d'**ARP spoofing**, de **tunnels ICMP/DNS**, d'**exfiltration DNS** et d'**exploitation Log4j** — un spectre large d'attaques courantes en environnement d'entreprise.
- **Attribution d'hôte** : grâce à DHCP, NetBIOS et Kerberos, je peux associer une IP à un **nom d'hôte, un utilisateur ou un compte machine**, ce qui est indispensable pour qualifier un incident et escalader avec des preuves.
- **Visibilité au-delà du chiffrement** : je sais utiliser un **key log TLS** pour déchiffrer du HTTPS et analyser le HTTP/2 sous-jacent — une compétence clé lorsque l'organisation dispose de la clé de session ou d'un proxy d'interception.
- **Chasse aux IOC dans les en-têtes** : les User-Agents (sqlmap, Nmap NSE, Log4Shell) sont des **indicateurs à bas coût** que je pense désormais à extraire systématiquement dans une capture HTTP.
- **Valeur pour un employeur** : cette room démontre que je suis capable de traiter une **capture complète** de bout en bout, de la reconnaissance à l'exploitation, et de documenter chaque étape avec le **filtre, le numéro de paquet et le champ** correspondant — la rigueur attendue d'un analyste SOC N1/N2 en analyse de trafic.

---

## ✅ Statut

- [x] Room terminée
- [x] Write-up publié