# 🔍 Search Skills

**Objectif de la room :** Apprendre à utiliser efficacement Internet et les services spécialisés (OSINT) pour la cybersécurité. Savoir où chercher est aussi important que savoir quoi chercher.

## 📝 Résumé des tâches et réponses

### Task 1 : Introduction
- **Concept :** La recherche d'informations est une compétence fondamentale, que ce soit pour l'attaque (Red Team) ou la défense (Blue Team).
- **Question :** Je suis prêt à commencer !
- **Réponse :** `No answer needed` (Aucune réponse requise)

### Task 2 : Shodan (TryScanMe)
- **Concept :** Shodan est un moteur de recherche pour les objets connectés (IoT), les serveurs et les équipements réseau. Il scanne Internet en continu.
- **Filtres utiles :** `country:` (pays), `port:` (port), `org:` (organisation), `hostname:` (nom de domaine).
- **Action :** Rechercher "apache" dans le simulateur TryScanMe et examiner le premier résultat.
- **Question :** Quel domaine est associé à l'adresse IP 185.243.115.47 ?
- **Réponse :** `tryhackme.thm`

### Task 3 : VirusTotal (TryDetectMe)
- **Concept :** VirusTotal analyse des fichiers, URL et domaines via plus de 70 moteurs antivirus. Idéal pour vérifier la dangerosité d'un fichier suspect.
- **Action :** Analyser le fichier `invoice_payment.exe` sur TryDetectMe.
- **Question :** Combien de fournisseurs de sécurité ont identifié le fichier comme dangereux ?
- **Réponse :** `52`

### Task 4 : Vulnerability Databases (CVE)
- **Concept :** Le programme CVE (Common Vulnerabilities and Exposures) est le dictionnaire universel des vulnérabilités connues. Chaque faille reçoit un identifiant unique (ex: `CVE-2026-1337`) et un score de gravité (CVSS).
- **Action :** Chercher la CVE-2026-1337 dans la base de données.
- **Question :** Quelle classification CVSS (score) la vulnérabilité a-t-elle obtenue ?
- **Réponse :** `10` (C'est le score maximum, indiquant une criticité extrême).

### Task 5 : Technical Documentation (MAN)
- **Concept :** La documentation officielle (comme les pages `man` sous Linux) est la meilleure source pour comprendre un outil. 
- **Commande Linux :** `man <commande>` (ex: `man nc`).
- **Action :** Chercher la commande d'exemple pour `nc` (netcat).
- **Question :** Quelle est la commande d'exemple pour se connecter à `host.example.com` sur le port `42` ?
- **Réponse :** `nc host.example.com 42`

### Task 6 : GitHub
- **Concept :** GitHub est une mine d'or pour trouver des Preuves de Concept (PoC), des scripts d'exploitation et des analyses techniques de vulnérabilités.
- **⚠️ Attention :** Les PoCs ne sont pas toujours fiables ou sûrs. Il faut toujours vérifier le code avant de l'exécuter.
- **Action :** Lire le README du dépôt pour la CVE-2026-1337.
- **Question :** Quel est le nom du script dans le dépôt qui démontre la vulnérabilité ?
- **Réponse :** `exploit.py`

## 🧠 Ce qu'il faut retenir
- **Shodan :** Pour trouver des appareils connectés à Internet.
- **VirusTotal :** Pour scanner des fichiers suspects avec plusieurs antivirus.
- **CVE :** Pour se renseigner sur une faille de sécurité spécifique.
- **MAN :** Pour lire le manuel d'une commande directement dans le terminal.
- **GitHub :** Pour trouver des codes d'exploitation et des outils (avec prudence).