# Linux Fundamentals Part 3 — Cyber Security 101 (TryHackMe)

**Catégorie :** Linux  
**Date de sortie :** Juillet 2021  
**Date de complétion :** 25/10/2026  
**Lien :** https://tryhackme.com/room/linuxfundamentalspart3  
**Parcours :** [Cyber Security 101](https://tryhackme.com/path/outline/cybersecurity101)

---

## 🎯 Objectif de la room

Maîtriser les utilitaires Linux du quotidien : éditeurs de texte, transfert de fichiers, gestion des processus, automatisation avec cron, gestion des paquets et lecture des logs.

---

## 🧠 Ce que j'ai appris

### Les éditeurs de texte

- **Nano** : éditeur simple en ligne de commande.
- **Vim** : éditeur plus puissant avec différents modes (insertion, commande).

### Les utilitaires généraux

- `wget` : télécharger un fichier depuis une URL.
- `scp` : copier un fichier via SSH.
- `python3 -m http.server` : lancer un serveur web simple pour partager des fichiers.

### La gestion des processus

- `ps` : lister les processus en cours.
- `top` : surveiller les processus en temps réel.
- `kill` : terminer un processus (signal par défaut : SIGTERM).
- `systemctl` : gérer les services systemd (`start`, `stop`, `enable`).

### L'automatisation (cron)

`cron` permet de planifier des tâches à intervalles réguliers. On édite les tâches avec `crontab -e`.

### La gestion des paquets

`APT` (Advanced Package Tool) est utilisé sur Debian/Ubuntu pour installer, mettre à jour et supprimer des logiciels (`apt install`, `apt update`, etc.).

### Les logs

Les logs système se trouvent dans `/var/log`. On y trouve notamment les logs d'accès Apache (`/var/log/apache2/access.log`).

---

## 📌 Ce que je retiens pour un poste d'analyste SOC

- Les logs sont la matière première de l'analyse. Savoir où ils se trouvent et comment les lire est crucial.
- La gestion des processus permet de repérer une activité suspecte (processus inconnu, consommation anormale).
- `cron` peut être utilisé par les attaquants pour maintenir une persistance ; il faut donc savoir le vérifier.
- Les utilitaires comme `wget` et `scp` sont utiles pour récupérer des outils ou des preuves.

---

## ✅ Statut

- [x] Room terminée
- [x] Write-up publié