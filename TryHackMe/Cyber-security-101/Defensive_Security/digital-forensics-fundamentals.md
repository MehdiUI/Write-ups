# 🔍 Digital Forensics Fundamentals

**Objectif de la room :** Découvrir les bases de l'investigation numérique (forensique), les méthodologies d'acquisition de preuves et l'analyse des métadonnées (documents et images).

## 📝 Résumé des tâches et réponses

### Task 1 : Introduction to Digital Forensics
- **Concept :** La forensique numérique est l'application de méthodes scientifiques pour enquêter sur des cybercrimes. L'objectif est de trouver et d'analyser les preuves sur les appareils numériques pour les autorités légales.
- **Question :** À quelle équipe les forces de l'ordre ont-elles confié l'affaire ?
- **Réponse :** `digital forensics`

### Task 2 : Digital Forensics Methodology
- **Concept :** Le NIST définit un processus en 4 phases :
  1. **Collection** (Collecte des appareils sans altérer les données).
  2. **Examination** (Filtrage des données pour extraire ce qui est pertinent).
  3. **Analysis** (Corrélation des preuves pour tirer des conclusions).
  4. **Reporting** (Rédaction du rapport final pour la justice).
- **Question 1 :** Quelle phase consiste à corréler les données collectées pour en tirer des conclusions ?
  - **Réponse :** `Analysis`
- **Question 2 :** Quelle phase consiste à extraire les données d'intérêt des preuves collectées ?
  - **Réponse :** `Examination`

### Task 3 : Evidence Acquisition
- **Concept :** Pour que les preuves soient recevables au tribunal, il faut :
  - Une **autorisation légale**.
  - Une **Chain of Custody** (document qui trace qui a touché la preuve, quand et où).
  - Un **Write Blocker** (outil physique qui empêche l'ordinateur d'enquête de modifier accidentellement le disque dur du suspect).
- **Question 1 :** Quel outil est utilisé pour garantir l'intégrité des données lors de la collecte ?
  - **Réponse :** `write blocker`
- **Question 2 :** Quel est le nom du document qui contient tous les détails des preuves numériques collectées ?
  - **Réponse :** `chain of custody`

### Task 4 : Windows Forensics
- **Concept :** Sur Windows, on fait des copies exactes appelées **images forensiques**.
  - **Disk Image** : Copie du disque dur (non volatile).
  - **Memory Image** : Copie de la RAM (volatile, contient les processus en cours et connexions réseau, à capturer en priorité).
  - *Outils : FTK Imager, Autopsy, DumpIt, Volatility.*
- **Question :** Quel type d'image forensique est prélevé pour collecter les données volatiles du système d'exploitation ?
  - **Réponse :** `Memory image`

### Task 5 : Practical Example of Digital Forensics
- **Concept :** L'analyse des métadonnées (EXIF pour les images, PDF metadata) permet de retrouver l'auteur d'un document, la date de création, le modèle d'appareil photo et même les coordonnées GPS de la prise de vue.
- **Question 1 :** En utilisant `pdfinfo`, trouvez l'auteur du fichier PDF (ransom-letter.pdf).
  - **Réponse :** `Ann Gree She`
- **Question 2 :** En utilisant `exiftool`, trouvez le nom de la rue où l'image a été prise.
  - **Réponse :** `Hanover Square`
- **Question 3 :** Quel est le nom du modèle de l'appareil photo utilisé ?
  - **Réponse :** `Canon EOS 5D Mark III`

## 🧠 Ce que je retiens pour un poste d'Analyste SOC
- **La préservation de la preuve** : Une preuve altérée est inutilisable. L'utilisation d'un Write Blocker et d'une Chain of Custody stricte est la base du travail forensique.
- **La mémoire avant tout** : Lors d'une saisie, il faut toujours capturer la RAM (Memory image) en premier, car elle contient les données volatiles (malwares en cours d'exécution, connexions C2) qui disparaîtront si la machine est éteinte.
- **Les métadonnées sont une mine d'or** : Les documents (PDF, Word) et les images (EXIF) contiennent des informations cachées (auteur, GPS, logiciel utilisé) qui peuvent permettre de géolocaliser un suspect ou de prouver qu'un document est un faux.