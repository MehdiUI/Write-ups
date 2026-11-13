# MITRE — Cyber Defence Frameworks (TryHackMe)

**Catégorie :** Blue Team / SOC / Threat Intelligence  
**Date de complétion :** 13/11/2026  
**Lien :** https://tryhackme.com/room/mitre  
**Parcours :** [SOC Level 1](https://tryhackme.com/path/outline/soclevel1)

---

## 🎯 Objectif de la room

Explorer l’écosystème **MITRE** dans son ensemble : le framework **ATT&CK** (base de connaissances des TTPs adverses), son utilisation opérationnelle pour la **Threat Intelligence** et le **profilage de groupes APT**, le **Cyber Analytics Repository (CAR)** pour la détection, le framework défensif **D3FEND**, ainsi que les projets plus récents (**AADAPT**, **ATLAS**, **Caldera**, **Adversary Emulation Library**). L’objectif est de passer d’une lecture passive de la matrice à une utilisation concrète pour qualifier une alerte, construire une détection ou argumenter une remédiation.

---

## 🧠 Ce que j'ai appris

### ATT&CK : TTPs, matrice et Navigator

- **Tactic** : l’objectif de l’adversaire — le “pourquoi” (ex. Reconnaissance, Defense Evasion, Exfiltration).
- **Technique** : comment il atteint cet objectif (ex. `T1136` Create Account, `T1564` Hide Artifacts).
- **Procedure** : l’implémentation concrète par un groupe ou un outil.

La **matrice ATT&CK** organise les tactiques en colonnes et les techniques en lignes, avec des sous-techniques dépliables. L’**ATT&CK Navigator** permet d’annoter et de superposer des couches (layers) pour visualiser la couverture d’un groupe APT ou d’une défense.

### ATT&CK en opération : profilage de groupes APT

La room met en pratique le profilage de deux groupes :

- **Mustang Panda (`G0129`)** : groupe basé en **Chine**, ciblant gouvernements et ONG. Sa technique de Reconnaissance mappée est **`T1598`** (Phishing for Information). Il est connu pour utiliser **Cobalt Strike** pour l’**Access Token Manipulation** (`T1134`).
- **APT33 (`G0064`)** : groupe actif depuis au moins **2013**, ciblant le secteur **aviation**. Pour les entreprises utilisant Office 365, la sous-technique critique est **`T1078.004` Cloud Accounts**. L’outil associé est **Ruler** (outil d’attaque sur Exchange). La mitigation recommandée est **User Account Management** (suppression des comptes inactifs). La stratégie de détection associée est **`DET0546`**.

### Threat Intelligence et partage standardisé

Bien que la room se concentre sur ATT&CK, le rôle de **STIX** (langage standard, lisible par machine, pour représenter les menaces) et **TAXII** (protocole de transport pour échanger du STIX via HTTPS) est essentiel pour automatiser l’enrichissement des alertes en SOC. Le serveur TAXII officiel de MITRE expose les données ATT&CK sous forme d’API.

### CAR (Cyber Analytics Repository)

Base de connaissances d’**analytiques de détection** développée par MITRE, directement alignée sur ATT&CK. Chaque analytique décrit **comment détecter** un comportement, avec des implémentations pour des outils comme **Splunk**, **EQL** ou **LogPoint**. La room utilise deux exemples :

- **`CAR-2019-07-001`** : associée à la tactique **Defense Evasion**. Son type d’analytique est **Situational Awareness**.
- **`CAR-2020-09-001`** (Scheduled Task - File Access) : illustre la traduction d’un TTP en requête SIEM concrète.

CAR fournit également une **couche ATT&CK Navigator** pour visualiser la couverture des analytiques.

### D3FEND

Framework de **contre-mesures défensives** qui complète ATT&CK : là où ATT&CK décrit l’attaque, D3FEND décrit la défense. Organisé en **sept tactiques** (Model, Harden, Detect, Isolate, Deceive, Evict, Restore), il relie chaque technique défensive aux techniques offensives d’ATT&CK et aux **artefacts numériques** concernés. Exemple étudié : la sous-technique **User Geolocation Logon Pattern Analysis** (analyse des tentatives de connexion par géolocalisation) repose sur l’artefact **Network Traffic**.

### Autres projets MITRE

- **Adversary Emulation Library (CTID)** : plans d’émulation pas à pas imitant des groupes APT réels.
- **Caldera** : outil d’**émulation d’adversaire automatisé**, utilisant ATT&CK pour simuler des comportements réels dans un environnement contrôlé (red + blue team).
- **AADAPT** : framework récent pour les **actifs numériques** (blockchain, smart contracts, wallets). Exemple de technique : **`ADT3025` Scrape Blockchain Data**.
- **ATLAS** : framework pour les menaces ciblant l’**IA et le machine learning**. Exemple de technique : **LLM Prompt Obfuscation** (`AML.T0068`), rattachée à la tactique **Defense Evasion**.

---

## 🛠️ Ce que j'ai manipulé

- **ATT&CK Matrix & Navigator** : recherche de techniques (`T1136`, `T1564`), exploration de pages de groupes (`G0129`, `G0064`) et de leurs couches Navigator.
- **Pages de techniques ATT&CK** : lecture des procédures, mitigations (`User Account Management`), détections (`DET0546`) et outils associés (`Cobalt Strike`, `Ruler`).
- **CAR** : consultation d’analytiques (`CAR-2019-07-001`, `CAR-2020-09-001`), identification de la tactique parente et du type d’analytique, lecture des implémentations SIEM.
- **D3FEND** : exploration de techniques défensives (`User Behavior Analysis`), de leurs sous-techniques et des artefacts numériques associés.
- **AADAPT & ATLAS** : navigation dans les matrices, identification d’IDs de techniques (`ADT3025`, `AML.T0068`) et des tactiques correspondantes.
- **Caldera & Emulation Library** : découverte du principe de l’émulation adversary automatisée et des plans d’émulation fournis par la CTID.

---

## 📌 Ce que ça m'apporte pour un SOC

- **Lecture structurée d’une menace** : je sais décomposer une alerte ou un rapport Threat Intel en TTPs ATT&CK, identifier le groupe susceptible d’en être à l’origine et évaluer la gravité en fonction du secteur ciblé.
- **Passerelle vers la détection** : je comprends comment relier une technique ATT&CK à une analytique CAR, puis à une règle de détection opérationnelle (SIEM, EDR) — un attendu central pour un analyste L1/L2.
- **Vision défensive complémentaire** : D3FEND me donne un vocabulaire standard pour proposer des contre-mesures (Harden, Detect, Isolate, Evict…) en réponse à une technique observée, et pour dialoguer avec les équipes de remédiation.
- **Automatisation de la Threat Intelligence** : je connais le rôle de STIX/TAXII et je peux expliquer comment intégrer des flux de Threat Intel dans un SOC de manière standardisée.
- **Culture de l’écosystème MITRE** : je sais distinguer ATT&CK (offensif), CAR (détection), D3FEND (défensif), Caldera (émulation) et les frameworks émergents (AADAPT pour la blockchain, ATLAS pour l’IA), et choisir l’outil adapté à chaque besoin.

---

## ✅ Statut

- [x] Room terminée
- [x] Write-up publié