# Man-in-the-Middle Detection — Network Security Monitoring (TryHackMe)

**Catégorie :** Blue Team / SOC / Network Security Monitoring  
**Date de complétion :** 26/11/2026  
**Lien :** https://tryhackme.com/room/mitmdetection  
**Parcours :** [SOC Level 1](https://tryhackme.com/path/outline/soclevel1)

---

## 🎯 Objectif de la room

Cette room plonge l'analyste dans une **investigation MITM complète** à partir d'une capture réseau unique. Le scénario : un portail de connexion d'entreprise (Acme Corp) fait l'objet d'une attaque en trois étapes enchaînées — **ARP Spoofing → DNS Spoofing → SSL Stripping** — aboutissant au vol d'identifiants en clair. L'objectif est d'apprendre à **repérer les empreintes de chaque technique** dans le trafic, de les **corréler** pour reconstruire la chaîne d'attaque, et de produire une preuve exploitable (filtre, numéro de paquet, valeur extraite).

---

## 🧠 Ce que j'ai appris

### Le modèle en deux temps du MITM

Un MITM se décompose toujours en deux phases :
1. **Interception** : l'attaquant s'insère dans le chemin de communication (ARP spoofing, DNS spoofing, rogue AP).
2. **Manipulation / Déchiffrement** : il dégrade ou contourne le chiffrement (SSL stripping) ou injecte du contenu (fausse page de login).

**Point clé pour le SOC** : chaque phase laisse une trace dans un protocole différent. La détection ne repose pas sur un seul filtre magique, mais sur une **chaîne de preuves** à recoller.

### Détection de l'ARP Spoofing (couche 2)

ARP n'a **aucune authentification** : n'importe quel hôte peut répondre « *192.168.10.1 is at <MA_MAC>* » et empoisonner les caches.

**Indicateurs dans Wireshark :**

| Indicateur | Filtre / Observation | Résultat dans la capture |
|---|---|---|
| Deux MAC différentes revendiquent la même IP (gateway) | `arp.opcode == 2 && arp.src.proto_ipv4 == 192.168.10.1` | **2 MAC distinctes** pour `192.168.10.1` |
| Volume anormal de réponses ARP depuis la MAC suspecte | `arp.opcode == 2 && arp.src.proto_ipv4 == 192.168.10.1 && eth.src == 02:fe:fe:fe:55:55` | **14 paquets** de spoofing |
| Gratuitous ARP (réponses non sollicitées) | `arp.isgratuitous && arp.opcode == 2 && arp.src.proto_ipv4 == 192.168.10.1` | **2 réponses gratuites** |
| MAC légitime de la gateway (référence) | `arp && eth.src == 02:aa:bb:cc:00:01` | **10 paquets** légitimes |
| Alerte native Wireshark | `arp.duplicate-address-detected` | Conflit IP↔MAC confirmé |

**MAC usurpatrice identifiée :** `02:fe:fe:fe:55:55` — elle se fait passer pour la gateway `192.168.10.1`.

### Détection du DNS Spoofing (couche 7)

Une fois en position de MITM, l'attaquant forge des **réponses DNS** pour rediriger le domaine de login (`corp-login.acme-corp.local`) vers **sa propre IP**.

**Filtres et observations :**

- `dns.flags.response == 1 && dns.qry.name == "corp-login.acme-corp.local"` → **211 réponses DNS** pour ce domaine.
- Exclure le résolveur légitime (`8.8.8.8`) : `dns.flags.response == 1 && ip.src != 8.8.8.8 && dns.qry.name == "corp-login.acme-corp.local"` → **2 réponses** provenant d'une source inattendue.
- **IP retournée par la réponse forgée :** `192.168.10.55` — c'est l'adresse de l'attaquant, vers laquelle la victime est redirigée.

**Lien avec l'ARP spoofing :** la MAC source de ces réponses DNS correspond à `02:fe:fe:fe:55:55` — la même que celle qui usurpait la gateway. La corrélation est directe.

### Détection du SSL Stripping (couche 7)

L'attaquant **rétrograde HTTPS en HTTP** : la victime croit se connecter au portail, mais la requête part en clair vers l'IP de l'attaquant.

**Preuves dans la capture :**

- `tls.handshake.type == 1 && tls.handshake.extensions_server_name == "corp-login.acme-corp.local"` → des `ClientHello` existent (la victime **a tenté** TLS), mais aucun handshake complet ne suit vers le vrai serveur.
- `http.request.method == "POST" && http.host == "corp-login.acme-corp.local"` → **1 requête POST** vers le portail, envoyée **en HTTP simple**.
- **Mot de passe extrait en clair :** `Secret123!` (visible dans `HTML Form URL Encoded` → champ `password`).

### La chaîne d'attaque complète

> **ARP Spoofing** (l'attaquant se place entre la victime et la gateway)  
> → **DNS Spoofing** (le domaine de login résout vers l'IP de l'attaquant)  
> → **SSL Stripping** (la victime est forcée en HTTP, ses identifiants partent en clair)

Chaque étape est **détectable indépendamment**, mais c'est leur **enchaînement chronologique** qui constitue la preuve d'une intrusion active.

---

## 🛠️ Ce que j'ai manipulé

Investigation menée dans **Wireshark** sur la capture `network-traffic.pcap` fournie dans la VM (`/home/ubuntu/Desktop/mitm_traffic/`).

- **ARP Spoofing** :
  - Filtres `arp`, `arp.opcode == 2`, `arp.isgratuitous`, `arp.duplicate-address-detected`.
  - Comptage des paquets légitimes (**10**) vs usurpés (**14**) depuis la MAC `02:fe:fe:fe:55:55`.
  - Identification des **2 MAC** revendiquant `192.168.10.1` et des **2 gratuitous ARP**.
- **DNS Spoofing** :
  - Filtre `dns.flags.response == 1 && dns.qry.name == "corp-login.acme-corp.local"` (**211** réponses).
  - Exclusion de `8.8.8.8` pour isoler les **2 réponses forgées**.
  - Lecture du champ `Answers` → **IP forgée `192.168.10.55`**.
- **SSL Stripping** :
  - Vérification des `ClientHello` TLS pour le domaine cible (tentative de chiffrement).
  - Filtre `http.request.method == "POST" && http.host == "corp-login.acme-corp.local"` (**1** requête).
  - Suivi du flux HTTP → extraction du mot de passe `Secret123!` dans le formulaire.
- **Corrélation** : recoupement des numéros de paquets, des MAC et des IP entre les trois phases pour confirmer qu'il s'agit du **même attaquant** et de la **même victime**.

---

## 📌 Ce que ça m'apporte pour un SOC

- **Réflexe de détection en chaîne** : je ne cherche plus un seul filtre « miracle » — je sais que le MITM laisse des traces à **chaque couche** (ARP en L2, DNS en L7, HTTP en L7) et qu'il faut les **corréler** pour qualifier l'incident.
- **Maîtrise des filtres Wireshark critiques** : `arp.duplicate-address-detected`, `arp.isgratuitous`, `dns.flags.response`, `tls.handshake.type`, `http.request.method` — je peux reproduire cette investigation sur n'importe quelle capture.
- **Lecture de la kill chain MITM** : je peux expliquer comment un attaquant passe d'une position d'écoute à un **vol d'identifiants**, et à quelle étape chaque preuve apparaît.
- **Extraction de preuve exploitable** : je sais documenter un incident avec le **filtre utilisé, le comptage, le numéro de paquet et la valeur extraite** — le format attendu dans un ticket SOC.
- **Vision défensive** : je comprends pourquoi la **segmentation réseau**, le **DHCP snooping / Dynamic ARP Inspection**, et le **HSTS** sont des contre-mesures directes à ce type d'attaque.
- **Valeur pour un employeur** : cette room démontre que je suis capable de traiter une **attaque MITM réelle** de bout en bout, de l'interception à l'exfiltration, et d'en tirer une conclusion argumentée — une compétence directement applicable en supervision réseau N1/N2.

---

## ✅ Statut

- [x] Room terminée
- [x] Write-up publié