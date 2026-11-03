# Logs Fundamentals — Cyber Security 101 (TryHackMe)

**Catégorie :** Defensive Security  
**Date de sortie :** 2024  
**Date de complétion :** 02/11/2026  
**Lien :** https://tryhackme.com/room/logsfundamentals  
**Parcours :** [Cyber Security 101](https://tryhackme.com/path/outline/cybersecurity101)  
**Room précédente :** [Incident Response Fundamentals](./incident-response-fundamentals.md)  
**Room suivante :** [Security Solutions](../Security_Solutions/README.md)

---

## 🎯 Objectif de la room

Savoir où trouver les traces d'une attaque et comment les filtrer dans Windows (Event Viewer) et sous Linux (logs web).

---

## 🧠 Ce que j'ai appris

### Les Event IDs Windows
Windows stocke des Event IDs précis : 
- `4624` (connexion réussie)
- `4625` (échec de connexion)
- `4720` (création de compte)
- `4722` (activation de compte)
- `4724` (réinitialisation de mot de passe)

### Les logs Web (Linux)
Sur Linux, les serveurs web (Apache) écrivent chaque requête dans un `access.log`. L'analyste doit savoir filtrer ces données massives pour trouver l'aiguille dans la botte de foin.

### Les outils
- **Event Viewer** (Windows) : permet de filtrer par Event ID.
- **`grep`** (Linux) : permet d'extraire des lignes spécifiques d'un fichier de logs.

---

## 📌 Ce que je retiens pour un poste d'analyste SOC

- **Les Event IDs** : Je connais maintenant les ID critiques. Si je vois un `4720` à 3h du matin suivi d'un `4722` (activation), j'aurai un doute immédiat.
- **La ligne de commande** : `grep` est mon meilleur ami. Sur un serveur sans interface graphique, je passerai mon temps à filtrer des logs avec cette commande.
- **Le volume de logs est énorme** : Il faut toujours filtrer par date ou par IP avant de lire, sinon on s'y perd.

---

## ✅ Statut

- [x] Room terminée
- [x] Write-up publié

---

*Write-up rédigé dans le cadre de ma préparation au poste d'Analyste SOC junior.*