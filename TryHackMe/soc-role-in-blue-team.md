# SOC Role in Blue Team — TryHackMe

**Catégorie :** Blue Team  
**Niveau :** Facile  
**Date :** 25/10/2026  
**Lien :** https://tryhackme.com/room/socroleinblueteam

---

## 🎯 Objectif de la room

Comprendre le rôle et les responsabilités d'un analyste SOC au sein d'une équipe Blue Team, ainsi que son positionnement dans la chaîne de défense d'une organisation.

---

## 🧠 Ce que j'ai appris

- **Le rôle du SOC** : le Security Operations Center est le centre de supervision qui détecte, analyse et répond aux incidents de sécurité en temps réel.
- **Les niveaux d'analystes** :
  - **L1** : triage et qualification des alertes
  - **L2** : investigation approfondie
  - **L3** : expertise, threat hunting, réponse avancée
- **Les responsabilités clés** : surveiller les alertes, qualifier les incidents, escalader si nécessaire, documenter chaque action.
- **Le lien avec la Blue Team** : le SOC collabore avec le DFIR, la Threat Intelligence et l'équipe Malware Analysis.

> 💡 **Point clé retenu** : un analyste SOC L1 est un **trieur d'alertes**. Il ne résout pas tout : il qualifie et oriente. C'est le premier maillon de la défense.

---

## 🛠️ Outils / concepts manipulés

| Outil / Concept | Rôle |
|---|---|
| SIEM | Centralise et corrèle les logs pour générer des alertes |
| Alertes | Événements suspects à qualifier |
| Triage | Priorisation et qualification des alertes |
| Escalade | Transmission au niveau supérieur si nécessaire |

---

## 🔍 Démarche / workflow retenu

Bien que la room soit théorique, j'ai retenu le **workflow de traitement d'une alerte** :

1. **Détection** : le SIEM génère une alerte à partir des logs.
2. **Triage (L1)** : l'analyste vérifie si l'alerte est légitime.
3. **Qualification** : vrai positif / faux positif, niveau de sévérité.
4. **Escalade** : transmission au L2 si nécessaire.
5. **Documentation** : rapport d'alerte avec décision et actions.

---

## 📌 Ce que je retiens pour un poste d'analyste SOC

- Un analyste L1 doit savoir **qualifier une alerte rapidement** et **documenter sa décision**.
- La rigueur du rapport d'alerte est aussi importante que la détection elle-même.
- Le SOC est un travail d'équipe : **communication et escalade** sont des compétences clés.

---

## ✅ Statut

- [x] Room terminée
- [x] Write-up publié
- [ ] Notions revues

---

*Write-up rédigé dans le cadre de ma préparation au poste d'Analyste SOC junior.*