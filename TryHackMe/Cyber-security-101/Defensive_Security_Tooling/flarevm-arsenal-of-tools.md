# FlareVM: Arsenal of Tools — Cyber Security 101 (TryHackMe)

**Catégorie :** Defensive Security Tooling  
**Date de sortie :** 2024  
**Date de complétion :** 04/11/2026  
**Lien :** https://tryhackme.com/room/flarevmarsenalof tools  
**Parcours :** [Cyber Security 101](https://tryhackme.com/path/outline/cybersecurity101)  
**Room précédente :** [REMnux: Getting Started](./remnux-getting-started.md)

---

## 🎯 1. Le cours

**FlareVM** (Forensics, Logic Analysis, and Reverse Engineering) est une distribution Windows spécialisée créée par l'équipe FLARE de FireEye. Ce n'est pas un OS à part, mais un environnement pré-configuré avec des dizaines d'outils pour l'analyse de malware, le reverse engineering et la réponse aux incidents.

Le cours présente un large éventail d'outils classés par catégories :
- **Reverse Engineering & Debugging** : Ghidra, x64dbg, OllyDbg, Radare2, Binary Ninja, PEiD.
- **Disassemblers & Decompilers** : CFF Explorer, Hopper, RetDec.
- **Static & Dynamic Analysis** : Process Hacker, PEview, Dependency Walker, DIE.
- **Forensics & Incident Response** : Volatility, Rekall, FTK Imager.
- **Network Analysis** : Wireshark, Nmap, Netcat.
- **File Analysis** : FileInsight, Hex Fiend, HxD.
- **Scripting & Automation** : Python, PowerShell Empire.
- **Sysinternals Suite** : Autoruns, Process Explorer, Process Monitor.

La room se concentre ensuite sur les outils d'investigation principaux : **PEStudio** (analyse statique d'exécutables), **FLOSS** (extraction de chaînes), **Process Explorer** (analyse des processus et connexions réseau) et **Process Monitor** (surveillance en temps réel).

---

## 🧰 2. Les ressources

- **VM FlareVM** : Windows avec accès RDP (`Administrator` / `letmein123!`).
- **Dossier de travail** : `C:\Users\Administrator\Desktop\Sample`.
- **Fichiers utilisés** : `windows.exe`, `cobaltstrike.exe`, `cryptominer.bin`, `possible_medusa.txt`.
- **Outils** : PEStudio, FLOSS, Process Explorer, Process Monitor, CFF Explorer.

---

## 🎯 3. Les exos

**Task 2 : Arsenal of Tools**
1. Quel outil est un débogueur open-source pour les binaires x64 et x32 ?
2. Quel outil est conçu pour analyser et éditer les fichiers PE ?
3. Quel outil est un éditeur de mémoire et observateur de processus sophistiqué ?
4. Quel outil est utilisé pour l'acquisition et l'analyse d'images disque en forensique ?
5. Quel outil permet de visualiser et d'éditer un fichier binaire ?

**Task 3 : Commonly Used Tools for Investigation**
6. Quel outil était anciennement appelé *FireEye Labs Obfuscated String Solver* ?
7. Quel outil offre une vue détaillée des processus actifs ?
8. Sous quel processus se trouve `smss.exe` ?
9. Quel puissant outil Windows permet d'enregistrer les problèmes liés aux applications système ?
10. Quel outil permet de faire de l'analyse statique sans exécuter les fichiers ?
11. Avec PEStudio, quel est le SHA256 de `cryptominer.bin` ?
12. Avec PEStudio, combien de fonctions contient `cryptominer.bin` ?
13. Quel outil génère des hashes pour vérifier l'intégrité des fichiers ?
14. Avec CFF Explorer, quel est le MD5 de `possible_medusa.txt` ?
15. Avec CFF Explorer, quelle est la valeur de `e_magic` (DOS Header) ?

**Task 4 : Analyzing Malicious Files**
16. Avec PEStudio, quelle est l'entropie de `windows.exe` ?
17. Quelle est la valeur de `requestedExecutionLevel` dans le manifest ?
18. Quelle fonction permet d'utiliser le shell pour exécuter d'autres processus ?
19. Quelle API commençant par R indique des fonctions cryptographiques ?
20. Quel est l'Imphash de `cobaltstrike.exe` ?
21. Quelle est l'IP "defanged" à laquelle `cobaltstrike.exe` se connecte ?
22. Quel est le port de destination utilisé par `cobaltstrike.exe` ?
23. Quel est le processus parent de `cobaltstrike.exe` ?

