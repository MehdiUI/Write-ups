# Incident Response Fundamentals — Cyber Security 101 (TryHackMe)

**Catégorie :** Defensive Security  
**Date de sortie :** 2024  
**Date de complétion :** 02/11/2026  
**Lien :** https://tryhackme.com/room/incidentresponsefundamentals  
**Parcours :** [Cyber Security 101](https://tryhackme.com/path/outline/cybersecurity101)  
**Room précédente :** [Digital Forensics Fundamentals](./digital-forensics-fundamentals.md)  
**Room suivante :** [Logs Fundamentals](./logs-fundamentals.md)

---

## 🎯 Objectif de la room

Comprendre le cycle de vie de la réponse aux incidents (IR), apprendre à catégoriser les menaces et utiliser les méthodologies (SANS/NIST) pour contenir et éradiquer une attaque.

---

## 🧠 Ce que j'ai appris

### Triage des alertes
Tous les incidents ne sont pas égaux. Il faut d'abord trier les alertes (False Positive vs True Positive) pour ne pas paniquer.

### Framework SANS (PICERL)
Une fois qu'un incident est confirmé, on utilise une méthode, comme le framework SANS (PICERL) : 
- **Preparation**
- **Identification**
- **Containment**
- **Eradication**
- **Recovery**
- **Lessons Learned**

L'objectif est de limiter les dégâts (Containment) avant de nettoyer (Eradication).

### Playbooks
On utilise aussi des "Playbooks" pour savoir exactement quoi faire selon le type d'attaque (ex: phishing).

### Exercice pratique
J'ai fait un exercice pratique (Lab) où je devais analyser un email de phishing. J'ai identifié l'expéditeur, le vecteur (pièce jointe) et le nombre de machines infectées. J'ai vu comment les playbooks guident la réponse.

---

## 📌 Ce que je retiens pour un poste d'analyste SOC

- **Le framework PICERL** : C'est la feuille de route. Si je suis L1 et que je vois un ransomware, je sais que mon rôle immédiat est de contenir (isoler la machine) et de ne surtout pas passer à l'éradication avant l'ordre de l'équipe L3.
- **Les Playbooks** : Ils sont ma bible. En cas de stress, je n'invente rien, je suis les étapes prédéfinies.
- **Ne pas sauter d'étapes** : Passer directement à l'éradication sans contenir la menace peut permettre à l'attaquant de se propager.

---

## ✅ Statut

- [x] Room terminée
- [x] Write-up publié

---

*Write-up rédigé dans le cadre de ma préparation au poste d'Analyste SOC junior.*