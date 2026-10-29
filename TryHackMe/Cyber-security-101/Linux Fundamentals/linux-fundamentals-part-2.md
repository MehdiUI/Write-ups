# Linux Fundamentals Part 2 — Cyber Security 101 (TryHackMe)

**Catégorie :** Linux  
**Date de sortie :** Juillet 2021  
**Date de complétion :** 25/10/2026  
**Lien :** https://tryhackme.com/room/linuxfundamentalspart2  
**Parcours :** [Cyber Security 101](https://tryhackme.com/path/outline/cybersecurity101)

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

## 📌 Ce que je retiens pour un poste d'analyste SOC

- SSH est le moyen standard d'accéder à un serveur Linux, ce qui est courant en SOC.
- Les opérateurs comme `|` et `>` sont essentiels pour filtrer et sauvegarder des résultats de commandes (ex : logs).
- Comprendre les permissions (`chmod`, `chown`) permet de repérer des fichiers mal configurés (ex : permissions 777).

---

## ✅ Statut

- [x] Room terminée
- [x] Write-up publié