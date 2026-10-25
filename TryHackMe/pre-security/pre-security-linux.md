# Pre-Security — Linux Fundamentals — TryHackMe

**Catégorie :** Linux  
**Date de sortie :** Juillet 2021  
**Date de complétion :** 23/10/2026  
**Lien :** https://tryhackme.com/path/outline/presecurity

---

## 🎯 Objectif du module

Acquérir les bases de Linux indispensables à un analyste SOC : navigation, gestion des fichiers, permissions, processus et logs.

---

## 🧠 Ce que j'ai appris

### Les modules couverts

- **Linux Fundamentals Part 1** — navigation, fichiers, commandes de base
- **Linux Fundamentals Part 2** — permissions, utilisateurs, groupes
- **Linux Fundamentals Part 3** — processus, services, logs, tâches planifiées

### Les commandes clés

| Commande | Rôle |
|---|---|
| `ls` | Lister les fichiers |
| `cd` | Changer de répertoire |
| `cat` | Afficher un fichier |
| `grep` | Rechercher un motif |
| `chmod` | Modifier les permissions |
| `chown` | Changer le propriétaire |
| `ps` | Lister les processus |
| `top` | Surveiller les processus |
| `journalctl` | Consulter les logs système |

### Les notions clés

- **Permissions** : lecture (r), écriture (w), exécution (x) pour propriétaire, groupe, autres.
- **Utilisateurs et groupes** : gestion des droits, sudo.
- **Processus** : PID, état, ressources.
- **Logs** : `/var/log/auth.log`, `/var/log/syslog`, `journalctl`.
- **Tâches planifiées** : cron, systemd timers.

> 💡 **Point clé retenu** : un analyste SOC doit savoir **naviguer dans un système Linux** et **lire les logs** pour investiguer un incident.

---

## 🛠️ Concepts manipulés

| Concept | Rôle |
|---|---|
| Permissions | Contrôler l'accès aux fichiers |
| Utilisateurs / groupes | Gestion des droits |
| Processus | Identifier une activité suspecte |
| Logs | Source de preuve pour l'investigation |
| Cron | Tâches planifiées (peut être abusé) |

---

## 🔍 Ce que je retiens pour la détection

- Un **processus inconnu** qui tourne en root est suspect.
- Un **fichier avec des permissions 777** est une mauvaise pratique de sécurité.
- Des **connexions SSH échouées** répétées dans `auth.log` indiquent un brute force.
- Une **tâche cron ajoutée récemment** peut être une persistance malveillante.

---

## 📌 Ce que je retiens pour un poste d'analyste SOC

- Linux est **omniprésent** dans les serveurs et les infrastructures cloud.
- Savoir **lire les logs Linux** est indispensable pour investiguer un incident.
- Comprendre les **permissions** et les **processus** permet de repérer une activité suspecte.

---

## ✅ Statut

- [x] Module terminé
- [x] Write-up publié
---

*Write-up rédigé dans le cadre de ma préparation au poste d'Analyste SOC junior.*