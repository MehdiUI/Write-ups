# Linux Fundamentals Part 3 — Cyber Security 101 (TryHackMe)

**Catégorie :** Linux  
**Date de sortie :** Juillet 2021  
**Date de complétion :** 25/10/2026  
**Lien :** https://tryhackme.com/room/linuxfundamentalspart3  
**Parcours :** [Cyber Security 101](https://tryhackme.com/path/outline/cybersecurity101)  
**Room précédente :** [Linux Fundamentals Part 2](./linux-fundamentals-part-2.md)

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

## 🖥️ Lignes de commande utilisées

Toutes les commandes ont été exécutées dans le terminal de la machine cible.

| Commande | Description |
|---|---|
| `wget https://example.com/fichier` | Télécharger un fichier depuis une URL. |
| `scp fichier.txt user@ip:/chemin/` | Copier un fichier vers une machine distante via SSH. |
| `python3 -m http.server 8000` | Lancer un serveur web simple sur le port 8000. |
| `ps aux` | Lister tous les processus en cours. |
| `top` | Surveiller les processus en temps réel. |
| `kill 1234` | Terminer le processus avec le PID 1234. |
| `kill -9 1234` | Terminer de force le processus (SIGKILL). |
| `systemctl start apache2` | Démarrer le service Apache. |
| `systemctl stop apache2` | Arrêter le service Apache. |
| `systemctl enable apache2` | Activer le démarrage automatique d'Apache au boot. |
| `crontab -e` | Éditer les tâches cron de l'utilisateur. |
| `crontab -l` | Lister les tâches cron de l'utilisateur. |
| `apt update` | Mettre à jour la liste des paquets disponibles. |
| `apt install nom_du_paquet` | Installer un paquet. |
| `apt remove nom_du_paquet` | Supprimer un paquet. |
| `tail -f /var/log/apache2/access.log` | Suivre les logs Apache en temps réel. |
| `grep "GET /contact" /var/log/apache2/access.log` | Filtrer les logs pour ne garder que les requêtes GET vers `/contact`. |

---

## 📌 Ce que je retiens pour un poste d'analyste SOC

- **Les logs** sont la matière première de l'analyse. Savoir où ils se trouvent et comment les lire est crucial.
- **La gestion des processus** permet de repérer une activité suspecte (processus inconnu, consommation anormale).
- **`cron`** peut être utilisé par les attaquants pour maintenir une persistance ; il faut donc savoir le vérifier.
- **Les utilitaires comme `wget` et `scp`** sont utiles pour récupérer des outils ou des preuves.

---

## ✅ Statut

- [x] Room terminée
- [x] Write-up publié

---

*Write-up rédigé dans le cadre de ma préparation au poste d'Analyste SOC junior.*