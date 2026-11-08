# SOC Workbooks and Lookups — SOC Level 1 (TryHackMe)

**Catégorie :** Blue Team / SOC  
**Date de complétion :** 08/11/2026  
**Lien :** https://tryhackme.com/room/socworkbooksandlookups  
**Parcours :** [SOC Level 1](https://tryhackme.com/path/outline/soclevel1)

---

## 🎯 Objectif de la room

Découvrir les ressources d'entreprise (inventaires, diagrammes réseau, workbooks/playbooks) qui aident un analyste SOC L1 à structurer son triage, à gagner du contexte et à enquêter de manière méthodique. Cette room est une simulation interactive via une interface web.

---

## 🧠 Ce que j'ai appris

### L'importance du contexte
Une alerte brute ne suffit pas. Pour prendre une bonne décision, l'analyste L1 doit s'appuyer sur :
- **L'inventaire des actifs (Asset Inventory)** : Comprendre le rôle d'une machine (ex: serveur de base de données, poste RH) permet de juger la gravité d'une alerte.
- **L'inventaire des identités (Identity Inventory)** : Des outils comme BambooHR permettent de savoir à quel département appartient un utilisateur (IT, RH, Finance) et si son comportement est normal pour son rôle.
- **Les diagrammes réseau (Network Diagrams)** : Indispensables pour visualiser les sous-réseaux et comprendre un chemin d'attaque (ex: une IP externe qui force brute le VPN, obtient une IP interne, puis scanne d'autres sous-réseaux).

### Les SOC Workbooks (Playbooks)
Un **workbook** (ou playbook/runbook) est un document structuré qui définit les étapes exactes à suivre pour enquêter sur un type d'alerte spécifique. 
Ils sont créés par les analystes seniors pour guider les L1 et garantir une analyse de haute qualité. Ils sont divisés en trois phases logiques :
1. **Enrichissement** : Récupérer le contexte (qui est l'utilisateur, quelle est la machine, réputation de l'IP).
2. **Investigation** : Analyser les logs, construire l'arbre des processus, utiliser la sandbox ou la Threat Intelligence.
3. **Escalade** : Rédiger un rapport, contacter l'utilisateur si nécessaire, et escalader au L2 avec les preuves.

---

## 🛠️ Ce que j'ai manipulé

J'ai utilisé une interface web pour résoudre des scénarios de triage basés sur des playbooks :
- **Analyse d'un scénario réseau** : J'ai utilisé un diagramme pour comprendre qu'une alerte de scan interne provenait en fait d'une compromission via un VPN mal sécurisé (True Positive).
- **Réorganisation de Workbooks** : J'ai dû remettre dans l'ordre logique les étapes de trois playbooks différents :
  1. Un email externe contenant un script ou un binaire (analyse EML -> sandbox -> rapport).
  2. Un téléchargement d'exécutable via PowerShell (arbre des processus -> analyse de l'URL -> contact utilisateur -> rapport).
  3. Une analyse réseau (investigation des connexions, corrélation des logs).

---

## 📌 Ce que ça m'apporte pour un SOC

- **La méthode avant tout** : Suivre un workbook évite de sauter des étapes cruciales sous la pression. Cela garantit que chaque alerte est traitée avec le même niveau de rigueur.
- **Le gain de temps** : Grâce à l'enrichissement automatisé (BambooHR, Threat Intel) et aux playbooks, je peux qualifier une alerte en quelques minutes au lieu de repartir de zéro.
- **La communication avec le L2** : Un rapport bien structuré, avec les preuves issues des recherches SIEM et des analyses (sandbox, EML), permet au L2 de prendre le relais immédiatement.

---

## ✅ Statut

- [x] Room terminée
- [x] Write-up publié