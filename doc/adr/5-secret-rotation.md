# 5. Stratégie de rotation des secrets (Sécurité)

## Statut

Accepté

## Contexte

Le système utilise plusieurs secrets sensibles :

- mots de passe PostgreSQL → lié à [ADR 2](2-base-de-donnees.md),
    
- clés Redis → lié à [ADR 4](4-cache.md),
    
- clés de chiffrement,
    
- API keys (notifications).
    

Les secrets statiques augmentent les risques de compromission. Une rotation régulière est nécessaire pour respecter les bonnes pratiques de sécurité.

## Décision

Mettre en place une **rotation automatique des secrets** via un gestionnaire centralisé (HashiCorp Vault ou équivalent).

Rotation proposée :

- Credentials PostgreSQL : secrets dynamiques avec TTL court.
    
- Clés Redis : rotation mensuelle.
    
- Clés de chiffrement : rotation périodique selon RFC 8890.
    

## Alternatives envisagées

- **Fichiers .env versionnés manuellement** : rejeté, trop risqué.
    
- **Variables GitLab/GitHub sans rotation** : rejeté, non conforme aux pratiques sécurité.
    
- **Aucun mécanisme de rotation** : rejeté (surface d’attaque élevée).
    

## Conséquences

**Positives :**

- Forte réduction de l’impact en cas de fuite.
    
- Conformité aux standards (OWASP, NIST).
    
- Secrets éphémères → moindre exposition.
    
- Audit et traçabilité intégrés.
    

**Négatives :**

- Complexité supplémentaire (déploiement et maintenance d’un Vault).
    
- Dépendance à un service central (disponibilité critique).
    
- Intégration technique plus complexe dans CI/CD et l’application.