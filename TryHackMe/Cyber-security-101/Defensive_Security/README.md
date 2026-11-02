# 🛡️ Module 10 : Defensive Security

Ce module pose les bases de la sécurité défensive (Blue Team). Il est indispensable pour comprendre comment les entreprises se protègent, détectent les intrusions et répondent aux incidents.

## 📝 Rooms du module

| Room | Description | Statut | Write-up |
|---|---|---|---|
| **SOC Fundamentals** | Découverte du SOC, des rôles (L1, L2, L3) et des processus (Triage, 5 W). | ✅ Terminé | [Lire](./soc-fundamentals.md) |
| **Digital Forensics Fundamentals** | Méthodologie d'investigation, acquisition de preuves et analyse de métadonnées. | ✅ Terminé | [Lire](./digital-forensics-fundamentals.md) |
| **Incident Response Fundamentals** | Cycle de vie d'un incident (PICERL), gestion de crise et Playbooks. | ✅ Terminé | [Lire](./incident-response-fundamentals.md) |
| **Logs Fundamentals** | Analyse des journaux Windows (Event Viewer) et Web (Access logs). | ✅ Terminé | [Lire](./logs-fundamentals.md) |

## 🧠 Ce que je retiens de ce module
- **Le rôle du SOC** : C'est le centre névralgique de la défense. Son but est de détecter (Detect) et de répondre (Respond).
- **Les 3 piliers** : Un SOC mature repose sur l'équilibre entre les **Personnes** (analystes), les **Processus** (triage, escalade) et la **Technologie** (SIEM, EDR).
- **La forensique** : L'investigation numérique exige une rigueur absolue. La collecte des données volatiles (RAM) et l'analyse des métadonnées sont cruciales.
- **La réponse à incident** : Le framework SANS (PICERL) est la référence. Contenir (Containment) une menace avant de l'éradiquer.
- **L'analyse de logs** : Que ce soit via l'Event Viewer ou `grep`, les logs sont la clé pour reconstituer le puzzle d'une attaque et comprendre les actions de l'attaquant.