# Azure Key Vault

## 🔐 1. Qu’est‑ce qu’Azure Key Vault

- Service géré pour stocker secrets, clés (software/HSM) et certificats.
- Deux types de conteneurs : Vault (software/HSM), Managed HSM (uniquement HSM).
- Deux niveaux de service : Standard (logiciel), Premium (avec HSM).

## 🧩 2. Principaux cas d’usage

- Stockage centralisé de tokens, mots de passe, clés d’API, secrets d’applications.
- Gestion de clés pour le chiffrement de données.
- Gestion de certificats (TLS/SSL) : génération self-signed, CSR, intégration CA, import PFX/PEM.
- Renforcement de la sécurité via Managed Identities (réduction des informations d’identification manuelles) ([turn0search5], [turn0search10]).

## 🧭 3. Authentification & autorisation

- Authentification via Azure AD :
  - Identité managée recommandée (automatiquement gérée).
  - Sinon, service principal avec certificat ou secret (moins recommandé).
- Autorisation :
  - Azure RBAC pour le plan de gestion.
  - Politiques d'accès Key Vault (data-plane) pour accéder aux secrets, clés, certificats.
  - Possibilité de combiner RBAC + politiques d’accès.

## 🛠️ 4. Gestion des secrets / clés / certificats (data-plane)

- SDK (.NET v4, Python, Java…) :
  - Secrets : set/get.
  - Keys : créer, récupérer, utiliser pour opérations cryptographiques.
  - Certificates : génération self-signed, CSR, import, liaison CA.
- CLI / PowerShell :
  - `az keyvault secret set/get`
  - `Add-AzKeyVaultKey`
  - `New-AzKeyVaultCertificate` ou import (PFX/PEM).

## 🗄️ 5. Résilience & récupération

- Soft‑delete : permet récupérer vaults, secrets, clés supprimés pendant 90 jours par défaut.
- Purge protection : empêche la suppression définitive pendant la période de soft-delete ; doit être activé après soft-delete.

Exemple CLI :

```bash
az keyvault update \
  --enable-soft-delete true \
  --enable-purge-protection true
```

En PowerShell lors de la création :

```powershell
New-AzKeyVault -Name ... -EnableSoftDelete -EnablePurgeProtection
```

## 🔄 6. Rotation & alertes (plan de gestion)

- Rotation automatique des clés via Key Rotation Policy à la création de la clé.
- Alertes avant expiration :
  - Configurer les Azure Key Vault alerts avec Azure Monitor (notifications avant expiration).
- Option avancée : dispatcher les événements via Event Grid si besoin de réaction spécifique (ex. microservices).


## 📊 7. Supervision & journalisation

- Journaux d’accès & audits via :
  - Azure Monitor Logs
  - Storage Account (archivage)
  - Event Hub (streaming)
- Exemple de contrôle : nombre d’erreurs, requêtes anormales, latence de requêtes.


## 🧭 8. Bonnes pratiques

- Séparer per environment ou application (DEV/QA/PROD), vaults dédiés.
- Utiliser Managed Identity, éviter secrets codés.
- Activer soft-delete + purge protection.
- Configurer accès au minimum (principes du moindre privilège).
- Activer la journalisation et configurer des alertes.
- Faire des sauvegardes régulières (backup / restore).

## 📝 9. Ce qui est attendu à l’examen AZ‑204

- Implémenter et consommer secrets, clés, certificats depuis le code ou CLI/PowerShell.
- Utiliser Managed Identity pour accéder à Key Vault.
- Configurer soft-delete et purge protection (CLI ou PowerShell).
- Mettre en place rotation automatique + alertes avant expiration.
- Structurer les politiques d’accès (RBAC / Access Policies).
- Activer monitoring, journaux et alertes.

## 💡 Conseils de révision

- Suivre le module Microsoft Learn Implémenter Azure Key Vault.
- Pratique :
  1. Créer un vault, ajouter secrets/clés/certs.
  2. Tester accès via identités managées dans Azure Functions ou Web App.
  3. Activer soft-delete + purge protection et tester suppression puis récupération.
  4. Créer rotation policy, générer alertes.
- Explorer les SDK : .NET, Python, Java, etc.
- Consulter les guides GitHub comme arvigeus/AZ-204 Key Vault.

## 📚 Resources
- [Présentation d’Azure Key Vault](https://learn.microsoft.com/azure/key-vault/general/overview)
- [Tutoriel Key Vault avec Azure CLI](https://learn.microsoft.com/azure/key-vault/secrets/quick-create-cli)
