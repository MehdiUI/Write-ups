# 🕸️ Module 14 : OWASP Top 10 (2025)

Ce module explore les risques de sécurité les plus critiques pour les applications web, selon le classement OWASP. L'objectif est de comprendre comment ces failles sont exploitées et comment les défendre.

## 📝 Rooms du module

| Room | Description | Statut | Write-up |
|---|---|---|---|
| **OWASP Top 10 2025: IAAA Failures** | Modèle IAAA et failles A01 (Broken Access Control), A07 (Authentication), A09 (Logging). | ✅ Terminé | [Lire](./owasp-iaaa-failures.md) |
| **OWASP Top 10 2025: Application Design Flaws** | Failles de conception : AS02, AS03, AS04, AS06. | ✅ Terminé | [Lire](./owasp-application-design-flaws.md) |
| **OWASP Top 10 2025: Insecure Data Handling** | Failles de gestion des données : A04, A05, A08 (désérialisation Python). | ✅ Terminé | [Lire](./owasp-insecure-data-handling.md) |

## 🧠 Ce que je retiens de ce module
- **Le modèle IAAA** : Identification, Authentification, Autorisation, Imputabilité.
- **A01 (IDOR)** : Toujours vérifier les contrôles d’accès côté serveur.
- **A09 (Logging)** : Sans logs, pas de détection.
- **AS06 (Insecure Design)** : Certaines failles sont dans l’architecture ; il faut repenser la conception.
- **A08 (Désérialisation)** : Ne jamais désérialiser des données non fiables. Un payload `pickle` peut exécuter du code.