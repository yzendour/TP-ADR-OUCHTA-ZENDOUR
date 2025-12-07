# 1. Choix de l’architecture générale

## Statut

Accepté

## Contexte

Le système de gestion de bibliothèque doit gérer plusieurs domaines fonctionnels (emprunts, réservations, notifications) avec fiabilité et maintenabilité. Le besoin principal est de limiter la complexité tout en gardant une possibilité d’évolution.

## Décision

Adopter une **architecture monolithique modulaire** : un seul déploiement mais des modules internes clairement séparés.

Cette décision impacte notamment :

- la gestion des transactions → voir [ADR 3](3-transactions.md),
    
- la stratégie de sécurité centralisée → voir  [ADR 5](5-secret-rotation.md).
    

## Alternatives envisagées

- **Microservices** : rejeté car trop complexe pour la taille du projet (orchestration, monitoring, gestion réseau).
    
- **Monolithe non modulaire** : rejeté pour manque de maintenabilité et risque de dette technique rapide.
    

## Conséquences

**Positives :**

- Déploiement simple, peu coûteux.
    
- Pas de surcoût réseau interne → meilleures performances.
    
- Architecture facile à comprendre pour les nouveaux arrivants.
    

**Négatives :**

- Scalabilité moins fine que des microservices.
    
- Risque d'un refactoring lourd si la charge augmente fortement.