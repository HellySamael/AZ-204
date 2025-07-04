# AZ-204

## Azure App Service web-apps

Service HTTP pour héberger des web apps ("serveur web").
`ARR Affinity` in Application Request Routing: permet de rediriger les requêtes vers certaines instances (utile pour le statefull).


## Azure Functions

Différents plans : **Consumption plan** (défaut, temps de warmup...) ; **Flex consumption** avec possibilité d'avoir un _alwaysReady_ ; **Premium** avec option pour pré-warmup d'autres instances (pratique pour le scale up).

## CosmosDB

Cohérence des données :
Strong ➡️ Bounded staleness ➡️ Session ➡️ Consistent prefix ➡️ Eventual
Plus de consistence ➡️ plus de performances
- **strong** :  on récupère toujours la dernière version de la donnée ; moins bonnes performances.
- **eventual** : meilleures performances, mais on peut ne pas récupérer la dernière version de la donnée.

## Containers

- Azure Container Registry (**ACR**) pour héberger les images.
- Run images sur (Azure Container Instances (**ACI**).
- Azure Container Apps (**ACA**) : surcouche à AKS pour simplification.

## Authentification

- Access key : 2 keys pour un Storage Account. Donne accès à tout le S.A. 😱
- **Shared Access Signature** : clé avec permissions (read, write, add, create, delete, list) ; période de validité.
- Les SAS keys sont liées aux Access Key => regénérer les Access Keys révoquent les SAS keys existantes.
- Access Policy pour les SAS keys : définit la 


### Managed identities

- **System assigned** : identité directement associée à une instance d'un service Azure.
- **User assigned** : identité créée directement comme une ressource standalone - peut donc être utilisées par plusieurs services.

## Ressources

### Liens

- https://docs.microsoft.com/training/courses/AZ-204T00
- https://microsoftlearning.github.io/AZ-204-DevelopingSolutionsforMicrosoftAzure/
- UDemy : https://societegenerale.udemy.com/course/az204-azure-practice/learn/quiz/5304416#content

### Glossaire

| Terme | Signification | Définition |
| ----- | ------------- | ---------- |
| SKU   | Stock Keeping Unit | Type / forme d'un produit |
| RBAC  | Role Based Access Control | |
