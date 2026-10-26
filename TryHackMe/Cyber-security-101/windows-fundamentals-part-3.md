# Windows Fundamentals Part 3 — Cyber Security 101 (TryHackMe)

**Catégorie :** Windows  
**Date de sortie :** Juillet 2021  
**Date de complétion :** 26/10/2026  
**Lien :** https://tryhackme.com/room/windowsfundamentals3  
**Parcours :** [Cyber Security 101](https://tryhackme.com/path/outline/cybersecurity101)  
**Room précédente :** [Windows Fundamentals Part 2](./windows-fundamentals-part-2.md)

---

## 🎯 Objectif de la room

Découvrir les outils de sécurité intégrés à Windows : Windows Update, Windows Security (Defender, Firewall), BitLocker et le service de cliché instantané des volumes (Volume Shadow Copy).

---

## 🧠 Ce que j'ai appris

### Windows Update

- **Rôle** : Télécharger et installer les correctifs de sécurité (patchs). C'est la première ligne de défense contre les vulnérabilités connues.
- **Patch Management** : Le fait de ne pas mettre à jour un système expose à des attaques (ex : la faille EternalBlue exploitée par WannaCry).

### Windows Security (Windows Defender Security Center)

C'est le centre de sécurité intégré de Windows qui regroupe plusieurs protections :
- **Virus & threat protection** : Gère Windows Defender (l'antivirus natif). Permet de lancer des analyses (Quick, Full) et de consulter l'historique des menaces bloquées.
- **Firewall & network protection** : Le pare-feu natif qui filtre le trafic réseau entrant et sortant. Il peut être configuré par profil (Domain, Private, Public).
- **App & browser control** : Protège contre les applications et sites web malveillants (SmartScreen).
- **Device security** : Fonctionnalités de sécurité matérielle, comme la **Core Isolation** (isolation du noyau) et le **TPM** (Trusted Platform Module).

### BitLocker

- **Rôle** : Chiffrement complet du disque dur. Si un ordinateur portable est volé, les données sont illisibles sans la clé de déchiffrement.
- **Utilité en entreprise** : Protège contre les fuites de données physiques.

### Volume Shadow Copy (VSS)

- **Rôle** : Le service de cliché instantané des volumes crée des copies de sauvegarde automatiques ou manuelles des fichiers et du système (ce qui permet d'utiliser "Restauration du système").
- **Lien avec la cybersécurité** : Les ransomwares ciblent souvent le Volume Shadow Copy pour supprimer les sauvegardes (via la commande `vssadmin delete shadows`) et empêcher la victime de restaurer ses fichiers sans payer.

---

## 📌 Ce que je retiens pour un poste d'analyste SOC

- **Patching** : Un système non mis à jour est une cible facile. En SOC, surveiller les machines qui ne reçoivent pas les mises à jour est crucial.
- **Windows Defender** : Savoir lire les logs de Defender (menaces détectées et bloquées) est indispensable.
- **Volume Shadow Copy** : Si un analyste voit une alerte de suppression de clichés instantanés, c'est souvent le signe d'une attaque par ransomware en cours.
- **BitLocker** : Comprendre le chiffrement des postes de travail aide à évaluer le risque en cas de perte ou de vol.

---

## ✅ Statut

- [x] Room terminée
- [x] Write-up publié

---

*Write-up rédigé dans le cadre de ma préparation au poste d'Analyste SOC junior.*