# 🥷 CyberChef: The Basics

**Objectif de la room :** Découvrir CyberChef, l'outil web incontournable pour manipuler, décoder et analyser des données (extraction d'IOC, conversions de formats, décodages).

## 📝 Résumé des tâches et réponses

### Task 4 & 5 : Catégories et Pratique
- **Concept :** CyberChef fonctionne avec un système de "Recipe" (Recette). On insère des données dans l'**Input**, on glisse des **Operations** (opérations) au milieu, et on obtient le résultat dans l'**Output**. 
- **Extractors :** Permet d'extraire des IP, des URL ou des emails d'un gros bloc de texte.
- **Data Format :** Encode/Décode du Base64, Base85, URL, etc.
- **Date / Time :** Convertit les timestamps UNIX en dates lisibles.

- **Questions Task 5 :**
  - **Email caché :** `hidden@cyberchef.thm`
  - **IP finissant par .232 :** `102.23.14.232`
  - **Domaine commençant par T :** `tryhackme.com`
  - **Valeur binaire de 78 :** `01001110` (d'après la table ASCII)
  - **Valeur URL encodée :** `https%3A%2F%2Ftryhackme%2Ecom%2Fr%2Fcareers`

### Task 6 : Your First Official Cook
- **Questions Task 6 :**
  - **IP commençant et finissant par 10 :** `10.10.1.10`
  - **Base64 de "Nice Room!" :** `TmljZSBSb29tIQ==`
  - **URL décodée :** `https://tryhackme.com/r/room/cyberchefbasics`
  - **Date du timestamp 1725151258 :** `Sun 1 September 2024 02:00:58 UTC`
  - **Base85 décodé :** `This is a test`

## 🧠 Ce que je retiens pour un poste d'Analyste SOC
- **Décodage rapide** : Les attaquants utilisent souvent le Base64 ou l'URL encoding pour obfusquer leurs scripts (ex: PowerShell malveillant) ou cacher des URL de phishing. CyberChef permet de les décoder instantanément en toute sécurité (sandbox).
- **Extraction d'IOC** : Face à un énorme fichier de log, l'opération "Extract IP/Email" permet d'isoler les indicateurs de compromission (IOC) en un clic.
- **Conversion de temps** : Les logs utilisent souvent des timestamps UNIX. CyberChef permet de les convertir en dates lisibles pour reconstituer la chronologie d'une attaque (Timeline).