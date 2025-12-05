# 2. Choix de la base de données

## Statut

Accepté

## Contexte

Le système doit gérer des transactions ACID (emprunts, retours, réservations). Les relations sont complexes (livres ↔ usagers ↔ emprunts), ce qui nécessite une base relationnelle.

## Décision

Utiliser **PostgreSQL** comme base de données principale.

## Alternatives envisagées

- **MongoDB** : rejeté, pas adapté aux transactions fortes ni aux relations structurées.
    
- **MySQL** : rejeté, moins performant pour requêtes avancées et moins flexible (JSON, extensions).
    

## Conséquences

**Positives :**

- Transactions robustes.
    
- Requêtes complexes efficaces.
    
- Compatible avec rotation automatique de credentials → voir [ADR 5](5-secret-rotation.md).
    

**Négatives :**

- Administration plus exigeante qu’une solution NoSQL.
    
- Peut nécessiter optimisation pour forte charge.