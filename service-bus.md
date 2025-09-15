# Service Bus

Voici ta fiche de révision sur **Azure Service Bus** pour l’examen **AZ‑204**, avec smileys et explications claires 😊:

---

## 🔹 1. Qu’est-ce que c’est ? 🌐

* **Azure Service Bus** est un service de messagerie cloud managé, orienté file/topic, conçu pour des communications fiables et structurées entre applications distribuées ([marabesi.com][1]).
* Il prend en charge les files d’attente (queues) et le modèle pub/sub via topics + subscriptions.

---

## 🔹 2. Concepts clés 🧩

* **Namespace** : conteneur logique pour queues, topics, subscriptions.
* **Queues** : traitement point-à-point.
* **Topics & Subscriptions** : modèle publish-subscribe (un topic, plusieurs abonnés).
* **Sessions** : pour garantir l’ordre FIFO sur des séquences de messages ([hugobarona.com][2], [github.com][3], [hugobarona.com][4]).
* **Règles / filtres** : SQL/Correlation/Booléens sur les subscriptions .

---

## 🔹 3. Tiers & quotas 🔢

* **Standard** : queues et topics, messages jusqu’à 256 KB.
* **Premium** : isolation dédiée, jusqu’à 1 MB, fonctionnalités avancées (sessions, transactions…) ([marabesi.com][1]).
* **Basic** : files basiques (1-to-1), pas de topics .

---

## 🔹 4. Fonctionnalités avancées 🚀

* **Dead-letter queue (DLQ)** : messages non livrés ou expirés ([github.com][3]).
* **Scheduled delivery** : planifier l’envoi ultérieur d’un message .
* **Message deferral** : repousser le traitement d’un message ([github.com][3]).
* **Transactions** : regrouper plusieurs opérations atomiquement.
* **Auto-forwarding** : transférer automatiquement entre queues/topics ([github.com][3]).
* **Duplicate detection** : détection de doublons sur intervalle([github.com][3]).
* **Autodelete on idle** : suppression automatique après période d’inactivité ([github.com][3]).
* **Geo-disaster recovery** : reprise après sinistre cross-région ([github.com][3]).

---

## 🔹 5. Sécurité & protocoles 🔒

* Support des **Azure RBAC**, **SAS tokens**, **identités managées** ([learn.microsoft.com][5]).
* Utilise **AMQP 1.0** (standard) et HTTP/REST ([github.com][3]).
* Premium conforme à **JMS 2.0** (Java) ([github.com][3]).

---

## 🔹 6. Modèles d’accès messagerie 📬

* **Peek‑Lock** : lire sans supprimer, puis confirmer ou abandonner.
* **Receive‑and‑Delete** : supprimer immédiatement après lecture.
* Sessions : traitement groupé, FIFO, messages liés ([reddit.com][6], [marabesi.com][1]).

---

## 🔹 7. Paramètres à connaître pour AZ‑204 🎯

* Messages maximum : **256 KB** (standard), **1 MB** (premium) ([reddit.com][7]).
* Taille namespace standard \~ 80 GB ([reddit.com][8]).
* Utiliser AZ CLI / SDK : création namespace, queue/topic/subscription, peek, dead‑letter, filtrage ([marabesi.com][1]).

---

## 🔹 8. Exemples d’usage (AZ‑204)

* **Load leveling** : bufferiser les pics (web → queue → traitement) ([examtopics.com][9]).
* **Orchestration** : orchestrer les workflows via topics/subscriptions.
* **Reliability** : messages dédoublés, transactions, DLQ géré automatiquement.
* **Intégration cross‑langues** : AMQP + JMS utilisé en .NET, Java, Python ([reddit.com][10]).

---

## 🔹 9. Bonnes pratiques ✅

