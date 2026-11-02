# 📜 Logs Fundamentals

**Objectif de la room :** Comprendre ce qu'est un log (journal d'événements), découvrir les différents types de logs, et apprendre à les analyser manuellement (Windows Event Viewer et Web Server Access Logs) pour investiguer sur un incident.

## 📝 Résumé des tâches et réponses

### Task 1 : Introduction to Logs
- **Concept :** Les logs sont les "empreintes digitales" numériques laissées par toute activité (normale ou malveillante). Ils sont essentiels pour le monitoring de sécurité, l'investigation (Forensics), le troubleshooting et la conformité (Auditing).
- **Question :** Où peut-on trouver la majorité des traces d'attaque dans un système numérique ?
  - **Réponse :** `Logs`

### Task 2 : Types of Logs
- **Concept :** Pour éviter de se perdre, les logs sont séparés par catégories :
  - **System** : Démarrage, pilotes, erreurs matérielles.
  - **Security** : Authentification, autorisation, changements de politiques.
  - **Application** : Erreurs et interactions liées à des logiciels spécifiques.
  - **Network** : Trafic entrant et sortant (pare-feu, connexions).
  - **Access** : Accès aux serveurs web, bases de données, API.
- **Question 1 :** Quel type de logs contient les informations sur le trafic entrant et sortant ?
  - **Réponse :** `Network Logs`
- **Question 2 :** Quel type de logs contient les événements d'authentification et d'autorisation ?
  - **Réponse :** `Security Logs`

### Task 3 : Windows Event Logs Analysis
- **Concept :** Windows utilise l'**Event Viewer** (Observateur d'événements) pour afficher les logs. Chaque action possède un **Event ID** unique (ex: `4624` pour un login réussi, `4720` pour la création d'un compte, `4722` pour l'activation, `4724` pour un reset de mot de passe).
- **Scénario :** Un serveur de fichiers a été compromis. L'attaquant a créé un compte, l'a activé et a changé son mot de passe.
- **Question 1 :** Quel est le nom du dernier compte utilisateur créé ?
  - **Réponse :** `hacked`
- **Question 2 :** Quel compte utilisateur a créé ce compte ?
  - **Réponse :** `Administrator`
- **Question 3 :** À quelle date ce compte a-t-il été activé ? (Format : M/D/YYYY)
  - **Réponse :** `6/7/2024`
- **Question 4 :** Ce compte a-t-il subi une réinitialisation de mot de passe ?
  - **Réponse :** `Yes`

### Task 4 : Web Server Access Logs Analysis
- **Concept :** Les serveurs web (comme Apache) enregistrent chaque requête HTTP dans un fichier `access.log`. On peut l'analyser en ligne de commande avec `cat`, `grep` (pour filtrer) et `less` (pour lire page par page). Le fichier se trouve dans `/var/log/apache2/access.log` ou dans le dossier de l'exercice.
- **Question 1 :** Quelle est l'IP qui a fait la dernière requête GET vers l'URL `/contact` ?
  - **Commande :** `grep "GET /contact" access.log`
  - **Réponse :** `10.10.17.242`
- **Question 2 :** Quand a été faite la dernière requête POST par l'IP `172.16.0.1` ?
  - **Commande :** `grep "172.16.0.1" access.log | grep "POST"`
  - **Réponse :** `06/Jun/2024:13:55:44`
- **Question 3 :** Vers quelle URL la requête POST a-t-elle été faite ?
  - **Réponse :** `/contact`

## 🧠 Ce que je retiens pour un poste d'Analyste SOC
- **La centralisation** : Les logs sont dispersés partout. Savoir où chercher (Event Viewer sur Windows, `/var/log` sur Linux) est la première étape.
- **Les Event IDs** : Connaître les IDs critiques (comme 4624, 4625, 4720) permet de filtrer des milliers de lignes en quelques secondes pour repérer une activité suspecte (ex: création de compte pirate).
- **Le pouvoir de `grep`** : Sur un serveur web, `grep` est indispensable pour extraire une adresse IP spécifique, une erreur 500, ou une tentative d'injection SQL dans un fichier de logs de plusieurs gigaoctets.