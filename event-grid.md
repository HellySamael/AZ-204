# Azure Event Grid

- intégration sur tous les services Azure. Par ex. événement à la création d'un blob sur un Storage Account.
  - Sources : Blob Storage, Resource Groups, Cloud Events Sources, Souscriptions, Custom Events, etc.
  - Handlers : serverless code / worklflow, App Service, Functions, etc.
- élimine le besoin du _constant polling_.
- mode **push** (mode principal) : Event Grid informe les souscripteurs de l'événement.
- **Topic** : ensemble d'événements liés. Une souscription s'enregistre auprès d'un topic.
- Durabilité :
  - Retry schedule : choix entre retenter, dead-letter ou drop le message.
  - Retry policy : nombre maximum de tentatives, TTL.
  - Delayed delivery : en cas d'échec, il retente plus tard.
  - Dead-letter events : si le message n'a pu être délivré, il est envoyé dans un storage account.
  - Order : pas de garanti d'ordre.

<hr/>

## Résumé ChatGPT

Voici ta fiche de révision sur **Azure Event Grid**, adaptée pour l’examen **AZ‑204** en français :

---

## 🔹 1. Définition & concepts clés

* **Azure Event Grid** est un service managé de type pub/sub, serverless et hautement scalable, conçu pour la distribution d’événements en quasi‑temps réel, entre services Azure, applications ou webhooks ([learn.microsoft.com][1]).
* Principaux concepts :

  * **Éditeurs (Publishers)** : sources générant des événements (ex. Azure Blob, services personnalisés) .
  * **Topics** : points d’entrée pour publier des événements (custom topics, system topics, domains) ([docs.azure.cn][2]).
  * **Abonnements (subscriptions)** : définissent où envoyer, comment filtrer (par type, sujet) les événements ([learn.microsoft.com][1]).
  * **Handlers** : destinataires finaux (Azure Functions, Logic Apps, webhooks, Event Hubs, Service Bus…) ([learn.microsoft.com][3]).

---

## 🔹 2. Modes de livraison

* **Push** : Event Grid pousse les événements vers les handlers via HTTP/webhook ([learn.microsoft.com][1]).
* **Pull** : les clients se connectent pour extraire les événements, supporte CloudEvents et Private Link ([learn.microsoft.com][1]).

---

## 🔹 3. Fiabilité & gestion des erreurs

* Garantie de livraison **"au moins une fois"**, avec réessais par back‑off exponentiel (jusqu’à 24 h en GA) ([red-gate.com][4]).
* Événements non livrés finissent dans la **dead‑letter queue** si configurée ([c-sharpcorner.com][5]).

---

## 🔹 4. Sécurité et conformité

* Intégration avec **Azure AD** pour l’authentification/autorisation.
* Support des **Private Endpoints** (pull only), VNet, DDoS, WAF ([technetmagazine.com][6], [reddit.com][7]).
* Conformité aux normes sécurité Azure (SLA, certifications...) .

---

## 🔹 5. Scénarios d’usage (AZ‑204)

1. **Applications serverless** :

   * Déclenchement d’une Azure Function ou Logic App à chaque création de blob ([azure.microsoft.com][8]).
2. **Automatisation d’infra** :

   * Réagir à la création de VM, SQL, etc. pour appliquer des politiques ([azure.microsoft.com][8]).
3. **Intégration d’applications** :

   * Routage d’événements personnalisés ou SaaS (Auth0, Graph, SAP) vers des services ([learn.microsoft.com][3]).
4. **IoT & MQTT** :

   * Support des messages MQTT v3.1/v5 via MQTT broker pour télémetrie & contrôle ([learn.microsoft.com][1]).

---

## 🔹 6. Éviter les confusions avec Event Hub & Service Bus

* **Event Grid = push d’événements (statut)** (fire‑and‑forget) ([reddit.com][9]).
* **Event Hub = ingestion de flux haute volume, pull**.
* **Service Bus = file d’attente avec garantie d’ordre/transaction** (fire‑and‑don’t‑forget) ([reddit.com][9]).
* **Choisir selon le besoin** :

  * Notification/trigger → Event Grid.
  * Stream haute capacité → Event Hub.
  * Messages ordonnés/fiables → Service Bus.

---

## 🔹 7. Intégration dans l’AZ‑204

Les objectifs de l’examen incluent :

* **Explorer** Event Grid via Azure CLI/SDK (création topic, gestion abonnements, filtrage) ([reddit.com][9], [reddit.com][10], [learn.microsoft.com][11]).
* **Implémenter** contrôle d’accès, events personnalisés vers webhook/Azure Functions ([learn.microsoft.com][12]).

