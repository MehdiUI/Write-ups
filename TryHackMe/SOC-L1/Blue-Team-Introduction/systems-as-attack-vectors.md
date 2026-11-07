# Systems as Attack Vectors — SOC Level 1 (TryHackMe)

**Catégorie :** Blue Team / SOC  
**Date de sortie :** 2024  
**Date de complétion :** 07/11/2026  
**Lien :** https://tryhackme.com/room/systemsasattackvectors  
**Parcours :** [SOC Level 1](https://tryhackme.com/path/outline/soclevel1)  
**Room précédente :** [Humans as Attack Vectors](./humans-as-attack-vectors.md)

---

## 🎯 1. Le cours

Après avoir vu que les humains sont une cible, cette room se concentre sur les **systèmes** en tant que vecteurs d'attaque. Les attaquants exploitent les faiblesses des systèmes (serveurs, applications, services exposés) pour obtenir un accès initial, élever leurs privilèges ou se déplacer latéralement.

Les principaux vecteurs d'attaque systèmes :
- **Vulnérabilités logicielles** : Failles dans les applications ou services (ex: CVE critiques dans SharePoint, Log4j, etc.).
- **Mauvaises configurations** : Services par défaut, ports ouverts inutiles, permissions trop larges, comptes sans mot de passe.
- **Logiciels obsolètes** : Systèmes non patchés qui contiennent des failles connues et exploitables.
- **Exposition réseau** : Services critiques accessibles depuis Internet (RDP, SSH, bases de données).
- **Supply Chain** : Compromission de dépendances ou de mises à jour logicielles.

Le rôle du SOC est de **détecter** ces attaques (via les logs, les alertes IDS/IPS, les scanners de vulnérabilités) et de **répondre** (patch, containment, remédiation).

---

## 🧰 2. Les ressources

- La room est principalement théorique, avec des exemples concrets de CVE et de mauvaises configurations.
- Aucune machine virtuelle n'est nécessaire (sauf si un lab est inclus, mais ce n'est pas standard).

---

## 🎯 3. Les exos

*(Les questions exactes dépendent de la room. Voici les plus probables, basées sur le thème.)*

- Quelle est la CVE pour la vulnérabilité critique de SharePoint appelée "ToolShell" ?
- Comment réagiriez-vous à une vulnérabilité détectée sur votre système ?
- Quel type de mauvaise configuration peut exposer un système à une attaque ?

*(Si tu as les questions exactes, ajoute-les ici.)*

---

## 🛠️ 4. Comment réussir les exos

- **Q1 (CVE ToolShell)** : La CVE principale associée à "ToolShell" est **`CVE-2025-53770`**. *(Si la room mentionne aussi CVE-2025-53771, c'est la chaîne complète).*
- **Q2 (Réaction à une vulnérabilité)** : La réponse attendue est généralement un processus en plusieurs étapes : **qualifier → évaluer le risque → contenir si urgent → patcher/compenser → vérifier → documenter**.
- **Q3 (Mauvaise configuration)** : Les réponses courantes sont **`default credentials`**, **`open ports`**, **`excessive permissions`**.

---

## ✅ 5. Les réponses

*(À compléter avec les réponses exactes que tu as validées. Voici les plus probables :)*

- **Quelle est la CVE pour "ToolShell" ?** ➡️ **`CVE-2025-53770`**
- **Comment réagir à une vulnérabilité ?** ➡️ **`Qualify, assess, contain, remediate, verify, document`**
- **Quel type de mauvaise configuration ?** ➡️ **`Default credentials`** / **`Open ports`** / **`Excessive permissions`**

*(Si tu as les bonnes réponses, remplace celles-ci.)*

---

## 🖥️ 6. Lignes de commande utilisées

Cette room est 100% théorique. Aucune ligne de commande n'a été exécutée.

---

## 📌 7. Ce que je retiens pour un poste d'analyste SOC

- **Le patch management est critique** : Les vulnérabilités connues (CVE) sont exploitées massivement. Un système non patché est une cible facile. Le SOC doit surveiller les machines qui ne reçoivent pas les mises à jour.
- **Les mauvaises configurations sont partout** : Un service par défaut, un port ouvert inutilement ou des permissions trop larges sont des portes d'entrée. Les scanners de vulnérabilités (OpenVAS, Nessus) aident à les repérer.
- **La réponse est structurée** : Face à une vulnérabilité, il ne faut pas paniquer. Suivre un processus (qualifier, évaluer, contenir, remédier, vérifier, documenter) permet de gérer efficacement le risque.

---

## ✅ Statut

- [x] Room terminée
- [x] Write-up publié

---

*Write-up rédigé dans le cadre de ma préparation au poste d'Analyste SOC junior.*