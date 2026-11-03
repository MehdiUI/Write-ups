# 🛠️ Module 12 : Defensive Security Tooling

Ce module est dédié aux outils pratiques utilisés quotidiennement par les analystes SOC et les experts en forensique pour analyser des fichiers, décoder des données et enquêter sur des malwares.

## 📝 Rooms du module

| Room | Description | Statut | Write-up |
|---|---|---|---|
| **CyberChef: The Basics** | Le couteau suisse pour décoder, encoder et extraire des données (Base64, URL, IP, etc.). | ✅ Terminé | [Lire](./cyberchef-basics.md) |
| **CAPA: The Basics** | Analyse statique de malwares pour identifier leurs capacités (MITRE ATT&CK, MBC, Namespaces). | ✅ Terminé | [Lire](./capa-basics.md) |
| **REMnux** | Distribution Linux spécialisée pour l'analyse de malwares. | ⏳ À venir | — |
| **FlareVM** | Environnement Windows pour le reverse engineering. | ⏳ À venir | — |

## 🧠 Ce que je retiens de ce module
- **L'analyse sans exécution** : Des outils comme CyberChef et CAPA permettent d'analyser des données et des malwares sans risquer d'infecter sa machine.
- **Gain de temps** : Savoir utiliser ces outils permet d'automatiser des tâches d'analyse répétitives et de se concentrer sur l'investigation.
- **Chaîne d'analyse** : Chaque outil a son rôle (CyberChef pour le décodage rapide, CAPA pour les capacités du malware, REMnux/FlareVM pour l'analyse approfondie).
- **CAPA & MITRE ATT&CK** : CAPA mappe automatiquement les capacités d'un malware aux techniques ATT&CK, ce qui permet de comprendre la stratégie de l'attaquant et de préparer les défenses.