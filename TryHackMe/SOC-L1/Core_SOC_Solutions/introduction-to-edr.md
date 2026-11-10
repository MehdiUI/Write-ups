# Introduction to EDR — SOC Level 1 (TryHackMe)

**Catégorie :** Blue Team / SOC  
**Date de complétion :** 10/11/2026  
**Lien :** https://tryhackme.com/room/introductiontoedr  
**Parcours :** [SOC Level 1](https://tryhackme.com/path/outline/soclevel1)

---

## 🎯 Objectif de la room

Comprendre les fondamentaux de l'EDR (Endpoint Detection and Response), son fonctionnement, sa télémétrie, ses techniques de détection avancées et ses capacités de réponse.

---

## 🧠 Ce que dit le cours

### EDR vs Antivirus (Analogie)
- **Antivirus (AV)** : Comparé au contrôle d'immigration dans un aéroport. Il vérifie les passeports des personnes entrantes par rapport à une liste de criminels connus (détection par signature). Il ne détecte pas les menaces inconnues.
- **EDR** : Comparé aux agents de sécurité à l'intérieur de l'aéroport. Ils surveillent les caméras et les capteurs de mouvement (télémétrie) pour détecter des comportements suspects, même si la personne est entrée légalement.

### Le scénario d'attaque
Le cours détaille une attaque étape par étape :
1. Email de phishing avec un document Word contenant une macro malveillante.
2. Téléchargement et ouverture du document.
3. La macro s'exécute silencieusement et lance PowerShell.
4. PowerShell exécute une commande obfusquée pour télécharger une charge utile.
5. La charge utile est injectée dans le processus légitime `svchost.exe`.
6. L'attaquant obtient un accès distant.

**Comparaison AV vs EDR :**
- L'AV ne détecte rien si le fichier n'a pas de signature connue, si l'outil est légitime (`winword.exe`), si le script est obfusqué, ou s'il y a une injection mémoire. Il manque de visibilité réseau et peut marquer l'activité comme "clean".
- L'EDR enregistre le téléchargement, surveille `winword.exe`, détecte la relation parent-enfant inhabituelle (`winword.exe` → `powershell.exe`), signale le script obfusqué, détecte l'injection dans `svchost.exe` et signale la connexion sortante inattendue. Il génère une alerte avec la chaîne d'attaque complète.

### Fonctionnement de l'EDR
- **Agents (ou Sensors)** : Déployés sur les endpoints, ce sont les "yeux et oreilles". Ils surveillent les activités et envoient les données à la console.
- **Console EDR** : Corrèle et analyse les données avec du machine learning et de la Threat Intelligence. Génère les alertes et donne une vue d'ensemble.
- **Rôle de l'analyste** : Acquitter l'alerte, la prioriser selon la sévérité (Critical, High, Medium, Low, Informational), investiguer les détails (fichiers, processus, réseau, registre) et déterminer si c'est un faux ou vrai positif.
- **Écosystème** : L'EDR travaille avec d'autres outils (pare-feux, DLP, passerelles email, IAM) et s'intègre souvent à un SIEM pour une investigation centralisée.

### Télémétrie collectée
- **Process Executions and Terminations** : Suivi des processus (relations parent-enfant).
- **Network Connections** : Détection des connexions C2, ports inhabituels, exfiltration, mouvement latéral.
- **Command Line Activity** : Capture des commandes (CMD, PowerShell) pour repérer les scripts obfusqués.
- **Files and Folders Modifications** : Détection du data staging, ransomwares, dépôt de fichiers malveillants.
- **Registry Modifications** : Suivi des changements dans le registre (cible fréquente des malwares).

### Techniques de détection avancées
- **Behavioral Detection** : Analyse du comportement (ex: `winword.exe` lançant `powershell.exe`).
- **Anomaly Detection** : Détection des écarts par rapport à la baseline de l'endpoint.
- **IOC Matching** : Comparaison avec des indicateurs de compromission connus (hashes, etc.) issus de la Threat Intelligence.
- **MITRE ATT&CK Mapping** : Chaque alerte est associée à une tactique et technique ATT&CK.
- **Machine Learning Algorithms** : Détection de chaînes d'activités complexes (attaques fileless, intrusions multi-étapes).

### Capacités de réponse
- **Isolate Host** : Isoler un endpoint du réseau pour contenir l'attaque.
- **Terminate Process** : Tuer un processus malveillant (à utiliser avec précaution sur les processus critiques).
- **Quarantine** : Déplacer un fichier malveillant dans un emplacement isolé.
- **Remote Access** : Accéder au shell de l'endpoint à distance (ex: CrowdStrike Falcon RTR).
- **Artefacts Collection** : Extraire des données pour l'investigation (Memory Dump, Event Logs, contenu de dossiers, ruches de registre).

---

## 🛠️ Ce que le cours mentionne comme manipulation

Le cours inclut une démonstration statique d'une console EDR (CrowdStrike Falcon). Il mentionne l'analyse de télémétries pour investiguer des détections (processus, lignes de commande, chemins de fichiers, connexions réseau) et la possibilité de prendre des actions (isoler, tuer un processus, collecter des artefacts) directement depuis la console.

---

## ✅ Statut

- [x] Room terminée
- [x] Write-up publié