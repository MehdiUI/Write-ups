# Network Fundamentals — LetsDefend

**Catégorie :** Réseau  
**Date de sortie :** 2024
**Date de complétion :** 25/10/2026  
**Lien :** https://app.letsdefend.io/training/lessons/network-fundamentals

---

## 🎯 Objectif de la room

Acquérir les fondamentaux réseau nécessaires à un analyste SOC : modèle OSI, TCP/IP, protocoles courants et analyse de trafic.

---

## 🧠 Ce que j'ai appris

### Le modèle OSI (7 couches)

| Couche | Nom | Rôle |
|---|---|---|
| 7 | Application | Interface utilisateur (HTTP, DNS, SMTP) |
| 6 | Présentation | Chiffrement, encodage |
| 5 | Session | Gestion des sessions |
| 4 | Transport | TCP, UDP |
| 3 | Réseau | IP, routage |
| 2 | Liaison | MAC, Ethernet |
| 1 | Physique | Câbles, signaux |

### Le modèle TCP/IP (4 couches)

| Couche | Correspondance OSI |
|---|---|
| Application | OSI 5-6-7 |
| Transport | OSI 4 |
| Internet | OSI 3 |
| Accès réseau | OSI 1-2 |

### Les protocoles clés

| Protocole | Rôle | Port courant |
|---|---|---|
| **IP** | Adressage et routage | — |
| **TCP** | Connexion fiable (handshake SYN / SYN-ACK / ACK) | — |
| **UDP** | Sans connexion, plus rapide | — |
| **DNS** | Résolution de noms | 53 |
| **HTTP** | Requêtes web | 80 |
| **HTTPS** | Requêtes web chiffrées | 443 |
| **SMTP** | Envoi d'emails | 25 |
| **SSH** | Connexion distante sécurisée | 22 |
| **RDP** | Bureau à distance | 3389 |

> 💡 **Point clé retenu** : un analyste SOC doit savoir **lire un flux réseau** et **reconnaître un protocole anormal** dans les logs.

---

## 🛠️ Concepts manipulés

| Concept | Rôle |
|---|---|
| Modèle OSI | Décomposer une communication en 7 couches |
| Modèle TCP/IP | Modèle pratique d'Internet |
| Handshake TCP | Vérifier la connexion entre deux hôtes |
| DNS | Résolution de noms |
| Ports | Identifier le service associé à un flux |
| Adressage IP | Identifier la source et la destination |

---

## 🔍 Ce que je retiens pour la détection

- Un **scan de ports** génère beaucoup de paquets SYN vers des ports différents : c'est détectable dans les logs firewall.
- Un **trafic DNS anormal** (requêtes vers des domaines suspects, requêtes fréquentes vers le même domaine) peut indiquer une exfiltration ou un malware.
- Un **trafic HTTP vers une IP inconnue** peut être un signe de beaconing (communication périodique avec un C2).
- Connaître les **ports légitimes** permet de repérer les ports inhabituels (ex : un serveur web qui écoute sur le port 4444).
- Le **handshake TCP** permet de distinguer une connexion légitime d'un scan.

---

## 📌 Ce que je retiens pour un poste d'analyste SOC

- Comprendre le réseau est **indispensable** pour lire les logs firewall, proxy et IDS.
- Un analyste SOC doit savoir **distinguer un trafic normal d'un trafic suspect**.
- Les protocoles **DNS, HTTP et TCP** sont les plus fréquemment impliqués dans les incidents.
- La connaissance des ports et des protocoles permet de **qualifier une alerte réseau** rapidement.

---

## ✅ Statut

- [x] Room terminée
- [x] Write-up publié


---

*Write-up rédigé dans le cadre de ma préparation au poste d'Analyste SOC junior.*