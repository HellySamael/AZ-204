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


# Récapitulatif – Monitoring (AZ-204)

## 1. Monitoring

### Azure Monitor
- Service central pour **metrics** et **logs** de toutes les ressources.
- Collecte :
  - Metrics → valeurs numériques en temps réel (CPU, RU/s, latence…).
  - Logs → traces détaillées, diagnostics, activité.
- Permet de définir des **alertes** :
  - **Metric Alert** → sur seuil numérique (ex. CPU > 80 %).
  - **Log Alert** → sur résultats d’une requête KQL.
  - **Activity Log Alert** → sur événements Azure (création, suppression…).

### Application Insights
- Spécialisé dans le **monitoring applicatif** :
  - Requêtes, exceptions, dépendances, temps de réponse.
  - **Custom telemetry** via SDK.
- Fonctionnalités :
  - **Live Metrics Stream** (temps réel).
  - **Distributed Tracing** (corrélation à travers microservices).
  - **Smart Detection** (anomalies automatiques).

### Diagnostic Settings
- Export des logs vers :
  - **Log Analytics** (requêtes, KQL).
  - **Event Hub** (streaming).
  - **Storage** (archivage).
- Base pour connecter Azure Monitor avec d’autres outils.

### Log Analytics & KQL
- Centralise les logs de plusieurs services (APIM, Functions, Cosmos…).
- Utilise **Kusto Query Language (KQL)**.
  - `where` → filtre.
  - `summarize` → agrégation.
  - `bin()` → regroupement par temps.

---

## 2. Points d’examen à retenir
- **Azure Monitor** = metrics/logs de toutes les ressources.
- **App Insights** = monitoring applicatif (exceptions, dépendances, tracing).
- **Diagnostic Settings** = envoyer logs vers Log Analytics/Event Hub/Storage.
- **KQL** = langage de requête pour logs.

