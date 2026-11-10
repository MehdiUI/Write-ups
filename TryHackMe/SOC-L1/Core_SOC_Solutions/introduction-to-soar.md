# Introduction to SOAR — SOC Level 1 (TryHackMe)

**Catégorie :** Blue Team / SOC  
**Date de complétion :** 10/11/2026  
**Lien :** https://tryhackme.com/room/introductiontosoar  
**Parcours :** [SOC Level 1](https://tryhackme.com/path/outline/soclevel1)

---

## 🎯 Objectif de la room

Comprendre les concepts de Security Orchestration, Automation, and Response (SOAR), comment il résout les défis des SOC traditionnels et comment les analystes construisent des playbooks pour automatiser les enquêtes.

---

## 🧠 Ce que dit le cours

### 1. Fonctionnement et défis des SOC traditionnels
Un SOC est un centre centralisé de surveillance et de protection. Ses capacités incluent la surveillance (SIEM), la remédiation (EDR, pare-feu, IAM), la Threat Intelligence et la communication (ticketing).

Cependant, les SOC font face à des défis majeurs :
- **Alert Fatigue** : Trop d'alertes (souvent des faux positifs) submergent les analystes.
- **Too many Disconnected Tools** : Les outils ne sont pas intégrés, obligeant les analystes à jongler entre plusieurs interfaces.
- **Manual Processes** : Les procédures ne sont pas documentées et reposent sur l'expérience des seniors.
- **Talent Shortage** : Difficulté à recruter face à la croissance des menaces.

### 2. Qu'est-ce que le SOAR ?
Le SOAR unifie tous les outils de sécurité d'un SOC au sein d'une seule interface. Il propose également des fonctionnalités de ticketing et de gestion des cas. Ses trois capacités principales sont :
- **Orchestration** : Coordonner différents outils via des workflows prédéfinis appelés **Playbooks**.
- **Automation** : Exécuter automatiquement les étapes des playbooks sans intervention manuelle.
- **Response** : Permettre à l'analyste de prendre des mesures (bloquer une IP, désactiver un utilisateur) depuis l'interface unique.

*Note du cours : Le SOAR ne remplace pas les analystes. Les enquêtes complexes et la création des playbooks nécessitent un jugement humain.*

### 3. Construction des Playbooks
Le cours présente deux exemples de playbooks :
- **Phishing** : Le SOAR automatise la vérification des URL/pièces jointes (VirusTotal, calcul de hash) et la création de tickets. L'analyste conserve les étapes manuelles critiques (analyse dans une sandbox, mise à jour du ticket avec les IOC).
- **CVE Patching** : Le SOAR surveille les listes d'avis de sécurité, extrait les nouvelles CVE et vérifie leur applicabilité. L'analyste valide le ticket, identifie les actifs concernés, déploie les correctifs et vérifie leur bon fonctionnement. Si l'actif reste vulnérable, le SOC développe un plan de mitigation.

*(Le cours souligne que si la majorité des étapes sont automatisées, l'analyste reste indispensable pour les décisions et vérifications).*

---

## ✅ Statut

- [x] Room terminée
- [x] Write-up publié