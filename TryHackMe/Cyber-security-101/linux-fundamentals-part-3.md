# Linux Fundamentals Part 3 — Cyber Security 101 (TryHackMe)

**Catégorie :** Linux  
**Date de sortie :** Juillet 2021  
**Date de complétion :** 25/10/2026  
**Lien :** https://tryhackme.com/room/linuxfundamentalspart3  
**Parcours :** [Cyber Security 101](https://tryhackme.com/path/outline/cybersecurity101)  
**Room précédente :** [Linux Fundamentals Part 2](./linux-fundamentals-part-2.md)  
**Room suivante :** Windows and AD Fundamentals

---

## 🎯 Objectif de la room

Maîtriser les aspects avancés de Linux utiles à un analyste SOC : processus, services, logs, tâches planifiées et édition de fichiers.

---

## 🧠 Ce que j'ai appris

### Les processus

- **`ps`** : lister les processus
- **`top`** / **`htop`** : surveiller les processus en temps réel
- **`kill`** : terminer un processus (par PID)
- **PID** : identifiant unique d'un processus
- **PPID** : identifiant du processus parent

### Les services et le démarrage

- **`systemctl`** : gérer les services systemd (`start`, `stop`, `status`, `enable`)
- **`service`** : alternative pour les anciens systèmes
- **Services courants** : `sshd`, `cron`, `nginx`, `apache2`

### Les logs

- **`/var/log/auth.log`** : authentifications (SSH, sudo)
- **`/var/log/syslog`** : logs système
- **`/var/log/kern.log`** : logs du noyau
- **`journalctl`** : logs systemd
- **`/var/log/apache2/access.log`** : requêtes web

### Les tâches planifiées

- **`cron`** : tâches planifiées à intervalles réguliers
- **`crontab -e`** : éditer les tâches de l'utilisateur courant
- **`crontab -l`** : lister les tâches
- **Format cron** : `* * * * * commande` (minute, heure, jour, mois, jour de semaine)

### L'édition de fichiers

- **`nano`** : éditeur simple
- **`vim`** : éditeur avancé (modes insertion, commande)
- **Redirections** : `>`, `>>`, `|` (pipe)

> 💡 **Point clé retenu** : les **logs** sont la source de preuve d'un analyste SOC. Sur Linux, `auth.log` et `syslog` sont les premiers fichiers à consulter en cas d'incident.

---

## 🛠️ Commandes et concepts manipulés

| Commande / Concept | Rôle |
|---|---|
| `ps` | Lister les processus |
| `top` / `htop` | Surveiller les processus |
| `kill` | Terminer un processus |
| `systemctl` | Gérer les services |
| `journalctl` | Consulter les logs systemd |
| `crontab` | Gérer les tâches planifiées |
| `nano` / `vim` | Éditer des fichiers |
| `>` / `>>` / `|` | Redirections et pipes |

---

## 🔍 Ce que je retiens pour la détection

- Un **processus inconnu qui tourne en root** est suspect (persistance, backdoor).
- Un **service activé récemment** (`systemctl enable`) peut être une persistance.
- Une **tâche cron ajoutée récemment** (surtout en root) est une technique classique de persistance.
- Des **connexions SSH échouées** répétées dans `auth.log` indiquent un brute force.
- Un **processus avec un nom imitant un processus légitime** (ex : `sshd` au lieu de `sshd`) est un signe de malware.

---

## 📌 Ce que je retiens pour un poste d'analyste SOC

- Les **logs Linux** sont la base de l'investigation sur serveur.
- Comprendre **processus, services et cron** permet de repérer une persistance.
- Savoir **lire `auth.log`** est indispensable pour détecter un brute force SSH.
- Cette room clôt le module Linux et prépare **Windows and AD Fundamentals**.

---

## ✅ Statut

- [x] Room terminée
- [x] Write-up publié

---

*Write-up rédigé dans le cadre de ma préparation au poste d'Analyste SOC junior.*