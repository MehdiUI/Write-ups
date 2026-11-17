# Snapped Phish-ing Line!!! — Phishing Emails in Action (TryHackMe)

**Catégorie :** Blue Team / SOC / Email Security  
**Date de complétion :** 17/11/2026  
**Lien :** https://tryhackme.com/room/snappedphishingline
**Parcours :** [SOC Level 1](https://tryhackme.com/path/outline/soclevel1)

---

## 🎯 Objectif de la room

Passer de la théorie à la **pratique de l'investigation** : analyser un lot d'emails suspects réels et déterminer, pour chacun, s'il s'agit de phishing, de spam ou d'un message légitime. La room met l'accent sur l'**analyse des en-têtes**, l'**extraction d'indicateurs de compromission (IOC)**, l'inspection des **pièces jointes** et des **URLs**, ainsi que sur le raisonnement de triage qu'un analyste SOC doit mener face à une boîte de réception compromise.

---

## 🧠 Ce que j'ai appris

### Méthodologie d'analyse d'un email suspect

Face à un email douteux, j'applique désormais une **checklist systématique** :

1. **Expéditeur** : le domaine `From` correspond-il réellement à l'organisation prétendue ? Attention aux domaines look-alike (`micros0ft.com`, `paypa1.com`).
2. **En-têtes complets** : analyser `Received`, `Return-Path`, `Reply-To` et les résultats d'authentification (SPF/DKIM/DMARC).
3. **Corps du message** : urgence artificielle, fautes d'orthographe, incohérences de ton, liens masqués.
4. **URLs** : survol du lien pour révéler l'URL réelle, détection de typosquatting, de redirections et de domaines récemment enregistrés.
5. **Pièces jointes** : type réel vs extension affichée, encodage, macros, exécutables déguisés.

### Analyse des en-têtes

- **`Received`** : lire la chaîne **de bas en haut** pour retracer le chemin réel du message et repérer le premier serveur non fiable.
- **`Return-Path` vs `From`** : une incohérence est un signal fort (usurpation, mailing-list, spoofing).
- **`Reply-To`** : un `Reply-To` pointant vers un domaine différent de l'expéditeur est un classique du **Business Email Compromise (BEC)**.
- **Résultats d'authentification** : `spf=fail`, `dkim=none`, `dmarc=fail` confirment souvent une usurpation — mais un `pass` ne garantit pas la légitimité (domaine compromis ou nouvellement enregistré).

### Analyse des URLs

- **Techniques d'obfuscation** : sous-domaines trompeurs (`login.microsoft.com.phish.ru`), caractères homoglyphes, URLs raccourcies, redirections en chaîne.
- **Vérification défensive** : ne jamais cliquer — utiliser des outils comme **URLScan.io**, **VirusTotal** ou un **sandbox** de navigateur pour résoudre l'URL.
- **Indices** : domaine en `.xyz`/`.top`/`.tk`, absence de HTTPS, paramètres de tracking suspects, page de login imitant un service connu.

### Analyse des pièces jointes

- **Double extension** : `facture.pdf.exe`, `cv.docx.scr` — l'extension réelle est la dernière.
- **Archives** : un `.zip`/`.rar` protégé par mot de passe (souvent fourni dans le corps du mail) est un vecteur classique pour contourner les filtres.
- **Documents Office avec macros** : `.docm`, `.xlsm` — vérifier la présence de macros malveillantes (obfuscation, `AutoOpen`, appels `Shell`).
- **Encodage base64** : un binaire encodé dans le corps ou en pièce jointe doit être décodé et analysé en sandbox.

### Indicateurs de compromission (IOC)

| Type | Exemple |
|---|---|
| Domaine expéditeur | `secure-paypal-verify.com` |
| URL malveillante | `hxxp://malicious[.]site/login` |
| Hash de pièce jointe | SHA256 du fichier |
| IP d'envoi | IP du relais SMTP suspect |
| Sujet type | "URGENT: votre compte sera suspendu" |

---

## 🛠️ Ce que j'ai manipulé

- **Analyse d'en-têtes** : lecture de la chaîne `Received` pour identifier le serveur d'origine et détecter une incohérence entre `From`, `Return-Path` et `Reply-To`.
- **Résultats d'authentification** : interprétation de `spf=softfail` / `dmarc=fail` comme signaux d'usurpation, corrélation avec le domaine expéditeur.
- **Extraction d'URLs** : identification d'une URL de phishing imitant un service de paiement, avec un domaine look-alike et un chemin de login factice.
- **Inspection de pièces jointes** : détection d'un fichier `.scr`/`.exe` déguisé, analyse d'une archive protégée par mot de passe.
- **Triage** : classement des emails en **phishing / spam / légitime** avec justification basée sur les preuves collectées (domaine, en-têtes, contenu, IOC).
- **Documentation** : rédaction d'une **fiche d'incident** par email analysé (expéditeur, sujet, IOC, verdict, recommandation).

---

## 📌 Ce que ça m'apporte pour un SOC

- **Réflexe de triage** : je sais analyser un email suspect de bout en bout (expéditeur → en-têtes → contenu → URLs → pièces jointes) et rendre un verdict argumenté.
- **Lecture des en-têtes** : je maîtrise `Received`, `Return-Path`, `Reply-To` et les résultats SPF/DKIM/DMARC, et je sais repérer les incohérences typiques du spoofing et du BEC.
- **Extraction d'IOC** : je peux produire une liste d'indicateurs exploitable par un SIEM ou un EDR (domaines, URLs, hashes, IPs).
- **Analyse défensive des URLs et pièces jointes** : je connais les techniques d'obfuscation et les bons réflexes (sandbox, URLScan, VirusTotal) sans jamais exposer mon poste.
- **Rédaction d'incident** : je sais documenter une analyse de manière claire et reproductible — une compétence clé pour un analyste SOC N1/N2.
- **Valeur pour un employeur** : cette room démontre ma capacité à traiter une **file d'emails suspects** de manière méthodique, à prioriser et à escalader avec des preuves — exactement le quotidien d'un analyste phishing.

---

## ✅ Statut

- [x] Room terminée
- [x] Write-up publié