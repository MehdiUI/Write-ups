# Networking Core Protocols — Cyber Security 101 (TryHackMe)

**Catégorie :** Réseau  
**Date de sortie :** 2024  
**Date de complétion :** 29/10/2026  
**Lien :** https://tryhackme.com/room/networkingcoreprotocols  
**Parcours :** [Cyber Security 101](https://tryhackme.com/path/outline/cybersecurity101)  
**Room précédente :** [Networking Essentials](./networking-essentials.md)  
**Room suivante :** Networking Secure Protocols

---

## 🎯 Objectif de la room

Découvrir les protocoles réseau fondamentaux utilisés au quotidien (Web, Email, Transfert de fichiers, Résolution de noms) et comprendre comment interagir avec eux.

---

## 🧠 Ce que j'ai appris

### Les protocoles du Web
- **HTTP** (HyperText Transfer Protocol) : Le protocole de base du web. Il fonctionne en texte clair sur le port **80**. Les requêtes principales sont `GET` (récupérer une page) et `POST` (envoyer des données, comme un formulaire).
- **HTTPS** : La version sécurisée de HTTP (chiffrée avec TLS/SSL) sur le port **443**.

### Les protocoles de transfert de fichiers
- **FTP** (File Transfer Protocol) : Permet de transférer des fichiers. Il utilise les ports **20** (données) et **21** (contrôle). **Attention : FTP est en texte clair** (les identifiants sont visibles sur le réseau).
- **SFTP** (SSH File Transfer Protocol) : Version sécurisée de FTP, fonctionne via SSH sur le port **22**.

### Les protocoles de messagerie (Email)
- **SMTP** (Simple Mail Transfer Protocol) : Utilisé pour **envoyer** des e-mails (port **25** ou **587**).
- **POP3** (Post Office Protocol v3) : Utilisé pour **télécharger** les e-mails sur un appareil (port **110**). Les messages sont souvent supprimés du serveur.
- **IMAP** (Internet Message Access Protocol) : Utilisé pour **synchroniser** les e-mails sur plusieurs appareils (port **143**). Les messages restent sur le serveur.

### Le système de noms de domaine (DNS)
- **DNS** (Domain Name System) : Traduit les noms de domaine (ex: `google.com`) en adresses IP (ex: `142.250.201.174`). Il utilise le port **53** (UDP ou TCP). 
- **WHOIS** : Un protocole (et une commande) qui permet de savoir à qui appartient un nom de domaine.

### Les protocoles d'accès à distance
- **Telnet** : Ancien protocole pour prendre le contrôle d'une machine à distance (port **23**). **Très dangereux aujourd'hui** car tout le trafic (y compris les mots de passe) circule en texte clair.
- **SSH** (Secure Shell) : Le remplaçant sécurisé de Telnet (port **22**). Tout le trafic est chiffré.

---

## 📌 Ce que je retiens pour un poste d'analyste SOC

- **Détection de texte clair** : Les analystes SOC doivent repérer l'utilisation de protocoles non chiffrés (HTTP, FTP, Telnet) dans les logs, car ils sont une faille de sécurité majeure.
- **Phishing et Email** : Comprendre SMTP, POP3 et IMAP est crucial pour analyser les en-têtes d'e-mails (Email Headers) lors d'une enquête sur du phishing.
- **DNS Tunneling** : Les attaquants utilisent souvent le protocole DNS (port 53) pour exfiltrer des données sans se faire remarquer. Savoir comment fonctionne DNS permet de détecter ces anomalies.
- **Telnet vs SSH** : Si vous voyez du trafic Telnet dans un réseau d'entreprise moderne, c'est une énorme alerte de sécurité.

---

## ✅ Statut

- [x] Room terminée
- [x] Write-up publié

---

*Write-up rédigé dans le cadre de ma préparation au poste d'Analyste SOC junior.*