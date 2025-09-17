# App Service

Service PaaS pour héberger des applications web, API et jobs de fond.

## 🏗️ Plans d'hébergement
- **Free/Shared** : ressources mutualisées, idéal pour tests sans SLA.
- **Basic** : calcul dédié, pas d’auto-scale.
- **Standard** : auto-scale, sauvegardes, 5 slots de déploiement.
- **Premium v2/v3** : meilleures performances, VNet, stockage local, scale-out accru.
- **Isolated (ASE)** : environnement dédié dans un VNet, isolement réseau complet.

## 🚀 Déploiement & intégration continue
- Déploiement via GitHub Actions, Azure DevOps, ZIP/`run-from-package`, FTP ou conteneurs Docker.
- **Slots** de déploiement pour blue/green ; swap avec warmup.
- Support des **Private Endpoints** et **VNet integration** pour restreindre l’accès.

## ⚙️ Configuration & gestion
- **App Settings** et `Connection strings` chiffrées, variables d’environnement.
- Gestion des secrets via **Key Vault references**.
- Redémarrage, scale up/out, configuration via CLI (`az webapp`).

## 📈 Mise à l’échelle
- **Scale up** : changement de plan pour plus de ressources.
- **Scale out** : jusqu’à 30 instances (Standard) ou 30+ (Premium) avec règles CPU, RAM, horaires ou queue.
- **Health check** et `ARR Affinity` pour les sessions persistantes.

## 🔒 Sécurité & réseau
- HTTPS obligatoire, certificats gérés ou personnalisés (SNI).
- Authentification intégrée (Easy Auth) avec Azure AD, providers sociaux.
- **Managed Identity** pour appeler d’autres services Azure sans secret.

## 📊 Diagnostic & surveillance
- Intégration **Application Insights** : traces, dépendances, Live Metrics.
- Journaux d’accès, Web Server Logs, diagnostics streaming vers Log Analytics/Event Hub/Storage.

## ✅ Pour l'examen
- Créer une Web App via CLI/Portal et choisir le bon plan.
- Configurer l’authentification, les slots et l’auto‑scale.
- Déployer via Git/GitHub Actions ou conteneurs et surveiller avec Application Insights.
## 📚 Resources
- [Documentation App Service](https://learn.microsoft.com/azure/app-service/overview)
- [Plans d'hébergement](https://learn.microsoft.com/azure/app-service/overview-hosting-plans)



# Récapitulatif – Azure App Service (AZ-204)

## 1. Plans et capacités

| Plan            | Ressources         | Custom domain / SSL | Slots | Always On | VNet Integration |
|-----------------|-------------------|----------------------|-------|------------|------------------|
| Free / Shared   | Mutualisé         | ❌                   | 0     | ❌         | ❌               |
| Basic           | Dédié             | ✅                   | 0     | ✅         | ❌               |
| Standard        | Dédié             | ✅                   | 5     | ✅         | ❌               |
| Premium (V2/V3) | Dédié + perf ↑    | ✅                   | 20    | ✅         | ✅               |
| Isolated (ASE)  | Environnement privé | ✅                 | 20    | ✅         | ✅ (dans ton VNet) |

---

## 2. Déploiement et disponibilité
- **Méthodes** : FTP, GitHub Actions, Azure DevOps, ZIP deploy, ACR/Docker.  
- **Slots** : déployer/tester → swap sans interruption.  
- **Scale up/down** : changer la taille des VM.  
- **Scale out/in** : ajouter ou retirer des instances, auto-scale possible.  

---

## 3. Sécurité et réseau
- **EasyAuth (App Service Authentication)** : intégration Entra ID, Google, GitHub, etc.  
- **Managed Identity** : accès sécurisé à Key Vault, Azure SQL, Storage.  
- **Access Restrictions** : filtrage IP/service tags sur endpoint public.  
- **Private Endpoint** : IP privée dans VNet, DNS privatelink, accès public désactivé.  
- **VNet Integration** : accès sortant privé (Premium/Isolated).  

---

## 4. Configuration & secrets
- **App Settings** : variables d’environnement, écrasent appsettings.json.  
- **Connection strings** : injectées automatiquement dans certaines SDK.  
- **Key Vault references** : secret lu en direct depuis Key Vault (via Managed Identity).  

---

## 5. Surveillance & diagnostic
- **App Insights** : télémétrie, Profiler, Snapshot Debugger, Availability tests.  
- **Streaming Logs** : suivi temps réel (utile pour erreurs de démarrage).  
- **App Service Diagnostics** : troubleshooting guidé.  
- **Health Check** : retire instance du LB si endpoint KO.  

---

## 6. Certificats et domaines
- **Certificat gratuit auto-renouvelé** : App Service Managed Certificate (non-wildcard).  
- **Certificat custom** : import manuel ou via Key Vault.  
- **HTTPS Only** : forcer TLS (TLS 1.2 minimum).  

