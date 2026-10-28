# Linux Shells — Cyber Security 101 (TryHackMe)

**Catégorie :** Linux & Command Line  
**Date de sortie :** Juillet 2021  
**Date de complétion :** 28/10/2026  
**Lien :** https://tryhackme.com/room/linuxshells  
**Parcours :** [Cyber Security 101](https://tryhackme.com/path/outline/cybersecurity101)  
**Room précédente :** [Windows PowerShell](./windows-powershell.md)

---

## 🎯 Objectif de la room

Découvrir ce qu'est un shell Linux, les différents types de shells existants (Bash, Zsh, etc.) et apprendre à utiliser les fonctionnalités de base de Bash pour l'administration et l'investigation.

---

## 🧠 Ce que j'ai appris

### Qu'est-ce qu'un shell ?

Le shell est l'interface qui permet à l'utilisateur de communiquer avec le noyau du système d'exploitation. C'est un programme qui lit les commandes tapées par l'utilisateur et les transmet au système.

### Les différents types de shells

Il existe plusieurs shells sous Linux, avec des fonctionnalités variables :
- **Bash** (Bourne Again SHell) : le plus courant, celui par défaut sur la plupart des distributions Linux.
- **Zsh** : très populaire, avec des fonctionnalités avancées (autocomplétion, thèmes).
- **Fish** : orienté utilisateur, avec une configuration interactive.
- **Sh** : le shell historique de base.

### Les fonctionnalités de Bash

- **Historique des commandes** : accessible avec la flèche du haut, ou via la commande `history`.
- **Variables d'environnement** : création, modification et affichage de variables (ex : `export NOM=valeur`, `echo $NOM`).
- **Scripts Bash** : création de fichiers `.sh` pour automatiser des tâches.
- **Pipes et redirections** : `|`, `>`, `>>`, `<`, utilisés pour manipuler les flux de données.

### Les commandes essentielles

- **Navigation & fichiers** : `ls`, `cd`, `pwd`, `cat`, `less`, `head`, `tail`, `grep`, `find`.
- **Gestion des processus** : `ps`, `top`, `kill`, `jobs`.
- **Gestion des permissions** : `chmod`, `chown`.
- **Réseau** : `ping`, `netstat`, `ss`, `curl`.
- **Recherche** : `locate`, `which`, `whereis`.

### Exercice pratique

La room inclut des exercices pratiques pour manipuler des fichiers, filtrer des logs avec `grep`, et utiliser les pipes pour enchaîner des commandes.

---

## 📌 Ce que je retiens pour un poste d'analyste SOC

- **Le terminal est roi** : la grande majorité des serveurs en entreprise (et dans le cloud) tournent sous Linux et n'ont pas d'interface graphique.
- **Analyse de logs** : les commandes `grep`, `head`, `tail` et `less` sont indispensables pour filtrer et parcourir les fichiers de logs volumineux (ex : `/var/log/auth.log`).
- **Automatisation** : savoir écrire un script Bash simple permet d'automatiser des tâches répétitives d'extraction ou de tri de données.
- **Détection** : repérer des commandes suspectes dans l'historique (`history`) ou des processus anormaux (`ps aux`) fait partie des réflexes de l'analyste SOC.

---

## ✅ Statut

- [x] Room terminée
- [x] Write-up publié

---

*Write-up rédigé dans le cadre de ma préparation au poste d'Analyste SOC junior.*