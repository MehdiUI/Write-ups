# 👁️ IDS Fundamentals

**Objectif de la room :** Comprendre ce qu'est un système de détection d'intrusion (IDS), découvrir les différents types (HIDS/NIDS, Signature/Anomalie) et manipuler Snort pour analyser du trafic réseau.

## 📝 Résumé des tâches et réponses

### Task 1 & 2 : What Is an IDS & Types of IDS
- **Concept :** Un IDS **détecte** les intrusions mais ne les **bloque** pas (contrairement à un IPS).
  - **HIDS (Host-based)** : Installé sur un seul hôte.
  - **NIDS (Network-based)** : Surveille tout le trafic du réseau.
  - **Signature-based** : Détecte les attaques connues (comme un antivirus). Rapide mais aveugle face aux zero-days.
  - **Anomaly-based** : Apprend le comportement normal et alerte en cas de déviation (détecte les zero-days mais fait plus de faux positifs).
  - **Hybrid** : Combine les deux méthodes.
- **Question 1 :** Quel type d'IDS est déployé pour détecter les menaces sur l'ensemble du réseau ?
  - **Réponse :** `Network Intrusion Detection System`
- **Question 2 :** Quel IDS exploite à la fois les techniques de détection par signature et par anomalie ?
  - **Réponse :** `Hybrid IDS`

### Task 3 : IDS Example: Snort
- **Concept :** Snort est un IDS open-source. Il possède 3 modes :
  1. **Packet sniffer mode** : Affiche le trafic (comme Wireshark).
  2. **Packet logging mode** : Enregistre le trafic dans un fichier PCAP pour analyse ultérieure.
  3. **NIDS mode** : Le mode principal, analyse le trafic en temps réel et génère des alertes.
- **Question 1 :** Quel mode de Snort nous aide à enregistrer le trafic réseau dans un fichier PCAP ?
  - **Réponse :** `Packet Logging mode`
- **Question 2 :** Comment s'appelle le mode principal de Snort ?
  - **Réponse :** `Network Intrusion Detection System mode`

### Task 4 : Snort Usage
- **Concept :** Les fichiers de configuration de Snort sont dans `/etc/snort`. Les règles personnalisées sont dans `local.rules`. 
  - Une règle contient : Action, Protocole, Source, Port, Destination, Port, et des métadonnées (msg, `sid` pour l'ID unique, `rev` pour la révision).
- **Question 1 :** Où se trouve le répertoire principal de Snort qui stocke ses fichiers ?
  - **Réponse :** `/etc/snort`
- **Question 2 :** Quel champ dans la règle Snort indique le numéro de révision de la règle ?
  - **Réponse :** `rev`
- **Question 3 :** Quel protocole est défini dans l'exemple de règle créé dans la tâche ?
  - **Réponse :** `icmp`
- **Question 4 :** Quel est le nom du fichier qui contient les règles personnalisées pour Snort ?
  - **Réponse :** `local.rules`

### Task 5 : Practical Lab
- **Concept :** Analyse du fichier `Intro_to_IDS.pcap` avec Snort pour investiguer une attaque.
- **Commande exécutée :** `sudo snort -q -l /var/log/snort -r Intro_to_IDS.pcap -A alert_fast -c /etc/snort/snort.lua`
- **Question 1 :** Quelle est l'adresse IP de la machine qui a tenté de se connecter en SSH ?
  - **Réponse :** `10.10.17.5`
- **Question 2 :** Quel autre message de règle (autre que le SSH) est détecté ?
  - **Réponse :** `Ping Detected`
- **Question 3 :** Quel est le `sid` de la règle qui détecte le SSH ?
  - **Réponse :** `1000002`

## 🧠 Ce que je retiens pour un poste d'Analyste SOC
- **La différence IDS / IPS** : L'IDS est une alarme (il te prévient), l'IPS est un videur (il bloque). Le SOC utilise l'IDS pour enquêter, mais s'appuie sur d'autres outils (pare-feu, EDR) pour bloquer.
- **Snort** : Savoir lire et créer des règles Snort est une compétence très recherchée. Comprendre la structure (Action, Proto, IP, Port, Metadata) permet de créer des alertes sur mesure.
- **L'analyse de PCAP** : Le mode "Packet Logging" suivi d'une analyse post-incident est le quotidien des analystes forensiques. Snort permet de rejouer une attaque enregistrée pour comprendre comment elle s'est déroulée.