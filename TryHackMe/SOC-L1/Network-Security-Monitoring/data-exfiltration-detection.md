# Data Exfiltration Detection — Network Security Monitoring (TryHackMe)

**Catégorie :** Blue Team / SOC / Network Security Monitoring  
**Date de complétion :** 25/11/2026  
**Lien :** https://tryhackme.com/room/dataexfildetection  
**Parcours :** [SOC Level 1](https://tryhackme.com/path/outline/soclevel1)

---

## 🎯 Objectif de la room

Apprendre à **détecter l'exfiltration de données** à travers quatre canaux réseau distincts : **DNS Tunneling**, **FTP**, **HTTP** et **ICMP**. La room fournit des captures PCAP et des logs DNS pré-ingérés dans une instance Splunk, et demande d'investiguer chaque canal pour identifier les hôtes compromis, les fichiers exfiltrés et les flags cachés dans les transferts. L'objectif est de passer d'une détection basée sur la réputation à une détection **comportementale**, en repérant les anomalies de volume, de pattern et de contenu dans le trafic sortant.

---

## 🧠 Ce que j'ai appris

### Les canaux d'exfiltration et leurs signatures

L'exfiltration de données est l'**objectif final** de la plupart des intrusions. L'attaquant cherche à faire sortir l'information sans être détecté, en utilisant des protocoles légitimes comme vecteur.

| Canal | Technique d'exfiltration | Signature de détection |
|---|---|---|
| **DNS** | Encodage des données dans des sous-domaines de requêtes DNS | Requêtes longues (> 30 caractères), volume anormal vers un même domaine parent, labels encodés (base64, hex) |
| **FTP** | Upload de fichiers via des comptes compromis (guest, root) | Connexions répétées depuis un compte, fichiers `STOR` inhabituels (ex. `customer_data.xlsx`), volume de données sortant élevé |
| **HTTP** | POST de données vers un serveur externe | Requêtes `POST` avec un `frame.len` élevé, corps de requête contenant des données sensibles, destination inconnue |
| **ICMP** | Données encapsulées dans des paquets `echo request` | Paquets ICMP de taille anormale (`frame.len > 100`), payload ASCII lisible au lieu des données de remplissage habituelles |

### La méthodologie de détection

La room suit une approche systématique pour chaque canal :

1. **Analyse de volume** : identifier les hôtes qui envoient anormalement plus de données que les autres (ex. `192.168.1.103` pour DNS, `192.168.1.105` pour FTP).
2. **Analyse de pattern** : repérer les requêtes qui sortent de l'ordinaire (longueur des requêtes DNS, taille des paquets ICMP, `frame.len` des POST HTTP).
3. **Analyse de contenu** : suivre le flux (TCP Stream, HTTP Stream) pour extraire les données réelles et confirmer la nature sensible du transfert.
4. **Corrélation** : relier l'hôte source, le canal utilisé et le fichier/flagg exfiltré pour produire une conclusion exploitable.

### L'importance du contexte

Un transfert sortant n'est pas forcément malveillant : les sauvegardes cloud, les mises à jour logicielles ou les API légitimes génèrent aussi du trafic sortant. La détection d'exfiltration repose donc sur la **combinaison** de plusieurs signaux : volume anormal, pattern inhabituel, destination inconnue, compte compromis. Un seul signal ne suffit pas.

---

## 🛠️ Ce que j'ai manipulé

### Environnement

- **VM Ubuntu** avec le dossier `~/Desktop/data_exfil/` contenant :
  - `dns_exfil/dns_exfil.log` (logs DNS au format texte)
  - `dns_exfil/dns_exfil.pcap`
  - `ftp_exfil/ftp_lab.pcap`
  - `http_exfil/http_lab.pcap`
  - `icmp_exfil/icmp_lab.pcap`
- **Instance Splunk** accessible sur `MACHINE_IP:8000`, avec les logs pré-ingérés dans l'index `data_exfil` (sourcetype `dns_logs`).

### Task 3 — Classification des techniques

- Identification de la catégorie d'exfiltration pour HTTP : **Network-based** (par opposition à Physical, Host-based, etc.).

### Task 4 — DNS Tunneling

- **Analyse des logs DNS** avec Splunk :
  - `index="data_exfil" sourcetype="dns_logs" | stats count by query | sort -count` pour identifier les domaines les plus interrogés.
  - `eval query_length=len(query) | where query_length > 30` pour isoler les requêtes anormalement longues.
- **Résultats** :
  - Domaine suspect : **`tunnelcorp.net`**
  - Nombre de requêtes suspectes : **315**
  - IP locale ayant envoyé le plus de requêtes : **`192.168.1.103`**
- **Méthode alternative** (hors Splunk) : script Python pour extraire les suffixes de domaine et compter les requêtes longues, confirmant les mêmes résultats.

### Task 5 — FTP

- **Ouverture de `ftp_lab.pcap` dans Wireshark**.
- **Comptage des connexions guest** : filtre `ftp.request.command == "USER" && ftp.request.arg == "guest"` → **5** connexions.
- **Identification du fichier exfiltré par le compte root** : filtre `ftp.request.command == "USER" && ftp.request.arg == "root"`, puis `Follow → TCP Stream` pour lire la commande `STOR` → **`customer_data.xlsx`**.
- **Identification de l'IP interne envoyant le plus gros payload** : filtre `ftp && frame.len > 90`, tri par taille de frame → **`192.168.1.105`**.
- **Extraction du flag** dans le flux TCP contenant le fichier CSV → **`THM{ftp_exfil_hidden_flag}`**.

### Task 6 — HTTP

- **Ouverture de `http_lab.pcap` dans Wireshark**.
- **Filtrage des POST volumineux** : `http.request.method == "POST" && frame.len > 750` pour isoler la requête d'exfiltration parmi les uploads normaux.
- **Hôte compromis identifié** : **`192.168.1.103`** (colonne `Source` de la requête POST).
- **Extraction du flag** dans le corps de la requête via `Follow → HTTP Stream` → **`THM{http_raw_3xf1ltr4t10n_succ3ss}`**.

### Task 7 — ICMP

- **Ouverture de `icmp_lab.pcap` dans Wireshark**.
- **Filtrage des echo requests volumineux** : `icmp.type == 8 && frame.len > 100` pour repérer les paquets anormalement gros.
- **Inspection du contenu** : lecture du panneau `Packet Bytes` en ASCII pour reconstituer les fragments d'un document caché dans le payload ICMP.
- **Extraction du flag** à partir des fragments ASCII lisibles, en préservant les caractères sur les coupures de ligne.

---

## 📌 Ce que ça m'apporte pour un SOC

- **Détection multi-canal** : je sais investiguer l'exfiltration à travers quatre protocoles différents (DNS, FTP, HTTP, ICMP) en appliquant les bons filtres Wireshark et les bonnes requêtes Splunk pour chaque canal.
- **Réflexe "volume + pattern + contenu"** : face à un trafic sortant suspect, je ne me limite pas à une seule dimension ; je corrèle le volume anormal, le pattern inhabituel et le contenu du transfert pour confirmer ou infirmer l'exfiltration.
- **Maîtrise de Wireshark avancé** : je suis à l'aise avec les filtres d'affichage (`ftp.request.command`, `http.request.method`, `icmp.type`), le suivi de flux (`Follow → TCP/HTTP Stream`) et la lecture du payload en ASCII/hex.
- **Requêtes Splunk appliquées** : je sais construire des requêtes pour agréger, filtrer par longueur et trier des logs DNS afin d'isoler un domaine suspect et son émetteur principal.
- **Compréhension de l'exfiltration par DNS Tunneling** : je reconnais les signatures d'un tunnel DNS (requêtes longues, labels encodés, domaine parent unique) et je sais pourquoi ce canal est prisé des attaquants (souvent autorisé par les firewalls).
- **Production de preuves** : pour chaque canal, je peux documenter l'hôte source, le canal utilisé, le fichier ou les données exfiltrées et le flag associé — une compétence directement transférable à la rédaction d'un rapport d'incident.

---

## ✅ Statut

- [x] Room terminée
- [x] Write-up publié