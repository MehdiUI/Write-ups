# Offensive Security Intro — Cyber Security 101 (TryHackMe)

**Catégorie :** Offensive Security  
**Date de sortie :** 2024  
**Date de complétion :** 20/10/2026  
**Lien :** https://tryhackme.com/room/offensivesecurityintro  
**Parcours :** [Cyber Security 101](https://tryhackme.com/path/outline/cybersecurity101)  
**Room suivante :** [Defensive Security Intro](./defensive-security-intro.md)

---

## 🎯 Objectif de la room

Découvrir le métier d'ethical hacker et réaliser son premier "hack" légal sur une application bancaire factice.

---

## 🧠 Ce que j'ai appris

### La sécurité offensive
La sécurité offensive consiste à penser comme un attaquant pour trouver les failles avant les vrais hackers. J'ai découvert l'importance de l'énumération : chercher des pages cachées peut mener à un panneau d'administration mal sécurisé.

### L'énumération
C'est une phase bruyante mais souvent efficace. En tant qu'analyste, je verrai des scans de répertoires dans les logs web et je devrai les repérer.

---

## 🖥️ Lignes de commande utilisées

Toutes les commandes ont été exécutées dans le terminal de l'AttackBox.

| Commande | Description |
|---|---|
| `dirb http://fakebank.thm` | Scanner les répertoires et fichiers cachés du site. |

*Note : l'outil `dirb` a permis de trouver la page `/bank-transfer` qui a servi à ajouter de l'argent sur le compte 8881.*

---

## 📌 Ce que je retiens pour un poste d'analyste SOC

- **Comprendre l'attaquant** : En voyant comment un attaquant exploite une faille, je pourrai mieux la détecter côté défense.
- **L'énumération** : C'est une phase bruyante mais souvent efficace. En tant qu'analyste, je verrai des scans de répertoires dans les logs web et je devrai les repérer.
- **Ne jamais faire cela sans autorisation** : Le hacking éthique se pratique dans un cadre légal.

---

## ✅ Statut

- [x] Room terminée
- [x] Write-up publié

---

*Write-up rédigé dans le cadre de ma préparation au poste d'Analyste SOC junior.*