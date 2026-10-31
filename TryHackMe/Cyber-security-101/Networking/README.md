# 🌐 Module 5 : Networking

Ce module est le socle de toute compréhension en cybersécurité. Impossible de détecter une attaque réseau ou de comprendre les logs d'un pare-feu sans maîtriser les concepts de base du réseau.

## 📝 Rooms du module

| Room | Description | Statut | Write-up |
|---|---|---|---|
| **Networking Concepts** | Modèle OSI/TCP-IP, adressage IP (IPv4/IPv6), TCP/UDP et encapsulation. | ✅ Terminé | [Lire](./networking-concepts.md) |
| **Networking Essentials** | Attribution d'IP (DHCP), résolution d'adresses (ARP), dépannage (ICMP), routage et NAT. | ✅ Terminé | [Lire](./networking-essentials.md) |
| **Networking Core Protocols** | Protocoles du web (HTTP), e-mails (SMTP, POP3, IMAP), DNS, FTP et Telnet/SSH. | ✅ Terminé | [Lire](./networking-core-protocols.md) |
| **Networking Secure Protocols** | Chiffrement TLS/SSL, HTTPS, versions sécurisées des e-mails et VPN. | ✅ Terminé | [Lire](./networking-secure-protocols.md) |
| **Wireshark: The Basics** | Analyse de paquets en temps réel avec l'interface graphique. | ✅ Terminé | [Lire](./wireshark-basics.md) |
| **Tcpdump: The Basics** | Capture et analyse de paquets en ligne de commande. | ✅ Terminé | [Lire](./tcpdump-the-basics.md) |
| **Nmap: The Basics** | Découverte de réseau, scan de ports et détection de versions. | ✅ Terminé | [Lire](./nmap-the-basics.md) |

## 🧠 Ce que je retiens pour un poste d'Analyste SOC
- **Le modèle OSI** : C'est la grille de lecture pour savoir où se situe un problème ou une attaque (ex: une attaque ARP spoofing est en couche 2, une attaque HTTP en couche 7).
- **TCP vs UDP** : Savoir qu'un scan de port furtif utilise des paquets TCP (SYN) ou UDP, et comprendre le Three-Way Handshake pour repérer les connexions anormales.
- **Le NAT et le DHCP** : Comprendre comment les adresses IP privées sont traduites en IP publiques permet d'analyser les logs de connexions sortantes et de tracer une éventuelle exfiltration de données.
- **Le chiffrement (TLS/SSL)** : Comme 90% du trafic est chiffré, l'analyste doit se concentrer sur les métadonnées (adresses IP, certificats) pour détecter les communications suspectes (C2).
- **Wireshark & Tcpdump** : Wireshark est parfait pour l'analyse graphique sur un poste de travail, mais Tcpdump est indispensable pour capturer du trafic directement sur un serveur Linux distant (sans interface), puis exporter le fichier `.pcap` pour l'analyser.
- **Nmap** : C'est l'outil de cartographie réseau par excellence. Savoir repérer un port ouvert inattendu (comme un serveur web sur le port 8008) ou un service obsolète (via `-sV`) est la première étape de la chasse aux vulnérabilités.