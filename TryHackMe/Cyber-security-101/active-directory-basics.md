# Active Directory Basics — Cyber Security 101 (TryHackMe)

**Catégorie :** Windows & AD  
**Date de sortie :** Juillet 2021  
**Date de complétion :** 27/10/2026  
**Lien :** https://tryhackme.com/room/winadbasics  
**Parcours :** [Cyber Security 101](https://tryhackme.com/path/outline/cybersecurity101)  
**Room précédente :** [Windows Fundamentals Part 3](./windows-fundamentals-part-3.md)

---

## 🎯 Objectif de la room

Comprendre le fonctionnement d'Active Directory (AD) : la gestion centralisée des utilisateurs, des ordinateurs, des politiques de groupe (GPO) et des forêts.

---

## 🧠 Ce que j'ai appris

### Qu'est-ce qu'un Windows Domain ?

Un **Domaine Windows** est un groupe d'utilisateurs et d'ordinateurs gérés par une entreprise. L'idée centrale est de **centraliser l'administration**. Au lieu de configurer chaque ordinateur individuellement, on gère tout depuis un point central : le **Contrôleur de Domaine (Domain Controller - DC)**.

### La structure d'Active Directory

Active Directory est un annuaire qui stocke les objets du réseau. On y trouve :
- **Users (Utilisateurs)** : les comptes (ex : *Mark, Sophie, Administrateur*).
- **Machines (Ordinateurs)** : les postes de travail et serveurs joints au domaine.
- **Security Groups (Groupes de sécurité)** : pour attribuer des droits de manière groupée (ex : *Domain Admins*, *Domain Users*).
- **OU (Organizational Units)** : des "dossiers" pour organiser les utilisateurs et les machines par département (ex : *Marketing*, *IT*, *Comptabilité*).

### La gestion des utilisateurs et ordinateurs

- On peut déléguer l'administration d'une OU à un utilisateur spécifique (ex : donner le droit à un responsable RH de réinitialiser les mots de passe de son département).
- Les ordinateurs sont généralement organisés dans des OU distinctes (ex : *Workstations* vs *Servers*).

### Les Politiques de Groupe (GPO)

Les GPO (Group Policy Objects) permettent à l'administrateur d'imposer des règles à tous les utilisateurs ou ordinateurs d'une OU. Exemples :
- Imposer une longueur minimale pour les mots de passe.
- Interdire l'accès au Panneau de configuration.
- Déployer un logiciel sur tous les postes.

### Les méthodes d'authentification

- **Kerberos** : le protocole d'authentification par défaut d'Active Directory (basé sur des tickets).
- **NetNTLM** : ancien protocole d'authentification, encore utilisé pour la compatibilité (souvent ciblé par les attaques de type *Pass-the-Hash* ou *Brute Force*).

### Arbres, Forêts et Approbations (Trees, Forests & Trusts)

- **Domain Tree (Arbre de domaines)** : plusieurs domaines liés par une relation de confiance et partageant le même espace de noms (ex : `company.local`, `emea.company.local`).
- **Forest (Forêt)** : un ensemble d'arbres de domaines qui partagent le même schéma AD (la limite de sécurité ultime).
- **Trusts (Approbations)** : permettent à un utilisateur d'un domaine d'accéder aux ressources d'un autre domaine.

---

## 📌 Ce que je retiens pour un poste d'analyste SOC

- L'Active Directory est le **cœur névralgique** d'une entreprise. Si un attaquant le compromet, il contrôle tout le réseau.
- En SOC, on surveille particulièrement les **comptes à hauts privilèges** (Domain Admins, Enterprise Admins) et les modifications de GPO.
- La création d'un nouvel utilisateur dans une OU critique, ou son ajout soudain à un groupe d'administrateurs, est une alerte grave.
- Une attaque par **Kerberoasting** ou **Pass-the-Hash** (via NetNTLM) laisse des traces spécifiques dans les logs d'authentification Windows (EventID 4768, 4769, 4624, etc.).

---

## ✅ Statut

- [x] Room terminée
- [x] Write-up publié

---

*Write-up rédigé dans le cadre de ma préparation au poste d'Analyste SOC junior.*