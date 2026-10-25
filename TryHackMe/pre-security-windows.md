# Pre-Security — Windows Fundamentals — TryHackMe

**Catégorie :** Windows  
**Date de sortie :** Juillet 2021  
**Date de complétion :** 24/10/2026  
**Lien :** https://tryhackme.com/path/outline/presecurity

---

## 🎯 Objectif du module

Acquérir les bases de Windows indispensables à un analyste SOC : système, utilisateurs, permissions, registre, logs et Active Directory.

---

## 🧠 Ce que j'ai appris

### Les modules couverts

- **Windows Fundamentals 1** — interface, système de fichiers, utilisateurs
- **Windows Fundamentals 2** — permissions, UAC, registre, services
- **Windows Fundamentals 3** — mises à jour, sécurité, logs
- **Active Directory Basics** — concepts AD, domaines, utilisateurs, groupes

### Les notions clés

- **Système de fichiers** : NTFS, permissions.
- **Utilisateurs et groupes** : gestion des droits, UAC.
- **Registre** : base de configuration (clé `Run` souvent abusée pour la persistance).
- **Services** : processus en arrière-plan.
- **Event Logs** : Security, System, Application.
- **Active Directory** : annuaire centralisé, domaines, GPO.

### Les EventID clés

| EventID | Signification |
|---|---|
| 4624 | Connexion réussie |
| 4625 | Échec de connexion |
| 4688 | Création de processus |
| 4720 | Création d'utilisateur |

> 💡 **Point clé retenu** : un analyste SOC doit savoir **lire les Event Logs Windows** et **comprendre le registre** pour investiguer un incident.

---

## 🛠️ Concepts manipulés

| Concept | Rôle |
|---|---|
| NTFS | Système de fichiers avec permissions |
| UAC | Contrôle des comptes utilisateurs |
| Registre | Base de configuration Windows |
| Event Logs | Journaux d'événements |
| Active Directory | Annuaire centralisé des utilisateurs |

---

## 🔍 Ce que je retiens pour la détection

- Une **clé `Run` modifiée** dans le registre peut être une persistance.
- Un **EventID 4625** répété indique un brute force.
- Un **EventID 4688** avec un processus suspect (powershell, cmd) est à investiguer.
- Un **compte créé récemment** (EventID 4720) peut être une backdoor.

---

## 📌 Ce que je retiens pour un poste d'analyste SOC

- Windows est **omniprésent** en entreprise.
- Savoir **lire les Event Logs** est indispensable pour investiguer un incident.
- Comprendre le **registre** et les **services** permet de repérer une persistance.
- L'**Active Directory** est une cible privilégiée des attaquants.

---

## ✅ Statut

- [x] Module terminé
- [x] Write-up publié


---

*Write-up rédigé dans le cadre de ma préparation au poste d'Analyste SOC junior.*