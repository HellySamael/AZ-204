# Récapitulatif –  Deployment  (AZ-204)

## 1. Deployment (Infrastructure as Code)

### ARM Templates
- Fichiers **JSON** déclaratifs.
- Idempotents (répéter le déploiement = pas d’erreurs).
- Supporte paramètres, variables, outputs.

### Bicep
- Langage déclaratif simplifié → compile en ARM JSON.
- Plus lisible et maintenable.

### Azure CLI / PowerShell
- Approche **impérative** (commandes/scripts).
- Idéal pour scripts rapides ou automation légère.

### Comparaison
| Outil           | Type        | Format     | Cas d’usage |
|-----------------|-------------|------------|-------------|
| **ARM**         | Déclaratif  | JSON       | Prod, CI/CD |
| **Bicep**       | Déclaratif  | Bicep → ARM| Dev lisible |
| **CLI/PS**      | Impératif   | Commandes  | Scripts ad-hoc |


---

## 2. Points d’examen à retenir
- **ARM/Bicep** = déploiement déclaratif ; **CLI/PowerShell** = impératif.
