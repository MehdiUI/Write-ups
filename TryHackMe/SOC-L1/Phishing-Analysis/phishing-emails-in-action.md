# Phishing Emails in Action — Phishing Analysis (TryHackMe)

**Catégorie :** Blue Team / SOC / Phishing Analysis  
**Date de complétion :** 14/11/2026  
**Lien :** https://tryhackme.com/room/phishingemails2rytmuv  
**Parcours :** [SOC Level 1](https://tryhackme.com/path/outline/soclevel1)

---

## 🎯 Objectif de la room

Passer de la théorie à la **pratique** : analyser des échantillons réels d’emails de phishing et apprendre à identifier les indicateurs subtils qui rendent un email malveillant crédible. La room couvre six scénarios (annulation de commande PayPal, suivi de colis, téléchargement de document, compte suspendu Netflix, achat récent Apple, livraison DHL), chacun illustrant une combinaison de techniques : usurpation d’expéditeur, raccourcissement d’URL, pixels de tracking, harvesting d’identifiants, pièces jointes malveillantes et chaînes de redirection.

---

## 🧠 Ce que j'ai appris

### Les techniques d’attaque récurrentes

Chaque échantillon de la room combine plusieurs couches d’illusion. Les techniques observées de manière transversale :

- **Usurpation d’expéditeur (Sender Spoofing)** : le nom d’affichage (`service@paypal.com`) ne correspond pas à l’adresse d’enveloppe réelle (`gibberish@sultanbogor.com`). C’est le premier réflexe de vérification.
- **Usurpation HTML** : le corps de l’email est conçu en HTML pour reproduire fidèlement l’identité visuelle d’une marque légitime (PayPal, Netflix, Apple, DHL, OneDrive/Adobe).
- **Ingénierie sociale par l’urgence** : “annulez votre commande”, “votre compte est suspendu”, “téléchargement expire aujourd’hui” — l’objectif est de forcer une action rapide sans vérification.
- **Manipulation de liens** : URL raccourcies, chaînes de redirection, texte affiché différent de la destination réelle.
- **Harvesting d’identifiants** : pages de connexion factices (faux Microsoft, faux Adobe) qui capturent les identifiants saisis.
- **Pixels de tracking** : images minuscules (ex. `Tracking.png`) qui notifient l’expéditeur à l’ouverture de l’email.
- **Pièces jointes malveillantes** : PDF ou Excel contenant des liens intégrés ou des macros, utilisés pour contourner les filtres de liens.
- **Typosquatting et fautes** : erreurs dans les noms de marque, les domaines ou l’adresse email.

### Les méthodes d’investigation

La room insiste sur une règle : **ne jamais cliquer**. Toutes les investigations se font sur le **code source** de l’email.

- **Inspection des en-têtes bruts** : comparer le `From:` (nom d’affichage) avec l’enveloppe réelle, suivre les champs `Received:` pour tracer l’origine.
- **Révélation de la destination d’un lien** : survol du lien ou inspection de la balise `<a href>` dans le code HTML pour voir l’URL réelle.
- **Expansion d’URL raccourcies** : utilisation d’outils d’unshortening pour révéler la destination finale.
- **Détection des pixels de tracking** : recherche de petites images externes (ex. `Tracking.png`) qui déclenchent une requête à l’ouverture.
- **Analyse des pièces jointes en sandbox** : ouverture dans un environnement isolé (type Any.Run) plutôt que sur la machine de production.
- **Suivi des chaînes de redirection** : observation contrôlée des étapes menant à une page de harvesting.

### Les drapeaux rouges (red flags)

- Adresse expéditeur qui ne correspond pas à la marque ou au compte du destinataire.
- Destinataire inhabituel ou en **BCC** (pour masquer les autres cibles).
- Corps vide avec uniquement une pièce jointe (pour éviter l’analyse du contenu textuel).
- Lien dont le texte affiché ne correspond pas à la destination réelle.
- Fautes de grammaire ou d’orthographe dans une communication de marque.
- Urgence anormale ou menace de suspension de compte.

---

## 🛠️ Ce que j'ai manipulé

- **Analyse de six échantillons de phishing** : chaque email a été examiné via son code source, sans interaction avec les liens ou pièces jointes.

| Scénario | Techniques identifiées | Point d’investigation clé |
|---|---|---|
| **Cancel your PayPal order** | Usurpation d’expéditeur, URL raccourcie, HTML imitant PayPal | Le bouton “Cancel the order” pointe vers une URL raccourcie ; l’inspection du HTML révèle une redirection vers un domaine sans rapport |
| **Track your package** | Usurpation, pixel tracking, manipulation de lien | Image `Tracking.png` intégrée comme pixel de tracking ; le lien mène vers un domaine suspect (`devret[.]xyz`) |
| **Select your email provider to view document** | Chaîne de redirection multi-étapes, harvesting d’identifiants | Le bouton mène à une fausse page de connexion Microsoft/Adobe |
| **Your Account Is on Hold (Netflix)** | Usurpation, langage d’urgence, pièce jointe PDF avec lien intégré | La pièce jointe contourne l’analyse des liens en intégrant l’URL malveillante dans le PDF |
| **Your recent purchase (Apple)** | Usurpation, destinataire en BCC, corps vide avec pièce jointe `.dot` | La pièce jointe contient une image liée à des mots-clés malveillants |
| **DHL shipping notice** | Usurpation de l’identité DHL, pièce jointe Excel exécutable | La pièce jointe déclenche un payload qui affiche une erreur (comportement malveillant) |

- **Defanging** : conversion des IOC en format inoffensif (`devret[.]xyz`) avant partage dans le writeup.
- **Lecture de code HTML** : identification des balises `<a href>`, des images intégrées et des redirections.

---

## 📌 Ce que ça m'apporte pour un SOC

- **Triage d’email de phishing** : je sais décomposer un email suspect en artefacts vérifiables (expéditeur réel, destination des liens, pièces jointes, pixels) sans jamais interagir avec le contenu malveillant.
- **Réflexe “source first”** : face à un email douteux, je consulte systématiquement le code source et les en-têtes avant toute autre action — une discipline directement applicable en L1.
- **Reconnaissance des chaînes d’attaque** : je distingue une simple usurpation visuelle d’un harvesting d’identifiants multi-étapes, ce qui me permet d’évaluer le risque réel et de prioriser l’escalade.
- **Analyse de pièces jointes** : je comprends pourquoi une pièce jointe apparemment inoffensive (PDF, Excel) peut être plus dangereuse qu’un lien, et pourquoi l’analyse doit se faire en sandbox.
- **Vocabulaire opérationnel** : spoofing, tracking pixel, credential harvesting, URL shortener, defanging — employés correctement dans un rapport ou un ticket.
- **Passage à l’échelle** : les six échantillons couvrent des scénarios courants (e-commerce, livraison, compte suspendu, achat), ce qui me donne une base de patterns réutilisable pour des emails réels en production.

---

## ✅ Statut

- [x] Room terminée
- [x] Write-up publié