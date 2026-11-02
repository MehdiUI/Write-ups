# 🛠️ Module 11 : Security Solutions

Ce module explore les outils fondamentaux de la sécurité défensive. Après avoir compris les processus (SOC, Forensics, Logs), il est temps de découvrir les solutions technologiques qui permettent de protéger un réseau et de détecter les menaces.

## 📝 Rooms du module

| Room | Description | Statut | Write-up |
|---|---|---|---|
| **Firewall Fundamentals** | Types de pare-feux, règles et configuration (Windows Defender & UFW Linux). | ✅ Terminé | [Lire](./firewall-fundamentals.md) |
| **Introduction to SIEM** | Découverte du Security Information and Event Management (collecte, normalisation, corrélation). | ✅ Terminé | [Lire](./introduction-to-siem.md) |
| **IDS Fundamentals** | Découverte des systèmes de détection d'intrusion (Types, Snort, analyse de PCAP). | ✅ Terminé | [Lire](./ids-fundamentals.md) |
| **Vulnerability Scanner Overview** | Scan de vulnérabilités (CVE, CVSS) et pratique avec OpenVAS. | ✅ Terminé | [Lire](./vulnerability-scanner-overview.md) |

## 🧠 Ce que je retiens de ce module
- **La défense en profondeur** : Un bon réseau utilise plusieurs couches de sécurité (Pare-feu pour bloquer, IDS pour détecter, Scanner pour corriger).
- **Les pare-feux** : Ils sont la première ligne de défense. Comprendre la différence entre un filtrage basique (stateless) et une inspection profonde (NGFW) permet de choisir le bon outil.
- **Le SIEM** : C'est le cerveau de la défense. Il collecte, normalise et corrèle les logs pour donner aux analystes une vision claire des menaces.
- **L'IDS (Snort)** : C'est le chien de garde. Savoir écrire des règles et analyser des PCAP permet de repérer les intrusions.
- **Les scanners** : Ils permettent de corriger les failles (Patching) avant qu'elles ne soient exploitées, en se basant sur les scores CVSS pour prioriser les urgences.