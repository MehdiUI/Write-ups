# Digital Forensics Fundamentals — Cyber Security 101 (TryHackMe)

**Catégorie :** Defensive Security  
**Date de sortie :** 2024  
**Date de complétion :** 01/11/2026  
**Lien :** https://tryhackme.com/room/digitalforensicsfundamentals  
**Parcours :** [Cyber Security 101](https://tryhackme.com/path/outline/cybersecurity101)  
**Room précédente :** [SOC Fundamentals](./soc-fundamentals.md)  
**Room suivante :** [Incident Response Fundamentals](./incident-response-fundamentals.md)

---

## 🎯 Objectif de la room

Comprendre comment investiguer un cybercrime, collecter des preuves sans les altérer et analyser des métadonnées.

---

## 🧠 Ce que j'ai appris

### Le processus forensique
Une preuve altérée est inutilisable. Il faut suivre un processus strict (Collection, Examination, Analysis, Reporting).

### Les deux règles d'or
- **Write Blocker** : Un outil physique qui empêche l'ordinateur d'enquête de modifier accidentellement le disque dur du suspect.
- **Chain of Custody** : Un document qui trace qui a touché la preuve, quand et où.

### L'ordre de capture
Sur Windows, on capture d'abord la RAM (**Memory Image**) avant de capturer le disque (**Disk Image**), car la RAM contient des données volatiles très utiles (processus en cours, connexions réseau).

### Les outils
J'ai utilisé `pdfinfo` pour extraire les métadonnées d'un PDF (auteur) et `exiftool` pour extraire les données EXIF d'une image (GPS, modèle de caméra).

---

## 📌 Ce que je retiens pour un poste d'analyste SOC

- **L'analyse des métadonnées** : Les fichiers (images, PDF) parlent. Extraire l'auteur d'un document ou les coordonnées GPS d'une photo peut faire avancer une enquête en quelques secondes.
- **La rigueur** : Comprendre l'importance de la Chain of Custody me prépare à interagir avec les équipes de forensique si mon SOC gère un incident majeur.
- **Ne pas improviser** : L'analyse forensique ne s'improvise pas. Si on n'a pas les bons outils (Write Blocker), on risque de détruire la preuve.

---

## ✅ Statut

- [x] Room terminée
- [x] Write-up publié

---

*Write-up rédigé dans le cadre de ma préparation au poste d'Analyste SOC junior.*