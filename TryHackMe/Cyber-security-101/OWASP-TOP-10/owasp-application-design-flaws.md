# OWASP Top 10 2025: Application Design Flaws — Cyber Security 101 (TryHackMe)

**Catégorie :** OWASP Top 10 (2025) / Sécurité Web  
**Date de sortie :** 2025  
**Date de complétion :** 06/11/2026  
**Lien :** https://tryhackme.com/room/owaspapplicationdesignflaws  
**Parcours :** [Cyber Security 101](https://tryhackme.com/path/outline/cybersecurity101)  
**Room précédente :** [IAAA Failures](./owasp-iaaa-failures.md)  
**Room suivante :** [Insecure Data Handling](./owasp-insecure-data-handling.md)

---

## 🎯 Objectif de la room

Comprendre les failles liées à la conception et à la configuration des applications web : AS02 (Security Misconfigurations), AS03 (Software Supply Chain Failures), AS04 (Cryptographic Failures) et AS06 (Insecure Design).

---

## 🧠 Ce que j'ai appris

### AS02 : Security Misconfigurations
Erreurs humaines lors du déploiement : mots de passe par défaut, ports de debug ouverts, messages d'erreur trop bavards (qui révèlent la stack technique), ou permissions trop larges sur le cloud (S3 buckets publics).

### AS03 : Software Supply Chain Failures
Attaques ciblant les dépendances (bibliothèques open-source, packages npm/PyPI) ou les outils de build. Si un attaquant compromet une librairie populaire, il infecte toutes les applications qui l'utilisent (ex: Log4Shell).

### AS04 : Cryptographic Failures
Mauvaise utilisation de la cryptographie : algorithmes obsolètes (MD5, SHA1), clés codées en dur dans le code, absence de chiffrement sur les données sensibles en transit (HTTP au lieu de HTTPS) ou au repos.

### AS06 : Insecure Design
Faille logique ou architecturale présente dès le départ. On ne peut pas la "patcher" facilement, il faut revoir la conception. 
- **Exemple (Clubhouse)** : L'API backend n'avait aucune authentification car les développeurs partaient du principe que seule l'application mobile y accéderait. 
- **Défi pratique** : Le site `SecureChat` bloquait l'accès aux ordinateurs (User-Agent PC) mais laissait passer les mobiles. En usurpant le User-Agent d'un iPhone avec `curl`, on a pu énumérer l'API (`/api/users`) et découvrir des données exposées.

---

## 🖥️ Lignes de commande utilisées

| Commande | Description |
|---|---|
| `gobuster dir -u http://10.129.138.112:5005/api -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -q` | Énumérer les répertoires cachés de l'API. |
| `curl -A "Mozilla/5.0 (iPhone; CPU iPhone OS 14_0 like Mac OS X)..." http://10.129.138.112:5005/api/users` | Contourner la restriction mobile en usurpant le User-Agent avec `curl -A`. |

---

## 📌 Ce que je retiens pour un poste d'analyste SOC

- **Détecter les mauvaises configurations** : En tant qu'analyste, je verrai passer des alertes de scanners (comme OpenVAS) signalant des services par défaut ou des ports de debug. C'est souvent la porte d'entrée la plus simple pour un attaquant.
- **Surveiller les User-Agents** : Une requête `curl` avec un User-Agent d'iPhone vers une API interne (qui ne devrait recevoir que du JSON depuis une app mobile) est un excellent indicateur de compromission (IOC) ou de scan. Les WAF et les logs web permettent de repérer ces anomalies.
- **L'énumération d'API** : Voir un utilisateur faire des requêtes massives sur `/api/users/1`, `/api/users/2`, etc., est la signature d'une attaque IDOR ou d'une tentative d'exploitation d'une faille de conception.

---

## ✅ Statut

- [x] Room terminée
- [x] Write-up publié

---

*Write-up rédigé dans le cadre de ma préparation au poste d'Analyste SOC junior.*