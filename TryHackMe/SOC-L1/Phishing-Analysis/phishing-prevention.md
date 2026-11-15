# Phishing Prevention — Phishing Analysis (TryHackMe)

**Catégorie :** Blue Team / SOC / Email Security  
**Date de complétion :** 15/11/2026  
**Lien :** https://tryhackme.com/room/phishingemails4gkxh  
**Parcours :** [SOC Level 1](https://tryhackme.com/path/outline/soclevel1)

---

## 🎯 Objectif de la room

Passer de la détection à la **prévention** : comprendre les standards d’authentification email (**SPF**, **DKIM**, **DMARC**, **S/MIME**) qui permettent à une organisation de vérifier la légitimité d’un expéditeur et l’intégrité d’un message[reference:0]. La room combine théorie et pratique : analyse d’enregistrements DNS, lecture de résultats d’authentification dans les en-têtes, investigation de trafic **SMTP** dans **Wireshark**, inspection de pièces jointes suspectes et panorama des contrôles organisationnels (sandboxing, filtrage, formation).

---

## 🧠 Ce que j'ai appris

### SPF (Sender Policy Framework)

**Objectif** : authentifier les serveurs d’envoi autorisés pour un domaine, afin de prévenir l’usurpation d’adresse expéditeur[reference:2].

**Mécanisme** : le serveur destinataire interroge l’enregistrement SPF du domaine expéditeur dans le DNS et compare l’IP source à la liste des IP autorisées.

**Syntaxe d’un enregistrement** :
- `v=spf1` : version du protocole.
- `ip4:` / `include:` : IP ou domaine autorisé.
- `-all` / `~all` : politique par défaut pour les sources non listées (`-all` = rejet strict, `~all` = SoftFail).

**Résultats de vérification** :
- **Pass / Neutral / None** : email accepté.
- **SoftFail / PermError** : email marqué comme suspect (**Flag**).
- **Fail / TempError** : email rejeté[reference:3].

**Outil** : **SPF Surveyor** pour visualiser un enregistrement SPF, et **Google Admin Toolbox (Messageheader)** pour lire les résultats d’authentification dans les en-têtes[reference:4].

### DKIM (DomainKeys Identified Mail)

**Objectif** : garantir l’authenticité et l’intégrité d’un message via une **signature cryptographique**[reference:5].

**Mécanisme** : le serveur expéditeur signe le message avec une **clé privée** ; le serveur destinataire récupère la **clé publique** dans le DNS (enregistrement `v=DKIM1; k=rsa; p=<clé>`) et vérifie la signature.

**Erreur courante** : `permerror` — signature ou enregistrement DKIM invalide/absent (`no key for signature`)[reference:7].

**Outil** : **DKIM Inspector / Validator (Dmarcian)** pour vérifier la santé et la syntaxe d’un enregistrement DKIM[reference:8].

### DMARC (Domain-based Message Authentication, Reporting, and Conformance)

**Objectif** : aligner les résultats SPF et DKIM sur le domaine **From visible** et définir une politique de traitement en cas d’échec[reference:9].

**Principe d’alignement** : soit SPF aligné, soit DKIM aligné, suffit à satisfaire l’exigence d’authentification DMARC.

**Politiques (`p=`)** :
| Politique | Niveau de protection |
|---|---|
| `p=none` | Aucune action (monitoring seul) |
| `p=quarantine` | Placement en quarantaine / spam |
| **`p=reject`** | **Blocage complet** — protection maximale[reference:11] |

**Enregistrement type** : `v=DMARC1; p=reject; rua=mailto:postmaster@domaine.com`[reference:12].

**Outil** : **Domain Checker (Dmarcian)** pour analyser la configuration SPF/DKIM/DMARC d’un domaine.

### S/MIME (Secure/Multipurpose Internet Mail Extensions)

**Objectif** : ajouter **confidentialité** et **intégrité** aux emails via le chiffrement et les signatures numériques[reference:13].

- **Signature numérique** : authentifie l’expéditeur, garantit la non-répudiation et vérifie l’intégrité du message.
- **Chiffrement** : protège la **confidentialité** du contenu — seul le destinataire prévu peut lire le message (via sa clé privée)[reference:14].

### Analyse du trafic SMTP (Wireshark)

La room met en pratique l’analyse d’une capture `traffic.pcap` pour investiguer des réponses SMTP réelles.

- **Filtre clé** : `smtp.response.code` — isole les paquets contenant un code de réponse SMTP numérique[reference:17].
- **Codes observés** :
  - `220` : *Service ready*.
  - **`553`** : *Requested action not taken: mailbox name not allowed* — blocage par **spamhaus.org**[reference:18].
  - `552` : blocage pour **raison de sécurité**.
- **Inspection des pièces jointes** :
  - Filtre `imf` pour identifier le client mail utilisé (ex. **Microsoft Outlook Express 6.00.2600.0000**).
  - Détection d’une pièce jointe `document.zip` non délivrée car l’hôte `212.253.25.152` ne répondait pas.
  - Identification d’une pièce jointe `attachment.scr` encodée en **base64** — un exécutable déguisé[reference:19].

### Défenses organisationnelles

- **Sandboxing** : analyse comportementale d’un fichier suspect dans un environnement isolé, sans risque pour les systèmes de production[reference:20].
- **Filtrage email** : passerelles de sécurité, blocage des pièces jointes exécutables, analyse des URLs.
- **Formation utilisateur** : sensibilisation au phishing, simulations d’attaque.
- **Défense en profondeur** : combinaison de SPF + DKIM + DMARC + S/MIME + filtrage + sandbox + sensibilisation.

---

## 🛠️ Ce que j'ai manipulé

- **Enregistrements DNS** : lecture d’un enregistrement SPF (`v=spf1 ip4:127.0.0.1 include:_spf.google.com -all`) pour identifier les **3 domaines** autorisés à envoyer pour le compte de TryHackMe, et association du résultat **SoftFail** à l’action **Flag**[reference:21].
- **En-têtes DKIM** : analyse d’un header en `permerror` avec la raison **no key for signature**[reference:22].
- **Politique DMARC** : identification de **`p=reject`** comme politique offrant la protection maximale par blocage[reference:23].
- **S/MIME** : identification du **chiffrement** comme composant garantissant que seul le destinataire prévu peut lire le message[reference:24].
- **Wireshark** :
  - Filtre **`smtp.response.code`** pour isoler les réponses SMTP.
  - Comptage des réponses `220 Service ready` (**19 paquets**).
  - Identification du code **553** pour un blocage spamhaus, avec le message complet *Requested action not taken: mailbox name not allowed (553)*.
  - Comptage des messages bloqués avec le code **552** pour raison de sécurité (**6 messages**)[reference:25].
- **Inspection d’emails** :
  - **512 paquets SMTP** disponibles pour analyse.
  - Pièce jointe **`document.zip`** (packet 270), avec l’IP **`212.253.25.152`** en non-réponse.
  - Filtre `imf` pour identifier **Microsoft Outlook Express 6.00.2600.0000** comme client d’envoi.
  - Encodage **base64** d’une pièce jointe **`attachment.scr`** — un exécutable potentiellement malveillant[reference:26].
- **Défenses** : identification du **sandboxing** comme technique permettant d’observer le comportement d’un fichier suspect en toute sécurité[reference:27].

---

## 📌 Ce que ça m'apporte pour un SOC

- **Lecture des en-têtes d’authentification** : je sais interpréter les résultats SPF, DKIM et DMARC dans un header email pour déterminer si un message est usurpé ou légitime — un réflexe de triage fondamental.
- **Compréhension de la chaîne de confiance email** : je peux expliquer comment SPF, DKIM et DMARC fonctionnent ensemble, et pourquoi `p=reject` est la politique la plus protectrice.
- **Analyse de trafic SMTP** : je maîtrise les filtres Wireshark essentiels (`smtp.response.code`, `imf`) pour investiguer des rejets, des pièces jointes suspectes et des échecs de livraison.
- **Détection de pièces jointes malveillantes** : je sais reconnaître un encodage **base64** et un fichier `.scr` comme des signaux d’alerte, et je comprends le rôle du **sandboxing** pour les analyser sans risque.
- **Vision défensive complète** : je connais les contrôles organisationnels (SPF/DKIM/DMARC, S/MIME, filtrage, sandbox, formation) et je peux argumenter leur complémentarité dans une stratégie de prévention du phishing.
- **Valeur pour un employeur** : cette room démontre que je ne me limite pas à “ouvrir un email suspect” — je sais auditer la configuration de sécurité email d’un domaine et proposer des remédiations concrètes (passer en `p=reject`, activer DKIM, déployer S/MIME).

---

## ✅ Statut

- [x] Room terminée
- [x] Write-up publié