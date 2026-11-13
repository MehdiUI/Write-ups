# Eviction — Cyber Defence Frameworks (TryHackMe)

**Catégorie :** Blue Team / SOC / Threat Hunting  
**Date de complétion :** 13/11/2026  
**Lien :** https://tryhackme.com/room/eviction  
**Parcours :** [SOC Level 1](https://tryhackme.com/path/outline/soclevel1)

---

## 🎯 Objectif de la room

Incarner **Sunny**, analyste SOC chez **E-corp** (fabricant de terres rares pour des clients gouvernementaux et non-gouvernementaux). Un rapport de renseignement classifié indique que le groupe **APT28 (`G0007`)** cible des organisations similaires à E-corp. À l’aide d’une **couche MITRE ATT&CK Navigator** fournie, l’objectif est triple : **profiler** les TTPs de l’APT, **chasser** les traces d’une intrusion déjà en cours dans le réseau, et **expulser** l’attaquant avant qu’il n’exfiltre de la propriété intellectuelle critique. La room est le challenge final du module **Cyber Defence Frameworks**.

---

## 🧠 Ce que j'ai appris

### Le scénario “Eviction”

La room illustre la **phase d’expulsion** (*eviction*) : une fois le périmètre de compromission confirmé, le SOC doit retirer l’accès de l’adversaire pour l’empêcher de maintenir sa persistance, de se déplacer latéralement ou de revenir. Le raisonnement suit le cycle de vie de l’attaque : de la reconnaissance jusqu’à la collection et l’exfiltration, en s’appuyant sur la carte des techniques d’APT28 fournie dans le Navigator[reference:0].

### Cartographie des TTPs d’APT28 par tactique

La couche Navigator met en évidence les techniques et sous-techniques réellement utilisées par le groupe. Chaque question de la room amène à en identifier une :

| Tactique (ATT&CK) | Technique / Sous-technique identifiée | Rôle dans le scénario |
|---|---|---|
| **Reconnaissance + Initial Access** | `Spearphishing Link` (`T1566.002`) | Lien malveillant dans un email ciblé : sert à la fois à la reconnaissance (qui clique, depuis où) et à l’accès initial[reference:1] |
| **Resource Development** | `Email Accounts` (`T1586.002`) | Compromission de comptes email pour développer des ressources et rebondir vers des cibles de plus haute valeur[reference:2] |
| **Execution** | `Malicious File` et `Malicious Link` (`T1204.002` / `T1204.001`) | Deux modes d’exécution déclenchés par l’utilisateur (pièce jointe ou lien)[reference:3] |
| **Execution** | `PowerShell` et `Windows Command Shell` (`T1059.001` / `T1059.003`) | Interpréteurs à rechercher dans les logs pour confirmer l’exécution de scripts (souvent obfusqués)[reference:4] |
| **Persistence** | `Registry Run Keys` (`T1547.001`) | Clés de registre modifiées par les scripts obfusqués pour survivre au redémarrage[reference:5] |
| **Defense Evasion** | `Rundll32` (`T1218.011`) | Exécution de binaires système pour contourner les défenses (*System Binary Proxy Execution*)[reference:6] |
| **Discovery** | `Network Sniffing` (`T1040`) | Présence de `tcpdump` sur un hôte compromis : collecte d’informations réseau[reference:7] |
| **Lateral Movement** | `SMB / Windows Admin Shares` (`T1021.002`) | Déplacement latéral via l’exploitation de services distants[reference:8] |
| **Collection** | `SharePoint` (`T1213.002`) | Cible probable pour le vol de propriété intellectuelle dans les référentiels d’entreprise[reference:9] |
| **Command and Control** | `External Proxy` et `Multi-hop Proxy` (`T1090.002` / `T1090.003`) | Types de proxy que l’APT pourrait utiliser pour contourner le blocage de la connexion C2 et exfiltrer les données[reference:10] |

### La logique défensive : de la Threat Intel à l’éviction

La room montre comment une **couche ATT&CK Navigator** transforme un rapport de renseignement en **plan de chasse opérationnel**. Plutôt que de chercher au hasard, Sunny sait exactement quelles techniques surveiller à chaque étape : d’abord le clic sur un lien spearphishing, puis les interpréteurs PowerShell/CMD, puis les clés Run, puis `rundll32`, puis `tcpdump`, puis SMB, puis SharePoint, puis les proxys C2. Cette approche **TTP-driven** est ce qui permet d’expulser l’attaquant de manière méthodique, sans se limiter à des indicateurs éphémères.

---

## 🛠️ Ce que j'ai manipulé

- **MITRE ATT&CK Navigator** : chargement de la couche **APT28 (`G0007`)** fournie par la room (`static-labs.tryhackme.cloud/sites/eviction/`), lecture des tactiques en colonnes, identification des cellules bleues (techniques du groupe), exploration des sous-techniques et comparaison entre tactiques pour trouver les techniques partagées.
- **Analyse de la couche** : pour chaque question, localisation de la tactique concernée, inspection des enfants d’une technique parente, distinction entre techniques et sous-techniques, et vérification du libellé exact avant soumission.
- **Raisonnement de threat hunting** : à partir des techniques identifiées, déduction des sources de logs à consulter (ex. journaux de clics email, logs PowerShell/CMD, événements de modification du registre, connexions SMB, accès SharePoint, flux proxy).
- **Plan d’éviction** : identification des points de contrôle à bloquer ou surveiller pour retirer l’accès de l’APT (persistance via Run Keys, exécution via `rundll32`, mouvement latéral via SMB, exfiltration via proxys).

---

## 📌 Ce que ça m'apporte pour un SOC

- **Threat hunting guidé par les TTPs** : je sais utiliser une couche ATT&CK Navigator pour transformer un rapport de Threat Intelligence en une liste de techniques concrètes à chasser, tactique par tactique.
- **Maîtrise de l’ATT&CK Navigator** : je suis à l’aise avec la lecture d’une matrice, l’identification des sous-techniques pertinentes et la vérification des libellés — une compétence directement réutilisable en SOC.
- **Compréhension du cycle APT28** : je connais les techniques clés de ce groupe (spearphishing, comptes email, Run Keys, `rundll32`, `tcpdump`, SMB, SharePoint, proxys) et je peux les relier aux sources de logs correspondantes.
- **Réflexe “éviction”** : face à une compromission confirmée, je sais raisonner en termes de **retrait d’accès** (persistance, mouvement latéral, C2) plutôt que de simplement “nettoyer” un hôte.
- **Lien entre frameworks** : Eviction consolide l’usage opérationnel de la Pyramid of Pain, de la Cyber Kill Chain, de l’UKC et de MITRE ATT&CK dans un scénario de threat hunting réaliste — la conclusion logique du module Cyber Defence Frameworks.

---

## ✅ Statut

- [x] Room terminée
- [x] Write-up publié