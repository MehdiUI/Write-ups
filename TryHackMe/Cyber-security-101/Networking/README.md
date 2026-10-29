# 🌐 Module 5 : Networking

Ce module est le socle de toute compréhension en cybersécurité. Impossible de détecter une attaque réseau ou de comprendre les logs d'un pare-feu sans maîtriser les concepts de base du réseau.

## 📝 Rooms du module

| Room | Description | Statut | Write-up |
|---|---|---|---|
| **Networking Concepts** | Modèle OSI/TCP-IP, adressage IP (IPv4/IPv6), TCP/UDP et encapsulation. | ✅ Terminé | [Lire](./networking-concepts.md) |
| **Networking Essentials** | Attribution d'IP (DHCP), résolution d'adresses (ARP), dépannage (ICMP), routage et NAT. | ✅ Terminé | [Lire](./networking-essentials.md) |
| **Networking Core Protocols** | (En cours d'exploration) | ⏳ À venir | — |

## 🧠 Ce que je retiens pour un poste d'Analyste SOC
- **Le modèle OSI** : C'est la grille de lecture pour savoir où se situe un problème ou une attaque (ex: une attaque ARP spoofing est en couche 2, une attaque HTTP en couche 7).
- **TCP vs UDP** : Savoir qu'un scan de port furtif utilise des paquets TCP (SYN) ou UDP, et comprendre le Three-Way Handshake pour repérer les connexions anormales.
- **Le NAT et le DHCP** : Comprendre comment les adresses IP privées sont traduites en IP publiques permet d'analyser les logs de connexions sortantes et de tracer une éventuelle exfiltration de données.