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

# Récapitulatif – DevOps & CI/CD (AZ-204)

## 1. Outils de CI/CD

### GitHub Actions
- Intégré nativement à **GitHub**.
- Workflows définis dans `.github/workflows/*.yml`.
- Étapes typiques :
  1. Checkout du code  
  2. Build & tests  
  3. Login Azure (`azure/login@v2`)  
  4. Déploiement (`azure/webapps-deploy`, `azure/functions-action`, `azure/container-apps-deploy-action`)
- Secrets stockés dans **GitHub Secrets**.

### Azure Pipelines
- Service d’**Azure DevOps**.
- Fichier `azure-pipelines.yaml`.
- Étapes : Build → Test → Release.
- Intégration possible avec **Key Vault** pour les secrets.

---

## 2. Build vs Release Pipelines

| Type | Rôle | Contenu |
|------|------|---------|
| **Build (CI)** | Compiler, tester, publier artefacts | `npm test`, `dotnet build`, etc. |
| **Release (CD)** | Déployer en environnement cible | `az webapp deploy`, `func publish`, etc. |

---

## 3. Gestion des secrets
- Jamais stockés dans le code.
- Stockage :
  - **GitHub Secrets**
  - **Azure DevOps Library**
  - **Azure Key Vault**
- Authentification recommandée : **Service Principal (Contributor)** ou **Managed Identity**.

---

## 4. Stratégies de déploiement

### Deployment Slots
- Plusieurs environnements (production, staging…).
- **Swap** = échange instantané sans downtime.
- **Rollback rapide** via re-swap.

### Blue/Green Deployment
- Deux environnements identiques (Blue = prod, Green = staging).
- Bascule complète du trafic après validation.

### Canary Deployment
- Envoi progressif du trafic (ex. 10 % → 50 % → 100 %).
- Implémenté via **Traffic Routing** dans App Service.

---

## 5. Déploiement Functions
- Mode **Run From Package** :
  - Archive `.zip` montée en lecture seule.
  - Déploiement atomique, plus fiable que Zip Deploy.
- Supporté par GitHub Actions (`azure/functions-action`).

---

## 6. Health Checks et rollback
- **Health Checks** : vérifient la santé de l’application avant un swap.
- **Smoke Tests** : tests rapides post-déploiement dans le pipeline.
- Rollback instantané via re-swap ou redeploiement automatisé (IaC).

---

## 7. Bonnes pratiques
- Séparer Build et Release pipelines.
- Ne jamais exposer de secrets dans le code.
- Utiliser **Key Vault / GitHub Secrets** pour les credentials.
- Rôle minimal : **Contributor**.
- Valider les déploiements avec **Health Checks** avant mise en prod.
