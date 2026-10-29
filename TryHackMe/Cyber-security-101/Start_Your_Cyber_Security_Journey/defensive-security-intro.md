# 🛡️ Defensive Security Intro

**Objectif de la room :** Découvrir le rôle d'un analyste SOC (Security Operations Center) en gérant une attaque en cours contre la banque fictive "FakeBank" par le groupe de hackers "ShadowFigures".

## 📝 Résumé des tâches et réponses

### Task 1 : Introduction
- **Concept :** Le rôle d'une équipe SOC est de surveiller, détecter et répondre aux incidents de sécurité. 
- **Question :** Une équipe SOC détecte une brèche en cours. Leur priorité absolue est d'éliminer la menace immédiatement. Vrai ou faux ?
- **Réponse :** `False` (Il faut d'abord comprendre l'attaque et la contenir, l'élimination vient après l'investigation).

### Task 2 : Phase 1 - An Attack Begins
- **Action :** Analyser le tableau de bord de sécurité (SIEM) de FakeBank pour repérer l'alerte critique.
- **Question :** En examinant l'alerte "Suspicious Login", quel nom d'utilisateur est utilisé par l'attaquant ?
- **Réponse :** `dave.saunders`

### Task 3 : Phase 2 - Stopping the Attack
- **Action :** L'attaquant tente de forcer le mot de passe. Pour l'arrêter, il faut désactiver son compte ciblé via la page "Account Management".
- **Question :** Verrouillez le compte `dave.saunders` en cliquant sur le cadenas. Quel flag apparaît ?
- **Réponse :** `THM{ACCOUNT-LOCKED}`

### Task 4 : Phase 3 - Investigating the Attacker
- **Concept :** La *Threat Intelligence* (Renseignement sur les menaces) consiste à partager et documenter les techniques des attaquants pour anticiper leurs prochaines actions.
- **Action :** Mettre à jour le système de renseignement de FakeBank concernant le groupe "ShadowFigures" (la page ciblée et le nom d'utilisateur).
- **Question :** Quel flag apparaît après la mise à jour du renseignement ?
- **Réponse :** `THM{INTEL-UPDATED}`

### Task 5 : Phase 4 - Submitting Your Report
- **Concept :** Le rapport d'incident (Incident Report) est crucial pour garder une trace, comprendre ce qui s'est passé et améliorer les défenses futures.
- **Action :** Remplir le rapport final avec les informations collectées (utilisateur verrouillé et page cible).
- **Question :** Quel est l'identifiant du rapport d'incident généré (au format `SOC-2026-XXX` ou `SEC-2026-XXX`) ?
- **Réponse :** `SEC-2026-341`

## 🧠 Ce qu'il faut retenir (Blue Team)
1. **Le SOC (Security Operations Center)** est le cœur de la défense. Il utilise des outils comme un **SIEM** pour surveiller les logs.
2. **La réponse à incident** suit un processus : Détecter -> Contenir (bloquer le compte) -> Investiguer -> Rapporter.
3. **La Threat Intelligence** est l'art de connaître son ennemi (ex: le groupe ShadowFigures) pour mieux se préparer.