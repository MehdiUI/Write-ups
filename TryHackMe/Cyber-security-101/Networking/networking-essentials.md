# Networking Essentials — Cyber Security 101 (TryHackMe)

**Catégorie :** Réseau  
**Date de sortie :** 2024  
**Date de complétion :** 28/10/2026  
**Lien :** https://tryhackme.com/room/networkingessentials  
**Parcours :** [Cyber Security 101](https://tryhackme.com/path/outline/cybersecurity101)  
**Room précédente :** [Networking Concepts](./networking-concepts.md)  
**Room suivante :** Networking Core Protocols

---

## 🎯 Objectif de la room

Comprendre les mécanismes pratiques du réseau : l'adressage IP (IPv4 et IPv6), le découpage en sous-réseaux (subnetting), les ports et les protocoles de base.

---

## 🧠 Ce que j'ai appris

### L'adressage IPv4

Une adresse IPv4 est composée de 32 bits, divisés en 4 octets (ex: `192.168.1.1`). 
- **Adresses privées** (non routables sur Internet) : `10.0.0.0/8`, `172.16.0.0/12`, `192.168.0.0/16`.
- **Adresses publiques** : routables sur Internet.
- **Masque de sous-réseau** : détermine quelle partie de l'adresse correspond au réseau et quelle partie correspond à l'hôte (ex: `255.255.255.0` ou `/24`).

### L'adressage IPv6

IPv6 a été créé pour palier l'épuisement des adresses IPv4. Il utilise 128 bits (8 groupes de 4 chiffres hexadécimaux, ex: `2001:0db8:85a3:0000:0000:8a2e:0370:7334`).

### Le Subnetting (sous-réseaux)

Le subnetting permet de diviser un grand réseau en plusieurs petits réseaux logiques. C'est essentiel pour :
- La performance (réduire les domaines de broadcast).
- La sécurité (isoler des départements, cloisonner le réseau).

### Les ports et protocoles

Pour communiquer, les machines utilisent des ports. Les ports les plus importants à connaître pour un analyste SOC :
- **Port 22** : SSH (connexion distante sécurisée)
- **Port 53** : DNS (résolution de noms)
- **Port 80** : HTTP (web non chiffré)
- **Port 443** : HTTPS (web chiffré)
- **Port 3389** : RDP (bureau à distance Windows)

### Les protocoles réseau de base

- **DHCP** : Attribue automatiquement les adresses IP aux machines.
- **ARP** (Address Resolution Protocol) : Permet de trouver l'adresse MAC (physique) associée à une adresse IP.
- **ICMP** : Utilisé par la commande `ping` pour tester la connectivité.

---

## 📌 Ce que je retiens pour un poste d'analyste SOC

- **ARP** : L'ARP spoofing est une attaque très courante en réseau local (Man-in-the-Middle). Savoir comment fonctionne ARP permet de détecter ce type d'attaque.
- **RDP (3389)** : C'est le port le plus ciblé par les ransomwares (brute force RDP). Une alerte SOC sur des échecs de connexion RDP répétés est critique.
- **DHCP** : Un serveur DHCP rogue (non autorisé) peut distribuer de fausses adresses IP pour rediriger le trafic.
- **Subnetting** : En entreprise, les segments réseau sont séparés. Un mouvement latéral d'un attaquant se voit souvent par un trafic anormal entre deux sous-réseaux.

---

## ✅ Statut

- [x] Room terminée
- [x] Write-up publié

---

*Write-up rédigé dans le cadre de ma préparation au poste d'Analyste SOC junior.*