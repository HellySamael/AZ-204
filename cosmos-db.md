# Cosmos DB

## ⚙️ 1. Présentation & avantages

- Globally distributed, NoSQL multimodèle géré, faible latence, haute disponibilité 
- Données non structurées, semi‑structurées, structurées, vecteurs 
- Idéal pour applications à grande échelle et répartition globale.


## 🛠️ 2. Architecture & hiérarchie

- Compte → Base de données → Conteneur (partitionné) → Élément (item/document) .
- Indexation automatique par défaut, personnalisable via politique d’index .


## 🌐 3. API supportées

- SQL (Core/NoSQL) – syntaxe SQL + JS (procédures stockées, triggers, UDF).
- MongoDB, Cassandra, Gremlin, Table, PostgreSQL 
- Choisir l’API selon le modèle de données et les compétences existantes.


## 📏 4. Partitionnement & scalabilité

- Partition logique via clé de partition : items similaires ensemble.
- Partitions physiques → scale horizontally, redimensionnement transparent .
- Bien choisir la clé : éviter les requêtes cross-partition.


## 🧠 5. Throughput & Request Units (RUs)

- Unité de performance = RU/s garantis (<10 ms latence 99e centile) 
- Mode Provisioned ou Serverless/autoscale, au niveau base ou conteneur.


## ⏱️ 6. Niveaux de cohérence

- Strong, Bounded Staleness, Session, Consistent Prefix, Eventual 
- Par défaut : Session. Ajuster selon exigences latence/consistance.
- Bounded Staleness recommandé pour multi‑région écriture avec SLA latence 


## 🗺️ 7. Réplication & disponibilité géographique

- Activation multi‑régions pour haute disponibilité et proximité applicative.
- Failover automatique ou manuel.
- Mode multi-master possible (gestion des conflits : LWW ou personnalisé).


## 🔄 8. Change Feed & intégration event-based

- Change Feed pour capter insertions/mises à jour 
- Permet dénormalisation, agrégation, intégrité réf., archivage via Azure Functions, Event Hubs 


## 🧭 9. Indexation & optimisation des requêtes

- Index automatique ; possibilité de configurer manuellement (range, composite…).
- Analyser le coût RU d’une requête (point vs agrégat).
- Activer integrated cache pour optimiser les lectures 


## 🗃️ 10. Sauvegarde & restauration

- Modes périodique ou continue pour point-in-time restore 
- Clé de sauvegarde à configurer selon RPO/RTO requis.


## 🔒 11. Sécurité & accès

- Chiffrement au repos par défaut ; prise en charge de clés managées par client.
- Contrôle d’accès via Azure RBAC (control plane) et AAD (data plane) 
- Configurer Réseau (pare-feu", VNet, CORS…) pour durcir la sécurité.


## 📊 12. Monitoring & diagnostic

- Suivi des métriques RUs, latence, erreurs, distribution des partitions via Azure Monitor.
- Configurer alertes basées sur ces métriques 
- Journaux d’analyse via Log Analytics ou Event Hub.


## ✅ 13. Attendus pour l’examen AZ‑204

- SDK : opérations CRUD, cohérence, change feed.
- Configurat° compte : partitionnement, cohérence, autoscale, réplication.
- Integration event-based avec Azure Functions.
- Optimisation : RU, index, cache.
- Sécurité : RBAC, data plane, chiffrement.
- Backup & restore.


## 💡 14. Conseils d'étude

- Microsoft Learn modules Cosmos DB pour AZ‑204 
- Pratique :
  - Créer un compte en mode provisioned + autoscale.
  - Tester avec SQL API : CRUD, triggers, stored procedures.
  - Implémenter Change Feed + Azure Functions (ex. dénormalisation).
  - Modifier cohérence, ajouter régions, simuler failover manuel.
  - Vérifier consommation RU, configurer alertes.
  - Analyser cas d’usage réels (multi-master, SLA, requêtes complexes).

## 📚 Resources
- [Introduction à Azure Cosmos DB](https://learn.microsoft.com/azure/cosmos-db/introduction)
- [Choisir une clé de partition](https://learn.microsoft.com/azure/cosmos-db/partitioning-overview#choose-your-partition-key)


# Récapitulatif – Azure Cosmos DB (AZ-204)

## 1. Structure
- **Compte** Cosmos DB → multi-régions.
- **Database** → contient des containers.
- **Container** → unité de scalabilité (partitions).
- **Item** = document JSON (SQL API).
- **Clé unique** d’un item = `(PartitionKey + id)`.
- **Partition physique** ≤ 50 Go.

---

## 2. Provisionnement & RUs
- **RUs (Request Units)** = monnaie Cosmos DB (CPU + mémoire + I/O).
- Lecture 1 Ko ≈ 1 RU, écriture ≈ 5 RUs.
- Modes :
  - **Provisioned throughput** (min 400 RUs/s).
  - **Autoscale** (10 % à 100 % d’un plafond).
  - **Serverless** (≤ 50 Go, facturation à la consommation).

---

## 3. Niveaux de consistance (5)
1. **Strong** → lecture = dernière écriture (latence ↑, dispo limitée en multi-région).
2. **Bounded staleness** → retard max (opérations ou durée).
3. **Session** → par défaut, chaque client voit ses propres écritures immédiatement.
4. **Consistent prefix** → respect de l’ordre, pas forcément la fraîcheur.
5. **Eventual** → convergence finale, plus rapide/moins cher.

---

## 4. Indexation
- Indexation **automatique** de toutes les propriétés.
- **Indexing policy** → inclure/exclure des champs pour réduire coûts.
- **Index composite** → accélère `ORDER BY` sur plusieurs champs.
- ⚠️ Requêtes **cross-partitions** = coût RU ↑.

---

## 5. Change Feed
- Liste ordonnée d’inserts/updates.
- Pas de deletes sauf soft-delete flag.
- Intégration → **Azure Functions trigger**, **Stream Analytics**, **Databricks**.
- Cas d’usage → sync bases, analytics temps réel, ETL.

---

## 6. Sécurité
- Authentification : **clé de compte** (⚠️ trop large), **Azure AD RBAC** (recommandé), **SAS token**.
- Réseau : firewall IP, Private Endpoint.
- Chiffrement : par défaut + option CMK via Key Vault.

---

## 7. Multi-région & réplication
- **Multi-region write** (écriture partout) ou **single-region write**.
- **Failover** automatique ou manuel (priorité configurable).
- Impact consistance :
  - **Strong** → seulement ≤ 2 régions proches.
  - **Session** → par défaut, recommandé globalement.
  - Autres niveaux → compatibles multi-régions.

---

## 8. Limites
- Taille max item (SQL API) : **2 MB**.
- Partition physique : **50 Go max**.

