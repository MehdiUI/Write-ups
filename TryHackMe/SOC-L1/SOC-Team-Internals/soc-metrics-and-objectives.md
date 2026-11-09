# SOC Metrics and Objectives — SOC Level 1 (TryHackMe)

**Catégorie :** Blue Team / SOC  
**Date de complétion :** 09/11/2026  
**Lien :** https://tryhackme.com/room/socmetricsandobjectives  
**Parcours :** [SOC Level 1](https://tryhackme.com/path/outline/soclevel1)

---

## 🎯 Objectif de la room

Découvrir les indicateurs de performance (KPIs) qui mesurent l'efficacité d'un SOC (MTTD, MTTA, MTTR), comprendre le rôle des SLA et apprendre à résoudre des problèmes opérationnels en identifiant la cause racine et en assignant les bonnes tâches aux bons rôles. Cette room est une simulation interactive via une interface web.

---

## 🧠 Ce que j'ai appris

### Les métriques fondamentales d'un SOC
L'efficacité d'un SOC se mesure par des indicateurs de temps précis :
- **MTTD (Mean Time to Detect)** : Temps moyen entre l'attaque et sa détection par les outils. Un MTTD élevé indique que les règles de détection ne tournent pas assez souvent ou sont mal configurées.
- **MTTA (Mean Time to Acknowledge)** : Temps moyen pour qu'un analyste L1 commence le triage. Un MTTA élevé est souvent causé par un volume d'alertes trop important (bruit/faux positifs).
- **MTTR (Mean Time to Respond)** : Temps total depuis la réception de l'alerte jusqu'à l'arrêt de la brèche (inclut le MTTA).

### Les SLA (Service Level Agreements)
Un SLA est un contrat entre le SOC et la direction (ou le client). Il définit des objectifs de temps (ex: détecter en moins de 5 minutes, accuser réception en moins de 10 minutes, répondre en moins de 60 minutes). Le non-respect de ces SLA peut entraîner des pénalités ou une perte de confiance.

### Résolution de problèmes et assignation
Face à un problème de performance (ex: client insatisfait, analystes épuisés), il faut identifier la **cause racine** (la vraie métrique défaillante) et assigner la tâche d'amélioration au rôle compétent :
- **SOC Engineers** : Responsables de la configuration technique (tuning des règles SIEM, exclusion du bruit, automatisation).
- **Senior L2/L3** : Responsables des processus, de la création de workbooks et de la formation.
- **L1 Analysts** : Responsables du triage de base et du signalement des faux positifs.

---

## 🛠️ Ce que j'ai manipulé

J'ai utilisé une interface MDR (Managed Detection and Response) simulant les requêtes de la haute direction. J'ai analysé trois scénarios de crise et dû trouver la combinaison parfaite (Métrique racine -> Tâche corrective -> Assignation) :
1. **Unhappy Customer** : Identifier pourquoi un client est mécontent (temps de réponse trop long) et proposer une amélioration via la création de workbooks (assignée aux L2/L3).
2. **Delayed Alert** : Comprendre que le délai de détection vient de règles SIEM trop lentes, et assigner l'optimisation des règles au SOC Engineer.
3. **Tired Analysts** : Diagnostiquer que 95% des alertes sont du bruit (False Positive Rate) et assigner aux SOC Engineers la création de règles d'exclusion pour le bruit système et IT.

---

## 📌 Ce que ça m'apporte pour un SOC

- **Une vision globale** : Un analyste SOC ne fait pas que cliquer sur des alertes. Il doit comprendre comment son travail s'inscrit dans des métriques globales et pourquoi les managers se soucient du MTTD ou du MTTR.
- **Le rôle de chacun** : J'ai compris que le tuning des règles SIEM est le travail des SOC Engineers, et que les processus de remédiation sont gérés par les seniors. Un L1 doit savoir quand escalader et vers qui.
- **L'amélioration continue** : Un SOC efficace n'est pas un SOC qui travaille plus dur, mais un SOC qui optimise ses processus (réduction des faux positifs, tuning des règles) pour permettre aux analystes de se concentrer sur les vraies menaces.

---

## ✅ Statut

- [x] Room terminée
- [x] Write-up publié