* Toujours **activer la DLQ** et surveiller les messages expirés.
* Utiliser **duplicate detection** pour éviter les doublons.
* Appliquer **sessions** si l’ordre est critique.
* Configurer **scheduled delivery** pour les scénarios dépendant du temps.
* Protéger l’accès via des **identités managées** / SAS / RBAC.

---

## 🔹 10. Résumé visuel

| Aspect                      | Service Bus                                                                                    |
| --------------------------- | ---------------------------------------------------------------------------------------------- |
| Modèle                      | Queue (P2P), Topic/Sub (pub‑sub)                                                               |
| Taille message              | 256 KB (Standard), jusqu’à 1 MB (Premium)                                                      |
| Protocoles                  | AMQP 1.0, HTTP/REST                                                                            |
| Livraisons garanties        | Peek‑Lock / Receive‑Delete / DLQ                                                               |
| Fonctionnalités avancées    | Sessions, DLQ, schedule, deferral, transactions, duplicate detection, autoforward, auto-delete |
| Sécurité                    | RBAC, SAS, Managed Identity                                                                    |
| Principaux scénarios AZ‑204 | load levelling, workflows, fiabilité messaging                                                 |

---

### 🎯 Prépare-toi avec des exercices :

1. Crée un **namespace** via CLI, puis une **queue + topic + subscription**.
2. Envoie des messages (taille maxi), expérimente **duplicate detection** et **scheduled delivery**.
3. Teste les **Peek‑Lock** vs **Receive‑Delete** ; force des erreurs pour voir la DLQ.
4. Implémente un flux **pub-sub** avec filtre SQL sur subscription.
5. Intègre via SDK (.NET/Python), utilise sessions si besoin.

---

Besoin d’un exemple de code, d’un script CLI, ou d’un schéma ? Je suis là pour t’aider ! 😊

## 📚 Resources
- [Documentation Service Bus](https://learn.microsoft.com/azure/service-bus-messaging/service-bus-messaging-overview)
- [Comparer les services de messagerie Azure](https://learn.microsoft.com/azure/service-bus-messaging/compare-messaging-services)

[1]: https://marabesi.com/azure/204/6-connect-and-consume-services.html?utm_source=chatgpt.com "AZ-204 Developer Associate: Navigating Azure Service Connectivity and Consumption"
[2]: https://www.hugobarona.com/az-204-study-guide?utm_source=chatgpt.com "Microsoft Certified: Azure Developer Associate (AZ-204) Study Guide - Hugo Barona"
[3]: https://github.com/arvigeus/AZ-204/blob/master/Learning%20Path/Service%20Bus.md?utm_source=chatgpt.com "AZ-204/Learning Path/Service Bus.md at master · arvigeus/AZ-204 · GitHub"
[4]: https://www.hugobarona.com/az204-study-guide-23/?utm_source=chatgpt.com "Microsoft Certified: Azure Developer Associate (AZ-204) Study Guide 2023 - Hugo Barona"
[5]: https://learn.microsoft.com/fr-fr/credentials/certifications/resources/study-guides/az-204?utm_source=chatgpt.com "Guide d’étude pour l’examen AZ-204 : Développement de solutions pour Microsoft Azure | Microsoft Learn"
[6]: https://www.reddit.com/r/AzureCertification/comments/1apw2e0?utm_source=chatgpt.com "My Tips to pass the AZ-204 and Study Guide"
[7]: https://www.reddit.com/r/AZURE/comments/pxc1d3?utm_source=chatgpt.com "Help with an upcoming 204 exam"
[8]: https://www.reddit.com/r/AzureCertification/comments/pxbzir?utm_source=chatgpt.com "Azure 204 exam help"
[9]: https://www.examtopics.com/discussions/microsoft/view/130992-exam-az-204-topic-5-question-49-discussion/?utm_source=chatgpt.com "Exam AZ-204 topic 5 question 49 discussion - ExamTopics"
[10]: https://www.reddit.com/r/csharp/comments/mr4bp3?utm_source=chatgpt.com "I've started a series on using Azure Service Bus"

