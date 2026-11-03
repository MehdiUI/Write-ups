# Search Skills — Cyber Security 101 (TryHackMe)

**Catégorie :** OSINT & Recherche  
**Date de sortie :** 2024  
**Date de complétion :** 29/10/2026  
**Lien :** https://tryhackme.com/room/searchskills  
**Parcours :** [Cyber Security 101](https://tryhackme.com/path/outline/cybersecurity101)  
**Room précédente :** [Defensive Security Intro](./defensive-security-intro.md)

---

## 🎯 Objectif de la room

Apprendre à utiliser efficacement Internet et les services spécialisés (OSINT) pour la cybersécurité.

---

## 🧠 Ce que j'ai appris

Savoir où chercher est aussi important que savoir quoi chercher. J'ai découvert plusieurs outils :
- **Shodan** : moteur de recherche pour les objets connectés et serveurs.
- **VirusTotal** : analyse de fichiers suspects via plusieurs antivirus.
- **CVE** : base de données des vulnérabilités connues.
- **MAN** : pages de manuel Linux pour comprendre les commandes.
- **GitHub** : dépôt de PoC (Proof of Concept) pour les vulnérabilités.

---

## 🖥️ Lignes de commande utilisées

Certaines recherches ont été faites via des simulateurs en ligne (TryScanMe, TryDetectMe), mais voici les commandes Linux qui auraient pu être utilisées :

| Commande | Description |
|---|---|
| `nslookup example.com` | Résoudre un nom de domaine en adresse IP. |
| `whois example.com` | Obtenir les informations d'enregistrement d'un domaine. |
| `man nc` | Lire le manuel de la commande `nc` (netcat). |
| `curl -s https://example.com` | Récupérer le contenu d'une page web. |

*Note : l'exercice pratique a utilisé des interfaces web (Shodan, VirusTotal, base CVE) plutôt que des commandes.*

---

## 📌 Ce que je retiens pour un poste d'analyste SOC

- **L'OSINT** : Je peux retrouver l'auteur d'un mail, l'IP d'un serveur, ou vérifier si un fichier est malveillant.
- **Les CVE** : Si un scanner de vulnérabilités remonte une CVE, je peux chercher sur GitHub s'il existe un PoC pour comprendre le risque réel.
- **Les informations trouvées sur Internet ne sont pas toujours fiables** : Il faut croiser les sources.

---

## ✅ Statut

- [x] Room terminée
- [x] Write-up publié

---

*Write-up rédigé dans le cadre de ma préparation au poste d'Analyste SOC junior.*