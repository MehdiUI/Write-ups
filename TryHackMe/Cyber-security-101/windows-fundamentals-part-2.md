# Windows Fundamentals Part 2 — Cyber Security 101 (TryHackMe)

**Catégorie :** Windows  
**Date de sortie :** Juillet 2021  
**Date de complétion :** 26/10/2026  
**Lien :** https://tryhackme.com/room/windowsfundamentals2  
**Parcours :** [Cyber Security 101](https://tryhackme.com/path/outline/cybersecurity101)  
**Room précédente :** [Windows Fundamentals Part 1](./windows-fundamentals-part-1.md)  
**Room suivante :** Windows Fundamentals Part 3

---

## 🎯 Objectif de la room

Approfondir les outils d'administration Windows essentiels à un analyste SOC : gestion des systèmes, registre, journaux d'événements et partages réseau.

---

## 🧠 Ce que j'ai appris

### System Configuration (MSConfig)

- **Onglet Général** : options de démarrage (Normal, Diagnostic, Sélectif).
- **Onglet Démarrage** : gérer les programmes au démarrage.
- **Onglet Services** : voir et désactiver les services.

### Advanced System Settings

- **Performance** : options d'effets visuels, mémoire virtuelle.
- **Variables d'environnement** : chemins système.
- **Démarrage et récupération** : options de dépannage.

### Computer Management

- **Event Viewer** : consulter les journaux d'événements (Security, System, Application).
- **Shared Folders** : voir les dossiers partagés sur le réseau.
- **Local Users and Groups** : gérer les comptes locaux.
- **Performance** : surveiller les ressources.
- **Device Manager** : gérer le matériel.
- **Disk Management** : gérer les disques et partitions.
- **Services** : gérer les services Windows.

### Le Registre (Registry Editor)

- **Structure** : `HKEY_LOCAL_MACHINE`, `HKEY_CURRENT_USER`, `HKEY_CLASSES_ROOT`, `HKEY_USERS`, `HKEY_CURRENT_CONFIG`.
- **Clé `Run`** : `HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\Run` (persistance fréquente).
- **Clé `RunOnce`** : exécution unique au démarrage.

> 💡 **Point clé retenu** : l'**Event Viewer** et le **Registre** sont les deux sources d'information les plus importantes pour un analyste SOC sur Windows.

---

## 🛠️ Outils et concepts manipulés

| Outil / Concept | Rôle |
|---|---|
| MSConfig | Gérer le démarrage et les services |
| Event Viewer | Consulter les journaux d'événements |
| Local Users and Groups | Gérer les comptes locaux |
| Services | Gérer les services Windows |
| Registry Editor | Modifier la base de registre |
| Clé Run | Point de persistance fréquent |

---

## 🔍 Ce que je retiens pour la détection

- Une **clé `Run` modifiée** dans le registre est une technique de persistance classique.
- Un **EventID 4625** (échec de connexion) répété dans l'Event Viewer indique un brute force.
- Un **EventID 4688** (création de processus) avec un processus suspect (ex : `powershell.exe` lancé par un utilisateur non admin) est à investiguer.
- Un **dossier partagé (Shared Folder)** non justifié peut être une fuite de données.
- Un **service activé récemment** peut être une persistance.

---

## 📌 Ce que je retiens pour un poste d'analyste SOC

- L'**Event Viewer** est la première chose à consulter en cas d'incident sur Windows.
- Le **Registre** est une cible privilégiée des attaquants pour la persistance.
- Les **comptes locaux et les services** doivent être surveillés.
- Cette room prépare la **Part 3** (mises à jour, sécurité, Active Directory).

---

## ✅ Statut

- [x] Room terminée
- [x] Write-up publié


---

*Write-up rédigé dans le cadre de ma préparation au poste d'Analyste SOC junior.*