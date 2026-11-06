# 🕸️ Module 14 : OWASP Top 10 (2025)

Ce module explore les risques de sécurité les plus critiques pour les applications web, selon le classement OWASP (Open Worldwide Application Security Project). L'objectif est de comprendre comment ces failles sont exploitées et comment les défendre.

## 📝 Rooms du module

| Room | Description | Statut | Write-up |
|---|---|---|---|
| **OWASP Top 10 2025: IAAA Failures** | Comprendre le modèle IAAA et les failles A01 (Broken Access Control), A07 (Authentication), A09 (Logging). | ✅ Terminé | [Lire](./owasp-iaaa-failures.md) |
| **OWASP Top 10 2025: Application Design Flaws** | Failles de conception : AS02 (Misconfig), AS03 (Supply Chain), AS04 (Cryptographic), AS06 (Insecure Design). | ✅ Terminé | [Lire](./owasp-application-design-flaws.md) |
| **OWASP Top 10 2025: Insecure Data Handling** | Failles de gestion des données (Injection, Software Integrity, etc.). | ⏳ À venir | — |

## 🧠 Ce que je retiens de ce module
- **Le modèle IAAA** : C'est le squelette de la sécurité applicative.
- **A01 (IDOR)** : Les développeurs font souvent confiance au client (l'URL). L'analyste SOC doit se méfier des changements d'ID soudains dans les logs.
- **A09 (Logging)** : Une application qui ne logue pas est une application aveugle.
- **AS06 (Insecure Design)** : Certaines failles sont dans l'ADN de l'application. En tant qu'analyste, je dois apprendre à repérer les requêtes anormales (ex: User-Agent usurpé) pour détecter l'exploitation de ces failles.