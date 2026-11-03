# Introduction to SIEM — Cyber Security 101 (TryHackMe)

**Catégorie :** Security Solutions  
**Date de sortie :** 2024  
**Date de complétion :** 02/11/2026  
**Lien :** https://tryhackme.com/room/introductiontosiem  
**Parcours :** [Cyber Security 101](https://tryhackme.com/path/outline/cybersecurity101)  
**Room précédente :** [Firewall Fundamentals](./firewall-fundamentals.md)  
**Room suivante :** [IDS Fundamentals](./ids-fundamentals.md)

---

## 🎯 Objectif de la room

Comprendre comment centraliser, normaliser et corréler les logs pour détecter des menaces.

---

## 🧠 Ce que j'ai appris

### Le rôle du SIEM
Le SIEM est le cerveau du SOC. Il collecte les logs de partout (Windows, Linux, routeurs). Mais il ne fait pas que stocker : il **normalise** (traduit tous les formats), **corrèle** (relie des événements isolés pour créer une alerte) et affiche des dashboards. C'est ce qui permet de repérer une attaque complexe.

### L'architecture
J'ai découvert l'architecture d'un SIEM (agents vs sans agent). J'ai aussi vu comment on utilise un outil comme Splunk pour faire des recherches dans les logs.

---

## 🖥️ Lignes de commande utilisées

L'interface principale est graphique (Splunk), mais les requêtes de recherche (SPL) sont essentielles. Voici les requêtes utilisées dans le lab :

| Requête Splunk | Description |
|---|---|
| `index=*` | Afficher tous les logs ingérés dans l'index. |
| `index=* | stats count by sourcetype` | Compter les événements par type de source. |
| `index=* | search "failed login"` | Rechercher les échecs de connexion. |
| `index=* | search "error"` | Rechercher les erreurs. |

*Note : les commandes sont saisies dans la barre de recherche de Splunk, pas dans un terminal.*

---

## 📌 Ce que je retiens pour un poste d'analyste SOC

- **La corrélation** : Un log de login échoué seul ne veut rien dire. Mais 100 logins échoués en 1 minute, c'est une attaque brute force. C'est le SIEM qui fait ce lien pour moi.
- **La centralisation** : Je n'aurai pas à me connecter sur 50 serveurs différents. Tout est dans le SIEM, je gagne un temps fou.
- **Garbage in, garbage out** : Si les logs envoyés au SIEM sont mauvais ou incomplets, les alertes seront mauvaises.

---

## ✅ Statut

- [x] Room terminée
- [x] Write-up publié

---

*Write-up rédigé dans le cadre de ma préparation au poste d'Analyste SOC junior.*