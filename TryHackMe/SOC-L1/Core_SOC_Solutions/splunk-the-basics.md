# Splunk: The Basics — SOC Level 1 (TryHackMe)

**Catégorie :** Blue Team / SOC  
**Date de complétion :** 10/11/2026  
**Lien :** https://tryhackme.com/room/splunkthebasics  
**Parcours :** [SOC Level 1](https://tryhackme.com/path/outline/soclevel1)

---

## 🎯 Objectif de la room

Comprendre les bases de Splunk, l'une des principales solutions SIEM du marché, pour collecter, analyser et corréler les logs réseau et machines en temps réel. Cette room est théorique et inclut un laboratoire pratique pour ingérer et analyser des logs.

---

## 🧠 Ce que dit le cours

### 1. Les composants de Splunk
Splunk repose sur trois composants principaux :
- **Forwarder** : Un agent léger installé sur l'endpoint à surveiller. Sa tâche principale est de collecter les données et de les envoyer à l'instance Splunk. Il consomme peu de ressources. Sources de données typiques : serveurs web (trafic), machines Windows (Event Logs, PowerShell, Sysmon), hôtes Linux, bases de données (requêtes, erreurs).
- **Indexer** : Reçoit les données des forwarders. Il les parse, les normalise en paires champ-valeur, les catégorise et les stocke sous forme d'événements pour les rendre faciles à rechercher.
- **Search Head** : L'endroit (dans l'application Search & Reporting) où les utilisateurs recherchent les logs indexés via le langage **SPL (Search Processing Language)**. La requête est envoyée à l'indexer et les événements pertinents sont renvoyés. Permet aussi de créer des tableaux et visualisations (camembert, barres, colonnes).

### 2. Navigation dans Splunk
L'écran d'accueil de Splunk se divise en plusieurs sections :
- **Splunk Bar** (panneau supérieur) : Messages, Settings, Activity, Help, Find. Permet aussi de changer d'application directement.
- **Apps Panel** : Affiche les applications installées (l'application par défaut est *Search & Reporting*).
- **Explore Splunk** : Liens rapides pour ajouter des données, ajouter de nouvelles applications ou accéder à la documentation.
- **Home Dashboard** : Vide par défaut. Permet de choisir des tableaux de bord existants ou d'en créer (visibles dans l'onglet *Yours*).

### 3. Ajout de données (Adding Data)
Splunk peut ingérer n'importe quel type de données (logs d'événements, logs web, logs de pare-feu). Pour l'import, il faut suivre 5 étapes :
1. **Select Source** : Choisir le fichier.
2. **Select Source Type** : Choisir le type de logs (ex: JSON).
3. **Input Settings** : Choisir l'index de destination et le nom d'hôte associé.
4. **Review** : Vérifier la configuration.
5. **Done** : Finaliser l'import.

**Pratique de la room :**
Le cours utilisait un fichier `VPN_logs` (JSON délimité par des retours à la ligne). L'importation se fait via l'option **Upload**. Il faut garder le type de source JSON détecté par Splunk et créer un index nommé **`VPN_Logs`**. Une fois uploadé, on ouvre **Search & Reporting**, on règle le temps sur **All time**, et si les champs n'apparaissent pas, on utilise la commande **`| spath`** après la recherche de base pour parser les champs JSON.

---

## ✅ Statut

- [x] Room terminée
- [x] Write-up publié