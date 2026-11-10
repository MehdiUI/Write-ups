# Introduction to SIEM — SOC Level 1 (TryHackMe)

**Catégorie :** Blue Team / SOC  
**Date de complétion :** 10/11/2026  
**Lien :** https://tryhackme.com/room/introductiontosiem  
**Parcours :** [SOC Level 1](https://tryhackme.com/path/outline/soclevel1)

---

## 🎯 Objectif de la room

Comprendre le rôle d'un SIEM (Security Information and Event Management) dans un SOC : comment il collecte, normalise et corrèle les logs pour détecter des menaces.

---

## 🧠 Ce que j'ai appris (résumé du cours)

- **Le rôle du SIEM** : Le SIEM est une solution centralisée qui collecte les logs de toutes les machines (Windows, Linux, routeurs, serveurs web) pour les analyser. Il ne fait pas que stocker : il **normalise** (traduit tous les formats), **corrèle** (relie des événements isolés pour créer une alerte) et affiche des dashboards.
- **Les sources de logs** : Windows Event Logs, Linux Syslog, Web Access Logs, etc.
- **L'architecture** : 
  - **Agents / Forwarders** : Un petit logiciel installé sur la machine qui envoie les logs.
  - **Agentless** : La machine envoie elle-même ses logs via un protocole réseau (Syslog, SNMP).
- **Les fonctionnalités** : Dashboards, Alerting, Recherche (requêtes comme `index=*`).
- **Le principe "Garbage in, garbage out"** : Si les logs envoyés au SIEM sont mauvais ou incomplets, les alertes seront mauvaises.

---

## ✅ Statut

- [x] Room terminée
- [x] Write-up publié