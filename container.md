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


# Récapitulatif – Containers (ACR, ACI, ACA) (AZ-204)

## 1. Azure Container Registry (ACR)
- **Registry privé** pour images Docker/OCI.
- **Authentification** :
  - Admin user (⚠️ pas recommandé en prod).
  - Service principal (Azure AD app).
  - **Managed identity / Azure AD** (recommandé).
- **Fonctionnalités** :
  - **ACR Tasks** → builds automatisés (commit Git, timer, dépendances).
  - **Geo-replication** (Premium) → distribuer les images dans plusieurs régions.
- **SKUs** :
  - Basic → usage léger.
  - Standard → plus de throughput.
  - Premium → geo-replication, fonctionnalités avancées.

---

## 2. Azure Container Instances (ACI)
- Exécution **serverless** de conteneurs sans orchestrateur.
- Cas d’usage :
  - **Batch jobs ponctuels**.
  - Tester rapidement une image.
  - Complément AKS via **Virtual Kubelet** (burst capacity).
- Limitations :
  - Pas de scaling avancé.
  - Pas d’orchestration complexe.
  - Pas de stockage persistant natif (mais Azure Files possible).

---

## 3. Azure Container Apps (ACA)
- Service **serverless** pour exécuter des applications conteneurisées.
- Fonctionnalités clés :
  - **Scale-to-zero** → zéro facturation sans trafic.
  - **KEDA** (autoscaling basé sur événements, ex. messages Service Bus).
  - **Revisions** → gestion de versions, déploiements blue/green, A/B testing.
  - **Dapr** → simplifie les microservices (pub/sub, state, service discovery).
- Cas d’usage :
  - APIs REST containerisées.
  - Microservices avec event-driven scaling.
  - Déploiements progressifs (blue/green).

---

## 4. Comparaison rapide
| Service | Rôle principal | Points forts | Limitations |
|---------|---------------|--------------|-------------|
| **ACR** | Registry d’images | Auth AD/MI, Tasks, Geo-replication | Ne fait pas tourner de conteneurs |
| **ACI** | Exécution brute | Jobs ponctuels, test rapide | Pas de scaling complexe |
| **ACA** | Apps serverless | Scale-to-zero, KEDA, Revisions, Dapr | Plus limité qu’AKS pour orchestration avancée |

---

## 5. Points d’examen à retenir
- **ACR Tasks** = rebuild auto (Git, base image update).
- **Geo-replication** = Premium SKU.
- **ACI** = exécution ponctuelle, Virtual Kubelet pour burst.
- **ACA** = scale-to-zero, KEDA (event-driven), Revisions (blue/green), Dapr (microservices).
