# Blue Team Introduction — SOC Level 1 (TryHackMe)

**Catégorie :** Blue Team / SOC  
**Date de complétion :** 07/11/2026  
**Parcours :** [SOC Level 1](https://tryhackme.com/path/outline/soclevel1)  
**Lien du module :** https://tryhackme.com/module/blue-team-introduction

---

## 🎯 Objectif du module

Découvrir le rôle de la Blue Team et du Security Operations Center (SOC), comprendre les missions quotidiennes d’un analyste SOC junior, et identifier les principaux vecteurs d’attaque : humains et systèmes.

---

## 📝 Rooms du module

| Room | Description | Write-up |
|---|---|---|
| **Junior Security Analyst Intro** | Simulation d’une journée type d’un analyste L1 : triage, escalade, blocage d’IP. | [Lire](./junior-security-analyst-intro.md) |
| **SOC Role in Blue Team** | Organisation de la Blue Team, rôles L1/L2/L3 et évolution de carrière. | [Lire](./soc-role-in-blue-team.md) |
| **Humans as Attack Vectors** | Phishing, social engineering, insider threats et rôle du SOC dans la sensibilisation. | [Lire](./humans-as-attack-vectors.md) |
| **Systems as Attack Vectors** | Vulnérabilités systèmes, CVE, mauvaises configurations et réponse SOC. | [Lire](./systems-as-attack-vectors.md) |

---

## 🧠 Ce que j’ai appris

### 1. Le rôle du SOC
Le SOC est le centre de défense de l’entreprise. Il fonctionne 24/7 et repose sur trois piliers : **Personnes**, **Processus**, **Technologie**. L’analyste L1 est le premier rempart : il trie les alertes, qualifie les incidents et escalade les cas critiques.

### 2. Les rôles et l’évolution
La Blue Team s’organise souvent en niveaux :
- **L1** : triage initial et reporting.
- **L2** : investigation approfondie.
- **L3** : threat hunting, réponse avancée.
- **Ingénierie** : SIEM, EDR, automatisation.
- **Management** : coordination et lien avec le CISO.

### 3. Les humains comme vecteurs d’attaque
Les attaquants ciblent souvent les personnes via :
- **Phishing** : e-mails frauduleux.
- **Social engineering** : manipulation psychologique.
- **Insider threats** : employés malveillants ou négligents.

Le SOC doit détecter ces attaques et sensibiliser les utilisateurs. Un signalement rapide d’un employé est une source précieuse.

### 4. Les systèmes comme vecteurs d’attaque
Les attaquants exploitent :
- **Vulnérabilités logicielles** (CVE critiques, services non patchés).
- **Mauvaises configurations** (identifiants par défaut, ports ouverts, permissions excessives).
- **Exposition réseau** (RDP, SSH, bases de données accessibles).

La réponse SOC suit un processus structuré : **qualifier → évaluer le risque → contenir si nécessaire → remédier → vérifier → documenter**.

---

## 🖥️ Lignes de commande utilisées

Ce module est majoritairement théorique et interactif. Aucune ligne de commande système n’a été nécessaire.

Les actions ont été réalisées via :
- des tableaux de bord web (simulation SOC) ;
- des formulaires d’escalade et de blocage d’IP ;
- des quiz et des lectures.

---

## 📌 Ce que je retiens pour un poste d’analyste SOC

- **Le workflow L1** : détecter, analyser, escalader, remédier. C’est le cycle de base de toute alerte.
- **L’humain est une cible** : la sensibilisation et la détection des signalements utilisateurs sont essentielles.
- **Les systèmes sont des cibles** : le patch management, la réduction de surface d’attaque et la surveillance des mauvaises configurations sont prioritaires.
- **La communication** : un analyste SOC doit documenter ses actions et escalader au bon niveau, avec des preuves claires.

---

## ✅ Statut

- [x] Module terminé (4/4 rooms)
- [x] Write-ups publiés
- [x] README du module mis à jour

---

*Synthèse rédigée dans le cadre de ma préparation au poste d’Analyste SOC junior.*