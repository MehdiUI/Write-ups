# Network Traffic Basics — Network Traffic Analysis (TryHackMe)

**Catégorie :** Blue Team / SOC / Network Security  
**Date de complétion :** 17/11/2026  
**Lien :** https://tryhackme.com/room/networktrafficbasics  
**Parcours :** [SOC Level 1](https://tryhackme.com/path/outline/soclevel1)

---

## 🎯 Objectif de la room

Poser les **fondations de l'analyse de trafic réseau (NTA)** : comprendre pourquoi un analyste SOC doit aller au-delà des logs pour inspecter le contenu réel des paquets, ce que l'on peut observer à chaque couche du modèle TCP/IP, d'où vient le trafic (endpoints vs intermédiaires, flux North-South vs East-West), et comment capturer puis analyser le trafic (logs, capture complète, statistiques réseau)[citation:5][citation:8]. La room combine théorie et pratique avec deux scénarios concrets : une exfiltration via **DNS tunneling** et un téléchargement de fichier malveillant en HTTP.

---

## 🧠 Ce que j'ai appris

### Pourquoi analyser le trafic réseau ?

Les firewalls et équipements réseau **enregistrent les métadonnées** (requêtes DNS, ports, IPs) mais **pas le contenu** des communications. C'est précisément cette limite qui justifie l'analyse de trafic : un attaquant peut utiliser des enregistrements **TXT DNS** pour transmettre des commandes C2 à un hôte compromis, et seul le contenu du paquet révèle l'attaque[citation:1][citation:3].

**Cas concret de la room :** un hôte (`WIN-016`, `192.168.1.16`) génère un nombre inhabituel de requêtes DNS vers le même TLD avec des sous-domaines aléatoires (`aj39skdm.malicious-tld.com`, `msd91azx.malicious-tld.com`...), dont des requêtes **TXT**. En inspectant le contenu de la réponse DNS, on découvre une commande C2 encodée en base64 dans le champ TXT : c'est du **DNS Tunneling**[citation:1][citation:8].

**Pour un SOC, l'NTA permet de :**
- Détecter des activités suspectes ou malveillantes invisibles dans les logs seuls.
- Reconstruire une attaque lors d'une réponse à incident.
- Vérifier et valider les alertes (réduire les faux positifs).

### Ce que l'on peut observer à chaque couche (TCP/IP)

| Couche | Ce qu'on inspecte | Attaque détectable |
|---|---|---|
| **Application** | En-têtes HTTP, payload, noms de fichiers | Téléchargement de malware, exfiltration de données |
| **Transport** | Ports, flags TCP, **numéros de séquence** | **Session hijacking** (séquence incohérente) |
| **Internet** | Fragments IP, offsets | **Fragmentation attack** (évasion IDS) |
| **Lien** | Trames Ethernet, ARP | ARP poisoning |

**Détails pratiques retenus :**
- **Taille du ZIP** dans l'exemple HTTP : `Content-Length` révèle **10 485 760 octets** (10 Mo) — la taille seule est un signal (transfert inhabituel)[citation:5][citation:10].
- **Évasion IDS par fragmentation** : l'attaquant découpe le payload malveillant en petits fragments pour qu'aucune signature ne corresponde à un fragment isolé. La parade : la réassemblage côté IDS/NTA[citation:8][citation:9].
- **Détection de session hijacking** : surveiller les **numéros de séquence TCP** — une injection de paquets provoque des sauts ou doublons anormaux[citation:5][citation:9].

### Sources et flux de trafic

- **Endpoints** (postes, serveurs, VM, IoT) : génèrent la **majorité du trafic** — ils initient et terminent les communications[citation:9][citation:11].
- **Intermédiaires** (routeurs, switches, proxies) : forwardent le trafic, génèrent peu de paquets propres.
- **Flux North-South** : LAN ↔ WAN (Internet).
- **Flux East-West** : à l'intérieur du LAN (latéralisation, SMB interne).

**Point clé sur SMB :** avant qu'une session SMB ne s'établisse, **Kerberos** doit authentifier l'utilisateur auprès du contrôleur de domaine (KDC) et fournir un ticket de service. C'est pourquoi on voit du trafic Kerberos juste avant du SMB dans une capture[citation:9][citation:10].

**TLS (Transport Layer Security)** : chiffre le trafic applicatif (HTTPS). Conséquence pour l'NTA : sans inspection TLS (proxy intercepteur), on ne voit que les **métadonnées** (SNI, IPs, tailles de flux, timing)[citation:9].

### Méthodes d'observation du trafic

1. **Logs** : disponibles sur les équipements (firewall, proxy, DNS) — faciles d'accès mais incomplets (pas de payload).
2. **Full Packet Capture (PCAP)** : capture intégrale — soit via un **network tap** physique, soit via **port mirroring** sur un switch. Permet l'inspection du contenu mais coûteux en stockage.
3. **Statistiques réseau / NetFlow** : métadonnées agrégées (qui parle à qui, combien, quand) — idéal pour la détection d'anomalies à grande échelle[citation:11].

---

## 🛠️ Ce que j'ai manipulé

- **Scénario DNS Tunneling** : analyse d'une capture montrant des requêtes DNS répétées vers `malicious-tld.com` avec sous-domaines variables, puis inspection d'une réponse **TXT** contenant une commande C2 encodée (`SSBsb3ZlIHlvdXIgY3VyaW9zaXR5...`)[citation:1][citation:3].
- **Scénario HTTP** : identification de la taille d'un fichier ZIP téléchargé via l'en-tête `Content-Length` (**10 485 760 octets**), et extraction du flag `THM{FoundTheMalware}` dans le corps de la réponse HTTP[citation:5][citation:10].
- **Scénario DNS (flag)** : extraction du flag `THM{C2CommandFound}` dans une réponse DNS TXT[citation:5][citation:9].
- **Analyse TCP** : identification du **numéro de séquence** comme champ permettant de détecter une injection de paquets (session hijacking)[citation:5].
- **Analyse IP** : compréhension de l'attaque par **fragmentation** pour contourner les signatures IDS[citation:9].
- **Flux réseau** : distinction endpoints vs intermédiaires, North-South vs East-West, et rôle de **Kerberos** avant SMB[citation:11].

---

## 📌 Ce que ça m'apporte pour un SOC

- **Réflexe NTA** : je sais pourquoi et quand passer des logs à l'inspection de paquets — notamment pour détecter des canaux cachés comme le **DNS tunneling** que les logs seuls ne révèlent pas.
- **Lecture protocolaire** : je peux expliquer ce qu'on observe à chaque couche TCP/IP et quelles attaques y sont détectables (fragmentation → couche Internet, session hijacking → couche Transport).
- **Sources et flux** : je comprends la topologie du trafic (endpoints = majorité, Kerberos avant SMB) et je sais où placer une capture selon ce que je cherche à voir.
- **Méthodes de capture** : je connais les trois approches (logs, PCAP, NetFlow) et leurs compromis — une base pour choisir la bonne source selon le scénario d'investigation.
- **Valeur pour un employeur** : cette room démontre que je maîtrise les **fondamentaux de l'analyse réseau** côté défense — un prérequis indispensable pour tout poste SOC, avant même de toucher à des outils comme Zeek ou Security Onion.

---

## ✅ Statut

- [x] Room terminée
- [x] Write-up publié