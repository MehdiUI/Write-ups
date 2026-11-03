# SOC Fundamentals — Cyber Security 101 (TryHackMe)

**Catégorie :** Defensive Security  
**Date de sortie :** 2024  
**Date de complétion :** 01/11/2026  
**Lien :** https://tryhackme.com/room/socfundamentals  
**Parcours :** [Cyber Security 101](https://tryhackme.com/path/outline/cybersecurity101)  
**Room suivante :** [Digital Forensics Fundamentals](./digital-forensics-fundamentals.md)

---

## 🎯 Objectif de la room

Comprendre comment fonctionne un Security Operations Center, les rôles de l'équipe et les méthodes de triage des alertes.

---

## 🧠 Ce que j'ai appris

### Les 3 piliers du SOC
Un SOC mature repose sur l'équilibre entre les **Personnes** (analystes), les **Processus** (triage, escalade) et la **Technologie** (SIEM, EDR).

### La hiérarchie des rôles
- **SOC Analyst (L1)** : Premier rempart, fait le triage (triage) et le signalement (reporting) de base.
- **SOC Analyst (L2/L3)** : Enquêtes approfondies, chasse aux menaces proactives.
- **Security Engineer** : Déploie et configure les solutions.
- **Detection Engineer** : Crée les règles de détection (le "cerveau" des outils).
- **SOC Manager** : Gère l'équipe et fait le lien avec le CISO.

### Le processus de triage (5W)
Le triage d'alerte repose sur les **5 W** :
- **What?** (Quoi ?) : Que s'est-il passé (ex: exfiltration de données) ?
- **When?** (Quand ?) : L'heure de l'événement.
- **Where?** (Où ?) : La machine ou le dossier concerné.
- **Who?** (Qui ?) : L'utilisateur impliqué (ex: John).
- **Why?** (Pourquoi ?) : La cause (ex: téléchargement d'un logiciel piraté).

Une fois l'analyse terminée, un rapport (Reporting) est escaladé.

---

## 📌 Ce que je retiens pour un poste d'analyste SOC

- **La méthodologie des 5W** : C'est un réflexe à avoir. Quand une alerte tombe, je dois immédiatement me poser ces 5 questions pour structurer mon analyse, plutôt que de cliquer partout.
- **L'escalade** : Savoir que je serai L1 (le premier rempart) m'aide à comprendre mes limites. Mon rôle est de trier (vrai positif ou faux positif) et de rédiger un rapport clair pour les niveaux supérieurs.
- **Les outils font du bruit** : Les outils (SIEM, EDR) génèrent beaucoup de faux positifs. L'humain est indispensable pour donner du contexte et éviter l'épuisement.

---

## ✅ Statut

- [x] Room terminée
- [x] Write-up publié

---

*Write-up rédigé dans le cadre de ma préparation au poste d'Analyste SOC junior.*