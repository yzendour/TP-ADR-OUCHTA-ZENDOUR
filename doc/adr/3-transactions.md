# 3. Gestion des transactions

## Statut

Accepté

## Contexte

Les opérations d’emprunt doivent être atomiques :

- un livre ne peut pas être réservé deux fois,
    
- aucune donnée ne doit être laissée dans un état partiellement cohérent.
    

## Décision

Utiliser **les transactions natives de PostgreSQL**, avec une isolation `READ COMMITTED`.

Cette décision repose sur le choix de PostgreSQL → voir [ADR 2](2-base-de-donnees.md).

## Alternatives envisagées

- **Mécanisme de Saga (microservices)** : rejeté car incompatible avec l’architecture monolithique → voir [ADR 1](1-architecture-generale.md).
    
- **Opérations sans transactions explicites** : rejeté (risque majeur d’incohérence).
    

## Conséquences

**Positives :**

- Cohérence métier garantie.
    
- Intégration simple dans l’application.
    
- Bonne performance en contexte monolithique.
    

**Négatives :**

- Peut provoquer des verrous si le trafic augmente fortement.
    
- Nécessite une bonne discipline dans le code (commit/rollback propre).