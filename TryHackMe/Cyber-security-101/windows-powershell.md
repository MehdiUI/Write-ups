# Windows PowerShell — Cyber Security 101 (TryHackMe)

**Catégorie :** Windows & Command Line  
**Date de sortie :** Juillet 2021  
**Date de complétion :** 27/10/2026  
**Lien :** https://tryhackme.com/room/windowspowershell  
**Parcours :** [Cyber Security 101](https://tryhackme.com/path/outline/cybersecurity101)  
**Room précédente :** [Windows Command Line](./windows-command-line.md)  
**Room suivante :** Linux Shells

---

## 🎯 Objectif de la room

Découvrir PowerShell, le shell et langage de script de Windows, et comprendre pourquoi il est devenu un outil incontournable pour les administrateurs système comme pour les analystes SOC.

---

## 🧠 Ce que j'ai appris

### Qu'est-ce que PowerShell ?

PowerShell est un shell en ligne de commande et un langage de script construit sur le framework .NET. Contrairement au Command Prompt (CMD) qui travaille avec du texte brut, PowerShell travaille avec des **objets**. Cela signifie que les données retournées par une commande peuvent être manipulées, filtrées et formatées beaucoup plus facilement.

### Les concepts clés

- **Cmdlets** : Les commandes PowerShell suivent une structure **Verbe-Nom** (ex : `Get-Process`, `Set-Location`). C'est très intuitif.
- **Objets** : Les résultats ne sont pas juste du texte, ce sont des objets avec des propriétés.
- **Pipelines (`|`)** : Permettent de passer la sortie d'une commande à une autre (ex : `Get-Process | Where-Object CPU -gt 100`).
- **Alias** : Des raccourcis pour les commandes (ex : `ls` ou `dir` sont des alias de `Get-ChildItem`).

### Les commandes de base

- **Découverte** : `Get-Command` (lister les commandes), `Get-Help` (obtenir de l'aide).
- **Fichiers & Navigation** : `Get-ChildItem` (lister), `Get-Location` (dossier courant), `Get-Content` (lire un fichier), `Set-Location` (changer de dossier).
- **Système** : `Get-Process` (voir les processus en cours), `Get-Service` (voir les services), `Get-ComputerInfo` (infos système).
- **Réseau** : `Test-Connection` (l'équivalent de `ping`), `Get-NetTCPConnection` (voir les connexions actives).

---

## 📌 Ce que je retiens pour un poste d'analyste SOC

- **Living off the Land (LotL)** : Les attaquants utilisent massivement PowerShell (étant natif à Windows) pour télécharger et exécuter des payloads sans avoir besoin d'installer d'outils supplémentaires. Repérer ces commandes est vital.
- **Obfuscation** : Les attaquants encodent souvent leurs commandes PowerShell en Base64 (`-EncodedCommand`) pour contourner les antivirus. Savoir les décoder est un réflexe d'analyste.
- **Logs PowerShell** : En SOC, on surveille très attentivement les Event IDs 4103 et 4104 (Script Block Logging) pour voir exactement ce qui a été exécuté sur une machine.
- **Réponse à incident** : `Get-Process`, `Get-Service` ou `Get-NetTCPConnection` sont les premières commandes à lancer pour avoir une vision instantanée de l'état d'une machine compromise.

---

## ✅ Statut

- [x] Room terminée
- [x] Write-up publié

---

*Write-up rédigé dans le cadre de ma préparation au poste d'Analyste SOC junior.*