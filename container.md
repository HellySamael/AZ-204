# Containers

Services pour exécuter des conteneurs dans Azure.

## 🧱 Azure Container Instances (ACI)
- Démarrage rapide de conteneurs sans orchestrateur, facturation à la seconde.
- Groupes de conteneurs multi‑containers, support des volumes Azure Files/Secrets.
- Intégration VNet, IP publique ou privée, options GPU et Windows.
- Scénarios : tâches batch, jobs isolés, moteurs d’arrière-plan.

## 🌀 Azure Kubernetes Service (AKS)
- Cluster Kubernetes managé : plan de contrôle gratuit, nœuds payants.
- Auto‑scaler, mises à jour gérées, nœuds Windows/Linux, pool de nœuds multiples.
- Intégration **Azure AD**, **Kubernetes RBAC**, **Azure Policy**, Ingress, secrets via Key Vault CSI.
- Scénarios : microservices complexes, workloads stateful, contrôle total de Kubernetes.

## ⚡ Azure Container Apps (ACA)
- Service serverless basé sur Kubernetes + Dapr + KEDA.
- Scale à zéro, révisions pour blue/green, jobs planifiés.
- Ingress HTTP sécurisé, support des événements (Service Bus, Kafka, etc.).
- Environnements gérés avec Log Analytics et VNet optionnel.

## 📦 Azure Container Registry (ACR)
- Registre privé d’images : georeplication, Webhooks, **Tasks** pour build/scan.
- Authentification via Azure AD, Managed Identity ; pull depuis AKS/ACI/ACA.

## 🤔 Choisir le bon service
- **ACI** : exécutions rapides, sans gestion d’infrastructure.
- **AKS** : contrôle Kubernetes complet et personnalisation avancée.
- **Container Apps** : microservices serverless avec auto‑scale géré.

## ✅ Pour l'examen
- Déployer un conteneur via CLI/Portal et configurer ACR.
- Comparer ACI/AKS/ACA et choisir selon les besoins de scalabilité et de gestion.
- Sécuriser les images via ACR et Managed Identity.
## 📚 Resources
- [Azure Container Instances](https://learn.microsoft.com/azure/container-instances/container-instances-overview)
- [Azure Kubernetes Service](https://learn.microsoft.com/azure/aks/)
- [Azure Container Apps](https://learn.microsoft.com/azure/container-apps/)
- [Azure Container Registry](https://learn.microsoft.com/azure/container-registry/)
