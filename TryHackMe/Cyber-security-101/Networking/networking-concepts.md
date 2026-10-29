# Networking Concepts — Cyber Security 101 (TryHackMe)

**Catégorie :** Réseau  
**Date de sortie :** 2024  
**Date de complétion :** 28/10/2026  
**Lien :** https://tryhackme.com/room/networkingconcepts  
**Parcours :** [Cyber Security 101](https://tryhackme.com/path/outline/cybersecurity101)  
**Room précédente :** [Linux Shells](./linux-shells.md)  
**Room suivante :** Networking Essentials

---

## 🎯 Objectif de la room

Comprendre les concepts fondamentaux des réseaux informatiques : le modèle OSI, le modèle TCP/IP, les types de réseaux et le rôle des équipements.

---

## 🧠 Ce que j'ai appris

### Le modèle OSI (7 couches)

C'est un modèle théorique qui décompose la communication réseau en 7 couches distinctes. Chaque couche a un rôle précis et communique avec la couche au-dessus et en dessous d'elle.
- **7. Application** : Interface avec l'utilisateur (HTTP, DNS, SMTP).
- **6. Présentation** : Chiffrement, compression, encodage.
- **5. Session** : Gestion des sessions de communication.
- **4. Transport** : Fiabilité de la transmission (TCP, UDP).
- **3. Réseau** : Adressage logique et routage (IP).
- **2. Liaison de données** : Adressage physique (MAC) et accès au support.
- **1. Physique** : Transmission des bits (câbles, signaux).

### Le modèle TCP/IP (4 couches)

C'est le modèle pratique utilisé sur Internet. Il est plus simple et regroupe certaines couches du modèle OSI :
- **Application** (regroupe OSI 5, 6, 7).
- **Transport** (OSI 4).
- **Internet** (OSI 3).
- **Accès Réseau** (OSI 1, 2).

### Les types de réseaux

- **PAN** (Personal Area Network) : Très petite portée (ex : Bluetooth).
- **LAN** (Local Area Network) : Réseau local (maison, bureau).
- **WAN** (Wide Area Network) : Très grande échelle (Internet, réseaux d'entreprise).
- **CAN** (Campus Area Network) : Réseau à l'échelle d'un campus.
- **MAN** (Metropolitan Area Network) : Réseau à l'échelle d'une ville.

### Les équipements réseau

- **Hub** : Connecte les appareils mais diffuse les données à tout le monde (obsolète et peu sécurisé).
- **Switch** : Connecte les appareils et envoie les données uniquement au destinataire voulu (utilise les adresses MAC).
- **Routeur** : Connecte des réseaux différents entre eux (utilise les adresses IP).
- **Pare-feu (Firewall)** : Filtre le trafic réseau entrant et sortant selon des règles de sécurité.

---

## 📌 Ce que je retiens pour un poste d'analyste SOC

- **Modèle OSI** : Quand un analyste SOC reçoit une alerte, il doit savoir à quelle couche se situe le problème (Couche 3 pour une IP suspecte, Couche 4 pour un scan de ports, Couche 7 pour une attaque web).
- **Switch vs Routeur** : Comprendre comment les logs sont générés par ces équipements est crucial pour la détection.
- **LAN vs WAN** : En entreprise, le SOC surveille le trafic à la frontière entre le LAN (interne) et le WAN (Internet) pour détecter les intrusions.

---

## ✅ Statut

- [x] Room terminée
- [x] Write-up publié

---

*Write-up rédigé dans le cadre de ma préparation au poste d'Analyste SOC junior.*