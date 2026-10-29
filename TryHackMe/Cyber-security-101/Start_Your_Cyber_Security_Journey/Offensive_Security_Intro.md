# 🗡️ Offensive Security Intro

**Objectif de la room :** Comprendre ce qu'est la sécurité offensive et réaliser son premier "hack" légal sur une application bancaire factice (FakeBank).

## 📝 Résumé des tâches et réponses

### Task 1 : Think like a Hacker!
- **Concept :** La sécurité offensive consiste à penser comme un attaquant pour trouver les failles avant les vrais hackers.
- **Question :** Quel terme décrit la simulation des actions d'un hacker pour trouver des faiblesses ?
- **Réponse :** `Offensive Security`

### Task 2 : Starting the Lab
- **Action :** Lancement du site web factice "FakeBank" dans l'environnement virtuel.
- **Question :** Quel est le numéro de compte bancaire dans l'application FakeBank ?
- **Réponse :** `8881`

### Task 3 : Find Hidden Pages
- **Concept :** Les développeurs laissent parfois des pages cachées accessibles. On utilise un outil de "brute force" de répertoires pour les trouver.
- **Outil utilisé :** `dirb`
- **Commande :** `dirb http://fakebank.thm`
- **Question :** Dirb a trouvé `http://fakebank.thm/images`. Quelle est l'autre URL cachée ?
- **Réponse :** `http://fakebank.thm/bank-transfer`

### Task 4 : Attack the Admin Page
- **Action :** Utilisation de la page cachée `/bank-transfer` pour accéder à un panneau d'administration mal sécurisé et ajouter 2000$ au compte `8881`.
- **Question :** Lorsque le solde devient positif, une pop-up avec du texte vert apparaît. Quel est ce texte (en MAJUSCULES) ?
- **Réponse :** `BANK-HACKED`

## 🧠 Ce qu'il faut retenir
- L'énumération (trouver des fichiers/dossiers cachés) est une étape cruciale en pentest.
- Les outils comme `dirb` ou `gobuster` automatisent cette recherche.
- Une mauvaise configuration (comme un panneau d'admin accessible sans mot de passe) peut mener à une compromission totale.