---

## 🔹 8. Bonnes pratiques

* **Filtrage avancé** : sur eventType, subject, données du payload ([docs.azure.cn][2]).
* **Dead‑letter & monitoring** : activer dead‑letter, utiliser Azure Monitor pour les alertes (voire Serverless360) ([reddit.com][13]).
* **Batching** : activer regroupement d’événements pour améliorer le throughput ([reddit.com][9]).
* **Sécurité** : privilégier Private Endpoints/VNet, Azure AD, logging ([reddit.com][7]).

---

## ✅ Résumé visuel

| Aspect                  | Azure Event Grid                                     |
| ----------------------- | ---------------------------------------------------- |
| Modèle                  | Pub/Sub, push/pull                                   |
| Échelle                 | Millions événements/s, scaling automatique           |
| Livraison               | Au moins une fois, retries, dead‑letter              |
| Sécurité                | Azure AD, Private Endpoint, VNet                     |
| Intégrations Azure      | Functions, Logic Apps, Event Hubs, Service Bus…      |
| Scénarios               | Serverless, IoT, automatisation, intégration SaaS    |
| À connaître pour AZ‑204 | CLI/SDK, topics, abonnements, filtres, Custom events |

---

### ✅ Entraîne-toi pour l’examen

* Utilise les modules officiels AZ‑204 : *Explorer Azure Event Grid* ([docs.azure.cn][2], [learn.microsoft.com][14]).
* Crée des **Custom Topics**, un **Event Subscription** via Azure CLI ou PowerShell, et teste avec une **Azure Function**.
* Mets en œuvre des **filtres**, active la **dead‑lettering** et automatise une action sur la création d’un blob.

---

Si tu veux approfondir avec un exemple pratique ou un tutoriel CLI/SDK, je peux t’en préparer un avec plaisir !

[1]: https://learn.microsoft.com/fr-fr/azure/event-grid/overview?utm_source=chatgpt.com "Présentation d’Azure Event Grid - Azure Event Grid | Microsoft Learn"
[2]: https://docs.azure.cn/en-us/event-grid/overview?utm_source=chatgpt.com "Introduction to Azure Event Grid - Azure Event Grid | Azure Docs"
[3]: https://learn.microsoft.com/en-us/azure//event-grid/overview?utm_source=chatgpt.com "Overview - Azure Event Grid | Microsoft Learn"
[4]: https://www.red-gate.com/simple-talk/cloud/platform-as-a-service/introduction-azure-event-grid/?utm_source=chatgpt.com "An Introduction to Azure Event Grid - Simple Talk"
[5]: https://www.c-sharpcorner.com/article/understanding-azure-event-grid/?utm_source=chatgpt.com "Understanding Azure Event Grid"
[6]: https://www.technetmagazine.com/master-solutions-azure-event-grid/?utm_source=chatgpt.com "Master Event-Driven Solutions with Azure Event Grid: Setup, Best Practices, and Use Cases"
[7]: https://www.reddit.com/r/AZURE/comments/1dpnqi5?utm_source=chatgpt.com "Event Grid / Eventhub Security"
[8]: https://azure.microsoft.com/fr-fr/products/event-grid?utm_source=chatgpt.com "Azure Event Grid – Gestionnaire d’événements | Microsoft Azure"
[9]: https://www.reddit.com/r/AZURE/comments/xwh5xs?utm_source=chatgpt.com "Confused when to use Event Grid, Event Hub and Service Hub"
[10]: https://www.reddit.com/r/AZURE/comments/zrdmcu?utm_source=chatgpt.com "event grid vs event hubs for event driven microservices"
[11]: https://learn.microsoft.com/fr-fr/credentials/certifications/resources/study-guides/az-204?utm_source=chatgpt.com "Guide d’étude pour l’examen AZ-204 : Développement de solutions pour Microsoft Azure | Microsoft Learn"
[12]: https://learn.microsoft.com/fr-fr/azure/event-grid/?utm_source=chatgpt.com "Documentation Azure Event Grid | Microsoft Learn"
[13]: https://www.reddit.com/r/AZURE/comments/zqgcld?utm_source=chatgpt.com "How to monitor Azure Event Grid on multiple metrics at no extra cost?"
[14]: https://learn.microsoft.com/fr-fr/training/paths/az-204-develop-event-based-solutions/?utm_source=chatgpt.com "AZ-204 : Développer de solutions basées sur les événements - Training | Microsoft Learn"


