# Windows Fundamentals Part 2 — Cyber Security 101 (TryHackMe)

**Catégorie :** Windows  
**Date de sortie :** Juillet 2021  
**Date de complétion :** 26/10/2026  
**Lien :** https://tryhackme.com/room/windowsfundamentals2  
**Parcours :** [Cyber Security 101](https://tryhackme.com/path/outline/cybersecurity101)

---

## 🎯 Objectif de la room

Découvrir les principaux outils d'administration système de Windows, comment les lancer (via MSConfig, le menu Démarrer ou des commandes) et à quoi ils servent.

---

## 🧠 Ce que j'ai appris

### System Configuration (MSConfig)

L'outil `msconfig` permet de gérer le démarrage de Windows, les services et de lancer d'autres outils système.

### Les outils accessibles depuis MSConfig et le menu Démarrer

La room explique que l'on n'est pas obligé de passer par MSConfig pour lancer ces outils : ils peuvent être exécutés directement via le menu Démarrer ou des commandes.

- **UAC Settings** (`UserAccountControlSettings.exe`) : gérer les niveaux de sécurité de l'UAC.
- **Resource Monitor** (`resmon`) : surveiller l'utilisation du CPU, de la RAM, du disque et du réseau.
- **Command Prompt** (`cmd`) : l'invite de commande Windows.
- **Registry Editor** (`regedit`) : l'éditeur de base de registre.
- **Task Manager** (`taskmgr`) : gérer les processus, les performances et les utilisateurs.
- **System Information** (`msinfo32`) : afficher les détails matériels et logiciels du système.
- **Local Users and Groups** (`lusrmgr.msc`) : gérer les comptes locaux et les groupes (non disponible sur les éditions Home).
- **Windows Defender Firewall with Advanced Security** (`wf.msc`) : gérer les règles de pare-feu.
- **Performance Monitor** (`perfmon`) : surveiller les performances système en détail.

---

## 📌 Ce que je retiens pour un poste d'analyste SOC

- Connaître ces outils est indispensable pour diagnostiquer et investiguer sur une machine Windows.
- Savoir lancer ces outils rapidement (via `cmd` ou `Win + R`) est un réflexe à acquérir.
- Le **Registre** et le **Gestionnaire des tâches** sont fréquemment utilisés pour vérifier une activité suspecte.

---

## ✅ Statut

- [x] Room terminée
- [x] Write-up publié