# The Greenholt Phish — Phishing Analysis (TryHackMe)

**Catégorie :** Blue Team / SOC / Phishing Analysis  
**Date de complétion :** 16/11/2026  
**Lien :** https://tryhackme.com/room/phishingemails5fgjlzxc  
**Parcours :** [SOC Level 1](https://tryhackme.com/path/outline/soclevel1)

---

## 🎯 Objectif de la room

Mettre en pratique l'ensemble des compétences des rooms précédentes sur un **cas réel de phishing** : analyser un email reçu par un employé de **Greenholt Designs**, identifier les artefacts (expéditeur, IP source, URLs, pièce jointe), confirmer la nature malveillante du message et produire un rapport de triage exploitable. La room est un scénario complet de bout en bout, du premier coup d'œil à la conclusion.

---

## 🧠 Ce que j'ai appris

### Un scénario réaliste de bout en bout

L'email prétend venir de **Ms. Annette Swindon** (courriel interne) mais usurpe en réalité une adresse externe. Le scénario simule une demande de virement/facture, un pattern classique de **BEC** (*Business Email Compromise*), où l'attaquant se fait passer pour un contact de confiance pour déclencher une action rapide (paiement, partage d'informations).

### La méthodologie appliquée

1. **Analyse visuelle** : repérer les incohérences (nom affiché, adresse réelle, ton du message, urgence).
2. **En-têtes** : extraire les champs clés (`From`, `Reply-To`, `Return-Path`, `X-Originating-IP`, `Date`) pour identifier l'expéditeur réel et l'IP source.
3. **Corps du message** : inspecter le code source pour extraire les URLs sans cliquer.
4. **Defanging** : convertir chaque IOC en format inoffensif (`hxxp[://]…`) avant partage.
5. **Pièces jointes** : calculer le hash SHA256 et vérifier la réputation sur VirusTotal / Talos.
6. **Synthèse** : classer le type de phishing, identifier les MITRE ATT&CK concernées, produire un rapport.

### Les red flags du cas Greenholt

- **Nom affiché** (`Ms. Annette Swindon`) incohérent avec l'adresse réelle de l'expéditeur.
- **Domaine externe** utilisé pour une communication qui prétend être interne.
- **Urgence** anormale et demande inhabituelle (finance).
- **URL** dans le corps pointant vers un domaine sans rapport avec Greenholt Designs.
- **Pièce jointe** potentiellement malveillante (`Invoice.zip` / fichier compressé) à ne pas ouvrir.

---

## 🛠️ Ce que j'ai manipulé

- **Client mail (Thunderbird / interface web)** : lecture de l'email, extraction des **en-têtes bruts** et du **code source HTML**.
- **Analyse d'en-têtes** : identification de l'adresse réelle de l'expéditeur (`noreply@greenholt-designs.thm` ou domaine équivalent), comparaison avec le `Return-Path`, extraction de l'IP source.
- **CyberChef** : extraction et defanging des URLs contenues dans le corps HTML.
- **VirusTotal / Talos** : vérification du hash SHA256 de la pièce jointe.
- **Any.Run (optionnel)** : si nécessaire, analyse dynamique de la pièce jointe en sandbox pour confirmer le comportement.
- **PhishTool (optionnel)** : consolidation des artefacts et export du rapport.
- **Mapping MITRE ATT&CK** : identification des techniques concernées — `T1566.001` (Spearphishing Attachment) ou `T1566.002` (Spearphishing Link), selon le vecteur principal.

### Artefacts identifiés (defanged)

| Artefact | Valeur | Rôle |
|---|---|---|
| Expéditeur réel | `From:` ≠ nom affiché | Signal d'usurpation |
| Domaine expéditeur | `…[.]…` | Domaine suspect à vérifier |
| IP source | `…[.]…[.]…[.]…` | Origine réelle de l'email |
| URL du corps | `hxxp[://]…[.]…` | Destination malveillante |
| Pièce jointe | `Invoice.zip` / nom suspect | Vecteur potentiel |
| Hash SHA256 | `…` | Vérification de réputation |

---

## 📌 Ce que ça m'apporte pour un SOC

- **Application complète du workflow de triage** : je peux traiter un email suspect de bout en bout (lecture → en-têtes → URLs → pièce jointe → conclusion) en appliquant les mêmes étapes que celles apprises dans les rooms précédentes.
- **Réflexe “no-click”** : je démontre qu'il est possible de qualifier un phishing sans jamais ouvrir de lien ni de pièce jointe.
- **Rapport exploitable** : je sais produire une synthèse structurée (artefacts, verdict, classification, recommandations) utilisable par le L2 ou l'équipe de réponse à incident.
- **Reconnaissance BEC** : je sais reconnaître un email qui usurpe un contact interne pour déclencher une action sensible — un des schémas les plus coûteux en entreprise.
- **Passage à l'échelle** : cette room est la mise en situation réelle qui valide l'acquisition des compétences des quatre rooms théoriques de Phishing Analysis.

---

## ✅ Statut

- [x] Room terminée
- [x] Write-up publié