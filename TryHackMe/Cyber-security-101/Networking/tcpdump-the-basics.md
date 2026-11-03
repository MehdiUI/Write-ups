# Tcpdump: The Basics — Cyber Security 101 (TryHackMe)

**Catégorie :** Réseau  
**Date de sortie :** 2024  
**Date de complétion :** 02/11/2026  
**Lien :** https://tryhackme.com/room/tcpdumpthebasics  
**Parcours :** [Cyber Security 101](https://tryhackme.com/path/outline/cybersecurity101)  
**Room précédente :** [Wireshark: The Basics](./wireshark-basics.md)  
**Room suivante :** [Nmap: The Basics](./nmap-the-basics.md)

---

## 🎯 Objectif de la room

Apprendre à utiliser `tcpdump`, l'analyseur de paquets en ligne de commande le plus populaire sous Linux. Indispensable pour capturer, filtrer et lire le trafic réseau sur des serveurs distants sans interface graphique.

---

## 🧠 Ce que j'ai appris

### Capture de base
Contrairement à Wireshark, `tcpdump` s'utilise entièrement en ligne de commande. Il permet de choisir l'interface (`-i`), d'enregistrer dans un fichier (`-w`), de lire un fichier (`-r`), ou de limiter le nombre de paquets (`-c`).

### Filtres
On ne peut pas tout capturer. On filtre par hôte (`host`), par port (`port 53`), ou par protocole (`icmp`, `tcp`, `arp`). On peut combiner avec `and`, `or`, `not`.

### Filtres avancés
On peut filtrer selon la taille des paquets (`greater`, `less`) ou en utilisant des opérations binaires pour inspecter les headers (ex: les flags TCP comme SYN, ACK, RST).

### Affichage
On peut modifier l'affichage des paquets : `-q` (rapide), `-e` (affiche les adresses MAC), `-A` (ASCII), `-xx` (hexadécimal), `-X` (hexadécimal + ASCII).

---

## 🖥️ Lignes de commande utilisées

| Commande | Description |
|---|---|
| `tcpdump -i eth0 -c 5 -n` | Capturer 5 paquets sur l'interface eth0 sans résolution DNS. |
| `tcpdump -r traffic.pcap -c 5 -n` | Lire les 5 premiers paquets d'un fichier PCAP. |
| `tcpdump -r traffic.pcap icmp -n \| wc -l` | Compter les paquets ICMP dans un fichier PCAP. |
| `tcpdump -r traffic.pcap arp -n` | Filtrer les paquets ARP. |
| `tcpdump -r traffic.pcap port 53 -n` | Filtrer les paquets DNS (port 53). |
| `tcpdump -n -r traffic.pcap 'tcp[tcpflags] == tcp-rst' \| wc -l` | Compter les paquets avec uniquement le flag RST. |
| `tcpdump -n -r traffic.pcap 'greater 15000'` | Filtrer les paquets de plus de 15000 octets. |
| `tcpdump -r traffic.pcap -e arp -n` | Afficher les adresses MAC des paquets ARP. |

---

## 📌 Ce que je retiens pour un poste d'analyste SOC

- **L'outil de l'ombre** : `tcpdump` est souvent déjà installé sur les serveurs Linux. C'est l'outil parfait pour capturer du trafic rapidement en SSH, puis exporter le fichier `.pcap` pour l'analyser confortablement dans Wireshark.
- **Les flags TCP** : Comprendre comment filtrer sur les flags TCP (`tcp-syn`, `tcp-ack`, `tcp-rst`) est crucial pour repérer des scans de ports ou des connexions anormales.
- **Filtrage précis** : Savoir combiner `host`, `port` et `and`/`or` permet de réduire des millions de paquets à seulement ceux qui nous intéressent.

---

## ✅ Statut

- [x] Room terminée
- [x] Write-up publié

---

*Write-up rédigé dans le cadre de ma préparation au poste d'Analyste SOC junior.*