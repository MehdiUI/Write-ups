# Phishing Analysis Tools — Phishing Analysis (TryHackMe)

**Catégorie :** Blue Team / SOC / Phishing Analysis  
**Date de complétion :** 14/11/2026  
**Lien :** https://tryhackme.com/room/phishingemails3tryoe  
**Parcours :** [SOC Level 1](https://tryhackme.com/path/outline/soclevel1)

---

## 🎯 Objectif de la room

Passer de l’analyse manuelle à l’**outillage professionnel** du triage de phishing. La room présente la stack d’outils utilisée par un analyste SOC pour investiguer un email suspect sans jamais interagir avec le contenu malveillant : analyse d’en-têtes (MXToolbox, Message Header Analyzer), réputation d’IP et de domaine (IPinfo, URLScan.io, Talos Intelligence), extraction et décodage d’URL (CyberChef), réputation de fichiers par hash (VirusTotal, Talos), sandbox malware (Any.Run) et triage unifié (PhishTool). Trois cas pratiques (Netflix, mise à jour de paiement, Excel exécutable) servent de fil conducteur.

---

## 🧠 Ce que j'ai appris

### La règle d’or et les artefacts à collecter

**Ne jamais cliquer sur un lien ni ouvrir une pièce jointe** dans l’email original. Toute l’investigation se fait sur des **copies** (en-têtes bruts, code source, fichiers sauvegardés) ou dans des environnements isolés (sandbox).

Les artefacts à collecter systématiquement en premier :

- **En-têtes** : adresse expéditeur réelle (`Return-Path`, `Reply-To`), IP source (via les hops `Received:`), reverse DNS (PTR), sujet, destinataires, date/heure.
- **Corps** : URLs (résolues si raccourcies), domaines racines, noms des pièces jointes, hash SHA256 des pièces jointes, code source HTML.

### Les familles d’outils et leur rôle

| Famille | Outils | Usage en triage |
|---|---|---|
| **Analyse d’en-têtes** | Google Admin Toolbox (Messageheader), Message Header Analyzer (MHA), mailheader.org | Visualiser le routage, les hops, les résultats SPF/DKIM |
| **Réputation IP / domaine** | IPinfo.io, URLScan.io, Talos Reputation Center | Géolocalisation, ASN, réputation, screenshot sécurisé d’une URL |
| **Extraction / décodage d’URL** | CyberChef (recette “Extract URLs”, “Defang”), URL Extractor | Révéler la destination réelle d’un lien sans cliquer |
| **Réputation de fichiers** | VirusTotal, Talos File Reputation, Reversing Labs | Vérifier un hash SHA256 sans uploader le fichier |
| **Sandbox malware** | Any.Run, Hybrid Analysis, Joe Sandbox | Analyse dynamique : connexions réseau, processus, IOCs |
| **Triage phishing** | PhishTool | Consolidation : métadonnées, pièces jointes, URLs, intégration VirusTotal, extraction de hashes et de strings |

### Le workflow d’analyse

1. **Collecte** : extraire les en-têtes bruts et le corps source.
2. **Enrichissement** : faire tourner les IPs et domaines dans IPinfo, URLScan.io et Talos.
3. **Analyse du corps** : extraire les URLs avec CyberChef, les **defang**, vérifier leur réputation.
4. **Pièces jointes** : calculer le SHA256 (`sha256sum`), chercher le hash sur VirusTotal/Talos. Si nécessaire, soumettre à une sandbox.
5. **Synthèse** : PhishTool agrège les artefacts et permet de classer le type de phishing (credential harvesting, BEC, whaling…) et de produire un rapport.

### Le defanging systématique

Tout IOC partagé dans un ticket ou un rapport doit être **defang** : `209.85.167.226` → `209[.]85[.]167[.]226`, `https://t.co/...` → `hxxps[://]t[.]co/...`. C’est un réflexe de sécurité et de professionalisme.

---

## 🛠️ Ce que j'ai manipulé

- **Machine virtuelle avec Thunderbird** : ouverture des emails suspects dans le client mail, extraction des en-têtes bruts via “View Source” / “More → View source”, copie des liens sans clic.
- **Outils d’en-têtes** : analyse du routage et des résultats d’authentification (SPF) pour identifier l’origine réelle d’un email usurpant Capital One (`capitai-one.com` → `capitalone.com`).
- **CyberChef** : extraction et defanging d’IPs et d’URLs, décodage de contenus encodés.
- **IPinfo / URLScan.io / Talos** : vérification de la réputation des IPs et domaines identifiés dans les cas pratiques.
- **VirusTotal** : recherche de hash SHA256 de pièces jointes PDF et Excel.
- **Any.Run** : lecture de rapports d’analyse dynamique pour les cas 2 et 3 (classification “Suspicious activity”, “Malicious activity”, IPs malveillantes, processus `svchost.exe` flaggé).
- **PhishTool** : exploration de l’interface de triage unifié, lecture du output “Strings” (identification de `#454326_PDF.exe`).

### Les trois cas pratiques

| Cas | Menace | Outils principaux | IOC clés identifiés |
|---|---|---|---|
| **Cas 1 — Netflix** | Usurpation Netflix, lien raccourci `t.co` | En-têtes, CyberChef (defang) | IP `209[.]85[.]167[.]226`, domaine `etekno[.]xyz`, URL `hxxps[://]t[.]co/yuxfZm8KPg` |
| **Cas 2 — Mise à jour de paiement** | PDF malveillant `Payment-updateid.pdf` | Any.Run, VirusTotal (hash SHA256) | Hash `CC6F1A...E2C24`, IPs `2[.]16[.]107[.]24` et `2[.]16[.]107[.]83`, `svchost.exe` flaggé |
| **Cas 3 — Excel exécutable** | `CBJ200620039539.xlsx` exploitant `CVE-2017-11882` | Any.Run, VirusTotal, CyberChef (defang) | Hash `5f94a6...15f3eb`, domaines `biz9holdings[.]com`, `findresults[.]site`, `ww38[.]findresults[.]site`, IPs `75[.]2[.]11[.]242` → `204[.]11[.]56[.]48` |

---

## 📌 Ce que ça m'apporte pour un SOC

- **Stack d’outils maîtrisée** : je connais les outils gratuits standards du triage de phishing (MXToolbox, MHA, IPinfo, URLScan, Talos, CyberChef, VirusTotal, Any.Run, PhishTool) et je sais lequel utiliser à chaque étape.
- **Workflow reproductible** : je peux appliquer une méthodologie en 5 étapes (collecte → enrichissement → corps → pièces jointes → synthèse) à n’importe quel email suspect, sans improvisation.
- **Réflexe “no-click”** : je sais extraire et analyser un lien ou une pièce jointe sans jamais interagir avec le contenu malveillant, en utilisant le code source, CyberChef et les sandboxes.
- **Analyse de pièces jointes par hash** : je sais calculer un SHA256 et l’utiliser pour vérifier la réputation d’un fichier sans l’uploader, ce qui protège la confidentialité de l’organisation.
- **Lecture de rapports de sandbox** : je sais extraire d’un rapport Any.Run les IPs malveillantes, les processus suspects (`svchost.exe`) et les CVE exploitées (`CVE-2017-11882`).
- **Production de rapport** : avec PhishTool, je peux agréger les artefacts, classer le type de phishing et produire un rapport exploitable par le L2 ou par l’équipe de réponse à incident.

---

## ✅ Statut

- [x] Room terminée
- [x] Write-up publié