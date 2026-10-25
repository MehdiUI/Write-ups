# Linux Fundamentals Part 1 — Cyber Security 101 (TryHackMe)

**Catégorie :** Linux  
**Date de sortie :** Juillet 2021  
**Date de complétion :** 25/10/2026  
**Lien :** https://tryhackme.com/room/linuxfundamentalspart1  
**Parcours :** [Cyber Security 101](https://tryhackme.com/path/outline/cybersecurity101)  
**Room suivante :** Linux Fundamentals Part 2

---

## 🎯 Objectif de la room

Acquérir les bases indispensables de Linux pour un analyste SOC : navigation dans le système de fichiers, commandes essentielles, gestion des utilisateurs et lecture de fichiers.

---

## 🧠 Ce que j'ai appris

### Les bases du système Linux

- **Structure du système de fichiers** : `/` (racine), `/home`, `/etc`, `/var`, `/tmp`, `/bin`
- **Utilisateur root** : super-utilisateur avec tous les droits
- **Utilisateurs standards** : droits limités, séparation des privilèges
- **Shell** : interface en ligne de commande (bash par défaut)

### Les commandes essentielles

| Commande | Rôle |
|---|---|
| `ls` | Lister les fichiers et dossiers |
| `cd` | Changer de répertoire |
| `pwd` | Afficher le répertoire courant |
| `cat` | Afficher le contenu d'un fichier |
| `find` | Rechercher des fichiers |
| `grep` | Rechercher un motif dans un fichier |
| `whoami` | Afficher l'utilisateur courant |
| `id` | Afficher les UID/GID de l'utilisateur |
| `su` / `sudo` | Changer d'utilisateur / exécuter en root |

### La gestion des fichiers

- **Chemins absolus** (`/home/user`) vs **relatifs** (`./fichier`)
- **`~`** = répertoire personnel de l'utilisateur courant
- **`.`** = répertoire courant, **`..`** = répertoire parent
- **Permissions de base** : lecture (r), écriture (w), exécution (x)

> 💡 **Point clé retenu** : Linux est **partout** dans les infrastructures (serveurs, cloud, SOC). Un analyste SOC doit savoir **naviguer rapidement** et **lire un fichier** pour investiguer.

---

## 🛠️ Commandes et concepts manipulés

| Concept | Rôle |
|---|---|
| Système de fichiers | Organisation hiérarchique des données |
| Utilisateurs / groupes | Séparation des privilèges |
| Shell bash | Interface de commande |
| Permissions | Contrôle d'accès aux fichiers |
| Chemins | Localiser un fichier dans l'arborescence |

---

## 🔍 Ce que je retiens pour la détection

- Un **fichier dans `/tmp`** est souvent suspect : c'est un répertoire world-writable utilisé par les malwares.
- Un **utilisateur récemment créé** dans `/etc/passwd` doit être vérifié (persistance).
- Un **fichier dans `/var/log`** est une source de preuve pour l'investigation.
- **`whoami` et `id`** permettent de vérifier les privilèges d'un processus ou d'un utilisateur.

---

## 📌 Ce que je retiens pour un poste d'analyste SOC

- Linux est **omniprésent** sur les serveurs et dans le cloud.
- Savoir **naviguer dans l'arborescence** et **lire un fichier de log** est indispensable.
- Comprendre les **permissions** et les **utilisateurs** permet de repérer une activité suspecte.
- Cette room pose les bases pour les **Part 2 et Part 3** (permissions avancées, processus, logs, cron).

---

## ✅ Statut

- [x] Room terminée
- [x] Write-up publié


---

*Write-up rédigé dans le cadre de ma préparation au poste d'Analyste SOC junior.*