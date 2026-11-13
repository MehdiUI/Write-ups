# Summit — Cyber Defence Frameworks (TryHackMe)

**Catégorie :** Blue Team / SOC / Detection Engineering  
**Date de complétion :** 13/11/2026  
**Lien :** https://tryhackme.com/room/summit  
**Parcours :** [SOC Level 1](https://tryhackme.com/path/outline/soclevel1)

---

## 🎯 Objectif de la room

Mettre en pratique la **Pyramid of Pain** dans un scénario de **purple team** simulé. Un pentester externe (Sphinx Security) exécute une série d’échantillons malveillants contre un poste de travail interne ; l’analyste SOC doit configurer les outils de défense de l’entreprise pour détecter et bloquer chaque échantillon, en remontant progressivement la pyramide : du hash (trivial) jusqu’aux TTPs (difficile). Chaque blocage réussi force l’attaquant à adapter sa technique, augmentant son coût opérationnel jusqu’à l’abandon.

---

## 🧠 Ce que j'ai appris

### La Pyramid of Pain en conditions réelles

La room est la conclusion pratique du module Cyber Defence Frameworks : **Pyramid of Pain → Cyber Kill Chain → Unified Kill Chain → MITRE ATT&CK → Summit**. Chaque niveau de la pyramide correspond à un échantillon (`sampleN.exe`) et à un mécanisme de défense spécifique :

| Niveau (Pyramid of Pain) | Échantillon | Mécanisme de défense | Ce que ça bloque | Coût pour l’attaquant |
|---|---|---|---|---|
| **Hash Values** | `sample1.exe` | Hash blocklist (SHA1) | Un fichier exact | **Trivial** : un bit modifié change le hash |
| **IP Address** | `sample2.exe` | Firewall egress rule | La communication avec une IP C2 | **Easy** : VPN, proxy, Fast Flux |
| **Domain Names** | `sample3.exe` | DNS filtering rule | La résolution d’un domaine malveillant | **Simple** : DGA, typosquatting |
| **Host Artifacts** | `sample4.exe` | Sigma rule sur événement Sysmon (Registry Modification) | Le comportement local (ex. désactivation de Defender) | **Annoying** : l’attaquant doit modifier ses outils |
| **Network Artifacts** | `sample5.exe` (logs) | Sigma rule sur Network Connection (beaconing 97 bytes / 1800 s) | Le pattern de communication C2, même si l’IP change | **Annoying** : l’attaquant doit changer son mode opératoire réseau |
| **Tools / TTPs** | `sample6.exe` (logs de commandes) | Sigma rule sur Process Creation (pattern d’exfiltration vers `%temp%\exfiltr8.log`) | Le comportement, indépendamment de l’outil ou de l’infrastructure | **Tough / Challenging** : changement fondamental de méthode |

### Detection Engineering avec Sigma et Sysmon

La room introduit le **Sigma Rule Builder** : un outil qui traduit une intention de détection en une règle Sigma standardisée, directement exploitable par un SIEM. Les règles sont construites à partir d’événements **Sysmon** (Registry Modifications, Network Connections, Process Creation), avec un mapping systématique vers une **tactique MITRE ATT&CK** :

- **Defense Evasion (TA0005)** pour la désactivation de Windows Defender via le registre.
- **Command and Control (TA0011)** pour le beaconing C2.
- **Collection** pour le pattern d’exfiltration vers un fichier temporaire.

Cette approche illustre la transition d’une défense **réactive** (bloquer un IOC) à une défense **proactive** (détecter un comportement).

### La logique de l’escalade

Chaque fois qu’un échantillon est bloqué, Sphinx (l’attaquant simulé) change la couche d’indicateur qu’il utilise. La room démontre ainsi pourquoi un SOC ne peut pas se contenter de blocklists : l’attaquant contourne systématiquement les couches basses. Seules les couches hautes (Network Artifacts, TTPs) imposent un coût suffisant pour le faire reculer.

---

## 🛠️ Ce que j'ai manipulé

- **Malware Sandbox** : exécution des échantillons (`sample1.exe` à `sample4.exe`) pour obtenir des rapports d’analyse statique et dynamique (hashes, IPs, domaines, clés de registre, connexions réseau).
- **Hash Blocklist** : blocage du hash SHA1 d’un fichier malveillant.
- **Firewall Rule Manager** : création d’une règle **egress** (sortant) pour bloquer une IP C2.
- **DNS Filter** : création d’une règle de blocage d’un domaine classé “malware”.
- **Sigma Rule Builder** : construction de règles de détection à partir d’événements Sysmon :
  - **Registry Modification** : détection de `DisableRealtimeMonitoring = 1` (désactivation de Windows Defender).
  - **Network Connection** : détection d’un pattern de beaconing (taille 97 bytes, intervalle 1800 s), indépendamment de l’IP.
  - **Process Creation** : détection d’un pattern d’exfiltration (redirection de commandes vers `%temp%\exfiltr8.log`).
- **Mapping MITRE ATT&CK** : association de chaque règle Sigma à une tactique (Defense Evasion, Command and Control, Collection).
- **Analyse de logs** : lecture de `outgoing_connections.log` et `commands.log` pour identifier des patterns comportementaux (beaconing, exfiltration) plutôt que des IOC isolés.

---

## 📌 Ce que ça m'apporte pour un SOC

- **Detection engineering concrète** : je sais passer d’un rapport d’analyse malware à une règle Sigma déployable, avec un mapping ATT&CK explicite — une compétence directement attendue d’un analyste L1/L2 orienté détection.
- **Lecture critique des blocklists** : je comprends pourquoi bloquer un hash ou une IP est nécessaire mais insuffisant, et pourquoi un SOC doit investir dans les couches hautes de la pyramide.
- **Maîtrise de Sigma et Sysmon** : je connais les types d’événements Sysmon pertinents (Registry Modifications, Network Connections, Process Creation) et la syntaxe de base d’une règle Sigma.
- **Réflexe TTP-based** : face à une alerte, je cherche désormais à identifier le **comportement** sous-jacent (beaconing, exfiltration via redirection) plutôt que de me limiter à l’IOC qui a déclenché la détection.
- **Compréhension du purple team** : la room simule une collaboration red/blue ; je sais comment un pentester adapte ses techniques en fonction des défenses déployées, et comment un analyste SOC doit anticiper cette adaptation.
- **Lien avec les frameworks** : Summit consolide l’usage opérationnel de la Pyramid of Pain et de MITRE ATT&CK dans un contexte de détection réelle, en complément des rooms théoriques du module.

---

## ✅ Statut

- [x] Room terminée
- [x] Write-up publié