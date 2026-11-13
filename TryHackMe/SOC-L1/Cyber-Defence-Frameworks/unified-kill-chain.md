# Unified Kill Chain — Cyber Defence Frameworks (TryHackMe)

**Catégorie :** Blue Team / SOC / Threat Modelling  
**Date de complétion :** 13/11/2026  
**Lien :** https://tryhackme.com/room/unifiedkillchain  
**Parcours :** [SOC Level 1](https://tryhackme.com/path/outline/soclevel1)

---

## 🎯 Objectif de la room

Découvrir le framework **Unified Kill Chain (UKC)** créé par Paul Pols en 2017. L’UKC fusionne la **Cyber Kill Chain** de Lockheed Martin (7 phases linéaires) et **MITRE ATT&CK** (base de connaissances comportementale) pour produire un modèle plus complet et itératif de 18 phases. L’objectif défensif : mieux comprendre la progression d’un attaquant — de la reconnaissance initiale jusqu’à l’exfiltration — afin de placer des contrôles de détection et de prévention à chaque étape, plutôt que de se limiter à une vision linéaire de l’attaque[reference:0][reference:1].

---

## 🧠 Ce que j'ai appris

### Les trois grandes phases de l’UKC

L’UKC regroupe ses 18 phases en trois objectifs opérationnels :

1. **In (Initial Foothold)** : l’attaquant obtient un premier accès. Inclut la reconnaissance, l’arméisation, l’ingénierie sociale, l’exploitation, la persistance, l’évasion de défense, le C2 et le **pivoting** initial[reference:2].
2. **Through (Network Propagation)** : l’attaquant se déplace latéralement et consolide son emprise. Couvre la **découverte** interne, l’**élévation de privilèges**, l’**exécution** de charges, l’**accès aux identifiants** et le **mouvement latéral**[reference:3].
3. **Out (Action on Objectives)** : l’attaquant atteint son but final — **collecte** de données, **exfiltration**, impact (chiffrement, sabotage)[reference:4].

### La logique défensive

L’UKC insiste sur le caractère **itératif** des attaques : les phases ne sont pas strictement séquentielles, l’attaquant peut revenir en arrière (par exemple, re-énumérer après une élévation de privilèges). Cette granularité (18 phases vs 7 pour Lockheed Martin) permet aux équipes SOC de mapper plus finement les comportements observés à des techniques MITRE ATT&CK, et donc de construire des détections plus précises qu’un simple “kill chain” linéaire[reference:5].

---

## 🛠️ Ce que j'ai manipulé

- **Modélisation des menaces (Threat Modelling)** : identification des actifs critiques, évaluation des vulnérabilités et priorisation des mitigations (techniques et processuelles)[reference:6].
- **Comparaison de frameworks** : Lockheed Martin Cyber Kill Chain (7 phases) vs UKC (18 phases) vs MITRE ATT&CK (TTPs). L’UKC est présenté comme un **complément** à MITRE, pas un remplacement[reference:7].
- **Mapping des phases UKC vers ATT&CK** : pour chaque phase (Reconnaissance, Weaponization, Exploitation, Persistence, Privilege Escalation, Lateral Movement, Exfiltration…), identification des tactiques ATT&CK correspondantes (TA0043, TA0001, TA0002, TA0003, TA0004, TA0008, TA0010…)[reference:8].

---

## 📌 Ce que ça m'apporte pour un SOC

- **Vision complète du cycle d’attaque** : je sais situer une alerte dans l’une des 18 phases de l’UKC, ce qui me permet de qualifier plus précisément la progression d’un adversaire et de prioriser l’escalade.
- **Complémentarité des frameworks** : je comprends pourquoi l’UKC est plus adapté qu’une kill chain linéaire pour décrire des attaques modernes et itératives, et comment l’utiliser aux côtés de MITRE ATT&CK pour le threat hunting.
- **Threat modelling appliqué** : je peux participer à des exercices de modélisation des menaces en identifiant les actifs critiques, les chemins d’attaque probables et les mitigations associées.
- **Vocabulaire Threat Intelligence** : UKC, kill chain, threat modelling, pivoting, exfiltration, TTPs — employés correctement dans un rapport ou un échange avec un L2.
- **Lien direct avec les détections** : chaque phase de l’UKC correspond à des sources de logs et des règles de détection spécifiques, ce qui m’aide à argumenter des recommandations de visibilité.

---

## ✅ Statut

- [x] Room terminée
- [x] Write-up publié