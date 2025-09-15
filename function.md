# Azure Functions

Fonctions serverless déclenchées par des événements.

## ⚙️ Triggers & Bindings
- **Triggers** : HTTP, Timer, Queue/Service Bus, Event Grid, Blob, Cosmos DB, Event Hub… (un seul trigger par fonction).
- **Bindings** : entrées/sorties déclaratives vers Storage, Cosmos DB, SignalR, Twilio, etc. Pas de code de connexion.
- Support de nombreux langages (.NET, Node.js, Python, Java, PowerShell, Go).

## 🏗️ Plans d'hébergement
- **Consumption** : scale à zéro, 1,5 Mio GB‑s/mois inclus, timeout 5 min (ext. 10), froid possible.
- **Flex Consumption / Premium** : instances préchauffées, VNet, temps d’exécution illimité, scale de 0 à n.
- **Dedicated (App Service Plan)** : ressources réservées, aucun cold start mais pas de scale automatique.

## 👨‍💻 Développement & déploiement
- Outils **Azure Functions Core Tools** / Visual Studio / VS Code pour développer localement.
- Déploiement via ZIP, GitHub Actions, Azure DevOps, conteneurs Docker.
- Fichier `host.json` pour config globale, `function.json` pour chaque fonction.

## 🔒 Sécurité
- Niveaux d’autorisation HTTP (`anonymous`, `function`, `admin`).
- **Managed Identity** et Key Vault pour accéder à des ressources sans secret.
- Restreindre l’accès réseau via VNet ou restrictions IP (Premium/Dedicated).

## 📈 Scaling & limites
- Scale out automatique jusqu’à 200 instances (consumption), déclenché par queue/event.
- Concurrence limitée par plan, utilisation des files d’attente pour absorber les pics.

## ✨ Durable Functions
- Trois types : **Orchestrator**, **Activity**, **Entity**.
- Patterns : fan‑out/fan‑in, async HTTP, monitor, sous-orchestrations.
- Stockage d’état dans des tables/queues, idéal pour workflows complexes.

## 📊 Monitoring
- **Application Insights** intégré : traces, métriques, map de dépendances.
- Activer le sampling et les alerts pour suivre les échecs d’exécution.

## ✅ Pour l'examen
- Créer une Function via CLI/Portal et choisir le plan adéquat.
- Configurer les triggers/bindings (`function.json`, attributs).
- Comprendre le scaling, les limitations et les options de sécurité.
- Implémenter Durable Functions pour orchestrer des workflows.
## 📚 Resources
- [Documentation Azure Functions](https://learn.microsoft.com/azure/azure-functions/functions-overview)
- [Durable Functions](https://learn.microsoft.com/azure/azure-functions/durable/durable-functions-overview)
