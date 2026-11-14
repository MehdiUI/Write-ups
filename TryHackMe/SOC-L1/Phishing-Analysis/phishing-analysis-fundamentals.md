# Phishing Analysis Fundamentals — Phishing Analysis (TryHackMe)

**Catégorie :** Blue Team / SOC / Phishing Analysis  
**Date de complétion :** 14/11/2026  
**Lien :** https://tryhackme.com/room/phishingemails1tryoe  
**Parcours :** [SOC Level 1](https://tryhackme.com/path/outline/soclevel1)

---

## 🎯 Objectif de la room

Poser les bases de l’**analyse de phishing** en SOC : comprendre l’architecture d’un email (adresse, protocoles d’envoi et de réception, en-têtes, corps), savoir lire un email brut (source) pour en extraire les artefacts suspects, reconnaître les différents types d’attaques par email (phishing, spear phishing, whaling, smishing, vishing, BEC) et adopter les bons réflexes de défense (defanging, prudence avec les pièces jointes). La room prépare directement aux rooms pratiques d’analyse d’emails de phishing du parcours SOC Level 1.

---

## 🧠 Ce que j'ai appris

### Structure d’une adresse email

Une adresse email se décompose en trois parties : **user mailbox** (ou username), **`@`**, et **domain** — par exemple `billy@johndoe.com`. Le concept remonte aux années **1970** sur ARPANET, popularisé par **Ray Tomlinson** qui a rendu le symbole `@` célèbre.

### Protocoles d’envoi et de réception

Trois protocoles régissent le cycle de vie d’un email :

- **SMTP** (*Simple Mail Transfer Protocol*) : gère l’**envoi** des emails (port 25, ou **587** pour STARTTLS sécurisé).
- **POP3** (*Post Office Protocol v3*) : **télécharge** les emails sur un seul appareil ; les messages sont supprimés du serveur sauf si l’option “Keep on server” est activée. Port sécurisé : **995**.
- **IMAP** (*Internet Message Access Protocol*) : **synchronise** les emails sur plusieurs appareils, les messages restent stockés sur le serveur. Port sécurisé : **993**.

Le trajet d’un email : le client de l’expéditeur envoie via SMTP → le serveur SMTP interroge le DNS pour localiser le domaine du destinataire → le message traverse plusieurs serveurs SMTP → il est stocké sur le serveur du destinataire → le client du destinataire le récupère via POP3 ou IMAP.

### En-têtes et corps d’un email

- **En-têtes (headers)** : métadonnées de routage et d’authentification (From, To, Subject, Date, `X-Originating-IP`, `Reply-To`, `Return-Path`). L’analyse des en-têtes bruts permet de tracer l’origine réelle d’un email et de repérer une usurpation.
- **Corps (body)** : contenu en texte brut ou HTML. Le HTML permet d’intégrer des liens et des pièces jointes. Les pièces jointes ont des en-têtes spécifiques (`Content-Type`, `Content-Disposition`, `Content-Transfer-Encoding`) et sont souvent encodées en **base64**, décodable pour analyse.

### Types de phishing et menaces par email

| Type | Description |
|---|---|
| **Spam** | Emails non sollicités en masse, pouvant contenir des malwares (*malSpam*) |
| **Phishing** | Usurpation d’une entité de confiance pour voler des données ou des identifiants |
| **Spear Phishing** | Ciblage d’individus ou d’organisations spécifiques |
| **Whaling** | Ciblage de dirigeants (CEO, CFO) |
| **Smishing** | Phishing par SMS |
| **Vishing** | Phishing par appel vocal |
| **BEC** (*Business Email Compromise*) | Compromission d’un compte interne pour tromper des tiers (ex. virements frauduleux) — menace majeure en entreprise |

**Traits communs** : expéditeur usurpé, ton urgent (“facture”, “compte suspendu”), imitation de marque connue, grammaire approximative, liens raccourcis ou pièces jointes suspectes.

### Defanging

Avant de partager un IOC (URL, email) dans un rapport ou un ticket, il faut le **defang** pour le rendre inoffensif : `http://www.badsite.com` → `hxxp[://]www[.]badsite[.]com`. C’est un réflexe standard en SOC.

---

## 🛠️ Ce que j'ai manipulé

- **Machine virtuelle d’analyse** : lancement de la VM fournie pour examiner des emails bruts (`email1.txt`, `email2.txt`).
- **Analyse d’en-têtes** : identification des champs clés (`Return-Path`, `Reply-To`, `X-Originating-IP`) et traçage de l’IP source.
- **Analyse de corps HTML** : repérage d’une URI d’image bloquée, identification d’une pièce jointe PDF (`Payment-updateid.pdf`).
- **Décodage base64** : reconstruction d’un PDF à partir des données base64 de `email2.txt` pour en extraire le contenu (`THM{BENIGN_PDF_ATTACHMENT}`) — démonstration qu’une pièce jointe “inoffensive” peut cacher un contenu.
- **Analyse d’un email de phishing** : identification de l’entité usurpée (**Home Depot**), de l’expéditeur (`support@teckbe.com`), du subject line, et conversion de l’URL en format **defanged** (`hxxp[://]t[.]teckbe[.]com`).
- **Définition du BEC** : *Business Email Compromise* — notion clé pour les entretiens et la détection en entreprise.

---

## 📌 Ce que ça m'apporte pour un SOC

- **Lecture d’un email suspect** : je sais décomposer un email (adresse, en-têtes, corps, pièce jointe) et extraire les artefacts utiles (IP source, domaine expéditeur, URL, hash de pièce jointe) pour qualifier une alerte.
- **Maîtrise des protocoles email** : je connais le rôle de SMTP, POP3, IMAP et leurs ports sécurisés (587, 995, 993), ce qui m’aide à interpréter les logs de messagerie et les en-têtes.
- **Réflexe de defanging** : je sais partager un IOC de manière sécurisée dans un ticket ou un rapport sans risque de clic accidentel.
- **Reconnaissance des techniques de phishing** : je distingue spam, phishing, spear phishing, whaling, smishing, vishing et BEC, et je peux adapter le niveau de vigilance et d’escalade en fonction du type.
- **Analyse de pièces jointes** : je comprends l’encodage base64 et la nécessité de ne jamais ouvrir une pièce jointe directement — une base pour l’analyse en sandbox.
- **Base pour les rooms pratiques** : cette room fournit le socle théorique nécessaire pour les rooms suivantes du parcours (Phishing Emails in Action, Phishing Analysis Tools), où l’analyse portera sur de vrais emails de phishing.

---

## ✅ Statut

- [x] Room terminée
- [x] Write-up publié