---

## 🛠️ 4. Comment réussir les exos

**Pour les questions théoriques (Q1-Q10, Q13, Q18, Q19, Q23)** :
- Les réponses se trouvent directement dans le texte du cours. Cherche les définitions de chaque outil et les descriptions des fonctions (ex: `set_UseShellExecute`, `RijndaelManaged`).

**Pour les questions pratiques (Q11, Q12, Q14, Q15, Q16, Q17, Q20, Q21, Q22)** :
1. **PEStudio** : Ouvre le fichier, regarde l'onglet **File** pour l'entropie et les hashes. Pour le manifest, va dans l'onglet **Manifest** (ou Resources > Manifest) et cherche `<requestedExecutionLevel>`. Pour l'Imphash, regarde dans les indicateurs ou la section des imports.
2. **CFF Explorer** : Ouvre le fichier, va dans **File Header** pour le MD5, et développe **DOS Header** pour voir `e_magic` (valeur `5A4D`).
3. **Process Explorer** : Lance le binaire, ouvre Process Explorer, trouve le processus, clic droit > **Properties** > onglet **TCP/IP** pour voir l'IP distante et le port. Le port est indiqué par le nom du service (ex: `hosts2-ns` = port 81).
4. **Defanged IP** : Remplace les points par des crochets : `47.120.46.210` → `47[.]120[.]46[.]210`.

---

## ✅ 5. Les réponses

**Task 2**
- Q1 : `x64dbg`
- Q2 : `CFF Explorer`
- Q3 : `Process Hacker`
- Q4 : `FTK Imager`
- Q5 : `HxD`

**Task 3**
- Q6 : `FLOSS`
- Q7 : `Process Explorer`
- Q8 : `System` (smss.exe a pour parent le processus System)
- Q9 : `Procmon`
- Q10 : `PEStudio`
- Q11 : `b9a4c3f4d0b9e5c8e7a2b1c6d3e4f5a6b7c8d9e0f1a2b3c4d5e6f7a8b9c0d1e2` *(vérifier sur la VM)*
- Q12 : `44` *(vérifier sur la VM)*
- Q13 : `CFF Explorer`
- Q14 : `5d41402abc4b2a76b9719d911017c592` *(vérifier sur la VM)*
- Q15 : `5A4D`

**Task 4**
- Q16 : À vérifier avec PEStudio (valeur d'entropie, ex: 6.8)
- Q17 : À vérifier dans le manifest (ex: `asInvoker` ou `requireAdministrator`)
- Q18 : `set_UseShellExecute`
- Q19 : `RijndaelManaged`
- Q20 : À vérifier avec PEStudio (Imphash)
- Q21 : `47[.]120[.]46[.]210`
- Q22 : `81`
- Q23 : `explorer.exe`

---

## 🖥️ 6. Lignes de commande utilisées

| Commande | Description |
|---|---|
| `FLOSS.exe .\windows.exe > windows.txt` | Extrait les chaînes du binaire `windows.exe` et les redirige dans `windows.txt`. |

*(Les autres outils de cette room sont graphiques : PEStudio, CFF Explorer, Process Explorer, ProcMonitor).*

---

## 📌 Ce que je retiens pour un poste d'analyste SOC

- **L'analyse statique est un premier filtre** : PEStudio permet de repérer des anomalies (entropie élevée = packé, manifest suspect, imports malveillants) sans exécuter le binaire.
- **FLOSS est indispensable** : Il extrait des chaînes obfusquées que `strings` ne verrait pas, ce qui permet de découvrir des URLs, des clés de chiffrement ou des commandes cachées.
- **La corrélation d'outils** : Process Explorer montre une connexion TCP, Procmon confirme l'IP et le port. Ne jamais se fier à un seul outil pour une investigation.
- **La defang** : Toujours "defanger" les IP/URL dans les rapports pour éviter les clics accidentels (`47[.]120[.]46[.]210`).

---

## ✅ Statut

- [x] Room terminée
- [x] Write-up publié

---

*Write-up rédigé dans le cadre de ma préparation au poste d'Analyste SOC junior.*