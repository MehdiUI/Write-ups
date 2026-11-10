# Pyramid Of Pain — Cyber Defence Frameworks (TryHackMe)

**Catégorie :** Blue Team / SOC / Threat Intelligence  
**Date de complétion :** 10/11/2026  
**Lien :** https://tryhackme.com/room/pyramidofpainax  
**Parcours :** [SOC Level 1](https://tryhackme.com/path/outline/soclevel1)

---

## 🎯 Objectif de la room

Comprendre le modèle du **Pyramid of Pain** de David J. Bianco : classer les indicateurs de compromission (IOC) selon le coût qu’ils imposent à l’attaquant lorsqu’ils sont détectés et bloqués. La room explique pourquoi un SOC doit progressivement remonter la pyramide — des hashs triviaux à contourner jusqu’aux TTPs, très coûteux à modifier — et s’appuie sur des rapports réels (VirusTotal, Any.run, captures réseau) pour illustrer chaque niveau.

---

## 🧠 Ce que j'ai appris

### Les niveaux de la pyramide

Du plus facile au plus difficile à contourner pour l’attaquant :

- **Hash Values** : identifient un fichier unique. Un seul bit modifié change le hash — contournement trivial.
- **IP Address** : contournable via VPN, proxy ou Fast Flux.
- **Domain Names** : contournables via DGA, typosquatting ou attaque **Punycode** (caractères Unicode imitant un domaine légitime).
- **Host Artifacts** : traces locales (clés de registre, processus, fichiers déposés). Modifier ces artefacts oblige l’attaquant à retester ses outils.
- **Network Artifacts** : éléments observables dans le trafic (User-Agent, URI, POST, certificats). L’attaquant doit adapter son mode opératoire réseau.
- **Tools** : les outils eux-mêmes (mimikatz, Cobalt Strike…). Le **fuzzy hashing** (SSDeep, *context triggered piecewise hashes*) permet de repérer des variantes malgré des modifications mineures.
- **TTPs** : Tactics, Techniques and Procedures. Détecter un TTP force l’attaquant à réapprendre son métier — c’est le sommet et le coût maximal.

### La logique défensive

Bloquer un hash ou une IP est rapide mais éphémère. Détecter un comportement (TTP, mappé à MITRE ATT&CK) est difficile mais durable. Le SOC doit donc utiliser les IOC bas niveau pour le triage immédiat, et investir dans la détection comportementale pour les niveaux hauts.

---

## 🛠️ Ce que j'ai manipulé

- **Rapports d’analyse** : lecture de rapports VirusTotal et Any.run pour extraire des IOC (hash, IP, domaine, artefacts hôte) et évaluer leur niveau dans la pyramide.
- **Captures réseau** : analyse de trafic (pcap) pour identifier des artefacts réseau (User-Agent, requêtes POST).
- **Outils de Threat Intel** : résolution d’URL raccourcies (TinyURL), vérification de réputation, fuzzy hashing pour la similarité d’échantillons.
- **MITRE ATT&CK** : navigation dans la matrice pour relier les niveaux de la pyramide à des techniques adversaries concrètes.

---

## 📌 Ce que ça m'apporte pour un SOC

- **Priorisation des détections** : je sais expliquer pourquoi une règle basée uniquement sur un hash ou une IP est fragile, et pourquoi un SOC doit investir dans la détection de TTPs.
- **Lecture de rapports Threat Intel** : je sais extraire rapidement les informations actionnables d’un rapport VirusTotal / Any.run / pcap.
- **Vocabulaire technique** : IOC, TTP, Fast Flux, DGA, Punycode, fuzzy hashing, SSDeep — employés correctement dans un rapport ou un échange avec un L2.
- **Vision adversary-centric** : je comprends ce qui coûte cher à l’attaquant, ce qui m’aide à évaluer la valeur d’une alerte et à argumenter une escalade.
- **Lien avec MITRE ATT&CK** : préparation directe au mapping comportemental, attendu courant en SOC.

---

## ✅ Statut

- [x] Room terminée
- [x] Write-up publié