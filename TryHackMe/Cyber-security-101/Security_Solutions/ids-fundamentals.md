# IDS Fundamentals — Cyber Security 101 (TryHackMe)

**Catégorie :** Security Solutions  
**Date de sortie :** 2024  
**Date de complétion :** 02/11/2026  
**Lien :** https://tryhackme.com/room/idsfundamentals  
**Parcours :** [Cyber Security 101](https://tryhackme.com/path/outline/cybersecurity101)  
**Room précédente :** [Introduction to SIEM](./introduction-to-siem.md)  
**Room suivante :** [Vulnerability Scanner Overview](./vulnerability-scanner-overview.md)

---

## 🎯 Objectif de la room

Comprendre comment détecter les intrusions réseau et manipuler Snort.

---

## 🧠 Ce que j'ai appris

### Les types d'IDS
Un IDS (détecteur) n'est pas un IPS (bloqueur). Il regarde le trafic et sonne l'alarme.
- **Signature-based** : Cherche des attaques connues (rapide mais aveugle face aux zero-days).
- **Anomaly-based** : Cherche ce qui sort de l'ordinaire (voit les zero-days mais fait beaucoup de faux positifs).
- **Hybrid** : Combine les deux méthodes.

### Snort
Snort est l'outil open-source de référence. J'ai utilisé Snort en mode "Packet Logging" pour enregistrer du trafic, puis j'ai analysé un fichier `.pcap`. J'ai aussi regardé la structure d'une règle Snort (Action, Proto, IP, Port, metadata `sid`, `rev`).

---

## 🖥️ Lignes de commande utilisées

Toutes les commandes ont été exécutées dans un terminal Linux (sur la machine cible).

| Commande | Description |
|---|---|
| `sudo snort -q -l /var/log/snort -i lo -A alert_fast -c /etc/snort/snort.lua` | Lancer Snort en mode NIDS sur l'interface loopback. |
| `sudo snort -q -l /var/log/snort -r Intro_to_IDS.pcap -A alert_fast -c /etc/snort/snort.lua` | Analyser un fichier PCAP avec Snort. |
| `sudo nano /etc/snort/rules/local.rules` | Éditer le fichier de règles personnalisées. |
| `ping 127.0.0.1` | Générer du trafic ICMP pour tester la règle. |
| `ls /etc/snort` | Lister les fichiers de configuration de Snort. |
| `cat /etc/snort/rules/local.rules` | Afficher le contenu des règles personnalisées. |

**Exemple de règle ajoutée dans `local.rules` :**
```snort
alert icmp any any -> 127.0.0.1 any (msg:"Loopback Ping Detected"; sid:10003; rev:1;)