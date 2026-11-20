# NetworkMiner — Network Security and Traffic Analysis (TryHackMe)

**Catégorie :** Blue Team / SOC / Network Forensics  
**Date de complétion :** 20/11/2026  
**Lien :** https://tryhackme.com/room/networkminer  
**Parcours :** [SOC Level 1](https://tryhackme.com/path/outline/soclevel1)

---

## 🎯 Objectif de la room

Découvrir **NetworkMiner**, un outil open-source d'analyse forensique réseau (NFAT) développé par Netresec, et apprendre à l'utiliser pour investiguer des captures PCAP. Contrairement à Wireshark, qui est **centré sur les paquets**, NetworkMiner est **centré sur les hôtes** : il réorganise automatiquement le trafic autour des entités communicantes (IP, MAC, hostnames, OS) et extrait les artefacts tangibles (fichiers, images, identifiants, sessions DNS). La room couvre l'interface, les différents onglets (Hosts, Sessions, DNS, Credentials, Files, Images, Parameters, Keywords, Messages, Anomalies), les cas d'usage en forensique et incident response, ainsi que les différences entre versions Free et Pro.

---

## 🧠 Ce que j'ai appris

### NetworkMiner vs Wireshark : deux approches complémentaires

- **Wireshark** : analyse **paquet par paquet**, orientée protocole et payload. Idéal pour l'investigation profonde.
- **NetworkMiner** : analyse **hôte par hôte**, orientée entité et artefact. Idéal pour un **premier triage rapide** et l'extraction automatique d'évidence.

La pratique recommandée en SOC est de **combiner les deux** : NetworkMiner pour la vue d'ensemble et l'extraction, puis Wireshark pour l'analyse fine d'un paquet ou d'un flux spécifique.

### Les modes opératoires

- **Mode Sniffer (live)** : capture en direct. Disponible mais **limité** (Windows uniquement, moins robuste que d'autres outils). Non recommandé comme sniffer principal.
- **Mode PCAP Parsing (offline)** : **mode principal** de la room et de l'usage réel en SOC. NetworkMiner parse un fichier `.pcap` et reconstruit tout l'écosystème d'hôtes, sessions, fichiers et identifiants.

### L'interface et les onglets clés

| Onglet | Rôle |
|---|---|
| **Hosts** | Liste triable des hôtes : IP, MAC, hostname, OS fingerprinté, ports ouverts, nombre de paquets et de sessions |
| **Sessions** | Détail des sessions client/serveur (protocole, ports, frame de début, horodatage) avec quatre modes de recherche : Exact Phrase, All Words, Any Word, RegEx |
| **DNS** | Requêtes et réponses DNS avec timestamps et TTL ; lookup Alexa Top 1M en version Pro |
| **Credentials** | Identifiants et hashes extraits automatiquement (HTTP, FTP, IMAP, SMTP, Kerberos, NTLM, RDP, SQL) |
| **Files / Images** | Fichiers et images reconstruits depuis le trafic, avec métadonnées et viewers intégrés |
| **Parameters / Keywords** | Paramètres HTTP et chaînes de caractères configurables pour la recherche |
| **Messages** | Emails et messages extraits |
| **Anomalies** | Détections légères de patterns d'exploit (ex. heuristique EternalBlue) et de spoofing |
| **Case Panel** | Gestion des PCAP chargés, métadonnées (hash MD5, frames, durée) |

### Les forces et limites de NetworkMiner

**Forces** :
- Découverte rapide du contexte des hôtes (IP, MAC, OS, ports) sans mettre de trafic sur le réseau.
- Extraction automatique de fichiers, images et identifiants — un gain de temps considérable pour le triage.
- Vue synthétique de l'activité réseau, excellente pour un **premier passage** avant une analyse plus profonde.

**Limites** :
- Pas fiable comme sniffer live principal.
- Mauvaise scalabilité sur de très gros PCAP (pas conçu pour du packet-level triage intensif).
- Filtrage et recherche moins riches que Wireshark.

---

## 🛠️ Ce que j'ai manipulé

- **Environnement** : VM Ubuntu 20.04 fournie par la room, avec **split-view** et fichiers d'exercice sur le Desktop. Deux versions de NetworkMiner disponibles (Free et Pro).
- **Chargement de PCAP** : ouverture de `mx-3.pcap` via `File → Open`, consultation des métadonnées dans le **Case Panel** (frames, hash MD5, durée de capture).
- **Onglet Hosts** : tri par adresse MAC pour identifier des hôtes partageant la même MAC (détection de spoofing ou de NAT), exploration des détails d'un hôte (OS, bannière web, paquets envoyés).
- **Onglet Credentials** : extraction d'un identifiant `#B\Administrator` et d'un hash **NTLMv2** à partir de `mx-4.pcap`, avec la logique de sélection de la dernière tentative de connexion réussie.
- **Onglet Files / Images** : reconstruction de fichiers et d'images depuis `mx-7.pcap`, identification de la source d'une image (`ads.bmp…`) et du frame associé.
- **Onglet Messages** : extraction d'un email dont le sujet commence par “You have more”, avec identification de la plateforme émettrice (**Facebook**) et de l'adresse de l'expéditeur.
- **Onglet Anomalies** : repérage d'une anomalie TLS potentielle sur un frame spécifique.
- **Comparaison de versions** : identification des fonctionnalités propres à la version **2.7** (détection de MAC dupliquées, gestion de frames) par rapport à la version Free.

---

## 📌 Ce que ça m'apporte pour un SOC

- **Triage réseau rapide** : je sais ouvrir un PCAP dans NetworkMiner et obtenir en quelques minutes une vue d'ensemble des hôtes, sessions, fichiers et identifiants — sans écrire une seule ligne de filtre.
- **Extraction d'évidence** : je peux reconstruire des fichiers, des images et des identifiants à partir d'une capture, ce qui est directement utile en **incident response** pour documenter une compromission.
- **Complémentarité avec Wireshark** : je comprends quand utiliser NetworkMiner (vue d'ensemble, extraction) et quand passer à Wireshark (analyse paquet, protocole, payload).
- **Détection d'anomalies simples** : je sais repérer des indicateurs comme des MAC dupliquées, des bannières serveur inattendues ou des anomalies TLS, et les relier à des hypothèses d'attaque.
- **Culture forensique** : je maîtrise le vocabulaire de l'analyse réseau (NFAT, host-centric, PCAP parsing, fingerprinting OS via Satori/p0f) et je peux l'employer correctement dans un rapport ou un échange avec un L2.
- **Pratique SOC Level 1** : cette room consolide le module **Network Security and Traffic Analysis** et prépare directement aux investigations réseau en conditions réelles.

---

## ✅ Statut

- [x] Room terminée
- [x] Write-up publié