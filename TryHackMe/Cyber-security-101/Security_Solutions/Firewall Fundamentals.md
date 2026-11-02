# 🧱 Firewall Fundamentals

**Objectif de la room :** Comprendre le rôle d'un pare-feu, découvrir les différents types (Stateless, Stateful, Proxy, NGFW) et apprendre à configurer des règles sur Windows (Windows Defender Firewall) et Linux (UFW/iptables).

## 📝 Résumé des tâches et réponses

### Task 1 : What Is the Purpose of a Firewall
- **Concept :** Le pare-feu est le "videur" du réseau. Il inspecte le trafic entrant et sortant et l'autorise ou le bloque en fonction de règles prédéfinies.
- **Question :** Quelle solution de sécurité inspecte le trafic entrant et sortant d'un appareil ou d'un réseau ?
  - **Réponse :** `Firewall`

### Task 2 : Types of Firewalls
- **Concept :** 
  - **Stateless** : Filtre paquet par paquet sans se souvenir des connexions précédentes (rapide mais basique).
  - **Stateful** : Garde une "state table" (table d'état) pour suivre les connexions établies.
  - **Proxy** : Agit comme un intermédiaire (couche 7) et inspecte le contenu des paquets (application).
  - **NGFW (Next-Generation)** : Le plus avancé, fait de l'inspection profonde, du décryptage SSL et de l'analyse heuristique.
- **Question 1 :** Quel type de pare-feu maintient l'état des connexions ?
  - **Réponse :** `Stateful Firewall`
- **Question 2 :** Quel type de pare-feu offre une analyse heuristique du trafic ?
  - **Réponse :** `Next-Generation Firewall`
- **Question 3 :** Quel type de pare-feu inspecte le trafic arrivant à une application ?
  - **Réponse :** `Proxy Firewall`

### Task 3 : Rules in Firewalls
- **Concept :** Une règle est composée de : Source, Destination, Port, Protocole, Action (Allow/Deny/Forward) et Direction (Inbound/Outbound).
- **Question 1 :** Quel type d'action doit être défini pour permettre le trafic ?
  - **Réponse :** `Allow`
- **Question 2 :** Quelle est la direction de la règle pour le trafic quittant notre réseau ?
  - **Réponse :** `Outbound`

### Task 4 : Windows Defender Firewall (Lab)
- **Concept :** Utilisation de l'interface `wf.msc` (Advanced Settings) pour inspecter les règles de trafic entrant (Inbound Rules).
- **Question 1 :** Nom de la règle bloquant tout le trafic SSH entrant ?
  - **Réponse :** `Core Op`
- **Question 2 :** Nom de la règle autorisant le SSH depuis une seule IP ?
  - **Réponse :** `Infra team`
- **Question 3 :** Quelle adresse IP est autorisée sous cette règle (onglet Scope) ?
  - **Réponse :** `192.168.13.7`

### Task 5 : Linux iptables Firewall
- **Concept :** Le framework Linux est **Netfilter**. L'outil le plus simple est **UFW** (Uncomplicated Firewall). On peut définir des politiques par défaut (`ufw default allow/deny outgoing/incoming`) et des règles spécifiques (`ufw deny 22/tcp`).
- **Question 1 :** Quel utilitaire Linux est le successeur de "iptables" ?
  - **Réponse :** `nftables`
- **Question 2 :** Quelle règle ufw pour refuser tout le trafic sortant par défaut ? (sans sudo)
  - **Réponse :** `ufw default deny outgoing`

## 🧠 Ce que je retiens pour un poste d'Analyste SOC
- **La lecture des règles** : Savoir naviguer dans une console de pare-feu (Windows ou Linux) pour vérifier si une règle a été modifiée ou contournée est crucial.
- **Le principe du moindre privilège** : Un bon pare-feu doit avoir une politique par défaut "Deny all" (tout bloquer) et n'autoriser que le strict nécessaire (ex: le port 443 pour le web).
- **Les logs de pare-feu** : Les pare-feux génèrent énormément de logs (trafic bloqué). Savoir les envoyer vers un SIEM permet de détecter des scans de ports ou des tentatives d'intrusion.