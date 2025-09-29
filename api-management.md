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



# Récapitulatif – Azure API Management (APIM) (AZ-204)

## 1. Nature du service
- Passerelle pour exposer des APIs de manière sécurisée et gouvernée.
- Sert de **façade** entre les clients et les backends (Functions, App Service, Logic Apps…).
- Composants :
  - **Gateway** → reçoit requêtes, applique policies, appelle backend.
  - **Publisher portal** → config, gestion des policies, administration.
  - **Developer portal** → docs interactives, tests, gestion des abonnements.

---

## 2. Sécurité
- **Subscription key** obligatoire par défaut (header `Ocp-Apim-Subscription-Key`).
- Clés primaires/secondaires → rotation facile.
- Produits = regroupement d’APIs auxquels les devs s’abonnent → délivrent une clé.
- Supporte aussi :
  - **OAuth2 / OpenID Connect** (JWT).
  - **Certificats clients**.
  - **IP filtering**.
  - **Intégration VNET** (Premium uniquement).

---

## 3. Policies principales
- **Quota** → limite d’appels sur une période longue (jour/semaine/mois).
- **Rate-limit** → limite d’appels par intervalle court (ex. 10/min).
- **Transformation** → modification requêtes/réponses (XML ↔ JSON, headers).
- **Caching** → réponses mises en cache côté Gateway.
- **Rewrite-uri** → réécriture d’URL (ex. `/v1/*` → `/v2/*`).
- **Validate-jwt** → validation de tokens JWT (OAuth2/OpenID Connect).

---

## 4. Tiers (SKUs)
- **Developer** : non productif, dev/test.
- **Consumption** : serverless, facturation à l’appel, scalabilité auto.
- **Basic / Standard** : production classique (selon charge).
- **Premium** : multi-régions, VNET, fonctionnalités avancées.

---

## 5. Monitoring
- **Azure Monitor Metrics** → latence, nombre d’appels, codes de retour.
- **Diagnostic settings** → logs détaillés vers Log Analytics, Event Hub, Storage.
- **Application Insights** → suivi détaillé des traces et corrélations.

---

## 6. Points d’examen à retenir
- APIM = exposer une API interne de manière sécurisée (clé, quotas, OAuth2).
- **Developer portal** = docs + tests + clés pour développeurs.
- **Premium SKU** = requis pour **multi-régions** et **VNET**.
- **Policies en XML** (pas JSON ni YAML).
- Logs → passer par **Diagnostic settings** pour Log Analytics.

