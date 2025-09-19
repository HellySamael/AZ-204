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

# Récapitulatif – Azure Storage (AZ-204)

## 1. Blob Storage
- **Types de blobs** :
  - **Block Blob** : fichiers classiques (images, vidéos, documents, backups).
  - **Append Blob** : logs append-only (journalisation).
  - **Page Blob** : stockage aléatoire en pages, utilisé pour disques Azure.
- **Containers et accès** :
  - Private, Blob (public read blobs), Container (public read + listing).
  - Accès recommandé via SAS ou Azure AD, pas via clé partagée.
- **Fonctionnalités avancées** :
  - **Soft Delete** : restaure blobs supprimés (1–365 j).
  - **Blob Versioning** : nouvelle version automatique à chaque modif.
  - **Snapshots** : capture manuelle d’un état.
  - **Immutable Blob (WORM)** : Write Once, Read Many – conformité légale.
  - **Lifecycle Management** : règles automatiques de tiering (Hot → Cool → Archive) et suppression.

---

## 2. Queue Storage
- **Caractéristiques** :
  - File simple, messages ≤ 64 KB.
  - Nombre de messages quasi illimité.
  - Delivery = **at-least-once** (jamais exactly-once).
- **Visibility timeout** :
  - Message lu devient invisible pendant X secondes.
  - Si traitement OK → `DeleteMessage`.
  - Si échec ou timeout → message réapparaît.
- **Poison queue** :
  - Après N échecs (par défaut 5), message déplacé dans `nom-queue-poison`.
- **Différences avec Service Bus Queue** :
  - Pas de FIFO stricte (≈ ordre mais non garanti).
  - Pas de sessions, transactions, DLQ évolués.
  - Pas de topics/pub-sub.

---

## 3. Table Storage
- **Nature** : base NoSQL clé-valeur, sans schéma fixe.
- **Structure** :
  - Table → Entités → propriétés.
  - Clé primaire = `(PartitionKey + RowKey)`.
- **Transactions** :
  - Possible uniquement **dans une même partition**.
  - Pas de transactions multi-partitions.
- **Scénarios** :
  - Données simples, lookup rapide par ID, grande scalabilité.
  - Pas de relations complexes ni de jointures.
- **Comparaison Cosmos DB (Table API)** :
  - Cosmos DB offre SLA, réplication multi-région, indexation automatique, transactions avancées.

---

## 4. Sécurité et accès
- **Shared Key** : accès complet au compte (⚠️ à éviter).
- **SAS (Shared Access Signature)** :
  - **Service SAS** : accès limité à une ressource (blob, queue, table).
  - **Account SAS** : accès multi-services du compte.
  - **User Delegation SAS** : SAS signée via Azure AD → sans clé partagée (sécurité moderne).
- **Azure AD / RBAC** : recommandé pour accès applicatif sécurisé.

---

## 5. Points d’examen à retenir
- Blob :
  - Block = fichiers, Append = logs, Page = disques.
  - Soft Delete = récup après suppression, Versioning = historique, Snapshots = backup ponctuel, Immutable = WORM.
- Queue :
  - Messages 64 KB, poison queue, at-least-once delivery, visibility timeout.
- Table :
  - Clé = PartitionKey + RowKey, batch = même partition.
- SAS :
  - Service SAS = ressource précise.
  - Account SAS = multi-services.
  - User Delegation SAS = via Azure AD (sécurité moderne).


