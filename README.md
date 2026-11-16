# 👨‍💻 Mehdi Lemaire — Analyste SOC Junior

**En reconversion vers la cybersécurité défensive** · 2 ans d'expérience en maintenance et développement de sites web · Objectif : **intégrer un SOC en alternance ou en poste junior**.

📍 Profil actif · Membre Premium TryHackMe · Dernière mise à jour : **16/11/2026**

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

---

### 🚧 Parcours SOC Level 1 — En cours

| Module | Rooms | Statut | Write-ups |
|---|---|---|---|
| **Blue Team Introduction** | 4/4 | ✅ | [Voir](./TryHackMe/SOC-Level-1/Blue_Team_Introduction/README.md) |
| **SOC Team Internals** | 5/5 | ✅ | [Voir](./TryHackMe/SOC-Level-1/SOC_Team_Internals/README.md) |
| **Core SOC Solutions** | 5/5 | ✅ | [Voir](./TryHackMe/SOC-Level-1/Core_SOC_Solutions/README.md) |
| **Cyber Defence Frameworks** | 6/6 | ✅ | [Voir](./TryHackMe/SOC-Level-1/Cyber_Defence_Frameworks/README.md) |
| **Phishing Analysis** | 6/6 | ✅ | [Voir](./TryHackMe/SOC-Level-1/Phishing_Analysis/README.md) |
| Network Traffic Analysis | — | ⏳ | *à venir* |
| Network Security Monitoring | — | ⏳ | *à venir* |
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
| Junior Security Analyst Intro | [Voir](./TryHackMe/SOC-Level-1/Blue_Team_Introduction/junior-security-analyst-intro.md) |
| SOC Role in Blue Team | [Voir](./TryHackMe/SOC-Level-1/Blue_Team_Introduction/soc-role-in-blue-team.md) |
| Humans as Attack Vectors | [Voir](./TryHackMe/SOC-Level-1/Blue_Team_Introduction/humans-as-attack-vectors.md) |
| Systems as Attack Vectors | [Voir](./TryHackMe/SOC-Level-1/Blue_Team_Introduction/systems-as-attack-vectors.md) |

### SOC Team Internals (5/5 ✅)
| Room | Write-up |
|---|---|
| SOC L1 Alert Triage | [Voir](./TryHackMe/SOC-Level-1/SOC_Team_Internals/soc-l1-alert-triage.md) |
| SOC L1 Alert Reporting | [Voir](./TryHackMe/SOC-Level-1/SOC_Team_Internals/soc-l1-alert-reporting.md) |
| SOC Workbooks and Lookups | [Voir](./TryHackMe/SOC-Level-1/SOC_Team_Internals/soc-workbooks-and-lookups.md) |
| SOC Metrics and Objectives | [Voir](./TryHackMe/SOC-Level-1/SOC_Team_Internals/soc-metrics-and-objectives.md) |
| SOC Simulator: Phishing | [Voir](./TryHackMe/SOC-Level-1/SOC_Team_Internals/soc-simulator-phishing.md) |

### Core SOC Solutions (5/5 ✅)
| Room | Write-up |
|---|---|
| Intro to EDR | [Voir](./TryHackMe/SOC-Level-1/Core_SOC_Solutions/intro-to-edr.md) |
| Intro to SIEM | [Voir](./TryHackMe/SOC-Level-1/Core_SOC_Solutions/intro-to-siem.md) |
| Splunk: The Basics | [Voir](./TryHackMe/SOC-Level-1/Core_SOC_Solutions/splunk-basics.md) |
| Elastic Stack: The Basics | [Voir](./TryHackMe/SOC-Level-1/Core_SOC_Solutions/elastic-stack-basics.md) |
| Intro to SOAR | [Voir](./TryHackMe/SOC-Level-1/Core_SOC_Solutions/intro-to-soar.md) |

### Cyber Defence Frameworks (6/6 ✅)
| Room | Write-up |
|---|---|
| Pyramid Of Pain | [Voir](./TryHackMe/SOC-Level-1/Cyber_Defence_Frameworks/pyramid-of-pain.md) |
| Cyber Kill Chain | [Voir](./TryHackMe/SOC-Level-1/Cyber_Defence_Frameworks/cyber-kill-chain.md) |
| Unified Kill Chain | [Voir](./TryHackMe/SOC-Level-1/Cyber_Defence_Frameworks/unified-kill-chain.md) |
| MITRE | [Voir](./TryHackMe/SOC-Level-1/Cyber_Defence_Frameworks/mitre.md) |
| Summit | [Voir](./TryHackMe/SOC-Level-1/Cyber_Defence_Frameworks/summit.md) |
| Eviction | [Voir](./TryHackMe/SOC-Level-1/Cyber_Defence_Frameworks/eviction.md) |

### Phishing Analysis (6/6 ✅)
| Room | Write-up |
|---|---|
| Phishing Analysis Fundamentals | [Voir](./TryHackMe/SOC-Level-1/Phishing_Analysis/phishing-analysis-fundamentals.md) |
| Phishing Emails in Action | [Voir](./TryHackMe/SOC-Level-1/Phishing_Analysis/phishing-emails-in-action.md) |
| Phishing Analysis Tools | [Voir](./TryHackMe/SOC-Level-1/Phishing_Analysis/phishing-analysis-tools.md) |
| Phishing Prevention | [Voir](./TryHackMe/SOC-Level-1/Phishing_Analysis/phishing-prevention.md) |
| The Greenholt Phish | [Voir](./TryHackMe/SOC-Level-1/Phishing_Analysis/the-greenholt-phish.md) |
| Snapped Phish-ing Line | [Voir](./TryHackMe/SOC-Level-1/Phishing_Analysis/snapped-phish-ing-line.md) |

---

## 🎯 Ce que je cherche

- **Poste** : alternance bac +3 ou CDD/CDI junior — Analyste SOC L1/administrateur système et réseaux
- **Type de structure** : SOC interne, MSSP, ou éditeur
- **Localisation** : Lille, Ile de France
- **Disponibilité** : Immédiate (recherche active)

---

## 🛠️ Stack technique

**Systèmes** · Windows (CMD, PowerShell, NTFS, UAC, Event Viewer, Registre, Defender, Active Directory) · Linux (Bash, Zsh, permissions, processus, services, logs, cron, Ubuntu Server)

**Réseau** · TCP/IP, DNS, HTTP, SMTP, modèle OSI, Wireshark, adressage IPv4/IPv6, subnetting, DHCP, ARP, Nmap

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