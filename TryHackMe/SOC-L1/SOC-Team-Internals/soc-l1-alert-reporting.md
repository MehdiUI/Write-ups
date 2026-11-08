# SOC L1 Alert Reporting — SOC Level 1 (TryHackMe)

**Catégorie :** Blue Team / SOC  
**Date de complétion :** 08/11/2026  
**Lien :** https://tryhackme.com/room/socl1alertreporting  
**Parcours :** [SOC Level 1](https://tryhackme.com/path/outline/soclevel1)

---

## 🎯 Objectif de la room

Apprendre à rédiger un rapport d'alerte clair et structuré (méthode des 5W) et à escalader correctement les incidents vers le niveau supérieur (L2). Cette room est une simulation interactive via une interface web (SIEM).

---

## 🧠 Ce que j'ai appris

### L'importance du rapport et de l'escalade
Un analyste L1 ne doit pas seulement qualifier une alerte (True/False Positive). Il doit documenter son analyse avec la méthode des **5W** (Who, What, When, Where, Why) pour le L2. Un bon rapport fait gagner un temps précieux, conserve les preuves (les logs bruts expirent, pas les alertes) et améliore les compétences de l'analyste ("Si vous ne pouvez pas l'expliquer simplement, c'est que vous ne le comprenez pas assez bien").

**Quand escalader ?**
- L'alerte indique une cyberattaque majeure nécessitant une enquête approfondie (DFIR).
- Des actions de remédiation sont requises (isolation d'hôte, suppression de malware, reset de mot de passe).
- Une communication externe est nécessaire (clients, direction, autorités).
- L'analyste L1 ne comprend pas l'alerte et a besoin de l'aide d'un senior.

---

## 🛠️ Ce que j'ai manipulé

J'ai utilisé le tableau de bord SIEM pour traiter deux alertes en attente et les escalader vers le L2 de service (`E.Fleming`).

1. **Email Marked as Phishing after Delivery** : J'ai identifié un email usurpant l'identité de Microsoft (`support@microsoft.com`), avec des échecs d'authentification SPF/DKIM et une pièce jointe suspecte (`REPORT.rar`). J'ai rédigé un rapport 5W et escaladé l'alerte en True Positive.
2. **Spike of Domain Discovery Commands** : J'ai analysé une alerte de reconnaissance Active Directory sur le serveur `DMZ-MSEXCHANGE-2013`. J'ai identifié que les commandes (`whoami`, `nltest`) étaient lancées par un reverse shell (`revshell.exe`), lui-même exécuté par le processus IIS (`w3wp.exe`). Cela indique une compromission via une web shell. J'ai documenté ce raisonnement avec la méthode 5W et escaladé l'alerte en True Positive pour containment immédiat.

---

## 📌 Ce que ça m'apporte pour un SOC

- **La communication est une compétence clé** : Un analyste SOC ne travaille pas seul. La clarté du rapport conditionne la rapidité et l'efficacité de la réponse du L2.
- **La méthode des 5W** : C'est un framework universel pour ne rien oublier et structurer sa pensée sous pression.
- **Le workflow de l'escalade** : J'ai compris le cycle de vie complet d'une alerte (Assignation -> Analyse -> Rapport -> Escalade -> Prise en charge par le L2).

---

## ✅ Statut

- [x] Room terminée
- [x] Write-up publié