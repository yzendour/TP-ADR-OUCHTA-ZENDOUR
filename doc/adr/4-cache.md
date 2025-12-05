# 4. Stratégie de cache

## Statut

Accepté

## Contexte

Les informations sur les livres (disponibilité, détails) sont très fréquemment consultées. Interroger la base pour chaque requête serait coûteux et pourrait nuire à l’expérience utilisateur.

## Décision

Utiliser **Redis** comme cache in-memory** pour stocker :

- la disponibilité courante des livres,
    
- les détails les plus consultés.
    

La gestion des clés Redis nécessitera une politique de rotation → voir [ADR 5](5-secret-rotation.md).

## Alternatives envisagées

- **Cache local dans l’application** : rejeté, pas scalable et non partagé entre instances.
    
- **Pas de cache** : rejeté, surcharge de PostgreSQL et baisse de performance.
    

## Conséquences

**Positives :**

- Temps de réponse largement réduit.
    
- Allègement des charges sur PostgreSQL.
    
- Possibilité d’expiration automatique (TTL) pour cohérence.
    

**Négatives :**

- Ajout d’un composant externe à maintenir.
    
- Risque d’incohérence si invalidation mal gérée.