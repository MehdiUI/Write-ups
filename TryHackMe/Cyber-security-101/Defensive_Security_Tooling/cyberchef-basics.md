# CyberChef: The Basics — Cyber Security 101 (TryHackMe)

**Catégorie :** Defensive Security Tooling  
**Date de sortie :** 2024  
**Date de complétion :** 02/11/2026  
**Lien :** https://tryhackme.com/room/cyberchefbasics  
**Parcours :** [Cyber Security 101](https://tryhackme.com/path/outline/cybersecurity101)  
**Room suivante :** [CAPA: The Basics](./capa-basics.md)

---

## 🎯 Objectif de la room

Savoir décoder et extraire des données (IOC) rapidement sans exécuter de code.

---

## 🧠 Ce que j'ai appris

### Le fonctionnement de CyberChef
CyberChef est un outil web qui fonctionne avec des "Recipes" (recettes). On met une donnée en **Input**, on empile des **Operations** (décoder du Base64, extraire des IP, convertir des dates) et on lit le résultat en **Output**. C'est extrêmement puissant pour l'analyse d'IOC (Indicateurs de Compromission).

### Les opérations utilisées
- **Extract IP addresses** : Trouver des IP dans un texte.
- **From Base64** : Décoder une chaîne.
- **From UNIX Timestamp** : Convertir un timestamp en date lisible.
- **URL Decode / URL Encode** : Décoder ou encoder une URL.

---

## 🖥️ Lignes de commande utilisées

CyberChef étant un outil web (interface graphique), il n'y a pas de lignes de commande à proprement parler. Mais voici les opérations clés qui ont été manipulées via la Recipe :

| Opération (Recipe) | Usage |
|---|---|
| `Extract IP addresses` | Extraire toutes les adresses IPv4/IPv6 d'un bloc de texte. |
| `Extract URLs` | Extraire toutes les URL (nécessite un protocole pour éviter les faux positifs). |
| `Extract email addresses` | Extraire toutes les adresses email du format `user@domain.com`. |
| `From Base64` | Décoder une chaîne Base64 en texte brut. |
| `From UNIX Timestamp` | Convertir un timestamp (ex: `1725151258`) en date lisible. |
| `URL Decode` | Décoder les caractères URL-encodés (ex: `%3A` → `:`). |
| `URL Encode` | Encoder une URL (ex: `:` → `%3A`). |

---

## 📌 Ce que je retiens pour un poste d'analyste SOC

- **L'analyse d'obfuscation** : Les attaquants encodent souvent leur code (PowerShell, base64). Avec CyberChef, je peux le décoder en 2 clics sans exécuter le script.
- **L'extraction d'IOC** : Face à un mail suspect, je peux extraire toutes les URL et les IPs pour les bloquer.
- **Ne jamais exécuter le contenu décodé** sur sa machine. CyberChef est un outil d'analyse, pas un bac à sable.

---

## ✅ Statut

- [x] Room terminée
- [x] Write-up publié

---

*Write-up rédigé dans le cadre de ma préparation au poste d'Analyste SOC junior.*