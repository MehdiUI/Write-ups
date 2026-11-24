# Network Discovery Detection — Network Security Monitoring (TryHackMe)

**Catégorie :** Blue Team / SOC / Network Security Monitoring  
**Date de complétion :** 24/11/2026  
**Lien :** https://tryhackme.com/room/networkdiscoverydetection  
**Parcours :** [SOC Level 1](https://tryhackme.com/path/outline/soclevel1)

---

## 🎯 Objectif de la room

Apprendre à **détecter les activités de découverte réseau** (*network discovery*) dans des logs réels (exports Zeek/firewall au format CSV), en distinguant les scans **externes** des scans **internes**, les scans **horizontaux** des scans **verticaux**, et en identifiant les techniques de scan (ping sweep, TCP SYN, UDP). La room met l'accent sur le **contexte** : un scan n'est pas forcément malveillant (les défenseurs scannent aussi), et le rôle du SOC est de différencier un scan autorisé d'un scan malveillant à l'aide de l'inventaire, des allowlists et de la Threat Intelligence[reference:0][reference:1].

---

## 🧠 Ce que j'ai appris

### Pourquoi la découverte réseau est difficile à détecter

Attaquants **et** défenseurs scannent le réseau. Un scan de vulnérabilités interne (Nessus, Qualys) ressemble trait pour trait à un scan de reconnaissance malveillant. Le SOC doit donc s'appuyer sur trois leviers pour réduire les faux positifs et prioriser les vraies menaces[reference:2][reference:3] :

- **Allowlisting** : exclure les scanners internes connus des règles de détection.
- **Threat Intelligence** : élever la sévérité d'un scan provenant d'une IP connue comme malveillante.
- **Règles génériques** : conserver des règles de détection de scan comportemental, et utiliser la TI pour moduler la sévérité plutôt que pour bloquer.

### Externe vs Interne : la distinction la plus importante

| Type | Source → Destination | Sévérité | Signification |
|---|---|---|---|
| **Scan externe** | IP publique → actifs exposés de l'organisation | **Basse** | Reconnaissance (TA0043) ; l'attaquant n'est pas encore entré |
| **Scan interne** | IP privée → IP privée | **Haute** | Discovery (TA0007) ; l'attaquant a déjà un pied dans le réseau → risque de mouvement latéral |

Un scan interne est bien plus grave qu'un scan externe : il signifie qu'un hôte est déjà compromis et cherche à cartographier le réseau interne[reference:4].

### Horizontal vs Vertical

- **Scan horizontal** : même port sur plusieurs IP destinations. Objectif : trouver tous les hôtes exposant un service donné (ex. SMB sur le port 445). Indicateur : **plusieurs IP destinations, un seul port destination**[reference:5].
- **Scan vertical** : même IP destination sur plusieurs ports. Objectif : énumérer les services ouverts sur un hôte précis. Indicateur : **une seule IP destination, plusieurs ports destination**[reference:6].
- **Scan mixte** : combinaison des deux, pour une cartographie complète[reference:7].

### Mécanismes de scan et leur détection

| Technique | Fonctionnement | Détection / Limite |
|---|---|---|
| **Ping Sweep (ICMP)** | Envoie des echo requests à de nombreuses IP pour trouver les hôtes vivants | Souvent bloqué par les firewalls ; filtre `network.transport: icmp` dans Kibana |
| **TCP SYN Scan** | Envoie un SYN ; un SYN-ACK indique un port ouvert. Discret et rapide | Difficile à détecter ; `conn_state = S0` (pas de réponse) dans les logs Zeek[reference:8] |
| **UDP Scan** | Envoie des paquets UDP ; pas de réponse ICMP « port unreachable » = port potentiellement ouvert | Lent et peu fiable (timeouts) ; `network.transport: udp` |

---

## 🛠️ Ce que j'ai manipulé

- **Environnement** : VM TryHackMe avec trois exports de logs au format CSV dans `~/Downloads/logs/` (`log-session-0.csv`, `log-session-1.csv`, `log-session-2.csv`), et une instance **Kibana** accessible via le navigateur (`http://<IP>:5601`)[reference:9].
- **Linux CLI** : `head` pour prévisualiser la structure, `cut -d',' -f<colonnes>` pour isoler les champs (source/destination IP et port), `sort -u`, `uniq -c`, `grep -oE` pour extraire des plages d'IP, `wc -l` pour compter les entrées[reference:10][reference:11].
- **Analyse des logs** :
  - Identification du fichier contenant le scan **interne** (`log-session-2.csv`, avec une IP source privée `192.168.230.x` scannant d'autres IP privées)[reference:12][reference:13].
  - Comptage des entrées du scan interne (`2276` entrées après déduction de l'en-tête)[reference:14].
  - Identification de l'IP externe responsable d'un scan **externe** (`203.0.113.25`)[reference:15].
  - Identification de la plage IP scannée en **horizontal** (`203.0.113.0/24`, port 0 / ICMP)[reference:16][reference:17].
  - Identification de l'IP cible d'un scan **vertical** (`192.168.230.145`) et des ports scannés (80, 443, 445, etc.)[reference:18].
- **Kibana (Elastic Stack)** : exploration de l'interface **Discover**, ajout de colonnes (`source.ip`, `destination.ip`, `destination.port`), et filtrage via KQL :
  - `network.transport: icmp` pour les ping sweeps[reference:19].
  - `network.transport: udp` pour les scans UDP (peu d'événements = pas de scan UDP significatif)[reference:20].
  - Filtre sur une IP source et une IP destination spécifiques pour isoler un scan vertical et vérifier le `conn_state` (`S0` = SYN sans réponse, signature d'un TCP SYN scan)[reference:21].
- **Mapping MITRE ATT&CK** :
  - `T1595` — Active Scanning (phase Reconnaissance, pour les scans externes).
  - `T1046` — Network Service Discovery (phase Discovery, pour les scans internes)[reference:22][reference:23].

---

## 📌 Ce que ça m'apporte pour un SOC

- **Triage de scans réseau** : je sais qualifier un scan en quelques secondes à partir d'un export de logs, en distinguant externe/interne, horizontal/vertical, et en identifiant la technique (ICMP, SYN, UDP).
- **Priorisation par le contexte** : je comprends pourquoi un scan interne est bien plus grave qu'un scan externe, et je peux argumenter une escalade en m'appuyant sur la phase MITRE ATT&CK correspondante (Discovery vs Reconnaissance).
- **Réduction des faux positifs** : je sais que les scanners internes légitimes existent, et je peux proposer des allowlists ou un enrichissement Threat Intelligence plutôt que de bloquer aveuglément.
- **Double compétence CLI + SIEM** : je suis à l'aise avec `grep`/`cut`/`awk` pour un premier triage rapide sur un export brut, et avec **Kibana/KQL** pour une investigation plus visuelle et itérative.
- **Lecture de logs Zeek/firewall** : je connais les champs clés (`source.ip`, `destination.ip`, `destination.port`, `conn_state`) et les patterns qui trahissent un scan (`S0`, port 0 pour ICMP, absence de réponse UDP).
- **Réflexe “scan-first”** : je sais que la découverte réseau est souvent la **première étape** observable d'une attaque en SOC, et qu'elle mérite une investigation même quand elle semble anodine[reference:24].

---

## ✅ Statut

- [x] Room terminée
- [x] Write-up publié