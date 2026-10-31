# 🗺️ Nmap: The Basics

**Objectif de la room :** Apprendre à utiliser Nmap, l'outil de référence pour la découverte de réseaux, le scan de ports et la détection de services. Indispensable pour cartographier la surface d'attaque d'une cible.

## 📝 Résumé des tâches et réponses

### Task 2 : Host Discovery (Qui est en ligne ?)
- **Concept :** Avant de scanner les ports, il faut savoir quelles machines sont allumées. L'option `-sn` (ping scan) permet de découvrir les hôtes en direct sans scanner leurs ports. On peut cibler une plage d'IP (`192.168.0.1-10`), un sous-réseau (`/24`) ou un nom d'hôte.
- **Question :** Quelle est la dernière adresse IP qui sera scannée si la cible est `192.168.0.1/27` ?
  - **Explication :** Un masque `/27` découpe le réseau en blocs de 32 adresses (2^5). Le premier bloc va de `.0` à `.31`.
  - **Réponse :** `192.168.0.31`

### Task 3 : Port Scanning (Qui écoute ?)
- **Concept :** On scanne les ports TCP/UDP pour voir quels services tournent. 
  - `-sS` (SYN scan) : Furtif, n'ouvre pas de connexion complète (nécessite sudo).
  - `-sT` (Connect scan) : Ouvre une connexion complète (par défaut sans sudo).
  - `-F` : Scan rapide (100 ports les plus communs).
  - `-p` : Spécifier une plage de ports (`-p 1-1024`).
- **Question 1 :** Combien de ports TCP sont ouverts sur la cible ?
  - **Réponse :** `6` (ports 7, 9, 13, 17, 22, 8008).
- **Question 2 :** Trouver le serveur web et le visiter. Quel est le flag ?
  - **Explication :** Le serveur web est sur le port 8008. Il faut aller sur `http://<IP>:8008`.
  - **Réponse :** *(Le flag trouvé sur la page web)*

### Task 4 : Version Detection (Extraire plus d'infos)
- **Concept :** L'option `-sV` permet de connaître la version exacte du logiciel qui tourne sur un port. L'option `-O` tente de deviner le système d'exploitation. L'option `-A` fait tout ça en même temps (et plus encore). `-Pn` force le scan si la machine ne répond pas au ping.
- **Question :** Quel est le nom et la version du serveur web sur le port 8008 ?
  - **Réponse :** `lighttpd 1.4.74`

### Task 5 : Timing (À quel point c'est rapide ?)
- **Concept :** Pour éviter de se faire repérer par un IDS ou pour accélérer le scan, Nmap propose 6 templates de timing : `-T0` (paranoid) à `-T5` (insane).
- **Question :** Quel est l'équivalent non-numérique de `-T4` ?
  - **Réponse :** `aggressive`

### Task 6 : Output (Contrôler ce qu'on voit)
- **Concept :** L'option `-v` (verbosité) affiche les étapes du scan en temps réel. L'option `-d` affiche les informations de débogage (debugging) très techniques. On peut sauvegarder le résultat en format normal (`-oN`), XML (`-oX`) ou grepable (`-oG`).
- **Question :** Quelle option ajouter pour activer le débogage ?
  - **Réponse :** `-d`

### Task 7 : Conclusion
- **Concept :** Toujours exécuter Nmap avec `sudo` pour avoir accès à toutes les fonctionnalités. Sans `sudo`, Nmap bascule automatiquement sur un scan de type "connect" (`-sT`) au lieu d'un scan "SYN" (`-sS`), car la création de paquets SYN nécessite les privilèges root.
- **Question :** Quel type de scan Nmap utilisera s'il est exécuté avec des privilèges utilisateur locaux ?
  - **Réponse :** `TCP connect scan` (ou `-sT`)

## 🧠 Ce que je retiens pour un poste d'Analyste SOC
- **Cartographie de surface d'attaque** : Nmap est la première étape d'un pentest (Red Team), mais aussi un outil de vérification pour les Blue Teams. Il permet de voir ce qui est exposé sur le réseau (ex: un serveur web oublié sur le port 8008).
- **Le bruit du scan** : Un scan `-sS` est plus furtif qu'un `-sT`, mais les IDS modernes détectent les deux. Connaître les templates de timing (`-T0` à `-T5`) est crucial pour simuler des attaques ou pour éviter de faire planter un serveur fragile lors d'un audit.
- **L'importance des versions** : Connaître la version exacte d'un service (`-sV`) permet de croiser l'information avec des bases de données de vulnérabilités (CVE) pour voir si un serveur est obsolète ou vulnérable.