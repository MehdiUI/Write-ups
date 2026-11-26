# 👨‍💻 Mehdi Lemaire — Analyste SOC Junior

**En reconversion vers la cybersécurité défensive** · 2 ans d'expérience en maintenance et développement de sites web · Objectif : **intégrer un SOC en alternance ou en poste junior**.

📍 Profil actif · Membre Premium TryHackMe · Dernière mise à jour : **26/11/2026**

---

## 🎯 Ma démarche

Ce dépôt n'est pas une collection de solutions : c'est une **preuve de méthode**. Chaque write-up suit la même structure :
- Objectif de la room
- Ce que j'ai appris
- Outils manipulés
- Démarche
- **Ce que je retiens pour un poste d'analyste SOC**

---

## 🔧 Projets

| Projet | Techno | Description |
|---|---|---|
| [**SOC Brute-Force Detector**](https://github.com/Mehdisoc/soc-bruteforce-detector) | Python | Script de détection de brute force SSH dans les `auth.log`. Parsing regex, agrégation par IP, triage par sévérité, ground truth de test. |
| [**Lab SIEM — Detection & Triage (Wazuh)**](https://github.com/MehdiUI/wazuh-soc-lab) | Wazuh · Ubuntu Server · VirtualBox | Laboratoire SIEM complet déployé sur Ubuntu Server : manager + agent Wazuh, génération et collecte de logs, création de règles de détection personnalisées, simulation d'attaques (brute force SSH, FIM, reconnaissance), triage d'alertes dans le dashboard, et rédaction de rapports d'investigation. |

*D'autres projets à venir : pipeline d'enrichissement d'alertes (VirusTotal, AbuseIPDB), automatisation SOAR avec n8n, lab EDR (Sysmon + Velociraptor).*

---

## 📊 Progression — TryHackMe

### ✅ Parcours Cyber Security 101 — Terminé

L'ensemble du parcours **Cyber Security 101** (modules Blue Team) est terminé. Les write-ups sont disponibles dans le dossier [`./TryHackMe/Cyber-security-101/`](./TryHackMe/Cyber-security-101/).

> **Note** : la room **IDS Fundamentals** du module *Network Security Monitoring* (SOC L1) est documentée dans [`Cyber-security-101/Security_Solutions/ids-fundamentals.md`](./TryHackMe/Cyber-security-101/Security_Solutions/ids-fundamentals.md).

---

### 🚧 Parcours SOC Level 1 — En cours

| Module | Rooms | Statut | Write-ups |
|---|---|---|---|
| **Blue Team Introduction** | 4/4 | ✅ | [Voir](./TryHackMe/SOC-L1/Blue-Team-Introduction/README.md) |
| **SOC Team Internals** | 5/5 | ✅ | [Voir](./TryHackMe/SOC-L1/SOC-Team-Internals/README.md) |
| **Core SOC Solutions** | 5/5 | ✅ | [Voir](./TryHackMe/SOC-L1/Core_SOC_Solutions/README.md) |
| **Cyber Defence Frameworks** | 6/6 | ✅ | [Voir](./TryHackMe/SOC-L1/Cyber-Defence-Frameworks/README.md) |
| **Phishing Analysis** | 6/6 | ✅ | [Voir](./TryHackMe/SOC-L1/Phishing-Analysis/README.md) |
| **Network Traffic Analysis** | 5/5 | ✅ | [Voir](./TryHackMe/SOC-L1/Network%20Traffic%20Analysis/) |
| **Network Security Monitoring** | 5/6 | 🚧 | [Voir](./TryHackMe/SOC-L1/Network-Security-Monitoring/) |
| Web Security Monitoring | — | ⏳ | *à venir* |
| Windows Security Monitoring | — | ⏳ | *à venir* |
| Linux Security Monitoring | — | ⏳ | *à venir* |
| Malware Concepts for SOC | — | ⏳ | *à venir* |
| Threat Analysis Tools | — | ⏳ | *à venir* |

---

## 📚 Rooms documentées — SOC Level 1

### Blue Team Introduction (4/4 ✅)
| Room | Write-up |
|---|---|
| Junior Security Analyst Intro | [Voir](./TryHackMe/SOC-L1/Blue-Team-Introduction/junior-security-analyst-intro.md) |
| SOC Role in Blue Team | [Voir](./TryHackMe/SOC-L1/Blue-Team-Introduction/soc-role-in-blue-team.md) |
| Humans as Attack Vectors | [Voir](./TryHackMe/SOC-L1/Blue-Team-Introduction/humans-as-attack-vectors.md) |
| Systems as Attack Vectors | [Voir](./TryHackMe/SOC-L1/Blue-Team-Introduction/systems-as-attack-vectors.md) |

### SOC Team Internals (5/5 ✅)
| Room | Write-up |
|---|---|
| SOC L1 Alert Triage | [Voir](./TryHackMe/SOC-L1/SOC-Team-Internals/soc-l1-alert-triage.md) |
| SOC L1 Alert Reporting | [Voir](./TryHackMe/SOC-L1/SOC-Team-Internals/soc-l1-alert-reporting.md) |
| SOC Workbooks and Lookups | [Voir](./TryHackMe/SOC-L1/SOC-Team-Internals/soc-workbooks-and-lookups.md) |
| SOC Metrics and Objectives | [Voir](./TryHackMe/SOC-L1/SOC-Team-Internals/soc-metrics-and-objectives.md) |
| SOC Simulator: Phishing | [Voir](./TryHackMe/SOC-L1/SOC-Team-Internals/soc-simulator-phishing.md) |

### Core SOC Solutions (5/5 ✅)
| Room | Write-up |
|---|---|
| Intro to EDR | [Voir](./TryHackMe/SOC-L1/Core_SOC_Solutions/intro-to-edr.md) |
| Intro to SIEM | [Voir](./TryHackMe/SOC-L1/Core_SOC_Solutions/intro-to-siem.md) |
| Splunk: The Basics | [Voir](./TryHackMe/SOC-L1/Core_SOC_Solutions/splunk-basics.md) |
| Elastic Stack: The Basics | [Voir](./TryHackMe/SOC-L1/Core_SOC_Solutions/elastic-stack-basics.md) |
| Intro to SOAR | [Voir](./TryHackMe/SOC-L1/Core_SOC_Solutions/intro-to-soar.md) |

### Cyber Defence Frameworks (6/6 ✅)
| Room | Write-up |
|---|---|
| Pyramid Of Pain | [Voir](./TryHackMe/SOC-L1/Cyber-Defence-Frameworks/pyramid-of-pain.md) |
| Cyber Kill Chain | [Voir](./TryHackMe/SOC-L1/Cyber-Defence-Frameworks/cyber-kill-chain.md) |
| Unified Kill Chain | [Voir](./TryHackMe/SOC-L1/Cyber-Defence-Frameworks/unified-kill-chain.md) |
| MITRE | [Voir](./TryHackMe/SOC-L1/Cyber-Defence-Frameworks/mitre.md) |
| Summit | [Voir](./TryHackMe/SOC-L1/Cyber-Defence-Frameworks/summit.md) |
| Eviction | [Voir](./TryHackMe/SOC-L1/Cyber-Defence-Frameworks/eviction.md) |

### Phishing Analysis (6/6 ✅)
| Room | Write-up |
|---|---|
| Phishing Analysis Fundamentals | [Voir](./TryHackMe/SOC-L1/Phishing-Analysis/phishing-analysis-fundamentals.md) |
| Phishing Emails in Action | [Voir](./TryHackMe/SOC-L1/Phishing-Analysis/phishing-emails-in-action.md) |
| Phishing Analysis Tools | [Voir](./TryHackMe/SOC-L1/Phishing-Analysis/phishing-analysis-tools.md) |
| Phishing Prevention | [Voir](./TryHackMe/SOC-L1/Phishing-Analysis/phishing-prevention.md) |
| The Greenholt Phish | [Voir](./TryHackMe/SOC-L1/Phishing-Analysis/the-greenholt-phish.md) |
| Snapped Phish-ing Line | [Voir](./TryHackMe/SOC-L1/Phishing-Analysis/snapped-phish-ing-line.md) |

### Network Traffic Analysis (5/5 ✅)
| Room | Write-up |
|---|---|
| Network Traffic Basics | [Voir](./TryHackMe/SOC-L1/Network%20Traffic%20Analysis/Network%20Traffic%20Basics.md) |
| NetworkMiner | [Voir](./TryHackMe/SOC-L1/Network%20Traffic%20Analysis/networkminer.md) |
| Wireshark: The Basics | [Voir](./TryHackMe/SOC-L1/Network%20Traffic%20Analysis/wireshark-basics.md) |
| Wireshark: Packet Operations | [Voir](./TryHackMe/SOC-L1/Network%20Traffic%20Analysis/wiresharkpacketoperations.md) |
| Wireshark: Traffic Analysis | [Voir](./TryHackMe/SOC-L1/Network%20Traffic%20Analysis/wiresharktrafficanalysis.md) |

### Network Security Monitoring (5/6 🚧)
| Room | Write-up |
|---|---|
| Network Security Essentials | [Voir](./TryHackMe/SOC-L1/Network-Security-Monitoring/networksecurityessentials.md) |
| Network Discovery Detection | [Voir](./TryHackMe/SOC-L1/Network-Security-Monitoring/networkdiscoverydetection.md) |
| Data Exfiltration Detection | [Voir](./TryHackMe/SOC-L1/Network-Security-Monitoring/data-exfiltration-detection.md) |
| IDS Fundamentals | [Voir](./TryHackMe/Cyber-security-101/Security_Solutions/ids-fundamentals.md) |
| MITM Detection | [Voir](./TryHackMe/SOC-L1/Network-Security-Monitoring/mitm-detection.md) |
| Room restante (6/6) | *à venir* |

---

## 🎯 Ce que je cherche

- **Poste** : alternance bac +3 ou CDD/CDI junior — Analyste SOC L1/administrateur système et réseaux
- **Type de structure** : SOC interne, MSSP, ou éditeur
- **Localisation** : Lille, Ile de France
- **Disponibilité** : Immédiate (recherche active)

---

## 🛠️ Stack technique

**Systèmes** · Windows (CMD, PowerShell, NTFS, UAC, Event Viewer, Registre, Defender, Active Directory) · Linux (Bash, Zsh, permissions, processus, services, logs, cron, Ubuntu Server)

**Réseau** · TCP/IP, DNS, HTTP, SMTP, modèle OSI, Wireshark, adressage IPv4/IPv6, subnetting, DHCP, ARP, Nmap, NetworkMiner, analyse de trafic (NTA)

**Scripting** · Python (appliqué à l'analyse de logs), Bash, PowerShell, JavaScript, PHP

**SOC & Defensive Operations** · Triage d'alertes, priorisation, escalade, rédaction de rapport (5W), métriques SOC (MTTD, MTTA, MTTR), workbooks et playbooks, inventaires d'actifs et d'identités, diagrammes réseau.

**Solutions SOC** · **Wazuh (déploiement, agents, règles personnalisées, FIM, dashboard)** · EDR (Endpoint Detection & Response) · SIEM (Splunk, Elastic Stack) · SOAR (orchestration, playbooks, automatisation) · corrélation de logs · détection comportementale.

**Sécurité défensive** · MITRE ATT&CK (mapping TTPs), Pyramid of Pain, Cyber Kill Chain, Unified Kill Chain, Sigma (notions), IOC, analyse de logs, Incident Response (PICERL), IDS/IPS (Snort), Firewalls, Scan de vulnérabilités (OpenVAS), OWASP Top 10 (notions).

**Analyse de phishing** · SPF, DKIM, DMARC, S/MIME, analyse d'en-têtes, defanging, sandbox (Any.Run), PhishTool, VirusTotal, URLScan.io, Talos, CyberChef, Wireshark (filtres SMTP/IMF).

**Principes & Culture** · Triade CIA, DAD, Zero Trust, Défense en profondeur, Sensibilisation et ROI de la formation.

**Analyse de malware & outils** · CyberChef (décodage), CAPA (analyse statique), REMnux (oledump, INetSim, Volatility), FlareVM (PEStudio, FLOSS, Process Explorer, Procmon), Git, Visual Studio Code, Docker (notions), VirtualBox

---

## 🔗 Mes profils

- **TryHackMe** : [tryhackme.com/p/Mehdisoc](https://tryhackme.com/p/Mehdisoc)
- **LinkedIn** : [Mehdi Lemaire](https://www.linkedin.com/in/mehdi-lemaire)