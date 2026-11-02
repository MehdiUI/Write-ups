# 📊 Introduction to SIEM

**Objectif de la room :** Comprendre ce qu'est un SIEM (Security Information and Event Management), comment il collecte, normalise et corrèle les logs, et comment l'utiliser pour détecter des menaces dans un environnement réseau.

## 📝 Résumé des tâches et réponses

### Task 1 & 2 : Introduction et Log Sources
- **Concept :** Le SIEM est une solution centralisée qui collecte les logs de toutes les machines (Windows, Linux, routeurs, serveurs web) pour les analyser. 
- **Log Sources :** Windows Event Logs, Linux Syslog, Web Access Logs, etc.
- **Question (exemple) :** Que signifie SIEM ?
  - **Réponse :** `Security Information and Event Management`

### Task 3 : Why SIEM? (Les fonctionnalités)
- **Concept :** Un SIEM ne fait pas que stocker, il traite les données :
  - **Normalisation** : Convertit tous les logs dans un format standard (lisible par la machine).
  - **Corrélation** : Relie plusieurs événements entre eux pour détecter une attaque (ex: 10 échecs de connexion suivis d'un succès = brute force).
  - **Alerting** : Déclenche une alerte quand une règle de corrélation est satisfaite.
  - **Dashboards** : Fournit des visualisations graphiques pour voir l'état du réseau.

### Task 4 : Log Ingestion
- **Concept :** Comment les logs arrivent au SIEM ?
  - **Agent/Forwarder** : Un petit logiciel installé sur la machine qui envoie les logs (ex: Splunk Universal Forwarder).
  - **Agentless** : La machine envoie elle-même ses logs via un protocole réseau (ex: Syslog, SNMP).

### Task 5 : Lab (Splunk / ELK)
- **Concept :** Mise en pratique dans une interface SIEM (souvent Splunk dans cette room). Tu dois rechercher des adresses IP suspectes, des événements de sécurité spécifiques ou des erreurs.
- **Astuce pour le Lab :** 
  - Utilise la barre de recherche (`Search & Reporting`).
  - Tape `index=*` pour voir tous les logs.
  - Cherche les termes comme `failed login`, `error`, ou l'IP de l'attaquant mentionnée dans l'énoncé.

## 🧠 Ce que je retiens pour un poste d'Analyste SOC
- **La centralisation** : Le SIEM est la "tour de contrôle". Plus besoin d'aller machine par machine, tout est au même endroit.
- **La corrélation** : C'est la force du SIEM. Un log isolé (ex: une connexion) ne veut rien dire, mais 1000 logs similaires en 1 minute (ex: une attaque DoS) déclenchent une alerte.
- **Les requêtes (SPL/KQL)** : Savoir écrire une requête de recherche est indispensable pour extraire la bonne information sans se noyer sous des milliers de résultats.