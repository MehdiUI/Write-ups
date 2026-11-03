# 🧬 CAPA: The Basics

**Objectif de la room :** Apprendre à utiliser CAPA (par Mandiant FLARE) pour effectuer une analyse statique de malwares et identifier leurs capacités (réseau, persistance, obfuscation, etc.) sans les exécuter.

## 📝 Résumé des tâches et réponses

### Task 1 : Introduction
- **Concept :** CAPA est un outil d'analyse statique (sans exécution) qui utilise des règles pour identifier les comportements d'un fichier exécutable (PE, ELF, .NET).
- **Question :** I'm excited to learn more about CAPA!
  - **Réponse :** `No answer needed`

### Task 2 : Tool Overview: How CAPA Works
- **Concept :** Les options principales de CAPA :
  - `-h` : Aide.
  - `-v` : Mode verbeux (détails).
  - `-vv` : Mode très verbeux (encore plus de détails).
  - `Get-Content` : Commande PowerShell pour lire un fichier texte.
- **Questions :**
  - Option pour voir l'aide : `-h`
  - Option pour les détails : `-v`
  - Option pour les très détails : `-vv`
  - Commande PowerShell pour lire un fichier : `Get-Content`

### Task 3 : Dissecting CAPA Results Part 1
- **Concept :** Le rapport CAPA contient plusieurs blocs : informations générales (hashes), MITRE ATT&CK (tactiques/techniques) et MAEC (catégorie de malware : Launcher ou Downloader).
- **Questions :**
  - SHA256 de cryptbot.bin : `ae7bc6b6f6ecb206a7b957e4bb86e0d11845c5b2d9f7a00a482bef63b567ce4c`
  - Technique Identifier de Obfuscated Files or Information : `T1027`
  - Sub-Technique Identifier de Indicator Removal from Tools : `T1027.005`
  - MAEC value pour un fichier qui écrit et exécute : `Launcher`
  - MAEC value pour un fichier qui télécharge depuis Internet : `Downloader`

### Task 4 : Dissecting CAPA Results Part 2 (MBC)
- **Concept :** Le MBC (Malware Behavior Catalogue) décrit les objectifs et comportements des malwares. Les identifiants commencent par B (Behavior), C (Micro-behavior) ou E (technique ATT&CK enrichie).
- **Questions :**
  - Catalogue d'objectifs et comportements : `Malware Behavior Catalogue` (ou `MBC`)
  - Champ basé sur les tactiques ATT&CK : `Objective`
  - Identifier de "Create Process" : `C0017`
  - Comportement avec l'identifiant B0009 : `Virtual Machine Detection`
  - Micro-behavior pour base64 et XOR : `Encode Data`
  - Micro-behavior pour HTTP communications : `HTTP Communication`

### Task 5 : Dissecting CAPA Results Part 3 (Namespaces)
- **Concept :** Les Namespaces sont des "dossiers" logiques pour classer les règles. Le TLN (Top-Level Namespace) est le dossier principal (ex: `anti-analysis`, `communication`, `persistence`).
- **Questions :**
  - TLN pour obfuscation/packing/anti-debugging : `anti-analysis`
  - Namespace pour la détection de VM : `anti-vm/vm-detection`
  - TLN pour la persistance : `persistence`
  - Namespace pour Dotfuscator/SmartAssembly : `obfuscation`
  - TLN "terrain d'essai" : `nursery`
  - Question finale : `No answer needed`

### Task 6 : Dissecting CAPA Results Part 4 (Capability)
- **Concept :** La Capability est le nom de la règle. Le fichier YAML correspond au nom de la capacité en minuscules avec des tirets à la place des espaces.
- **Questions :**
  - Fichier YAML pour `check HTTP status code` : `check-http-status-code.yml`
  - Capacité pour `reference-anti-vm-strings.yml` : `reference anti-VM strings`
  - TLN pour `run PowerShell expression` : `load-code`
  - API recherchée par `check-for-windows-sandbox-via-registry.yml` : `RegOpenKeyEx`

### Task 7 : More Information, More Fun!
- **Concept :** Pour analyser les résultats très verbeux (`-vv`), on utilise l'option `-j` pour générer un fichier JSON. Ensuite, on ouvre ce fichier dans **CAPA Explorer Web** (interface graphique) pour explorer les résultats de manière interactive. La **Global Search box** permet de filtrer les résultats.
- **Questions :**
  - Paramètre pour sortir en JSON : `-j`
  - Outil pour explorer dans le navigateur : `CAPA Explorer Web`
  - Fonctionnalité de filtrage : `Global Search box`

### Task 8 : Conclusion
- **Question :** No answer needed

## 🧠 Ce que je retiens pour un poste d'Analyste SOC
- **L'analyse statique** : CAPA permet d'analyser un malware sans l'exécuter (pas de risque d'infection). C'est la première étape avant une analyse dynamique en sandbox.
- **Le mapping MITRE ATT&CK** : CAPA associe automatiquement les capacités du malware aux techniques ATT&CK (ex: `T1027` pour l'obfuscation). Cela permet de comprendre comment l'attaquant opère et de préparer les défenses.
- **Le MBC** : Le Malware Behavior Catalogue offre un vocabulaire standardisé pour décrire les comportements malveillants, facilitant la communication entre analystes et le partage de Threat Intelligence.
- **CAPA Explorer Web** : Face à des milliers de lignes de résultats, l'interface web permet de filtrer, rechercher et visualiser les correspondances de règles, ce qui est indispensable pour une investigation efficace.