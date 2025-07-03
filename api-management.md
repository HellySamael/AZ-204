# API Management

Standardiser les appels aux API : sécurité, ratings, transformations des requêtes, cache, etc.

- Admin interface :
  - gestion utilisateurs & groupes
  - sécurité
  - analytiques
  - API spécifications
- Gateway
  - ratings
  - sécurité
  - routing vers les backends
  - mise en cache
- Developer Portal
  - API docs
  - tests API
  - souscriptions
  - analytiques

## Policy

- inbound:
  - Forcer un rate limit
  - Usage quota
  - Filtrage d'IP
  - Validation de token JWT
- outbound :
  - formattage de la réponse
  - custom réponse
  - log dans Event Hub
  - mise en cache
 
