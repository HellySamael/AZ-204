# API Management

Standardiser les appels aux API : sécurité, quotas, transformation et cache.

## 🧩 Composants
- **Gateway** : applique les policies et route vers le backend.
- **Developer Portal** : documentation interactive, tests, gestion des souscriptions.
- **Publisher Portal** (Azure Portal) : administration, analytics, import OpenAPI/WSDL.

## 🎯 Scénarios
- Exposer une API (Function, App Service…) via un point d’entrée unique.
- Versionning, monétisation, limitation de débit.
- Transformation de formats (JSON/XML), injection d’en-têtes.

## 📊 Tiers
- **Consumption** : facturation à l’appel, idéal microservices.
- **Developer** : usage dev/test, pas de SLA.
- **Basic / Standard** : déploiements prod mono-région avec SLA.
- **Premium** : multi‑région, VNet, scale jusqu’à plusieurs gateways.

## 🛡️ Policies
- Déclarées en XML, exécutées **inbound**, **outbound**, **backend** ou **on-error**.
- Exemples inbound : `rate-limit`, `quota`, `ip-filter`, `validate-jwt`.
- Exemples outbound : `set-body`, `cache-store`, `log-to-eventhub`.
- Support des templates Liquid et variables de contexte.

## 🔐 Sécurité
- Authentification via clés d’API, JWT/OAuth2, certificats client.
- Intégration **Managed Identity** / **Key Vault** pour les secrets du backend.
- Self-hosted gateway pour déployer on-prem ou autre cloud.

## ✅ Pour l'examen
- Importer une API et publier via le portail développeur.
- Appliquer des policies (quota, transformation, JWT) pour sécuriser et gouverner.
- Choisir le bon tier selon besoins (Consumption vs Premium).
## 📚 Resources
- [Documentation API Management](https://learn.microsoft.com/azure/api-management/api-management-key-concepts)
- [Policies reference](https://learn.microsoft.com/azure/api-management/policies/)

