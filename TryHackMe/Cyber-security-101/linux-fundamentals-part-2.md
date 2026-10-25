# Linux Fundamentals Part 2 — Cyber Security 101 (TryHackMe)

**Catégorie :** Linux  
**Date de sortie :** Juillet 2021  
**Date de complétion :** 25/10/2026  
**Lien :** https://tryhackme.com/room/linuxfundamentalspart2  
**Parcours :** [Cyber Security 101](https://tryhackme.com/path/outline/cybersecurity101)  
**Room précédente :** [Linux Fundamentals Part 1](./linux-fundamentals-part-1.md)  
**Room suivante :** [Linux Fundamentals Part 3](./linux-fundamentals-part-3.md)

---

## 🎯 Objectif de la room

Approfondir les bases Linux : gestion des permissions, utilisateurs et groupes, accès distant via SSH et transfert de fichiers.

---

## 🧠 Ce que j'ai appris

### Les permissions Linux

| Symbole | Signification | Valeur |
|---|---|---|
| `r` | Lecture | 4 |
| `w` | Écriture | 2 |
| `x` | Exécution | 1 |

- **3 blocs** : propriétaire (user), groupe (group), autres (others)
- **Exemple** : `-rwxr-xr--` = user (7), group (5), others (4)
- **Commandes** : `chmod` (modifier les permissions), `chown` (changer le propriétaire), `chgrp` (changer le groupe)

### Les utilisateurs et groupes

- **Fichiers clés** : `/etc/passwd`, `/etc/shadow`, `/etc/group`
- **Commandes** : `useradd`, `usermod`, `userdel`, `groupadd`, `passwd`
- **`sudo`** : exécuter une commande avec les droits root
- **`su`** : changer d'utilisateur

### Les bases de l'accès distant

- **SSH** : connexion chiffrée à un serveur distant (`ssh user@ip`)
- **SCP** : transfert de fichiers via SSH (`scp fichier user@ip:/chemin`)
- **Clés SSH** : authentification par paire de clés (privée/publique)

> 💡 **Point clé retenu** : les permissions sont **la première barrière de sécurité** sur Linux. Un analyste SOC doit repérer un fichier `777` ou un utilisateur avec des droits excessifs.

---

## 🛠️ Commandes et concepts manipulés

| Commande / Concept | Rôle |
|---|---|
| `chmod` | Modifier les permissions d'un fichier |
| `chown` | Changer le propriétaire |
| `chgrp` | Changer le groupe |
| `useradd` | Créer un utilisateur |
| `passwd` | Modifier le mot de passe |
| `sudo` | Exécuter en tant que root |
| `ssh` | Connexion distante sécurisée |
| `scp` | Transfert de fichiers via SSH |

---

## 🔍 Ce que je retiens pour la détection

- Un **fichier `777`** est une mauvaise pratique : n'importe qui peut le modifier ou l'exécuter.
- Un **utilisateur ajouté dans `/etc/passwd`** sans autorisation est une persistance possible.
- Un **compte avec `sudo`** non justifié doit être vérifié.
- Une **connexion SSH depuis une IP inconnue** est à investiguer (brute force, vol de clé).

---

## 📌 Ce que je retiens pour un poste d'analyste SOC

- Les **permissions** et les **comptes** sont les premières cibles d'un attaquant.
- Savoir **lire `/etc/passwd` et `/etc/group`** permet de repérer un compte malveillant.
- Comprendre **SSH et SCP** aide à identifier un mouvement latéral ou une exfiltration.
- Cette room prépare la **Part 3** (processus, services, logs, cron).

---

## ✅ Statut

- [x] Room terminée
- [x] Write-up publié

---

*Write-up rédigé dans le cadre de ma préparation au poste d'Analyste SOC junior.*