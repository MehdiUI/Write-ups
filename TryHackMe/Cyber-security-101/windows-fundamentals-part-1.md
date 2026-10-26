# Windows Fundamentals Part 1 — Cyber Security 101 (TryHackMe)

**Catégorie :** Windows  
**Date de sortie :** Juillet 2021  
**Date de complétion :** 26/10/2026  
**Lien :** https://tryhackme.com/room/windowsfundamentals1  
**Parcours :** [Cyber Security 101](https://tryhackme.com/path/outline/cybersecurity101)  
**Room suivante :** [Windows Fundamentals Part 2](./windows-fundamentals-part-2.md)

---

## 🎯 Objectif de la room

Acquérir les bases de Windows pour un analyste SOC : système de fichiers, permissions, gestion des utilisateurs et des processus.

---

## 🧠 Ce que j'ai appris

### Le système de fichiers

- **NTFS** (New Technology File System) : le système de fichiers standard de Windows, avec gestion des permissions avancée.
- **FAT** : ancien système de fichiers, moins sécurisé.
- **Dossiers clés** : `C:\Windows`, `C:\Program Files`, `C:\Users`.
- **Variables d'environnement** : `%USERPROFILE%`, `%WINDIR%`, `%TEMP%`.

### Les permissions NTFS

- **Contrôle d'accès** : basé sur les ACL (Access Control Lists).
- **Permissions de base** : Lecture, Écriture, Exécution, Modification, Contrôle total.
- **Héritage** : les permissions se transmettent des dossiers parents aux enfants.

### La gestion des utilisateurs

- **Comptes locaux** : créés sur la machine.
- **Groupes** : `Administrateurs`, `Utilisateurs`, `Invités`.
- **UAC** (User Account Control) : demande une élévation de privilèges pour les actions sensibles.

### Les processus et services

- **Task Manager** : surveiller les processus, l'utilisation CPU/RAM, les services.
- **Services** : processus en arrière-plan (ex : Windows Update, Spooler).
- **Processus** : programmes en cours d'exécution (ex : `explorer.exe`, `svchost.exe`).

> 💡 **Point clé retenu** : un analyste SOC doit savoir **lire les permissions**, **repérer un compte suspect** et **identifier un processus anormal** dans le Task Manager.

---

## 🛠️ Concepts manipulés

| Concept | Rôle |
|---|---|
| NTFS | Système de fichiers avec permissions |
| ACL | Contrôle d'accès aux fichiers et dossiers |
| UAC | Élévation de privilèges |
| Task Manager | Surveillance des processus et services |
| Variables d'environnement | Chemins système standard |

---

## 🔍 Ce que je retiens pour la détection

- Un **processus inconnu** qui consomme beaucoup de CPU/RAM est suspect.
- Un **compte utilisateur créé récemment** doit être vérifié.
- Un **service activé sans justification** peut être une persistance.
- Des **permissions excessives** (ex : `Everyone` en Contrôle total) sont une mauvaise pratique.

---

## 📌 Ce que je retiens pour un poste d'analyste SOC

- Windows est **omniprésent** en entreprise.
- Savoir **naviguer dans les dossiers système** et **lire les permissions** est indispensable.
- Comprendre les **comptes et les processus** permet de repérer une activité suspecte.

---

## ✅ Statut

- [x] Room terminée
- [x] Write-up publié

---

*Write-up rédigé dans le cadre de ma préparation au poste d'Analyste SOC junior.*