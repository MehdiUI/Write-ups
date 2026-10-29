# 🐧 Module 2 : Linux Fundamentals

Ce module pose les bases de l'utilisation de Linux, le système d'exploitation le plus utilisé dans les serveurs et les infrastructures réseaux. Indispensable pour analyser des logs et manipuler des serveurs.

## 📝 Rooms du module

| Room | Description | Statut | Write-up |
|---|---|---|---|
| **Linux Fundamentals Part 1** | Découverte du terminal, navigation de base et commandes essentielles (ls, cd, cat). | ✅ Terminé | [Lire](./linux-fundamentals-part-1.md) |
| **Linux Fundamentals Part 2** | Connexion à distance via SSH, gestion des fichiers, permissions et recherche. | ✅ Terminé | [Lire](./linux-fundamentals-part-2.md) |
| **Linux Fundamentals Part 3** | Gestion des processus, automatisation avec Cron, gestion des paquets et des logs. | ✅ Terminé | [Lire](./linux-fundamentals-part-3.md) |

## 🧠 Ce que je retiens pour un poste d'Analyste SOC
- **Le terminal est roi** : L'interface graphique n'existe souvent pas sur les serveurs. Il faut être à l'aise avec `grep`, `cat`, `less` et `tail` pour lire les logs.
- **Gestion des processus** : Savoir utiliser `ps`, `top` et `kill` est vital pour repérer un processus malveillant qui consomme des ressources ou stopper une attaque.
- **Automatisation** : Les tâches répétitives (comme la sauvegarde ou l'extraction de logs) se font via des scripts Bash et des crontabs.