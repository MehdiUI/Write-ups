# Junior Security Analyst Intro — SOC Level 1 (TryHackMe)

**Catégorie :** Blue Team / SOC  
**Date de sortie :** 2024  
**Date de complétion :** 07/11/2026  
**Lien :** https://tryhackme.com/room/jrsecanalystintrouxo  
**Parcours :** [SOC Level 1](https://tryhackme.com/path/outline/soclevel1)

---

## 🎯 1. Le cours

Cette room est une simulation immersive. Tu endosses le rôle d'un analyste SOC junior (L1) et tu dois gérer des alertes de sécurité via un tableau de bord interactif.

Le quotidien d'un analyste SOC est rythmé par les **tickets** (alertes à traiter). Le processus est toujours le même :
1.  **Détecter** : Repérer une alerte dans le SIEM/dashboard.
2.  **Analyser** : Comprendre ce qui se passe (quelle IP, quel utilisateur, quel type d'attaque).
3.  **Escalader** : Si c'est une vraie menace (True Positive), transmettre l'alerte à un niveau supérieur (L2 ou SOC Manager).
4.  **Remédier** : Bloquer l'adresse IP malveillante sur le pare-feu (Firewall).

---

## 🧰 2. Les ressources

*   **Le site interactif** : ouvert via le bouton vert **"View Site"**.
*   **Le tableau de bord** : contient les alertes, les boutons d'escalade et la console du pare-feu.
*   **Le scénario** : une IP suspecte (`221.181.185.159`) tente de se connecter à un compte.

---

## 🎯 3. Les exos

1.  **What was the malicious IP address in the alerts?** (Quelle était l'adresse IP malveillante ?)
2.  **To whom did you escalate the alert with the malicious IP?** (À qui avez-vous escaladé l'alerte ?)
3.  **What message did you get after blocking the IP address on the firewall?** (Quel message avez-vous reçu après avoir bloqué l'IP sur le pare-feu ?)

---

## 🛠️ 4. Comment réussir les exos

1.  **Ouvre le lab** (bouton "View Site").
2.  **Pour la Q1** : Regarde les alertes générées. L'IP source suspecte est clairement indiquée (elle tente de se connecter en force brute ou de façon anormale).
3.  **Pour la Q2** : 
    *   Sélectionne l'alerte.
    *   Cherche le bouton **"Escalate"** (ou "Assign").
    *   Une liste de destinataires s'affiche. Choisis le **Team Lead** (c'est le nom qui apparaît dans le menu déroulant).
4.  **Pour la Q3** :
    *   Va dans la section **"Firewall"** (Pare-feu) du tableau de bord.
    *   Ajoute l'IP malveillante à la liste de blocage.
    *   Un message de confirmation (le flag) apparaît à l'écran.

---

## ✅ 5. Les réponses

*   **Q1 : Quelle était l'adresse IP malveillante ?**
    ➡️ **`221.181.185.159`**
*   **Q2 : À qui avez-vous escaladé l'alerte ?**
    ➡️ **`Will Griffin`**
*   **Q3 : Quel message avez-vous reçu après avoir bloqué l'IP ?**
    ➡️ **`THM{Found_The_Intruder}`**

---

## 🖥️ 6. Lignes de commande utilisées

Cette room est une simulation web interactive. Aucune ligne de commande n'a été exécutée. Les actions ont été réalisées via l'interface graphique (dashboard, formulaires, boutons).

---

## 📌 Ce que je retiens pour un poste d'analyste SOC

- **Le workflow du L1** : Détecter -> Analyser -> Escalader -> Remédier. C'est le cycle de base de toute alerte.
- **L'escalade** : Un analyste L1 ne doit pas tout gérer seul. Savoir quand et à qui escalader est crucial pour ne pas perdre de temps sur des menaces critiques.
- **Le blocage IP** : C'est une action de remédiation immédiate qui permet de stopper l'attaque. Mais attention aux faux positifs : bloquer une IP légitime peut couper un service important.

---

## ✅ Statut

- [x] Room terminée
- [x] Write-up publié

---

*Write-up rédigé dans le cadre de ma préparation au poste d'Analyste SOC junior.*