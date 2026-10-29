# Networking Secure Protocols — Cyber Security 101 (TryHackMe)

**Catégorie :** Réseau  
**Date de sortie :** 2024  
**Date de complétion :** 30/10/2026  
**Lien :** https://tryhackme.com/room/networkingsecureprotocols  
**Parcours :** [Cyber Security 101](https://tryhackme.com/path/outline/cybersecurity101)  
**Room précédente :** [Networking Core Protocols](./networking-core-protocols.md)  
**Room suivante :** Wireshark: The Basics

---

## 🎯 Objectif de la room

Comprendre comment les protocoles réseau (Web, Email, Accès distant) sont sécurisés grâce au chiffrement (TLS/SSL) et découvrir le fonctionnement des VPN.

---

## 🧠 Ce que j'ai appris

### TLS (Transport Layer Security)
TLS (et son prédécesseur SSL) est le protocole qui assure la confidentialité et l'intégrité des données sur le réseau. Il utilise des **certificats** pour authentifier le serveur et des algorithmes de chiffrement pour protéger les échanges.

### Les protocoles sécurisés (versions chiffrées)
Pour contrer les failles des protocoles en texte clair, des versions sécurisées ont été créées :
- **HTTPS** (HTTP Secure) : Utilise TLS sur le port **443**. Le trafic web est chiffré.
- **SMTPS** (SMTP Secure) : Envoi d'e-mails chiffré sur le port **465** (ou 587 avec STARTTLS).
- **POP3S** (POP3 Secure) : Réception d'e-mails chiffrée sur le port **995**.
- **IMAPS** (IMAP Secure) : Synchronisation d'e-mails chiffrée sur le port **993**.
- **SSH** (Secure Shell) : Remplace Telnet pour l'administration à distance (port **22**).

### Les VPN (Virtual Private Networks)
Un VPN crée un "tunnel" chiffré entre une machine et un réseau distant, permettant de traverser un réseau non sécurisé (comme Internet) de manière sécurisée.
- **IPsec** : Souvent utilisé pour les VPN site-à-site en entreprise.
- **WireGuard / OpenVPN** : Protocoles VPN modernes et rapides.

---

## 📌 Ce que je retiens pour un poste d'analyste SOC

- **Le défi du chiffrement** : Les analystes SOC ne peuvent pas lire le contenu du trafic HTTPS. Ils doivent donc se concentrer sur les **métadonnées** (adresses IP, noms de domaine via SNI, certificats TLS) pour détecter les menaces.
- **Command & Control (C2)** : Les attaquants utilisent le protocole HTTPS pour cacher leurs communications avec les machines compromises (beaconing) et contourner les pare-feux.
- **Certificats suspects** : Un certificat TLS auto-signé, expiré ou généré récemment sur un serveur inconnu est une excellente piste d'investigation.
- **VPN** : Les connexions VPN inhabituelles (un utilisateur qui se connecte depuis un pays lointain à 3h du matin) sont souvent le signe d'un compte compromis.

---

## ✅ Statut

- [x] Room terminée
- [x] Write-up publié

---

*Write-up rédigé dans le cadre de ma préparation au poste d'Analyste SOC junior.*