# Monitoring

Surveiller et diagnostiquer les applications Azure.

## 📈 Azure Monitor
- Plateforme centrale pour collecter **métriques** (séries temporelles) et **logs** (données structurées).
- Sources : ressources Azure, agents VM, Diagnostics Settings, SDKs.
- **Log Analytics Workspace** pour requêtes KQL, rétention configurable.
- **Metrics Explorer**, dashboards, workbooks, automatisation via REST/CLI.
- **Alerts** sur métriques ou logs, actions via **Action Groups** (email, webhook, Logic Apps, Functions…).

## 🧰 Application Insights
- Télémetrie applicative : requêtes, dépendances, exceptions, traces personnalisées.
- **Live Metrics**, **availability tests**, map de dépendances, profilage.
- Exportation vers Log Analytics, sampling pour optimiser les coûts.

## 🔍 Diagnostic & observabilité
- **Distributed tracing** pour microservices (correlation IDs).
- **Diagnostic Settings** pour acheminer logs/métriques vers Log Analytics, Storage ou Event Hub.
- **Container/VM insights** pour Kubernetes et machines virtuelles.

## ✅ Pour l'examen
- Configurer Application Insights pour une Function ou App Service.
- Créer des alertes et action groups sur métriques/logs.
- Écrire des requêtes KQL dans Log Analytics et activer les diagnostics sur une ressource.
## 📚 Resources
- [Azure Monitor](https://learn.microsoft.com/azure/azure-monitor/overview)
- [Application Insights](https://learn.microsoft.com/azure/azure-monitor/app/app-insights-overview)
