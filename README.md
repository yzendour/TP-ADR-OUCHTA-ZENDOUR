# TP ADR – Documentation des décisions d’architecture logicielle

Ce dépôt contient les Architecture Decision Records (ADR) du projet de gestion de bibliothèque.

## Structure
- `doc/adr/` : contient tous les ADR numérotés.
- `rapport.md` : rapport du TP.
- Chaque ADR = un fichier + un commit atomique.

## Ajouter un ADR
1. Copier le template ADR.
2. Créer un fichier `doc/adr/<numero>-titre.md`.
3. Rédiger toutes les sections.
4. Committer avec un message clair.

## Qualité
Un hook pre-commit valide automatiquement la présence des sections obligatoires.


```bash
  GNU nano 7.2                                                   .git/hooks/pre-commit                                                            
#!/bin/bash

for file in $(git diff --cached --name-only | grep "^doc/adr/"); do


    for section in "## Statut" "## Contexte" "## Décision" "## Alternatives envisagées" "## Conséquences"; do
        if ! grep -qi "$section" "$file"; then
            echo "Erreur : la section '$section' est manquante dans $file"
            exit 1
        fi
    done
done

exit 0


```
