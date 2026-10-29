# Wireshark: The Basics — Cyber Security 101 (TryHackMe)

**Catégorie :** Réseau & Analyse de trafic  
**Date de sortie :** 2024  
**Date de complétion :** 30/10/2026  
**Lien :** https://tryhackme.com/room/wiresharkthebasics  
**Parcours :** [Cyber Security 101](https://tryhackme.com/path/outline/cybersecurity101)  
**Room précédente :** [Networking Secure Protocols](./networking-secure-protocols.md)  
**Room suivante :** Tcpdump: The Basics

---

## 🎯 Objectif de la room

Apprendre à utiliser Wireshark, l'analyseur de protocoles réseau graphique, pour capturer, filtrer et analyser le trafic réseau.

---

## 🧠 Ce que j'ai appris

### Qu'est-ce que Wireshark ?

Wireshark est un outil d'analyse de paquets (packet sniffer). Il permet d'intercepter le trafic réseau qui passe par une interface (Ethernet, Wi-Fi) et de le disséquer pour voir exactement ce qui se dit entre deux machines (requêtes, réponses, données).

### L'interface

- **Barre de menus** : Fichier, Édition, Vue, etc.
- **Barre d'outils** : Boutons de démarrage/arrêt de capture.
- **Panneau de liste des paquets** : Affiche tous les paquets capturés avec leur numéro, heure, IP source/destination, protocole et informations.
- **Panneau des détails** : Affiche la structure du paquet sélectionné (couches OSI).
- **Panneau des octets (Bytes)** : Affiche les données brutes en hexadécimal et ASCII.

### Les filtres d'affichage (Display Filters)

C'est la compétence la plus importante. Wireshark capture des milliers de paquets, les filtres permettent de ne voir que ce qui nous intéresse.
- **Filtre par IP** : `ip.addr == 10.10.10.5`
- **Filtre par protocole** : `http`, `dns`, `tcp`, `udp`
- **Filtre par port** : `tcp.port == 80`
- **Filtre par combinaison** : `ip.addr == 10.10.10.5 and http`

### Le suivi de flux (Follow TCP Stream)

Un clic droit sur un paquet > "Follow" > "TCP Stream" permet de reconstituer une conversation complète entre deux machines. C'est extrêmement utile pour lire une requête HTTP, un échange de commandes, ou même extraire un fichier téléchargé.

### L'exportation d'objets

Wireshark permet d'extraire des fichiers (images, documents, exécutables) directement d'une capture réseau (File > Export Objects).

---

## 📌 Ce que je retiens pour un poste d'analyste SOC

- **Investigation de PCAP** : En cas d'alerte, un analyste SOC reçoit souvent une capture réseau (fichier `.pcap`) à analyser. Wireshark est l'outil indispensable pour la décortiquer.
- **Détection de C2 (Command & Control)** : Repérer des requêtes HTTP/DNS périodiques et suspectes vers une adresse IP inconnue (beaconing).
- **Analyse de malware** : Extraire des fichiers téléchargés (Payloads) via le trafic réseau (Export Objects).
- **Compréhension des protocoles** : Wireshark permet de voir la structure exacte des paquets (en-têtes TCP, IP) et de repérer les anomalies (fragmentation suspecte, TTL inhabituel).

---

## ✅ Statut

- [x] Room terminée
- [x] Write-up publié

---

*Write-up rédigé dans le cadre de ma préparation au poste d'Analyste SOC junior.*