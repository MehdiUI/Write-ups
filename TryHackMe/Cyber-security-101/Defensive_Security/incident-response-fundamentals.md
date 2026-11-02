# 🚨 Incident Response Fundamentals

**Objectif de la room :** Comprendre le cycle de vie de la réponse aux incidents (IR), apprendre à catégoriser les menaces et utiliser les méthodologies (SANS/NIST) pour contenir et éradiquer une attaque.

## 📝 Résumé des tâches et réponses

### Task 1 : Introduction to Incident Response
- **Concept :** La réponse aux incidents est le plan d'action complet pour gérer une cyberattaque, de la prévention à la gestion de crise, jusqu'à la restauration des systèmes.

### Task 2 : What are Incidents?
- **Concept :** Les outils de sécurité génèrent des alertes. 
  - **False Positive** : Une alarme qui sonne pour rien (ex: une sauvegarde cloud ressemble à une exfiltration).
  - **True Positive** : Une vraie menace (ex: email de phishing). Un True Positive confirmé devient un **Incident**.
- **Question 1 :** Qu'est-ce qui est déclenché après une activité nuisible ?
  - **Réponse :** `alert`
- **Question 2 :** Si l'activité est correctement identifiée comme nuisible, quel type d'alerte est-ce ?
  - **Réponse :** `true positive`
- **Question 3 :** Une alarme incendie déclenchée par la fumée de cuisson est un ?
  - **Réponse :** `false positive`

### Task 3 : Types of Incidents
- **Concept :** Les incidents ont plusieurs formes : Malware, Security Breaches, Data Leaks, Insider Attacks, et Denial of Service (DoS).
- **Question 1 :** Un système compromis après le téléchargement d'une pièce jointe email. Quel type d'incident ?
  - **Réponse :** `Malware Infection`
- **Question 2 :** Quel type d'incident vise à perturber la disponibilité d'une application ?
  - **Réponse :** `Denial of Service`

### Task 4 : Incident Response Process
- **Concept :** Utilisation de frameworks. Le SANS utilise **PICERL** (Preparation, Identification, Containment, Eradication, Recovery, Lessons Learned). Le NIST simplifie cela en 4 phases.
- **Question 1 :** L'équipe coupe la connexion internet d'une machine compromise. Quelle phase SANS ?
  - **Réponse :** `Containment`
- **Question 2 :** Quelle phase NIST correspond à "Lessons Learned" (SANS) ?
  - **Réponse :** `Post Incident Activity`

### Task 5 : Incident Response Techniques
- **Concept :** Utilisation d'outils comme le SIEM, l'AV ou l'EDR pour détecter. Pour répondre, on utilise des guides étape par étape.
- **Question :** Des directives complètes étape par étape pour la réponse aux incidents sont appelées ?
  - **Réponse :** `Playbooks`

### Task 6 : Lab Work Incident Response
- **Concept :** Mise en pratique sur un tableau de bord simulant une attaque par phishing. Il faut analyser l'email, identifier les machines infectées, et suivre la chronologie de l'attaque.
- **Question 1 :** Nom de l'expéditeur malveillant ?
  - **Réponse :** `Jeff Johnson`
- **Question 2 :** Quel était le vecteur de la menace ?
  - **Réponse :** `Email Attachment`
- **Question 3 :** Combien d'appareils ont téléchargé la pièce jointe ?
  - **Réponse :** `3`
- **Question 4 :** Combien d'appareils ont exécuté le fichier ?
  - **Réponse :** `1`
- **Question 5 :** Flag trouvé à la fin de l'exercice ?
  - **Réponse :** `THM{My_First_Incident_Response}`

## 🧠 Ce que je retiens pour un poste d'Analyste SOC
- **Le tri des alertes (Triage)** : Distinguer un faux positif d'un vrai positif est la compétence n°1 pour ne pas perdre son temps et réagir vite sur les vrais incidents.
- **Le cycle PICERL** : Savoir où on en est dans la gestion de crise. On ne supprime pas un malware (Eradication) avant d'avoir coupé le réseau de la machine (Containment) pour éviter qu'il ne se propage.
- **Les Playbooks** : En situation de stress, on ne réfléchit pas de zéro. On suit le Playbook défini par l'entreprise pour chaque type d'attaque (ex: Playbook Phishing, Playbook Ransomware).