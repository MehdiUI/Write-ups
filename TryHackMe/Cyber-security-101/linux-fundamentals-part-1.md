# Linux Fundamentals Part 1 — Cyber Security 101 (TryHackMe)

**Catégorie :** Linux  
**Date de sortie :** Juillet 2021  
**Date de complétion :** 25/10/2026  
**Lien :** https://tryhackme.com/room/linuxfundamentalspart1  
**Parcours :** [Cyber Security 101](https://tryhackme.com/path/outline/cybersecurity101)

---

## 🎯 Objectif de la room

Découvrir l'histoire de Linux, apprendre à interagir avec un terminal et maîtriser les premières commandes essentielles pour naviguer dans le système de fichiers.

---

## 🧠 Ce que j'ai appris

### Un peu d'histoire

Linux est un système d'exploitation open-source dérivé d'UNIX. La première version a été publiée en 1991[reference:20]. Il existe de nombreuses distributions (Ubuntu, Debian, etc.) adaptées à différents usages (serveurs, desktop, etc.).

### Les premières commandes

- `echo` : afficher du texte dans le terminal.
- `whoami` : afficher le nom de l'utilisateur courant.

### Interagir avec le système de fichiers

- `ls` : lister le contenu d'un répertoire.
- `cd` : changer de répertoire.
- `cat` : afficher le contenu d'un fichier.
- `pwd` : afficher le chemin du répertoire courant.

### Rechercher des fichiers

- `find` : rechercher des fichiers par nom.
- `grep` : rechercher un motif à l'intérieur d'un fichier.

### Les opérateurs shell

- `>` : rediriger la sortie vers un fichier (écrase).
- `>>` : rediriger la sortie vers un fichier (ajoute).
- `&` : exécuter une commande en arrière-plan.
- `&&` : exécuter une commande seulement si la précédente a réussi.

---

## 📌 Ce que je retiens pour un poste d'analyste SOC

- Le terminal est l'outil principal pour interagir avec un serveur Linux.
- Savoir naviguer dans l'arborescence et lire des fichiers est indispensable pour consulter des logs ou des configurations.
- Les opérateurs shell permettent d'enchaîner des commandes et de filtrer des résultats, ce qui est très utile pour l'investigation.

---

## ✅ Statut

- [x] Room terminée
- [x] Write-up publié