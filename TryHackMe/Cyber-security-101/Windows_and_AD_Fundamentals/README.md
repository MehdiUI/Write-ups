# 🪟 Module 3 : Windows and AD Fundamentals

Ce module explore l'environnement Windows sous un angle défensif et administratif. La maîtrise d'Active Directory (AD) est absolument cruciale, car c'est la cible principale des attaques en entreprise.

## 📝 Rooms du module

| Room | Description | Statut | Write-up |
|---|---|---|---|
| **Windows Fundamentals Part 1** | Interface Windows, gestion des utilisateurs, UAC (Contrôle des comptes), NTFS. | ✅ Terminé | [Lire](./windows-fundamentals-part-1.md) |
| **Windows Fundamentals Part 2** | Outils système avancés : `msconfig`, Registre (`regedit`), Gestion de l'ordinateur, Pare-feu. | ✅ Terminé | [Lire](./windows-fundamentals-part-2.md) |
| **Windows Fundamentals Part 3** | Windows Security, BitLocker, Volume Shadow Copy (VSS) et Windows Update. | ✅ Terminé | [Lire](./windows-fundamentals-part-3.md) |
| **Active Directory Basics** | Concepts fondamentaux de l'AD : Domaines, Unités d'Organisation (OU), Groupes, GPO et Délégation. | ✅ Terminé | [Lire](./active-directory-basics.md) |

## 🧠 Ce que je retiens pour un poste d'Analyste SOC
- **L'UAC et les privilèges** : Comprendre comment les utilisateurs obtiennent des droits d'administrateur est clé pour détecter les élévations de privilèges.
- **Les outils intégrés** : Le pare-feu Windows Defender et l'Observateur d'événements (Event Viewer) sont mes premières sources d'alerte lors d'un incident.
- **Active Directory** : C'est le cœur du réseau d'entreprise. Savoir ce qu'est une GPO et comment elle s'applique permet de comprendre comment un attaquant pourrait persister ou se propager (ex: Kerberoasting).