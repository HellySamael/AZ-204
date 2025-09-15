# Blob storage

## 📦 1. Types de blobs & cas d’usage

- **Block Blobs** : fichiers non structurés (images, PDF, vidéos). Composés de blocs individuels ≤ 100 Mo ; taille maximale ~190 TiB 
- **Page Blobs** : fichier accédés aléatoirement (ex. VHD). Taille max 8 TiB 
- **Append Blobs** : optimisés pour append, typiquement logs 

## 🏗️ 2. Comptes & niveaux de redondance

- Utiliser **General-purpose v2** (StorageV2) : supporte tous les services (Blob, File, Queue, Table) 

Principales options de réplication :

| Abbr. | Description |
| ----- | ----------- |
| LRS | 3 répliques dans un même DC |
| ZRS | 3 répliques dans 3 zones |
| GRS| LRS + réplication région éloignée |
| GZRS | Combinaison ZRS + GRS |

## 🔄 3. Niveaux d’accès (access tiers)

- **Hot** : accès fréquent, coût stockage élevé, coût accès faible.
- **Cool** : accès moins fréquent (≥30 jours), stockage moins cher, accès plus coûteux.
- **Archive** : stockage ultra économique, mais récupération lente (1–15 h), refroidissement ≥180 jours 

⚙️ Automatisation via règles de cycle de vie : transitions entre niveaux ou suppression automatique 

## 🛠️ 4. Opérations de gestion de données

- **AzCopy** : outil CLI très performant pour copier/déplacer les blobs 
- **Azure CLI / PowerShell** : commandes az storage blob upload/download/list… 
- **SDK client** (v12 .NET, Java, Python...) : instanciation, upload, download, set/get metadata & properties 

## 📝 5. Propriétés & métadonnées

- Propriétés : taille, type de média, en-têtes HTTP.
- Metadonnées : paires clé‑valeur (max ~8 Ko) stockés dans les headers 
- Manipulation via SDK ou CLI set blob metadata/properties .

## 🔐 6. Sécurité & accès

- **Shared Key** : accès complet au compte, via signature dans header. Utilisation réservée aux applications de confiance .
- **Shared Access Signatures** (SAS) : jetons avec accès restreint dans le temps à containers ou blobs 
- **User Delegation SAS** : SAS via àAzure AD, plus sécurisé, disponible uniquement sur Blob/Queue 

## 🧩 7. Événements et flux de modifications (change feed)

- **Event Grid** : réaction temps réel aux événements de blob (création, suppression…) – utile pour démarrer une Function en < 1 min 
- **Change Feed** : log ordonné, immuable, stocké dans le compte, accessible en batch ou streaming 
- Changement durable, commande : change feed, événements créés/mis à jour/supprimés/copiés, conservés pour compliance 

## 🌐 8. Hébergement de site statique

- Supporté via Blob Storage : conteneurs en public readonly, avec index.html et 404.html.
- HTTPS + domaines personnalisés → nécessite Azure CDN 

## 📚 9. Taille maximale

- Block Blob : ~190,7 TiB 
- Page Blob : jusqu’à 8 TiB 

## ✅ 10. Points clés pour l’examen

- Savoir quand utiliser block/page/append blobs.
- Connaître les réplications et leur but.
- Maîtriser les access tiers et leur automatisation.
- Maîtriser SDK, AzCopy, CLI pour manipuler les blobs.
- Comprendre la différence entre Event Grid vs Change Feed.
- Configurer la sécurité : Shared Key, SAS, User Delegation.
- Utiliser Static Website + CDN pour HTTPS custom domain.
- Mémoire des tailles limites blob.
## 📚 Resources
- [Introduction à Azure Blob Storage](https://learn.microsoft.com/azure/storage/blobs/storage-blobs-introduction)
- [Comparaison des options de redondance](https://learn.microsoft.com/azure/storage/common/storage-redundancy)

