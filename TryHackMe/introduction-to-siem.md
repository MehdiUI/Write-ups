# Introduction to SIEM — TryHackMe

**Catégorie :** SIEM  
**Date de sortie :** 2023  
**Date de complétion :** 21/10/2026  
**Lien :** https://tryhackme.com/room/introtosiem  
**Room précédente :** [Defensive Security Intro](./defensive-security-intro.md)  
**Room suivante :** [Introduction to EDR](./introduction-to-edr.md)

---

## 🎯 Objectif de la room

Comprendre ce qu'est un SIEM, comment il collecte et corrèle les logs, et pourquoi il est indispensable à un SOC.

---

## 🧠 Ce que j'ai appris

### Définition

**SIEM** = Security Information and Event Management. C'est une plateforme qui **centralise les logs** de plusieurs sources (serveurs, endpoints, firewall, applications) et **corrèle les événements** pour détecter des anomalies.

### Le pipeline SIEM

1. **Collecte** — les logs arrivent de sources multiples (Windows Event Logs, syslog Linux, firewall, proxy, EDR, applications).
2. **Normalisation** — les logs sont convertis dans un format commun.
3. **Corrélation** — le SIEM applique des règles qui déclenchent des alertes sur des patterns suspects.
4. **Alerte** — une alerte est générée quand une règle est déclenchée.
5. **Dashboard** — l'analyste visualise les alertes et les tendances.

### Les sources de logs principales

- **Windows** : Security, System, Application, Sysmon, PowerShell
- **Linux** : auth.log, syslog, kern.log, apache2/access.log
- **Réseau** : firewall, proxy, IDS/IPS, DNS
- **Applications** : logs applicatifs, API, bases de données

> 💡 **Point clé retenu** : sans SIEM, un analyste ne verrait que des logs isolés. Le SIEM transforme ces logs en **alertes exploitables**.

---

## 🛠️ Outils / concepts manipulés

| Outil / Concept | Rôle |
|---|---|
| SIEM | Centralisation et corrélation des logs |
| Logs | Données brutes d'événements |
| Règles de détection | Déclenchent des alertes sur patterns |
| Dashboard | Visualisation des alertes et tendances |
| Normalisation | Uniformisation du format des logs |

---

## 🔍 Workflow d'un événement dans un SIEM

J'ai retenu le **workflow complet** d'un événement dans un SIEM :

1. Un événement se produit sur un serveur (ex : échec de connexion SSH).
2. Le log est envoyé au SIEM.
3. Le SIEM applique ses règles de corrélation.
4. Si la règle est déclenchée → alerte.
5. L'analyste SOC reçoit l'alerte et la qualifie.

**Exemple concret** : 10 échecs de connexion SSH en 30 secondes depuis la même IP → la règle « brute force SSH » se déclenche → alerte générée → l'analyste vérifie si c'est un utilisateur légitime qui a oublié son mot de passe ou une attaque.

---

## 📌 Ce que je retiens pour un poste d'analyste SOC

- Un analyste SOC travaille **quotidiennement avec un SIEM** (Splunk, Wazuh, ELK, Microsoft Sentinel…).
- Comprendre la **corrélation** et les **règles de détection** est indispensable pour qualifier une alerte.
- La **qualité des logs** conditionne la qualité de la détection : sans logs, pas d'alerte.
- Savoir **écrire une requête** dans un SIEM est une compétence clé (Splunk SPL, KQL, Lucene…).

---

## ✅ Statut

- [x] Room terminée
- [x] Write-up publié

---

*Write-up rédigé dans le cadre de ma préparation au poste d'Analyste SOC junior.*