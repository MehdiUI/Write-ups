# Network Security Essentials — Network Security Monitoring (TryHackMe)

**Catégorie :** Blue Team / SOC / Network Security Monitoring  
**Date de complétion :** 23/11/2026  
**Lien :** https://tryhackme.com/room/networksecurityessentials  
**Parcours :** [SOC Level 1](https://tryhackme.com/path/outline/soclevel1)

---

## 🎯 Objectif de la room

Cette room pose les **fondations défensives du métier d'analyste SOC** : comprendre comment un réseau d'entreprise est structuré, où se trouve le **périmètre**, et comment exploiter les **logs de sécurité** (firewall, WAF, VPN, IDS) pour reconstruire une intrusion de bout en bout. La particularité de la room réside dans son **challenge final** : un mois de logs de périmètre à analyser pour déterminer les techniques utilisées par un adversaire, et surtout **s'il a réussi à franchir le périmètre**. C'est un exercice de **corrélation multi-sources** qui simule le quotidien d'un analyste N1/N2.

---

## 🧠 Ce que j'ai appris

### Composants réseau et pertinence défensive

Chaque composant d'un réseau produit des logs qui racontent une partie de l'histoire. Savoir **quel composant regarder** et **pour quel type d'événement** est un réflexe fondamental :

| Composant | Rôle | Ce qu'on y cherche |
|---|---|---|
| **Postes utilisateurs** | Point d'entrée (phishing, malware) | Processus, connexions sortantes, premiers signes de C2 |
| **Serveurs fichiers/BDD** | Données critiques | Accès massifs, sauvegardes anormales, exfiltration |
| **Serveurs applicatifs** (web, mail, VPN) | Exposés à Internet | Scans, SQLi, XSS, brute-force, exploits |
| **Active Directory / Auth** | Colonne vertébrale identitaire | Échecs de connexion, horaires inhabituels, élévation de privilèges |
| **Routeurs / Switches** | Tissu de communication | Flux, changements de config, compromission → MITM |
| **Firewall / Périmètre** | Gardien (allow/deny) | **Port scans, brute-force, tentatives d'exploit** — les **premiers indicateurs** |

### Visibilité : logs host-centric vs network-centric

La room insiste sur une distinction opérationnelle :

- **Host-centric** (logs OS, applications, EDR) : *ce qui se passe **sur** une machine* — processus, fichiers, registre, utilisateurs connectés. Idéal pour le **forensic détaillé**.
- **Network-centric** (firewall, IDS/IPS, proxy, VPN) : *ce qui se passe **entre** les machines* — qui parle à qui, quand, où, comment. Idéal pour **scoper large** (mouvement latéral, C2, exfiltration).

**Règle empirique retenue** : *"Inside the room = host logs ; in/out of the building = network logs"*. Et surtout : **corréler les deux** pour reconstruire une timeline.

### Le périmètre : première ligne de défense, première source de preuves

Le périmètre (firewall, routeurs, DMZ, passerelle VPN) est l'endroit où l'on voit **les premières tentatives** : scans, brute-force, exploitation, beaconing malveillant, sorties inhabituelles. L'analyste doit constamment se demander : **ce qui devrait être exposé** vs **ce qui l'est réellement**.

### Patterns de détection sur les logs de périmètre

La room formalise plusieurs **signatures comportementales** exploitables directement dans un SIEM :

| Pattern | Signature dans les logs | Source typique |
|---|---|---|
| **Port scan** | Une source → nombreux ports/destinations → répétition de `BLOCK` en peu de temps | Firewall |
| **Brute-force** | Une source → un endpoint de login → nombreux `FAILED_AUTH` | VPN, AD |
| **Exploitation web** | Signatures SQLi/XSS/traversal dans les requêtes bloquées | WAF / IDS |
| **Beaconing C2** | Connexions **périodiques et régulières** vers une destination fixe | Firewall / Proxy |
| **Exfiltration** | Volume sortant anormal, souvent HTTP/HTTPS vers un hôte inconnu | Firewall / Proxy |

### La chaîne d'attaque reconstituée dans le challenge

Le scénario final de la room suit une **kill chain défensive** classique, que j'ai pu reconstituer en corrélant firewall, VPN et IDS :

> **Reconnaissance externe** → **Brute-force VPN** → **Accès VPN réussi** (attribution d'une IP `10.8.0.x`) → **Scan interne** → **Mouvement latéral SMB (445)** → **Hôte interne compromis** → **Beaconing C2 (4444)** → **Exécution de commandes** → **Exfiltration HTTP (80/8080)**

Chaque étape laisse une trace dans un log différent. Le travail de l'analyste consiste à **recoller les morceaux** pour prouver (ou infirmer) le succès de l'intrusion.

---

## 🛠️ Ce que j'ai manipulé

Toutes les investigations ont été menées en **ligne de commande** sur la machine Ubuntu fournie (`~/Desktop/Perimeter_logs/`), avec les fichiers `task6/` (firewall_logs.txt, waf_logs.txt, vpn_logs.txt) puis `challenge/` (firewall.log, ids_alerts.log, vpn_auth.log).

- **Analyse firewall (port scan)** : `grep "BLOCK"` dans les logs firewall → identification de l'IP **`203.0.113.10`** comme source du scan de ports (tentatives répétées sur des ports variés).
- **Analyse WAF** : comptage et filtrage des requêtes `BLOCK` → une **seule IP source** responsable de toutes les attaques web bloquées : **`198.51.100.12`**.
- **Analyse VPN (brute-force)** : filtrage des `FAILED_AUTH` avec `wc -l` → **90 tentatives échouées** ; identification de l'IP suspecte **`45.137.22.13`** comme source de l'attaque.
- **Reconnaissance la plus active (challenge)** : agrégation des `BLOCK` par IP source (`cut`, `sort`, `uniq -c`) → l'IP **`203.0.113.45`** ressort comme la plus active en reconnaissance externe.
- **Corrélation multi-sources** : croisement des timestamps entre `firewall.log`, `vpn_auth.log` et `ids_alerts.log` pour **confirmer la chronologie** de l'attaque et vérifier si le périmètre a été franchi.

---

## 📌 Ce que ça m'apporte pour un SOC

- **Réflexe "composant → log → question"** : face à une alerte, je sais immédiatement **où regarder** : un scan suspect → firewall ; un brute-force → VPN/AD ; une exploitation web → WAF ; un beaconing → proxy/firewall.
- **Corrélation multi-sources** : je ne me limite plus à un seul fichier de logs — je **recoupe firewall, VPN et IDS** pour reconstruire une timeline et distinguer un bruit de fond d'une **intrusion réelle**.
- **Analyse de logs en ligne de commande** : je maîtrise les patterns `grep`/`cut`/`sort`/`uniq -c`/`wc -l` pour extraire rapidement des statistiques d'un fichier volumineux — une compétence directement transférable à un SIEM ou à un EDR.
- **Lecture de la kill chain côté défense** : je peux expliquer comment une intrusion se déroule (**recon → brute-force → accès → latéralisation → C2 → exfil**) et **quel log révèle chaque étape**.
- **Notion de périmètre** : je comprends pourquoi le périmètre est à la fois la **première ligne de défense** et la **première source de preuves**, et je sais évaluer l'écart entre l'exposition théorique et l'exposition réelle.
- **Valeur pour un employeur** : cette room démontre que je suis capable de **traiter un mois de logs de périmètre**, d'en extraire des indicateurs exploitables (IPs, comptages, séquences) et de rendre un **verdict argumenté** sur le succès ou l'échec d'une attaque — exactement ce qu'on attend d'un analyste SOC N1/N2 en supervision réseau.

---

## ✅ Statut

- [x] Room terminée
- [x] Write-up publié