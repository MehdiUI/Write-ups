# Windows Fundamentals Part 1 — Cyber Security 101 (TryHackMe)

**Catégorie :** Windows  
**Date de sortie :** Juillet 2021  
**Date de complétion :** 26/10/2026  
**Lien :** https://tryhackme.com/room/windowsfundamentals1  
**Parcours :** [Cyber Security 101](https://tryhackme.com/path/outline/cybersecurity101)

---

## 🎯 Objectif de la room

Acquérir les bases de Windows : système de fichiers, permissions, gestion des utilisateurs et des groupes.

---

## 🧠 Ce que j'ai appris

### Les versions de Windows

La room présente les différentes versions de Windows (client et serveur) et leurs usages.

### Le système de fichiers

- **NTFS** (New Technology File System) : le système de fichiers standard de Windows, avec gestion des permissions avancée.
- **FAT** : ancien système de fichiers, moins sécurisé.
- **ADS (Alternate Data Streams)** : fonctionnalité NTFS permettant de cacher des données dans un fichier, souvent utilisée par les malwares.

### Les permissions NTFS

- **Contrôle d'accès** : basé sur les ACL (Access Control Lists).
- **Permissions de base** : Lecture, Écriture, Exécution, Modification, Contrôle total.
- **Héritage** : les permissions se transmettent des dossiers parents aux enfants.

### La gestion des utilisateurs

- **Comptes locaux** : créés sur la machine (Administrateur, Utilisateur standard, Invité).
- **UAC** (User Account Control) : demande une élévation de privilèges pour les actions sensibles.

---

## 📌 Ce que je retiens pour un poste d'analyste SOC

- Windows est omniprésent en entreprise.
- Comprendre le système de fichiers et les permissions permet de repérer des configurations dangereuses ou des fichiers cachés (ADS).
- La gestion des utilisateurs et l'UAC sont des mécanismes de sécurité à surveiller.

---

## ✅ Statut

- [x] Room terminée
- [x] Write-up publié