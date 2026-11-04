# REMnux: Getting Started — Cyber Security 101 (TryHackMe)

**Catégorie :** Defensive Security Tooling  
**Date de sortie :** 2024  
**Date de complétion :** 04/11/2026  
**Lien :** https://tryhackme.com/room/remnuxgettingstarted  
**Parcours :** [Cyber Security 101](https://tryhackme.com/path/outline/cybersecurity101)  
**Room précédente :** [CAPA: The Basics](./capa-basics.md)  
**Room suivante :** FlareVM

---

## 🎯 Objectif de la room

Découvrir la distribution Linux REMnux, spécialisée dans l'analyse de malwares. Apprendre à analyser des documents Office malveillants, à simuler un réseau (INetSim) pour observer le comportement des malwares, et à utiliser Volatility 3 pour investiguer une image mémoire.

---

## 🧠 Ce que j'ai appris

### 1. Analyse de documents Office (OLE2)
Les documents Office (Word, Excel) peuvent contenir des macros VBA malveillantes. L'outil `oledump.py` permet de lister les flux de données (data streams) contenus dans un fichier OLE2. Un flux marqué d'un **`M` majuscule** indique la présence d'une macro. L'option `--vbadecompress` permet de décompresser le code VBA pour le rendre lisible.
Les attaquants utilisent souvent ces macros pour exécuter des commandes PowerShell (comme `Invoke-WebRequest`) et télécharger des payloads secondaires (ex: `Doc-3737122pdf.exe`) sans que l'utilisateur ne s'en rende compte.

### 2. Simulation réseau avec INetSim
Pour analyser le comportement réseau d'un malware sans risquer de compromettre un vrai réseau, on utilise **INetSim**. Il simule des services Internet (DNS, HTTP, HTTPS, etc.). En modifiant la configuration (`dns_default_ip`), on redirige les requêtes DNS vers la machine REMnux. On peut ensuite simuler le téléchargement de fichiers (avec `wget`) et consulter le rapport de session généré par INetSim pour voir exactement quelles URL et méthodes ont été utilisées.

### 3. Analyse mémoire avec Volatility 3
**Volatility 3** (`vol3`) est l'outil de référence pour l'analyse d'images mémoire (RAM). Il utilise des **plugins** pour extraire des artefacts spécifiques :
- `windows.pstree.PsTree` : Affiche les processus en arbre (parent/enfant).
- `windows.pslist.PsList` : Liste les processus actifs.
- `windows.malfind.Malfind` : Détecte les processus suspectés de contenir du code injecté.
- `windows.dlllist.DllList` : Liste les DLL chargées par les processus.
Pour gagner du temps, on peut utiliser une **boucle `for`** pour exécuter tous les plugins en une seule fois et rediriger les résultats vers des fichiers `.txt` (prétraitement des preuves). L'utilitaire Linux **`strings`** permet également d'extraire les chaînes de caractères (ASCII, Unicode) de l'image mémoire.

---

## 🖥️ Lignes de commande utilisées

Toutes les commandes ont été exécutées dans un terminal sur la VM REMnux.

### Analyse de documents OLE2 (Task 3)
| Commande | Description |
|---|---|
| `oledump.py agenttesla.xlsm` | Lister les flux du document. |
| `oledump.py agenttesla.xlsm -s 4` | Sélectionner le flux n°4. |
| `oledump.py agenttesla.xlsm -s 4 --vbadecompress` | Décompresser et afficher la macro VBA. |
| `oledump.py possible_malicious.docx` | Analyser un second document pour compter les flux. |

### Simulation réseau avec INetSim (Task 4)
| Commande | Description |
|---|---|
| `sudo nano /etc/inetsim/inetsim.conf` | Éditer la configuration (modifier `dns_default_ip`). |
| `cat /etc/inetsim/inetsim.conf \| grep dns_default_ip` | Vérifier que la modification a été prise en compte. |
| `sudo inetsim` | Lancer le simulateur INetSim. |
| `sudo wget https://10.128.151.48/flag.txt --no-check-certificate` | Télécharger un fichier depuis le faux serveur. |
| `cat flag.txt` | Lire le contenu du fichier téléchargé. |
| `sudo cat /var/log/inetsim/report/report.XXXXX.txt` | Lire le rapport généré par INetSim. |

### Analyse mémoire avec Volatility 3 (Task 5)
| Commande | Description |
|---|---|
| `sudo su` | Passer en root. |
| `cd /home/ubuntu/Desktop/tasks/Wcry_memory_image/` | Se rendre dans le dossier de travail. |
| `vol3 -f wcry.mem windows.malfind.Malfind` | Chercher les processus avec injection de code. |
| `vol3 -f wcry.mem windows.dlllist.DllList > dlllist.txt` | Sauvegarder la liste des DLL dans un fichier texte. |
| `grep "@WanaDecryptor@.exe" dlllist.txt` | Rechercher le chemin d'un binaire spécifique. |
| `for plugin in ...; do vol3 -q -f wcry.mem $plugin > wcry.$plugin.txt; done` | Boucle pour exécuter tous les plugins et sauvegarder les résultats. |
| `strings wcry.mem > wcry.strings.ascii.txt` | Extraire les chaînes ASCII de l'image mémoire. |
| `strings -e l wcry.mem > wcry.strings.unicode_little_endian.txt` | Extraire les chaînes Unicode little-endian. |
| `strings -e b wcry.mem > wcry.strings.unicode_big_endian.txt` | Extraire les chaînes Unicode big-endian. |

---

## 📌 Ce que je retiens pour un poste d'analyste SOC

- **Les documents Office sont une porte d'entrée** : Une macro VBA peut télécharger et exécuter un ransomware (comme WannaCry) en quelques secondes. L'analyse statique avec `oledump.py` permet de voir le code sans l'exécuter.
- **La simulation réseau est indispensable** : INetSim permet de voir quelles URL le malware essaie de contacter (C2, payloads) sans prendre le risque d'une vraie connexion.
- **L'analyse mémoire révèle l'invisible** : Un malware peut être effacé du disque mais rester actif en mémoire. Volatility permet d'extraire les processus injectés (`Malfind`) et les DLL chargées (`DllList`) pour comprendre comment l'attaquant a opéré.
- **Le prétraitement est la clé** : Face à des images mémoire de plusieurs Go, exécuter tous les plugins et extraire les `strings` en amont permet de gagner un temps précieux lors de l'investigation.

---

## ✅ Statut

- [x] Room terminée
- [x] Write-up publié

---

*Write-up rédigé dans le cadre de ma préparation au poste d'Analyste SOC junior.*