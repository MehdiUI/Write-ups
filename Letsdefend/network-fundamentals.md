# Network Fundamentals — LetsDefend

**Catégorie :** Réseau  
**Date de sortie :** 2024  
**Date de complétion :** 25/10/2026  
**Lien :** https://app.letsdefend.io/training/lessons/network-fundamentals

---

## 🎯 Objectif de la room

Acquérir les fondamentaux réseau nécessaires à un analyste SOC : types de réseaux, topologies, modèle OSI, équipements, adressage IP et NAT.

---

## 🧠 Ce que j'ai appris

### Les types de réseaux

Les réseaux sont classés selon leur taille géographique[reference:25] :
- **PAN** (Personal Area Network) : très petite portée (ex : Bluetooth).
- **LAN** (Local Area Network) : réseau local (maison, bureau).
- **MAN** (Metropolitan Area Network) : échelle d'une ville.
- **WAN** (Wide Area Network) : très grande échelle (Internet).
- **CAN** (Campus Area Network) : intermédiaire, pour un campus ou une entreprise.

### Les topologies réseau

La topologie décrit la disposition physique ou logique des équipements[reference:26] :
- **Bus** : tous les équipements partagent une ligne unique.
- **Star** : tous les équipements sont connectés à un hub central.
- **Ring** : les équipements forment une boucle.
- **Mesh** : les équipements sont interconnectés (redondance).
- **Tree** : hiérarchie de topologies en étoile.
- **Point-to-Point** : connexion directe entre deux équipements.

### Le modèle OSI

Le modèle OSI décompose les communications réseau en 7 couches (Physique, Liaison, Réseau, Transport, Session, Présentation, Application)[reference:27].

### Les équipements réseau

La room présente les équipements comme le hub, le switch, le routeur, etc., et leur rôle dans le réseau.

### Le modèle TCP/IP

Le modèle TCP/IP est le modèle pratique utilisé sur Internet (4 couches : Accès réseau, Internet, Transport, Application).

### L'adressage IP

La room couvre l'adressage IPv4 (classes, adresses privées/publiques) et IPv6.

### Le NAT (Network Address Translation)

Le NAT permet de traduire des adresses IP privées en adresses publiques pour accéder à Internet[reference:28].

---

## 📌 Ce que je retiens pour un poste d'analyste SOC

- Comprendre les types de réseaux et les topologies aide à visualiser l'infrastructure.
- Le modèle OSI et TCP/IP sont essentiels pour analyser les communications.
- L'adressage IP et le NAT sont partout dans les logs ; savoir les interpréter est crucial.
- Les équipements réseau (switch, routeur) sont des points de collecte de logs importants.

---

## ✅ Statut

- [x] Room terminée
- [x] Write-up publié