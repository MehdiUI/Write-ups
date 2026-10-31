# 🛡️ SOC Fundamentals

**Objectif de la room :** Découvrir le fonctionnement d'un Security Operations Center (SOC), les rôles de l'équipe, les processus de triage et les technologies utilisées pour détecter et répondre aux incidents de sécurité.

## 📝 Résumé des tâches et réponses

### Task 1 : Introduction to SOC
- **Concept :** Le SOC (Security Operations Center) est une équipe dédiée qui surveille le réseau et les systèmes d'une entreprise 24h/24 et 7j/7 pour identifier les activités suspectes et prévenir les dégâts.
- **Question :** Que signifie SOC ?
- **Réponse :** `Security Operations Center`

### Task 2 : Purpose and Components
- **Concept :** Le but principal du SOC est la **Détection** (vulnérabilités, activités non autorisées, intrusions) et la **Réponse** (soutien à l'incident response). Le SOC repose sur 3 piliers.
- **Question 1 :** L'équipe SOC découvre qu'un utilisateur non autorisé tente de se connecter. Quelle capacité de SOC s'agit-il ?
  - **Réponse :** `Detection`
- **Question 2 :** Quels sont les 3 piliers d'un SOC ?
  - **Réponse :** `People, Process, Technology`

### Task 3 : People (Les Personnes)
- **Concept :** Les outils de sécurité génèrent beaucoup de faux positifs (du "bruit"). L'humain est indispensable pour trier les vraies alertes des fausses.
- **Les rôles :**
  - **SOC Analyst (Level 1)** : Le premier rempart, fait le triage (triage) et le signalement (reporting) de base.
  - **SOC Analyst (Level 2/3)** : Enquêtes approfondies, chasse aux menaces proactives.
  - **Security Engineer** : Déploie et configure les solutions.
  - **Detection Engineer** : Crée les règles de détection (le "cerveau" des outils).
  - **SOC Manager** : Gère l'équipe et fait le lien avec le CISO.
- **Question 1 :** Le triage et le signalement des alertes sont de la responsabilité de ?
  - **Réponse :** `SOC Analyst (Level 1)`
- **Question 2 :** Quel rôle travaille dédié à l'établissement de règles pour les solutions d'alerte ?
  - **Réponse :** `Detection Engineer`

### Task 4 : Process (Le Processus)
- **Concept :** Le triage d'alerte (Alert Triage) repose sur les **5 W** :
  - **What?** (Quoi ?) : Que s'est-il passé (ex: exfiltration de données) ?
  - **When?** (Quand ?) : L'heure de l'événement.
  - **Where?** (Où ?) : La machine ou le dossier concerné.
  - **Who?** (Qui ?) : L'utilisateur impliqué (ex: John).
  - **Why?** (Pourquoi ?) : La cause (ex: téléchargement d'un logiciel piraté).
  Une fois l'analyse terminée, un rapport (Reporting) est escaladé.
- **Question 1 :** L'équipe SOC découvre que John a tenté de voler des données. Quel "W" cela répond-il ?
  - **Réponse :** `Who`
- **Question 2 :** L'équipe SOC détecte une grande quantité d'exfiltration de données. Quel "W" cela répond-il ?
  - **Réponse :** `What`

### Task 5 : Technology (La Technologie)
- **Concept :** Le SOC utilise de nombreux outils pour centraliser les données et détecter les menaces : SIEM (collecte de logs), EDR (protection des endpoints), SOAR (automatisation), et des solutions de Threat Intelligence (pour connaître les attaquants).

## 🧠 Ce que je retiens pour un poste d'Analyste SOC
- **Le triage est la base** : Savoir poser les bonnes questions (les 5 W) rapidement permet de prioriser les alertes et de ne pas se noyer sous le bruit.
- **L'humain est irremplaçable** : Les outils (SIEM, EDR) donnent des alertes, mais c'est l'analyste (Niveau 1, 2 ou 3) qui analyse le contexte pour comprendre si c'est une vraie attaque ou une erreur de configuration.
- **La communication** : Rédiger un bon rapport d'alerte (Reporting) avec des preuves (captures d'écran, logs) est essentiel pour que les niveaux supérieurs (L2/L3) puissent enquêter efficacement.