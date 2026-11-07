# SOC L1 Alert Triage — SOC Level 1 (TryHackMe)

**Catégorie :** Blue Team / SOC  
**Date de complétion :** 07/11/2026  
**Lien :** https://tryhackme.com/room/socl1alerttriage  
**Parcours :** [SOC Level 1](https://tryhackme.com/path/outline/soclevel1)

---

## 🎯 Objectif de la room

Apprendre à trier les alertes d'un SIEM, compétence centrale du métier d'analyste SOC L1. Cette room est une simulation interactive via une interface web.

---

## 🧠 Ce que j'ai appris

Le triage est le processus qui consiste à qualifier une alerte pour déterminer s'il s'agit d'une **vraie menace (True Positive)** ou d'une **activité légitime (False Positive)**. Un analyste L1 doit analyser le contexte (utilisateur, hôte, processus, destination) avant de prendre une décision.

Le processus de triage suit une méthodologie stricte :
1. **S'assigner l'alerte** et la passer en "In Progress".
2. **Analyser le contexte** : qui (utilisateur), quoi (processus), où (hôte), quand (heure), comment (technique).
3. **Prendre une décision** : True Positive (escalader au L2) ou False Positive (clôturer).
4. **Documenter** : ajouter un commentaire justifiant la décision (preuve, raisonnement).
5. **Clôturer** l'alerte.

---

## 🛠️ Ce que j'ai manipulé

J'ai utilisé une interface de SIEM simulée pour traiter 5 alertes de niveaux de sévérité différents. J'ai appliqué la méthodologie de triage sur trois alertes en attente :

- **Création de fichier à double extension** : un utilisateur a téléchargé un fichier `cats2025.mp4.exe` depuis un domaine suspect. J'ai identifié une tentative d'usurpation (technique classique de phishing) et recommandé l'escalade au L2 pour isolation de l'hôte.
- **Exfiltration potentielle de données (5 Go vers Zoom)** : j'ai analysé la destination (Zoom) et le contexte (salle de réunion) pour conclure qu'il s'agissait d'une visioconférence légitime, donc d'un faux positif.
- **Téléchargement depuis GitHub** : un développeur a téléchargé le framework React. J'ai reconnu un dépôt légitime et un utilisateur autorisé, donc un faux positif.

J'ai également observé le traitement de deux autres alertes déjà closes : un faux positif (connexion VPN depuis le Japon confirmée par la CFO) et un vrai positif (attaque par force brute RDP depuis une IP externe).

---

## 📌 Ce que ça m'apporte pour un SOC

- **Le triage est un art** : Il faut analyser le contexte, pas seulement l'alerte brute. Un téléchargement GitHub peut être malveillant ou légitime selon l'utilisateur et le dépôt.
- **La documentation est cruciale** : Un commentaire clair permet au L2 de comprendre ma décision sans refaire l'analyse. C'est une preuve de rigueur.
- **Le faux positif est normal** : Un analyste L1 passe beaucoup de temps à éliminer le bruit. C'est ce qui permet de se concentrer sur les vraies menaces.

---

## ✅ Statut

- [x] Room terminée
- [x] Write-up publié