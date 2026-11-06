# OWASP Top 10 2025: IAAA Failures — Cyber Security 101 (TryHackMe)

**Catégorie :** OWASP Top 10 (2025) / Sécurité Web  
**Date de sortie :** 2025  
**Date de complétion :** 06/11/2026  
**Lien :** https://tryhackme.com/room/owaspiaaafailures  
**Parcours :** [Cyber Security 101](https://tryhackme.com/path/outline/cybersecurity101)

---

## 🎯 Objectif de la room

Comprendre le modèle **IAAA** (Identification, Authentication, Authorization, Accountability) et découvrir comment les failles A01 (Broken Access Control), A07 (Authentication Failures) et A09 (Logging & Alerting Failures) de l'OWASP Top 10 2025 sont liées à des échecs dans ce modèle.

---

## 🧠 Ce que j'ai appris

### Le modèle IAAA
- **Identification** : Qui prétendez-vous être ? (ex: nom d'utilisateur)
- **Authentication (Authentification)** : Prouvez-le. (ex: mot de passe, MFA)
- **Authorization (Autorisation)** : Qu'avez-vous le droit de faire ? (ex: rôles, permissions)
- **Accountability (Imputabilité)** : Qui a fait quoi et quand ? (ex: logs, audit)

### A01 : Broken Access Control (Échec d'Autorisation)
Le serveur ne vérifie pas correctement les permissions. Le cas le plus courant est l'**IDOR** (Insecure Direct Object Reference). Si en changeant un ID dans l'URL (`?accountID=5` → `?accountID=6`), on accède aux données d'un autre utilisateur, la faille est présente.
- **Escalade horizontale** : Accéder aux données d'un autre utilisateur du même rôle.
- **Escalade verticale** : Accéder à des actions réservées aux administrateurs.

### A07 : Authentication Failures (Échec d'Authentification)
La faiblesse réside dans la vérification de l'identité. Cela inclut les mots de passe faibles, l'absence de MFA, les sessions mal gérées (qui ne se ferment pas), ou les attaques par force brute / credential stuffing.

### A09 : Logging & Alerting Failures (Échec d'Imputabilité)
L'application n'enregistre pas les événements critiques (connexions, erreurs, modifications) ou ne déclenche pas d'alertes en cas d'attaque. Sans logs, on ne peut pas savoir ce qui s'est passé, ni détecter une intrusion en cours.

---

## 🖥️ Lignes de commande / Outils utilisés

Cette room est 100% basée sur l'analyse d'une application web statique.

| Action | Description |
|---|---|
| Modification de l'URL | Changer la valeur du paramètre `accountID` dans la barre d'adresse du navigateur pour tester l'IDOR. |

**Note :** Aucune ligne de commande système n'a été utilisée. L'exercice consistait à manipuler l'URL dans le navigateur.

---

## 📌 Ce que je retiens pour un poste d'analyste SOC

- **Détecter l'IDOR dans les logs** : Une vague de requêtes avec des `accountID` séquentiels (1, 2, 3, 4...) provenant du même utilisateur est une alerte typique d'escalade horizontale.
- **A07 (Auth Failures)** : En tant qu'analyste, je verrai beaucoup d'alertes liées à des échecs de connexion (Event ID 4625 sur Windows). Savoir distinguer une erreur de l'utilisateur d'une attaque par force brute (volume, répartition des IP) est crucial.
- **A09 (Logging Failures)** : Si je ne vois pas de logs, je ne peux pas enquêter. La première tâche d'un SOC face à une nouvelle application est de s'assurer que les logs sont bien configurés et envoyés au SIEM.

---

## ✅ Statut

- [x] Room terminée
- [x] Write-up publié

---

*Write-up rédigé dans le cadre de ma préparation au poste d'Analyste SOC junior.*