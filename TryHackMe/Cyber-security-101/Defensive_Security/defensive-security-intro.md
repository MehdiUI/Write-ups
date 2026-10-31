# 🛡️ Defensive Security Intro

**Objectif de la room :** Découvrir le rôle d'un analyste SOC (Security Operations Center) en gérant une attaque en cours contre la banque fictive "FakeBank" par le groupe de hackers "ShadowFigures".

## 📝 Résumé des tâches et réponses

### Task 1 : Introduction
- **Question :** Une équipe SOC détecte une brèche en cours. Leur priorité absolue est d'éliminer la menace immédiatement. Vrai ou faux ?
- **Réponse :** `False`

### Task 2 : Phase 1 - An Attack Begins
- **Question :** En examinant l'alerte "Suspicious Login", quel nom d'utilisateur est utilisé par l'attaquant ?
- **Réponse :** `dave.saunders`

### Task 3 : Phase 2 - Stopping the Attack
- **Question :** Verrouillez le compte `dave.saunders` en cliquant sur le cadenas. Quel flag apparaît ?
- **Réponse :** `THM{ACCOUNT-LOCKED}`

### Task 4 : Phase 3 - Investigating the Attacker
- **Question :** Quel flag apparaît après la mise à jour du renseignement sur ShadowFigures ?
- **Réponse :** `THM{INTEL-UPDATED}`

### Task 5 : Phase 4 - Submitting Your Report
- **Question :** Quel est l'identifiant du rapport d'incident généré ?
- **Réponse :** `SEC-2026-341`

## 🧠 Ce que je retiens pour un poste d'Analyste SOC
1. **Le SOC (Security Operations Center)** est le cœur de la défense. Il utilise des outils comme un **SIEM** pour surveiller les logs.
2. **La réponse à incident** suit un processus : Détecter -> Contenir (bloquer le compte) -> Investiguer -> Rapporter.