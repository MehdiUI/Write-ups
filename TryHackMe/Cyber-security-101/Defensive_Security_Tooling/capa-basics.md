# CAPA: The Basics — Cyber Security 101 (TryHackMe)

**Catégorie :** Defensive Security Tooling  
**Date de sortie :** 2024  
**Date de complétion :** 03/11/2026  
**Lien :** https://tryhackme.com/room/capathebasics  
**Parcours :** [Cyber Security 101](https://tryhackme.com/path/outline/cybersecurity101)  
**Room précédente :** [CyberChef: The Basics](./cyberchef-basics.md)  
**Room suivante :** REMnux

---

## 🎯 Objectif de la room

Comprendre comment analyser un malware sans l'exécuter, en identifiant ses capacités grâce à l'analyse statique.

---

## 🧠 Ce que j'ai appris

### Le rôle de CAPA
CAPA (Mandiant FLARE) lit un binaire et applique des règles pour deviner ses capacités : réseau, persistance, injection, anti-VM. C'est de l'analyse statique (on ne lance pas le virus).

### La structure du rapport
Le rapport est structuré en blocs :
- **Hashs** : MD5, SHA1, SHA256.
- **MITRE ATT&CK** : Les tactiques et techniques auxquelles les capacités sont associées.
- **MBC (Malware Behavior Catalogue)** : Un catalogue de comportements malveillants, avec des identifiants (B, C, E).
- **Namespaces** : Une hiérarchie de dossiers pour classer les règles (ex: `anti-analysis`, `communication`, `persistence`).
- **Capabilities** : Le nom de la règle qui a matché, avec son namespace et le fichier YAML correspondant.

---

## 🖥️ Lignes de commande utilisées

Toutes les commandes ont été exécutées dans un **PowerShell** ouvert sur le bureau de la Lab Machine, après s'être placé dans le dossier `C:\Users\Administrator\Desktop\capa`.

| Commande | Description |
|---|---|
| `cd C:\Users\Administrator\Desktop\capa` | Se placer dans le dossier contenant les fichiers de la room. |
| `capa.exe .\cryptbot.bin` | Lancer l'analyse standard sur le binaire. |
| `capa.exe .\cryptbot.bin -v` | Lancer l'analyse en mode verbeux (plus de détails). |
| `capa.exe .\cryptbot.bin -vv` | Lancer l'analyse en mode très verbeux. |
| `capa.exe -j -vv .\cryptbot.bin > cryptbot_vv.json` | Générer un rapport JSON à partir du mode très verbeux. |
| `Get-Content .\cryptbot.txt` | Lire le rapport pré-généré en texte brut. |
| `Get-Content .\cryptbot_vv.txt` | Lire le rapport pré-généré en mode très verbeux. |

**Astuce :** l'analyse complète prend 6 à 8 minutes sur la VM. En pratique, les créateurs de la room ont fourni les rapports pré-générés (`cryptbot.txt`, `cryptbot_vv.txt`, `cryptbot_vv.json`) pour éviter l'attente.

**CAPA Explorer Web** : pour exploiter le JSON de manière interactive, on ouvre le raccourci Chrome `capa_web_explorer_offline` (ou `https://127.0.0.1` dans le navigateur) et on importe `cryptbot_vv.json` via le bouton **Upload from local**.

---

## 📌 Ce que je retiens pour un poste d'analyste SOC

- **Gain de temps** : Au lieu de passer des heures en reverse engineering, CAPA me dit en quelques minutes si le fichier communique en HTTP ou s'il tente de se cacher dans une VM.
- **Mapping ATT&CK** : CAPA me donne directement les techniques ATT&CK (ex: `T1027`). Je peux vérifier si mon SIEM détecte ces techniques.
- **L'outil peut être lent (6-8 min)**. En production, on utilise souvent des rapports pré-générés ou on le lance en arrière-plan.

---

## ✅ Statut

- [x] Room terminée
- [x] Write-up publié

---

*Write-up rédigé dans le cadre de ma préparation au poste d'Analyste SOC junior.*