# Introduction to SIEM — Cyber Security 101 (TryHackMe)

**Catégorie :** SIEM  
**Date de sortie :** 2023  
**Date de complétion :** 21/10/2026  
**Lien :** https://tryhackme.com/room/introtosiem  
**Parcours :** [Cyber Security 101](https://tryhackme.com/path/outline/cybersecurity101)

---

## 🎯 Objectif de la room

Comprendre les concepts de base d'un SIEM (Security Information and Event Management) : collecte, centralisation et corrélation des logs.

---

## 🧠 Ce que j'ai appris

### Qu'est-ce qu'un SIEM ?

Un SIEM est un outil qui collecte des données depuis diverses sources (endpoints, équipements réseau), les stocke de manière centralisée et effectue des corrélations[reference:12].

### La visibilité réseau

Pour qu'un SIEM soit efficace, il faut avoir une bonne visibilité sur ce qui se passe dans le réseau. Les sources de logs se divisent en deux catégories[reference:13] :
- **Host-Centric (centré sur l'hôte)** : événements internes à une machine (ex : accès à un fichier, exécution de processus, logs Windows Event, Sysmon, Osquery).
- **Network-Centric (centré sur le réseau)** : événements liés aux communications (ex : connexions SSH, VPN, trafic HTTP/FTP).

### L'ingestion des logs

Le SIEM doit être capable d'ingérer des logs de sources très variées et de les normaliser pour pouvoir les corréler.

### Pourquoi un SIEM est nécessaire

Sans SIEM, il est impossible d'examiner manuellement les centaines d'événements générés chaque seconde par les différentes machines. Le SIEM permet de centraliser et d'alerter sur les comportements suspects[reference:14].

### Analyse des logs et alertes

La room se termine par un exercice pratique où l'on utilise un SIEM (Splunk) pour analyser des logs et répondre à des questions sur des tentatives de connexion ou des activités suspectes.

---

## 📌 Ce que je retiens pour un poste d'analyste SOC

- Un analyste SOC passe son temps à naviguer dans les logs via un SIEM (Splunk, Wazuh, ELK, etc.).
- Il est crucial de comprendre la différence entre les logs host-centriques et network-centriques pour savoir où chercher.
- La corrélation est ce qui transforme des logs isolés en alertes exploitables.

---

## ✅ Statut

- [x] Room terminée
- [x] Write-up publié