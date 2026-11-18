# Wireshark: Packet Operations — Network Traffic Analysis (TryHackMe)

**Catégorie :** Blue Team / SOC / Network Security  
**Date de complétion :** 18/11/2026  
**Lien :** https://tryhackme.com/room/wiresharkpacketoperations  
**Parcours :** [SOC Level 1](https://tryhackme.com/path/outline/soclevel1)

---

## 🎯 Objectif de la room

Deuxième volet de la trilogie Wireshark, cette room passe des bases de la navigation à l'**analyse avancée au niveau paquet**[reference:0]. L'objectif est de savoir exploiter les **statistiques intégrées** de Wireshark pour prendre du recul sur une capture (qui parle à qui, quels protocoles, quels volumes), puis de maîtriser le **langage de filtrage** — des filtres d'affichage simples aux filtres avancés avec opérateurs, fonctions et expressions régulières — pour isoler l'aiguille dans la botte de foin[reference:1].

---

## 🧠 Ce que j'ai appris

### Le menu Statistics : prendre de la hauteur avant de filtrer

Avant de plonger dans les paquets, un analyste SOC doit d'abord **cadrer la capture**. Le menu `Statistics` de Wireshark offre cette vue d'ensemble[reference:2] :

| Sous-menu | Ce qu'il révèle | Usage SOC |
|---|---|---|
| **Resolved Addresses** | Correspondances IP ↔ noms DNS observés dans la capture | Identifier les ressources accédées (ex. repérer un domaine suspect) |
| **Protocol Hierarchy** | Répartition des protocoles en pourcentage | Détecter un protocole anormalement dominant (tunnel, exfiltration) |
| **Conversations** | Échanges entre paires d'endpoints (IPv4, TCP, UDP…) | Repérer des flux volumineux ou asymétriques |
| **Endpoints** | Liste des hôtes uniques avec détails (MAC vendor, ville, AS Organisation) | Enrichir le contexte : qui est réellement en face de cette IP ? |
| **GeoIP / Name Resolution** | Géolocalisation et résolution de noms | Prioriser l'investigation sur des sources géographiquement inattendues |

**Point clé sur les Endpoints** : les colonnes `Bytes`, `Tx Packets`, `Rx Packets`, `Tx Bytes`, `Rx Bytes` ne mesurent pas la même chose[reference:3]. `Bytes` = total échangé (Tx + Rx), tandis que `Tx Bytes` isole ce que l'hôte a **envoyé**. Cette distinction est essentielle pour repérer une exfiltration (Tx anormalement élevé) versus un simple téléchargement (Rx élevé).

### Protocol Details : zoomer sur un protocole

Une fois le cadre posé, `Statistics → [Protocole]` permet de descendre d'un niveau. Exemples concrets manipulés dans la room[reference:4] :
- **IPv4 → Destinations and Ports** : identifier l'adresse de destination la plus sollicitée (ex. `10.100.1.33`).
- **DNS** : lire le temps de réponse requête/réponse maximum (ex. `0.467897` s) — un délai anormal peut trahir un serveur DNS lent ou détourné.
- **HTTP** : compter les requêtes par hôte (ex. `39` requêtes vers `rad[.]msn[.]com`) — utile pour détecter du beaconing ou du polling C2.

### Le langage de filtrage : du simple au composé

La room couvre trois niveaux de filtrage :

**1. Filtres de protocole** (les plus simples) : `ip`, `tcp`, `dns`, `http`… Ils répondent à la question "combien de paquets de ce type ?"[reference:5].

**2. Filtres avec opérateurs de comparaison** : `==`, `!=`, `<`, `>`. Exemples :
- `ip.ttl < 10` → isole les paquets à TTL faible (signal de route complexe ou de spoofing)[reference:6].
- `tcp.port == 444` → cible un port précis[reference:7].
- `http.request.method == "GET" && tcp.port == 80` → combine protocole, méthode et port[reference:8].

**3. Filtres avancés avec fonctions et expressions régulières** :
- `ip.ttl matches "[02468]$"` → ne garder que les TTL **pairs** (technique d'échantillonnage pour réduire le bruit)[reference:9].
- `tcp.port in {3333, 4444, 9999}` → cibler plusieurs ports en une seule expression[reference:10].
- `http.server contains "Microsoft-IIS"` → filtrer sur une chaîne de caractères dans un champ applicatif[reference:11].

### Le profil "Checksum Control" : un cas d'usage défensif

La room introduit un **profil Wireshark** dédié au contrôle des checksums. En changeant de profil, on peut compter les paquets TCP avec un **checksum invalide** (ex. `34185` paquets "Bad TCP Checksum")[reference:12]. Pour un SOC, c'est un indicateur précieux : un checksum incorrect peut signifier une corruption, mais aussi une **altération malveillante** ou une tentative d'évasion.

---

## 🛠️ Ce que j'ai manipulé

- **Statistics → Resolved Addresses** : identification de l'IP associée à un hostname commençant par "bbc" (`199.232.24.81`)[reference:13].
- **Statistics → Conversations → IPv4** : comptage des conversations IPv4 (**435**)[reference:14].
- **Statistics → Endpoints (Ethernet)** : lecture des **bytes transférés** depuis l'adresse MAC "Micro-St" (**7474 kB**)[reference:15].
- **Statistics → Endpoints → IPv4** : comptage des IPs liées à "Kansas City" (**4**) et identification de l'IP liée à l'AS Organisation "Blicnet" (`188.246.82.7`)[reference:16].
- **Statistics → IPv4 → Destinations and Ports** : identification de la destination IPv4 la plus utilisée (`10.100.1.33`)[reference:17].
- **Statistics → DNS** : lecture du temps de réponse requête/réponse maximum (`0.467897`)[reference:18].
- **Statistics → HTTP** : comptage des requêtes HTTP vers `rad[.]msn[.]com` (**39**)[reference:19].
- **Filtres de protocole** : comptage des paquets IP (**81420**), des paquets avec TTL < 10 (**66**), des paquets sur le port TCP 444 (**632**), des requêtes HTTP GET vers le port 80 (**527**), des requêtes DNS de type A (**51**)[reference:20].
- **Filtrage avancé** :
  - Serveurs Microsoft IIS : paquets **non originaires du port 80** (**21**) et paquets avec **version 7.5** (**71**)[reference:21].
  - Ports **3333, 4444 ou 9999** : total de **2235** paquets[reference:22].
  - **TTL pairs** via regex (`matches "[02468]$"`) : **77289** paquets[reference:23].
- **Profil "Checksum Control"** : comptage des paquets **Bad TCP Checksum** (**34185**), puis utilisation d'un bouton de filtrage existant pour affiner (**261** paquets affichés)[reference:24].

---

## 📌 Ce que ça m'apporte pour un SOC

- **Cadrage avant creusage** : je ne me jette plus directement dans les filtres — je commence par `Statistics` pour comprendre la capture (protocoles, endpoints, géographie), puis je cible. C'est exactement la démarche d'un analyste qui doit **prioriser** face à des milliers de paquets.
- **Lecture des métadonnées d'endpoints** : je sais interpréter `Bytes` vs `Tx Bytes` vs `Rx Bytes` et en tirer des hypothèses (exfiltration vs téléchargement, beaconing régulier).
- **Maîtrise du langage de filtrage** : je peux construire des filtres simples, composés (`&&`, `||`) et avancés (`in {}`, `contains`, `matches` avec regex) — un gain de temps considérable en investigation.
- **Détection par anomalie de checksum** : je connais le profil "Checksum Control" et je sais pourquoi un checksum invalide mérite un coup d'œil (corruption vs altération).
- **Valeur pour un employeur** : cette room démontre que je ne me contente pas de "lire des paquets" — je sais **extraire des statistiques exploitables**, construire des filtres reproductibles et documenter une analyse avec des chiffres précis, ce qui est le quotidien d'un analyste N1/N2 en NTA.

---

## ✅ Statut

- [x] Room terminée
- [x] Write-up publié