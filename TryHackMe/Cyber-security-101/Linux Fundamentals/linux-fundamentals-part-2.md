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

Approfondir les compétences Linux : se connecter à distance via SSH, maîtriser les opérateurs de shell et gérer les permissions et les fichiers.

---

## 🧠 Ce que j'ai appris

### Se connecter à distance (SSH)

SSH (Secure Shell) permet de se connecter de manière sécurisée à une machine distante. On utilise la commande `ssh user@ip` (ou via Putty sur Windows).

### Les opérateurs Linux

- `&&` : n'exécute la commande suivante que si la précédente a réussi.
- `&` : exécute la commande en arrière-plan.
- `$` : accède à la valeur d'une variable d'environnement (ex : `$HOME`).
- `|` : pipe, envoie la sortie d'une commande vers une autre.
- `;` : exécute plusieurs commandes à la suite, indépendamment du succès.
- `>` : redirige la sortie vers un fichier (écrase).
- `>>` : redirige la sortie vers un fichier (ajoute).

### Gestion avancée des fichiers

- `chown` : changer le propriétaire d'un fichier.
- `chmod` : modifier les permissions d'un fichier (lecture, écriture, exécution).
- `rm` : supprimer un fichier.
- `mv` : déplacer ou renommer un fichier.

### Exercice pratique (shiba2)

La room inclut un exercice où l'on doit utiliser ces commandes pour interagir avec un utilisateur spécifique (`shiba2`) et manipuler des fichiers.

---

## 🖥️ Lignes de commande utilisées

Toutes les commandes ont été exécutées dans le terminal de la machine cible (via SSH ou directement).

| Commande | Description |
|---|---|
| `ssh user@ip` | Se connecter à une machine distante via SSH. |
| `ssh user@ip -p 2222` | Se connecter à une machine distante sur un port personnalisé. |
| `scp fichier.txt user@ip:/chemin/` | Copier un fichier vers une machine distante via SSH. |
| `command1 && command2` | Exécuter `command2` seulement si `command1` a réussi. |
| `command1 &` | Exécuter `command1` en arrière-plan. |
| `command1 \| grep "motif"` | Envoyer la sortie de `command1` vers `grep`. |
| `echo $HOME` | Afficher la valeur de la variable d'environnement `HOME`. |
| `command1 > fichier.txt` | Rediriger la sortie vers un fichier (écrase). |
| `command1 >> fichier.txt` | Rediriger la sortie vers un fichier (ajoute). |
| `chmod 755 fichier.sh` | Donner les permissions lecture/écriture/exécution au propriétaire, et lecture/exécution aux autres. |
| `chmod +x fichier.sh` | Rendre un fichier exécutable. |
| `chown user:group fichier.txt` | Changer le propriétaire et le groupe d'un fichier. |
| `rm fichier.txt` | Supprimer un fichier. |
| `mv fichier.txt /autre/dossier/` | Déplacer un fichier. |

---

## 📌 Ce que je retiens pour un poste d'analyste SOC

- **SSH** est le moyen standard d'accéder à un serveur Linux, ce qui est courant en SOC.
- **Les opérateurs comme `|` et `>`** sont essentiels pour filtrer et sauvegarder des résultats de commandes (ex : logs).
- **Comprendre les permissions** (`chmod`, `chown`) permet de repérer des fichiers mal configurés (ex : permissions 777).

---

## ✅ Statut

- [x] Room terminée
- [x] Write-up publié

---

*Write-up rédigé dans le cadre de ma préparation au poste d'Analyste SOC junior.*