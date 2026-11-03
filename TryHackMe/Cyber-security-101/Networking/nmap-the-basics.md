# Nmap: The Basics — Cyber Security 101 (TryHackMe)

**Catégorie :** Réseau  
**Date de sortie :** 2024  
**Date de complétion :** 02/11/2026  
**Lien :** https://tryhackme.com/room/nmapthebasics  
**Parcours :** [Cyber Security 101](https://tryhackme.com/path/outline/cybersecurity101)  
**Room précédente :** [Tcpdump: The Basics](./tcpdump-the-basics.md)  
**Room suivante :** [Cryptography](../Cryptography/README.md)

---

## 🎯 Objectif de la room

Apprendre à utiliser Nmap, l'outil de référence pour la découverte de réseaux, le scan de ports et la détection de services. Indispensable pour cartographier la surface d'attaque d'une cible.

---

## 🧠 Ce que j'ai appris

### Host Discovery (Qui est en ligne ?)
Avant de scanner les ports, il faut savoir quelles machines sont allumées. L'option `-sn` (ping scan) permet de découvrir les hôtes en direct sans scanner leurs ports. On peut cibler une plage d'IP (`192.168.0.1-10`), un sous-réseau (`/24`) ou un nom d'hôte.

### Port Scanning (Qui écoute ?)
On scanne les ports TCP/UDP pour voir quels services tournent.
- `-sS` (SYN scan) : Furtif, n'ouvre pas de connexion complète (nécessite sudo).
- `-sT` (Connect scan) : Ouvre une connexion complète (par défaut sans sudo).
- `-F` : Scan rapide (100 ports les plus communs).
- `-p` : Spécifier une plage de ports (`-p 1-1024`).

### Version Detection (Extraire plus d'infos)
L'option `-sV` permet de connaître la version exacte du logiciel qui tourne sur un port. L'option `-O` tente de deviner le système d'exploitation. L'option `-A` fait tout ça en même temps (et plus encore). `-Pn` force le scan si la machine ne répond pas au ping.

### Timing (À quel point c'est rapide ?)
Pour éviter de se faire repérer par un IDS ou pour accélérer le scan, Nmap propose 6 templates de timing : `-T0` (paranoid) à `-T5` (insane).

### Output (Contrôler ce qu'on voit)
L'option `-v` (verbosité) affiche les étapes du scan en temps réel. L'option `-d` affiche les informations de débogage (debugging) très techniques. On peut sauvegarder le résultat en format normal (`-oN`), XML (`-oX`) ou grepable (`-oG`).

---

## 🖥️ Lignes de commande utilisées

Toutes les commandes ont été exécutées dans le terminal de l'AttackBox.

| Commande | Description |
|---|---|
| `nmap -sn 10.128.151.125` | Découvrir si l'hôte est en ligne (ping scan). |
| `nmap 10.128.151.125` | Scanner les 1000 ports les plus communs. |
| `nmap -sV -p 8008 10.128.151.125` | Détecter la version du service sur le port 8008. |
| `nmap -sL 192.168.0.1/27` | Lister les cibles du sous-réseau sans les scanner. |
| `nmap -sS -O 10.128.151.125` | Scan SYN avec détection d'OS (nécessite sudo). |
| `nmap -sS -sV 10.128.151.125` | Scan SYN avec détection de versions. |
| `nmap -A 10.128.151.125` | Scan agressif (OS, versions, traceroute). |

---

## 📌 Ce que je retiens pour un poste d'analyste SOC

- **Cartographie de surface d'attaque** : Nmap est la première étape d'un pentest (Red Team), mais aussi un outil de vérification pour les Blue Teams. Il permet de voir ce qui est exposé sur le réseau (ex: un serveur web oublié sur le port 8008).
- **Le bruit du scan** : Un scan `-sS` est plus furtif qu'un `-sT`, mais les IDS modernes détectent les deux. Connaître les templates de timing (`-T0` à `-T5`) est crucial pour simuler des attaques ou pour éviter de faire planter un serveur fragile lors d'un audit.
- **L'importance des versions** : Connaître la version exacte d'un service (`-sV`) permet de croiser l'information avec des bases de données de vulnérabilités (CVE) pour voir si un serveur est obsolète ou vulnérable.

---

## ✅ Statut

- [x] Room terminée
- [x] Write-up publié

---

*Write-up rédigé dans le cadre de ma préparation au poste d'Analyste SOC junior.*