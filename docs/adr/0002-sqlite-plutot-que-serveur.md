# 2. Utilisation de SQLite plutôt qu'un serveur PostgreSQL ou un fichier JSON

* Statut : Accepté
* Date : 2026-10-05
* Décideurs : Pham Quoc Huy

## Contexte
Le logiciel Biblio doit pouvoir être installé et exécuté rapidement par des bénévoles qui n'ont pas forcément de compétences en administration système. Nous avons besoin de conserver les données (livres, membres, emprunts) de manière fiable sans imposer une installation complexe.

## Options envisagées
1. **Fichier JSON**
   - *Pour* : Très facile à manipuler, aucun outil externe requis.
   - *Contre* : Ne permet pas d'exécuter de requêtes SQL complexes et gère très mal les modifications simultanées.
2. **Serveur PostgreSQL**
   - *Pour* : Très puissant, adapté aux gros volumes et aux accès réseau multi-utilisateurs.
   - *Contre* : Nécessite l'installation, la configuration et la gestion d'un serveur lourd, trop difficile pour des bénévoles.
3. **Base de données SQLite**
   - *Pour* : Intégré nativement dans Python, stocké dans un simple fichier local, supporte le langage SQL standard sans aucun serveur à installer.
   - *Contre* : Accès concurrents limités si l'application grossit fortement.

## Décision
Utiliser SQLite car il ne nécessite aucune installation de serveur externe et s'intègre parfaitement avec Python.

## Conséquences
- *Positives* : L'installation est immédiate pour les bénévoles, l'exécution est très rapide et les données sont persistées dans un seul fichier local.
- *Négatives* : Si la bibliothèque grandit et nécessite plusieurs accès réseau simultanés, il faudra migrer vers un SGBD client-serveur.