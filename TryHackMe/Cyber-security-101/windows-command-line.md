# Windows Command Line — Cyber Security 101 (TryHackMe)

**Catégorie :** Windows & Command Line  
**Date de sortie :** Juillet 2021  
**Date de complétion :** 27/10/2026  
**Lien :** https://tryhackme.com/room/windowscommandline  
**Parcours :** [Cyber Security 101](https://tryhackme.com/path/outline/cybersecurity101)  
**Room suivante :** Windows PowerShell

---

## 🎯 Objectif de la room

Apprendre à utiliser l'invite de commande Windows (Command Prompt / CMD) pour naviguer dans le système, manipuler des fichiers et effectuer des diagnostics réseau.

---

## 🧠 Ce que j'ai appris

### Le Command Prompt (CMD)

L'invite de commande Windows est l'outil en ligne de commande historique. La room couvre les commandes essentielles :

- **Navigation & Fichiers** : `dir` (lister), `cd` (changer de dossier), `type` (lire un fichier), `cls` (effacer l'écran).
- **Aide** : `help` ou `[commande] /?` pour afficher le manuel d'une commande.
- **Manipulation** : `copy`, `move`, `del`, `mkdir` (créer un dossier), `rmdir` (supprimer un dossier).
- **Recherche de texte** : `find` et `findstr` pour chercher des motifs dans des fichiers.
- **Localisation** : `where` pour trouver l'emplacement d'un exécutable.

### Le diagnostic réseau

- **`ipconfig`** : Afficher la configuration IP (adresse, passerelle, DNS).
- **`ping`** : Tester la connectivité avec une autre machine.
- **`tracert`** : Tracer la route vers une destination.
- **`nslookup`** : Interroger les serveurs DNS pour résoudre un nom de domaine.
- **`netstat`** : Afficher les connexions réseau actives et les ports en écoute.

---

## 📌 Ce que je retiens pour un poste d'analyste SOC

- **Analyse de logs** : Savoir utiliser `findstr` permet de filtrer rapidement de gros fichiers de logs pour trouver une anomalie.
- **Diagnostic** : `netstat` est l'une des premières commandes à lancer pour voir si une machine communique avec une adresse IP malveillante (C2).
- **Réflexe d'investigation** : Comprendre les commandes CMD est indispensable, car les attaquants les utilisent souvent dans leurs scripts (ex : `net user` pour créer un compte).

---

## ✅ Statut

- [x] Room terminée
- [x] Write-up publié

---

*Write-up rédigé dans le cadre de ma préparation au poste d'Analyste SOC junior.*