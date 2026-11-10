# Elastic Stack: The Basics — SOC Level 1 (TryHackMe)

**Catégorie :** Blue Team / SOC  
**Date de complétion :** 10/11/2026  
**Lien :** https://tryhackme.com/room/elasticstackthebasics  
**Parcours :** [SOC Level 1](https://tryhackme.com/path/outline/soclevel1)

---

## 🎯 Objectif de la room

Comprendre comment les analystes SOC utilisent l'Elastic Stack (ELK) pour l'investigation des logs, en explorant ses composants et en pratiquant la recherche, la visualisation et la création de tableaux de bord dans Kibana.

---

## 🧠 Ce que dit le cours

### 1. Les composants de l'Elastic Stack (ELK)
L'ELK est une collection de composants open-source qui travaillent ensemble pour collecter, stocker, rechercher et visualiser des données en temps réel :
- **Elasticsearch** : Un moteur de recherche et d'analyse plein texte pour les documents au format **JSON**. Il stocke, analyse et corrèle les données via une API REST.
- **Logstash** : Un moteur de traitement de données. Il prend les données de différentes sources (Input), les filtre/normalise (Filter), et les envoie vers une destination (Output) comme Kibana ou Elasticsearch.
- **Beats** : Des agents légers installés sur les endpoints qui envoient des données spécifiques vers Elasticsearch (ex: *Winlogbeat* pour les logs Windows, *Packetbeat* pour le trafic réseau).
- **Kibana** : L'interface web de visualisation qui permet d'analyser, d'investiguer et de créer des dashboards à partir des données stockées dans Elasticsearch.

### 2. L'onglet Discover
C'est l'espace de travail principal de Kibana. L'analyste y passe la majorité de son temps pour :
- Visualiser les logs bruts.
- Utiliser le **panneau des champs** (à gauche) pour filtrer sur des valeurs spécifiques.
- Sélectionner l'**index pattern** (ex: `vpn_connections`).
- Ajuster le **filtre de temps** pour cibler une période précise.
- Consulter la **timeline** pour repérer des pics d'activité anormaux.
- Créer des **tableaux** en sélectionnant les champs pertinents pour réduire le bruit.

### 3. KQL (Kibana Query Language)
KQL est le langage de recherche utilisé dans la barre de recherche de Kibana. Il permet deux types de recherches :
- **Free text search** : Recherche un terme dans tous les champs (ex: `United*` avec un wildcard).
- **Field-based search** : Recherche une valeur dans un champ spécifique avec la syntaxe `Field: Value`.
Il supporte les opérateurs logiques : **AND**, **OR**, **NOT**.

### 4. Visualisations et Dashboards
- **Visualize tab** : Permet de créer des tableaux, camemberts ou graphiques en barres à partir des données. On peut créer des corrélations entre plusieurs champs (ex: Source_Country vs Source_IP).
- **Dashboard tab** : Permet de regrouper plusieurs visualisations et recherches sauvegardées sur une seule page pour avoir une vue d'ensemble de l'état du réseau.

---

## 🛠️ Ce que j'ai manipulé

J'ai utilisé Kibana pour investiguer des logs VPN :
- J'ai configuré l'index pattern `vpn_connections` et ajusté la plage de temps sur Janvier 2022.
- J'ai utilisé le panneau des champs pour identifier les IP et utilisateurs les plus actifs, et j'ai filtré sur des critères spécifiques (ex: tentatives échouées).
- J'ai utilisé KQL pour des recherches textuelles et par champ (avec les opérateurs AND/OR/NOT).
- J'ai créé des visualisations (tableaux) pour mettre en évidence les tentatives de connexion échouées.
- J'ai assemblé ces éléments dans un dashboard personnalisé pour synthétiser l'activité VPN.

---

## 📌 Ce que ça m'apporte pour un SOC

- **La maîtrise de Kibana** : Savoir naviguer dans l'onglet Discover, utiliser KQL et créer des visualisations est essentiel pour tout analyste travaillant avec ELK.
- **La chasse aux anomalies** : L'utilisation de la timeline et des filtres permet de repérer rapidement des pics suspects (ex: un pic de tentatives échouées ou une connexion hors horaires).
- **La centralisation** : Les dashboards permettent de garder une vue d'ensemble sans avoir à relancer des requêtes manuellement à chaque fois.

---

## ✅ Statut

- [x] Room terminée
- [x] Write-up publié