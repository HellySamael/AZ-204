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

# Récapitulatif – Azure Functions (AZ-204)

## 1. Plans d’hébergement
| Plan        | Facturation | Avantages | Limites |
|-------------|-------------|-----------|---------|
| **Consumption** | À l’exécution | Auto-scale massif, peu cher | Cold start, durée max ≈ 5-10 min, pas de SLA |
| **Premium** | Instances réservées | Pas de cold start, VNet Integration, slots, scaling illimité | Plus cher |
| **Dedicated (App Service Plan)** | VM réservées | Pas de cold start, intégration App Service | Pas vraiment serverless |

---

## 2. Triggers & Bindings
- **Triggers** : HTTP, Timer (cron), Queue/Blob, Event Grid, Event Hub, Service Bus.  
- **Bindings** : entrées/sorties déclaratives → simplifient le code (ex. écrire direct dans une queue).  
- Exemple : HTTP Trigger + Queue output binding pour pousser un message sans code de connexion.  

---

## 3. Authentification
- **AuthorizationLevel** : `Anonymous`, `Function` (clé fonction), `Admin` (host key).  
- **Keys** : function keys (locales à une fonction), host keys (globales).  
- **EasyAuth** (App Service Authentication) : intégration Entra ID, Google, GitHub sans code.  
- **API Management** : frontal possible pour OAuth2 + quotas.  

---

## 4. Configuration
- **`host.json`** : config globale (logs, retries, concurrence).  
- **`function.json`** : bindings par fonction.  
- **Identity-based connections** : via Managed Identity au lieu de secrets.  
- **AzureWebJobsStorage** : obligatoire pour le runtime (état, leases, logs).  

---

## 5. Scale & Concurrence
- **Consumption** : auto-scale basé sur événements (cold start possible).  
- **Premium** : instances préchauffées, pas de cold start.  
- **Dedicated** : lié à App Service Plan.  
- **Concurrence** : ex. Service Bus → `maxConcurrentCalls` pour limiter les messages traités en parallèle.  

---

## 6. Fiabilité et erreurs
- **Queue Storage** : messages échoués → `-poison` queue.  
- **Service Bus** : dead-letter intégré.  
- **Event Grid** : retries avec backoff côté Event Grid.  
- **Durable Functions** : `CallActivityWithRetryAsync()` avec RetryOptions.  

---

## 7. Durable Functions
- **Rôles** : Orchestrator (coordination déterministe), Activity (travail), Entity (état).  
- **Patterns** : fan-out/fan-in, human interaction (external event), scheduler.  
- **Date/heure** : utiliser `context.CurrentUtcDateTime` au lieu de `DateTime.Now`.  
- **État** : stocké dans Azure Storage (ou backend Netherite).  

---

## 8. Réseau et sécurité
- **VNet Integration** (Premium/Dedicated) → accès sortant vers réseau privé.  
- **Private Endpoint** → accès entrant/sortant privé aux dépendances (SQL, Storage, Cosmos).  
- **Access Restrictions** : filtre IP sur endpoints HTTP.  

---

## 9. Observabilité
- **Application Insights** intégré (télémétrie, Profiler, Snapshot Debugger).  
- **Sampling** configurable dans `host.json`.  
- **Live Metrics** pour voir le scale en direct.  
- **Streaming Logs** pour debug en temps réel.  

---

## 10. Points d’attention AZ-204
- Timeout plan Consumption ≈ 5 min (10 max).  
- Pas de SLA en Consumption (SLA dès Premium/Dedicated).  
- Linux Consumption + Docker custom → support de triggers limité (pas Blob/Queue/Timer).  
- Timer trigger → `useMonitor=true` pour éviter exécutions multiples en scale-out.  
- Blob Trigger préféré à Event Grid pour réactions simples aux uploads.  

