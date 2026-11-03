# Firewall Fundamentals — Cyber Security 101 (TryHackMe)

**Catégorie :** Security Solutions  
**Date de sortie :** 2024  
**Date de complétion :** 02/11/2026  
**Lien :** https://tryhackme.com/room/firewallfundamentals  
**Parcours :** [Cyber Security 101](https://tryhackme.com/path/outline/cybersecurity101)  
**Room précédente :** [Logs Fundamentals](../Defensive_Security/logs-fundamentals.md)  
**Room suivante :** [Introduction to SIEM](./introduction-to-siem.md)

---

## 🎯 Objectif de la room

Comprendre les différents types de pare-feux et savoir où configurer des règles sur Windows et Linux.

---

## 🧠 Ce que j'ai appris

### Les types de pare-feux
- **Stateless** : Filtre paquet par paquet sans se souvenir des connexions précédentes (rapide mais basique).
- **Stateful** : Garde une "state table" (table d'état) pour suivre les connexions établies.
- **Proxy** : Agit comme un intermédiaire (couche 7) et inspecte le contenu des paquets.
- **NGFW (Next-Generation)** : Le plus avancé, fait de l'inspection profonde, du décryptage SSL et de l'analyse heuristique.

### Les règles
Une règle est composée de : Source, Destination, Port, Protocole, Action (Allow/Deny/Forward) et Direction (Inbound/Outbound).

---

## 🖥️ Lignes de commande utilisées

### Windows (interface graphique `wf.msc`)
La console **Windows Defender Firewall with Advanced Security** (`wf.msc`) a été utilisée pour inspecter les règles entrantes. Aucune commande en ligne n'a été nécessaire.

### Linux (UFW)
| Commande | Description |
|---|---|
| `sudo ufw status` | Afficher l'état du pare-feu. |
| `sudo ufw enable` | Activer le pare-feu. |
| `sudo ufw disable` | Désactiver le pare-feu. |
| `sudo ufw default deny outgoing` | Politique par défaut : refuser tout le trafic sortant. |
| `sudo ufw default allow outgoing` | Politique par défaut : autoriser tout le trafic sortant. |
| `sudo ufw deny 22/tcp` | Bloquer le trafic SSH entrant. |
| `sudo ufw status numbered` | Lister les règles avec numéros. |
| `sudo ufw delete 2` | Supprimer la règle numéro 2. |

*Note : l'outil `iptables` a été mentionné, mais les exercices pratiques ont utilisé `ufw`.*

---

## 📌 Ce que je retiens pour un poste d'analyste SOC

- **La lecture des logs de pare-feu** : En tant qu'analyste, je verrai passer des alertes de paquets bloqués. Savoir qu'une règle "Deny" est en place m'aide à comprendre si une attaque a échoué ou non.
- **L'audit** : Vérifier qu'un serveur critique n'a pas son port SSH ouvert à tout le monde (règle "Any") est un réflexe de base.
- **Une règle mal configurée peut bloquer tout un service** (faux positif de blocage).

---

## ✅ Statut

- [x] Room terminée
- [x] Write-up publié

---

*Write-up rédigé dans le cadre de ma préparation au poste d'Analyste SOC junior.*