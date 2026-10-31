# 🦈 Tcpdump: The Basics

**Objectif de la room :** Apprendre à utiliser `tcpdump`, l'analyseur de paquets en ligne de commande le plus populaire sous Linux. Indispensable pour capturer, filtrer et lire le trafic réseau sur des serveurs distants sans interface graphique.

## 📝 Résumé des tâches et réponses

### Task 2 : Basic Packet Capture
- **Concept :** Contrairement à Wireshark, `tcpdump` s'utilise entièrement en ligne de commande. Il permet de choisir l'interface (`-i`), d'enregistrer dans un fichier (`-w`), de lire un fichier (`-r`), ou de limiter le nombre de paquets (`-c`).
- **Question :** Quel argument utiliser pour afficher uniquement les adresses IP et ports sous format numérique (sans résolution DNS) ?
- **Réponse :** `-n` (ou `-nn` pour bloquer aussi la résolution des ports).

### Task 3 : Filtering Expressions
- **Concept :** On ne peut pas tout capturer. On filtre par hôte (`host`), par port (`port 53`), ou par protocole (`icmp`, `tcp`, `arp`). On peut combiner avec `and`, `or`, `not`.
- **Question 1 :** Combien de paquets utilisent le protocole ICMP ?
  - **Commande :** `tcpdump -r traffic.pcap icmp -n | wc -l`
  - **Réponse :** `26`
- **Question 2 :** Quelle est l'adresse IP de l'hôte qui a demandé l'adresse MAC de 192.168.124.137 ?
  - **Commande :** `tcpdump -r traffic.pcap arp -n`
  - **Réponse :** `192.168.124.1`
- **Question 3 :** Quel nom d'hôte apparaît dans la première requête DNS ?
  - **Commande :** `tcpdump -r traffic.pcap port 53 -n`
  - **Réponse :** `dns.google.com`

### Task 4 : Advanced Filtering
- **Concept :** On peut filtrer selon la taille des paquets (`greater`, `less`) ou en utilisant des opérations binaires pour inspecter les headers (ex: les flags TCP comme SYN, ACK, RST).
- **Question 1 :** Combien de paquets ont uniquement le flag TCP Reset (RST) activé ?
  - **Commande :** `tcpdump -n -r traffic.pcap 'tcp[tcpflags] == tcp-rst' | wc -l`
  - **Réponse :** `57`
- **Question 2 :** Quelle est l'adresse IP de l'hôte qui a envoyé des paquets de plus de 15000 octets ?
  - **Commande :** `tcpdump -n -r traffic.pcap 'greater 15000'`
  - **Réponse :** `185.117.80.53`

### Task 5 : Displaying Packets
- **Concept :** On peut modifier l'affichage des paquets : `-q` (rapide), `-e` (affiche les adresses MAC), `-A` (ASCII), `-xx` (hexadécimal), `-X` (hexadécimal + ASCII).
- **Question :** Quelle est l'adresse MAC de l'hôte qui a envoyé une requête ARP ?
  - **Commande :** `tcpdump -r traffic.pcap -e arp -n`
  - **Réponse :** `44:df:65:d8:fe:6c`

## 🧠 Ce que je retiens pour un poste d'Analyste SOC
- **L'outil de l'ombre** : `tcpdump` est souvent déjà installé sur les serveurs Linux. C'est l'outil parfait pour capturer du trafic rapidement en SSH, puis exporter le fichier `.pcap` pour l'analyser confortablement dans Wireshark.
- **Les flags TCP** : Comprendre comment filtrer sur les flags TCP (`tcp-syn`, `tcp-ack`, `tcp-rst`) est crucial pour repérer des scans de ports ou des connexions anormales.
- **Filtrage précis** : Savoir combiner `host`, `port` et `and`/`or` permet de réduire des millions de paquets à seulement ceux qui nous intéressent.