# Récapitulatif – Service Bus / Event Grid / Event Hubs (AZ-204)

## 1. Service Bus
- **Nature** : message broker avancé, fiable.
- **Types** :
  - Queue (point-à-point).
  - Topic/Subscription (pub-sub avec filtres).
- **Caractéristiques** :
  - Taille message : 256 KB (Standard), 1 MB (Premium).
  - FIFO stricte possible avec **sessions**.
  - Transactions multi-messages.
  - **Dead-letter queue (DLQ)** intégrée.
  - **Scheduled delivery** : messages différés.
- **Modes de réception** :
  - **Receive & Delete** : supprime dès réception.
  - **Peek Lock** (par défaut) : message verrouillé, à supprimer/abandonner ensuite.
- **Sécurité** :
  - Shared Access Key ou **Azure AD RBAC** (recommandé).
  - Private Endpoint possible.
- **Scénarios** :
  - Workflows critiques, microservices, pub-sub filtré, intégrations ERP/CRM.

---

## 2. Event Grid
- **Nature** : distribution d’événements (*pub-sub léger*).
- **Caractéristiques** :
  - Latence < 100 ms.
  - Taille d’événement ≤ 64 KB.
  - Retention max : 24 h.
  - Retry automatique avec backoff.
- **Éléments** :
  - Sources (Blob, RG, IoT Hub, etc.).
  - Handlers (Functions, Logic Apps, Service Bus, Webhooks, etc.).
  - Subscriptions (avec filtres).
- **Sécurité** :
  - Validation handshake + signature.
- **Scénarios** :
  - Déclencher une Function à chaque upload.
  - Notifier plusieurs services d’un changement.
  - Monitoring d’état de ressources Azure.
- **Différences** :
  - Pas FIFO, pas de transactions, pas de stockage long terme.

---

## 3. Event Hubs
- **Nature** : ingestion massive d’événements (IoT, logs, analytics).
- **Caractéristiques** :
  - Taille max événement = 1 MB.
  - **Partitions** → parallélisme (producteurs/consommateurs).
  - **Consumer Groups** → vues indépendantes du flux (plusieurs applis lisent en parallèle).
  - **Retention** : 1 jour (par défaut) → 7 j (Standard), 90 j (Premium/Dedicated).
  - **Capture** : archivage auto vers Blob ou Data Lake.
- **Sécurité** :
  - Shared Access Policy ou Azure AD RBAC.
  - Private Endpoint possible.
- **Scénarios** :
  - Ingestion massive (millions d’événements/seconde).
  - IoT, logs, clicstream.
  - Intégration avec Stream Analytics, Databricks, Synapse.

---

## 4. Comparaison rapide
| Service       | Type             | Taille max | Latence | Cas d’usage |
|---------------|------------------|------------|---------|-------------|
| **Service Bus** | Message broker   | 256 KB / 1 MB | ms-s   | Workflows critiques, transactions, FIFO, pub-sub avec filtres |
| **Event Grid** | Notification     | 64 KB      | <100 ms | Notification de changement (Blob, VM, RG) |
| **Event Hubs** | Event ingestion  | 1 MB       | ms      | IoT, télémétrie massive, logs, big data |



# Récapitulatif comparatif – Service Bus / Event Grid / Event Hubs (AZ-204)

| Caractéristique | **Service Bus** | **Event Grid** | **Event Hubs** |
|-----------------|-----------------|----------------|----------------|
| **Type** | Message broker avancé | Notification d’événements (pub-sub léger) | Ingestion massive d’événements |
| **Taille max** | 256 KB (Std), 1 MB (Prem) | 64 KB | 1 MB |
| **Latence** | ms à secondes | < 100 ms | ms |
| **Retention** | Jusqu’à 80 Go (Std), illimité (Prem) | 24 h max | 1 jour (Std), 7 j (Std max), 90 j (Prem/Dedicated) |
| **Modèles** | Queue (P2P), Topic/Subscription (pub-sub) | Subscriptions filtrées (subject, eventType, data) | Partitions + Consumer Groups |
| **Transactions** | ✅ (multi-messages) | ❌ | ❌ |
| **FIFO stricte** | ✅ (Sessions) | ❌ | ❌ (ordre par partition uniquement) |
| **Dead-letter** | ✅ intégré | ❌ (retry 24 h) | ❌ (pas de DLQ, checkpointing côté consommateur) |
| **Scheduled delivery** | ✅ (messages différés) | ❌ | ❌ |
| **Filtrage** | Rules/filters sur subscriptions | Sujet, type, propriétés | ❌ |
| **Scénarios typiques** | Workflows critiques, microservices, intégrations ERP/CRM | Réagir à un upload Blob, changements de ressources Azure, notifs multi-handlers | IoT, logs, clicstream, ingestion massive temps réel |
| **SLA** | Standard/Premium | Oui | Oui |
| **Authentification** | Shared Key ou Azure AD RBAC | Azure AD + signatures | Shared Key ou Azure AD RBAC |

---

## Points clés à retenir pour l’examen
- **Service Bus** → transactions, DLQ, FIFO (sessions), scheduled delivery → pour **workflows critiques**.  
- **Event Grid** → 64 KB, 24 h retention, latence <100 ms, filtres → pour **notifications légères**.  
- **Event Hubs** → ingestion massive, partitions, consumer groups, capture → pour **IoT, logs, analytics**.  

