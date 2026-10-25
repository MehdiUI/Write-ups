# Defensive Security Intro — TryHackMe

**Catégorie :** Blue Team  
**Date de sortie :** 2025  
**Date de complétion :** 20/10/2026  
**Lien :** https://tryhackme.com/room/defensivesecurityintroqW  
**Room précédente :** [SOC Role in Blue Team](./soc-role-in-blue-team.md)  
**Room suivante :** [Introduction to SIEM](./introduction-to-siem.md)

---

## 🎯 Objectif de la room

Découvrir les grands domaines de la sécurité défensive : SOC, DFIR, Threat Intelligence, Malware Analysis et SIEM.

---

## 🧠 Ce que j'ai appris

### Les 5 domaines de la sécurité défensive

| Domaine | Rôle | Lien avec le SOC |
|---|---|---|
| **SOC** | Supervision et réponse en temps réel | Cœur du métier |
| **DFIR** | Investigation post-incident, collecte de preuves | Partenaire du SOC quand un incident est confirmé |
| **Threat Intelligence** | Collecte et exploitation d'informations sur les menaces | Fournit des IOC pour enrichir la détection |
| **Malware Analysis** | Analyse statique et dynamique d'échantillons | Analyse les échantillons remontés par le SOC |
| **SIEM** | Centralisation et corrélation des logs | Plateforme commune à tous |

### Les notions clés de chaque domaine

- **SOC** : supervision continue, alertes, triage, réponse.
- **DFIR** : collecte de preuves, reconstruction d'attaque, chronologie, rapport.
- **Threat Intelligence** : IOC (Indicators of Compromise), TTP (Tactics, Techniques, Procedures), acteurs de la menace.
- **Malware Analysis** : analyse statique (sans exécution) et dynamique (en sandbox).
- **SIEM** : collecte, normalisation, corrélation, alertes.

> 💡 **Point clé retenu** : la sécurité défensive n'est pas un seul métier, c'est un **écosystème de spécialités** qui collaborent autour du SOC.

---

## 🛠️ Concepts manipulés

| Domaine | Rôle |
|---|---|
| SOC | Supervision et réponse en temps réel |
| DFIR | Investigation post-incident |
| Threat Intelligence | Connaissance des menaces |
| Malware Analysis | Analyse des échantillons malveillants |
| SIEM | Corrélation des logs et alertes |

---

## 🔍 Le lien entre ces domaines

J'ai retenu le scénario suivant, qui illustre comment les 5 domaines collaborent :

1. Le **SOC** détecte une alerte (ex : connexion suspecte).
2. Le **SIEM** fournit les logs corrélés.
3. La **Threat Intelligence** enrichit l'alerte avec des IOC connus (IP malveillante, hash).
4. Si l'incident est confirmé, le **DFIR** intervient pour l'investigation.
5. Si un malware est identifié, le **Malware Analysis** l'analyse.

---

## 📌 Ce que je retiens pour un poste d'analyste SOC

- Un analyste SOC est au **carrefour de plusieurs spécialités** : il doit connaître leur rôle et savoir quand escalader.
- La Threat Intelligence et le DFIR sont des **partenaires naturels** du SOC.
- Comprendre l'écosystème permet de mieux **qualifier une alerte** et de **l'orienter** vers le bon interlocuteur.

---

## ✅ Statut

- [x] Room terminée
- [x] Write-up publié

---

*Write-up rédigé dans le cadre de ma préparation au poste d'Analyste SOC junior.*