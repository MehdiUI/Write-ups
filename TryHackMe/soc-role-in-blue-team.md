# SOC Role in Blue Team — TryHackMe

**Catégorie :** Blue Team  
**Date de sortie :** 2025  
**Date de complétion :** 19/10/2026   
**Lien :** https://tryhackme.com/room/socroleinblueteam  
**Room suivante :** [Defensive Security Intro](./defensive-security-intro.md)

---

## 🎯 Objectif de la room

Comprendre le rôle et les responsabilités d'un analyste SOC au sein d'une équipe Blue Team, ainsi que son positionnement dans la chaîne de défense d'une organisation.

---

## 🧠 Ce que j'ai appris

### Le SOC, c'est quoi ?

Le **Security Operations Center** est le centre de supervision qui détecte, analyse et répond aux incidents de sécurité en temps réel. C'est le premier rempart d'une organisation face aux menaces.

### Les niveaux d'analystes

| Niveau | Rôle | Responsabilités |
|---|---|---|
| **L1** | Triage | Qualifier les alertes, vrai/faux positif, escalader si nécessaire |
| **L2** | Investigation | Approfondir l'analyse, corréler les événements, proposer une remédiation |
| **L3** | Expertise | Threat hunting, réponse avancée, amélioration des détections |

### Les responsabilités clés d'un L1

- **Surveiller** les alertes remontées par le SIEM
- **Qualifier** chaque alerte : vrai positif / faux positif
- **Documenter** la décision dans un rapport d'alerte
- **Escalader** au L2 si l'incident est confirmé
- **Communiquer** avec les autres équipes (DFIR, Threat Intel, Malware Analysis)

> 💡 **Point clé retenu** : un analyste SOC L1 est un **trieur d'alertes**. Il ne résout pas tout : il qualifie et oriente. C'est le premier maillon de la défense.

---

## 🛠️ Outils / concepts manipulés

| Outil / Concept | Rôle |
|---|---|
| SIEM | Centralise et corrèle les logs pour générer des alertes |
| Alertes | Événements suspects à qualifier |
| Triage | Priorisation et qualification des alertes |
| Escalade | Transmission au niveau supérieur si nécessaire |
| Rapport d'alerte | Documentation de la décision et des actions |

---

## 🔍 Workflow de traitement d'une alerte

Bien que la room soit théorique, j'ai retenu le **workflow complet** qu'un analyste L1 suit au quotidien :

1. **Détection** — le SIEM génère une alerte à partir des logs.
2. **Triage (L1)** — l'analyste vérifie si l'alerte est légitime.
3. **Qualification** — vrai positif / faux positif, niveau de sévérité.
4. **Escalade** — transmission au L2 si nécessaire.
5. **Documentation** — rapport d'alerte avec décision et actions.

---

## 📌 Ce que je retiens pour un poste d'analyste SOC

- Un analyste L1 doit savoir **qualifier une alerte rapidement** et **documenter sa décision**.
- La rigueur du rapport d'alerte est aussi importante que la détection elle-même.
- Le SOC est un travail d'équipe : **communication et escalade** sont des compétences clés.
- Comprendre la hiérarchie L1/L2/L3 permet de savoir **quand escalader** et **à qui**.

---

## ✅ Statut

- [x] Room terminée
- [x] Write-up publié
---

*Write-up rédigé dans le cadre de ma préparation au poste d'Analyste SOC junior.*