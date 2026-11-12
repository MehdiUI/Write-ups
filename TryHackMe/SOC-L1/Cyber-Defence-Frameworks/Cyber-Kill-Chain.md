# Cyber Kill Chain — Cyber Defence Frameworks (TryHackMe)

**Catégorie :** Blue Team / SOC / Threat Intelligence  
**Date de complétion :** 12/11/2026  
**Lien :** https://tryhackme.com/room/cyberkillchainzmt  
**Parcours :** [SOC Level 1](https://tryhackme.com/path/outline/soclevel1)

---

## 🎯 Objectif de la room

Étudier le framework **Cyber Kill Chain** introduit par Lockheed Martin en 2011, qui décompose une intrusion en sept phases séquentielles. L’objectif défensif est de comprendre ce que l’attaquant doit accomplir à chaque étape pour pouvoir **briser la chaîne** le plus tôt possible — idéalement avant que l’attaquant n’atteigne ses objectifs finaux. La room illustre chaque phase avec des exemples concrets (OSINT, malvertising, zero-day, web shell, DNS tunnelling, etc.) et des pistes de détection ou de blocage associées.

---

## 🧠 Ce que j'ai appris

### Les sept phases de la Cyber Kill Chain

1. **Reconnaissance** : collecte d’informations sur la cible (infrastructure, employés, processus, technologies exposées). Se divise en **passive** (OSINT, WHOIS, réseaux sociaux, sans contact direct) et **active** (interaction directe : scan de ports, social engineering, banner grabbing). L’**email harvesting** est une activité clé de cette phase.
2. **Weaponization** : création ou modification d’un payload malveillant en fonction des vulnérabilités identifiées. Inclut le couplage d’un **exploit** avec un **backdoor** ou un **macro** malveillant dans un document Office, l’obfuscation pour échapper à la détection, etc.
3. **Delivery** : transmission du payload weaponisé à la cible. Vecteurs classiques : **phishing / spear-phishing**, **USB infectés**, **watering hole**, **malvertising**, **smishing** (phishing par SMS).
4. **Exploitation** : exécution du payload sur le système cible en tirant parti d’une vulnérabilité. Peut impliquer un **zero-day** (vulnérabilité inconnue de l’éditeur) ou une faille connue non patchée.
5. **Installation** : installation d’un mécanisme de persistance (backdoor, malware, **web shell**) pour maintenir l’accès sur l’environnement compromis.
6. **Command & Control (C2)** : établissement d’un canal de communication avec l’infrastructure de l’attaquant pour piloter la machine compromise. Techniques observées : **DNS tunnelling**, encapsulation du trafic dans **HTTPS**, etc.
7. **Actions on Objectives** : l’attaquant atteint son but final — **exfiltration de données**, chiffrement par ransomware, mouvement latéral vers d’autres systèmes, sabotage.

### La logique défensive

Chaque phase est une **opportunité d’interruption**. Plus la chaîne est brisée tôt, moins le coût pour l’attaquant et pour l’organisation est élevé. Un SOC efficace cherche à **détecter** (visibilité), **bloquer** (contrôles préventifs) et **perturber** (réponse) à chaque étape, plutôt que de se concentrer uniquement sur la phase finale (exfiltration), qui est souvent trop tardive.

---

## 🛠️ Ce que j'ai manipulé

- **Concepts OSINT** : email harvesting, WHOIS, Google Dorking, collecte via réseaux sociaux — utilisés pour illustrer la phase de reconnaissance passive et active.
- **Outils de reconnaissance** : `theHarvester` (emails, sous-domaines, IPs, URLs), `Hunter.io` (contacts associés à un domaine), **OSINT Framework** (interface web regroupant des outils OSINT par catégorie).
- **Mécanismes d’attaque** : macros Office malveillantes, obfuscation, malvertising, smishing, watering hole, zero-day, web shell, DNS tunnelling, exfiltration via HTTPS.
- **Lecture de scénarios défensifs** : pour chaque phase, identification des points de détection et des contrôles possibles (MFA, allowlisting, filtrage réseau, surveillance DNS, etc.).

---

## 📌 Ce que ça m'apporte pour un SOC

- **Grille de lecture d’une intrusion** : je sais situer une alerte ou un comportement suspect dans l’une des sept phases, ce qui m’aide à qualifier la gravité et à prioriser l’escalade.
- **Vision “break the chain”** : je comprends qu’un SOC doit chercher à interrompre l’attaque le plus tôt possible, et je peux argumenter en faveur de détections sur les phases amont (recon, delivery) plutôt que de se limiter à l’exfiltration.
- **Vocabulaire Threat Intelligence** : kill chain, TTP, OSINT, zero-day, C2, exfiltration — employés correctement dans un rapport ou un échange avec un L2.
- **Lien avec MITRE ATT&CK** : la Cyber Kill Chain est un modèle linéaire et “adversary-centric” ; savoir le comparer à ATT&CK (plus granulaire) est un attendu courant en SOC.
- **Culture défensive** : la room donne des exemples concrets de contre-mesures par phase (MFA, allowlisting, filtrage, surveillance), directement réutilisables dans des recommandations de remédiation.

---

## ✅ Statut

- [x] Room terminée
- [x] Write-up publié