# Pre-Security — Network Fundamentals — TryHackMe

**Catégorie :** Réseau  
**Date de sortie :** Juillet 2021  
**Date de complétion :** 22/10/2026  
**Lien :** https://tryhackme.com/path/outline/presecurity

---

## 🎯 Objectif du module

Acquérir les bases du réseau indispensables à un analyste SOC : modèle OSI, TCP/IP, adressage, protocoles et analyse de paquets.

---

## 🧠 Ce que j'ai appris

### Les modules couverts

- **What is Networking?** — notions de base, adresses IP, MAC
- **Intro to LAN** — topologies, switch, routeur, DHCP
- **OSI Model** — les 7 couches et leur rôle
- **Packets & Frames** — encapsulation, TCP/UDP, ports
- **Extending Your Network** — NAT, VPN, VLAN

### Les notions clés

- **Modèle OSI** : 7 couches, de la physique à l'application.
- **TCP vs UDP** : TCP fiable (handshake), UDP rapide (sans connexion).
- **Adressage** : IP (réseau) et MAC (liaison).
- **Ports courants** : 80 (HTTP), 443 (HTTPS), 53 (DNS), 22 (SSH), 25 (SMTP).
- **DHCP** : attribution automatique des adresses IP.
- **NAT** : traduction d'adresses pour sortir sur Internet.

> 💡 **Point clé retenu** : un analyste SOC doit savoir **lire un flux réseau** et **reconnaître un protocole anormal** dans les logs.

---

## 🛠️ Concepts manipulés

| Concept | Rôle |
|---|---|
| Modèle OSI | Décomposer une communication en 7 couches |
| TCP/IP | Modèle pratique d'Internet |
| Handshake TCP | Vérifier la connexion entre deux hôtes |
| DNS | Résolution de noms |
| DHCP | Attribution automatique des IP |
| NAT | Traduction d'adresses |

---

## 🔍 Ce que je retiens pour la détection

- Un **scan de ports** génère beaucoup de paquets SYN vers des ports différents.
- Un **trafic DNS anormal** peut indiquer une exfiltration ou un malware.
- Connaître les **ports légitimes** permet de repérer les ports inhabituels.
- Le **handshake TCP** permet de distinguer une connexion légitime d'un scan.

---

## 📌 Ce que je retiens pour un poste d'analyste SOC

- Comprendre le réseau est **indispensable** pour lire les logs firewall, proxy et IDS.
- Un analyste SOC doit savoir **distinguer un trafic normal d'un trafic suspect**.
- Les protocoles **DNS, HTTP et TCP** sont les plus fréquemment impliqués dans les incidents.

---

## ✅ Statut

- [x] Module terminé
- [x] Write-up publié


---

*Write-up rédigé dans le cadre de ma préparation au poste d'Analyste SOC junior.*