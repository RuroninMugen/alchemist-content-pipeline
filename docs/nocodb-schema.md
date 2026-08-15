# Schéma NocoDB — CRM Alchemist Motion

## Contexte

CRM local pour piloter la prospection commerciale d'Alchemist Motion. Flux cible :
`Apify (scraping leads) → NocoDB → Gmail (brouillons personnalisés) → Slack (résumé)`

## Environnement

- **Instance** : NocoDB en local sur MacBook M1, via Docker
- **Commande de lancement** :
```bash
  docker run -d --name nocodb \
    -p 8080:8080 \
    -v ~/nocodb-data:/usr/app/data \
    nocodb/nocodb:latest
```
- **Accès** : `http://localhost:8080`
- **Workspace** : Default Workspace → Base "Getting Started"

## Table : Leads

| Champ        | Type          | Détails |
|--------------|---------------|---------|
| Title        | Single line text | Champ par défaut NocoDB |
| Statut       | Single select | Voir options ci-dessous |
| Entreprise   | Single line text | Nom de l'entreprise du lead |
| Email        | Email         | Contact principal |
| Source       | Single select | Voir options ci-dessous |

### Options — Statut (pipeline)

1. Nouveau
2. Contacté
3. Qualifié
4. Proposition envoyée
5. Gagné
6. Perdu

### Options — Source

- Apify
- Manuel
- Référence
- Réseaux sociaux

## Vue : Kanban

- **Nom** : Kanban
- **Stacked by** : Statut
- **Édition** : Collaborative
- Colonnes générées automatiquement à partir des options du champ Statut (+ colonne "Uncategorized" pour les leads sans statut assigné)

## Prochaines étapes

- [ ] Table Interactions (historique des relances/emails, liée à Leads via Link to another record)
- [ ] Intégration Apify → NocoDB (insertion automatique des leads scrapés)
- [ ] Intégration NocoDB → Gmail (génération de brouillons personnalisés)
- [ ] Résumé Slack automatique
