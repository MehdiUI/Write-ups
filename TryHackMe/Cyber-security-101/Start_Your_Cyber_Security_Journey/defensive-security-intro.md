# Defensive Security Intro — Cyber Security 101 (TryHackMe)

**Catégorie :** Defensive Security  
**Date de sortie :** 2024  
**Date de complétion :** 20/10/2026  
**Lien :** https://tryhackme.com/room/defensivesecurityintro  
**Parcours :** [Cyber Security 101](https://tryhackme.com/path/outline/cybersecurity101)  
**Room précédente :** [Offensive Security Intro](./offensive-security-intro.md)  
**Room suivante :** [Search Skills](./search-skills.md)

---

## 🎯 Objectif de la room

Appliquer les bases du SOC dans un scénario concret (FakeBank) face à une attaque en cours.

---

## 🧠 Ce que j'ai appris

### La réponse à incident en pratique
La réponse à incident ne se fait pas au hasard. Le scénario m'a montré qu'il faut d'abord détecter l'alerte (connexions suspectes), puis contenir la menace (verrouiller le compte), ensuite investiguer (mettre à jour le renseignement sur le groupe attaquant) et enfin rédiger un rapport d'incident.

### Le tableau de bord SIEM
J'ai interagi avec un faux tableau de bord SIEM (dashboard de FakeBank). J'ai dû identifier l'utilisateur ciblé (`dave.saunders`), désactiver son compte via la console d'administration, et remplir un rapport d'incident (Incident Report) avec les bonnes informations.

---

## 🖥️ Lignes de commande utilisées

Cette room est un scénario interactif dans un navigateur. Aucune ligne de commande n'a été exécutée. Les actions ont été réalisées via l'interface graphique (dashboard, formulaire, boutons).

---

## 📌 Ce que je retiens pour un poste d'analyste SOC

- **Le containment en pratique** : Désactiver un compte est l'une des premières actions défensives. J'ai vu exactement où cliquer et comment cela s'intègre dans le processus global.
- **L'importance du rapport** : J'ai compris que le rapport d'incident (avec son ID unique) est la preuve de mon travail et sert aux équipes de niveau supérieur.
- **Ne jamais bloquer sans être sûr** : Ne jamais bloquer un compte sans être sûr de soi. Une erreur peut bloquer un employé légitime.

---

## ✅ Statut

- [x] Room terminée
- [x] Write-up publié

---

*Write-up rédigé dans le cadre de ma préparation au poste d'Analyste SOC junior.*