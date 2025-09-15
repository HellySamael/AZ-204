# Authentification

Gestion de l'identité et de l'accès dans Azure.

## 🔐 Azure AD
- Service d'annuaire et d'authentification centralisé.
- **App registrations** → crée un **Service Principal** pour l’application.
- Support OAuth2, OpenID Connect, SAML ; flux Client Credentials, Auth Code…
- **RBAC** : rôles built-in ou personnalisés pour contrôler l’accès aux ressources Azure.
- **Azure AD B2C** pour authentifier les utilisateurs externes (Google, Facebook…).

## 🔑 Tokens & autorisation
- Jetons **access** et **refresh**, porteurs de **scopes** / **roles**.
- Audiences (`aud`), durées de vie, signature JWT.
- Authentification API via MSAL, `WWW-Authenticate` et `Authorization: Bearer`.

## 🆔 Managed Identities
- Identités gérées pour services Azure, évite stocker des secrets.
- **System-assigned** : liée à la ressource, supprimée avec elle.
- **User-assigned** : ressource indépendante réutilisable.
- Utilisation avec Key Vault, Storage, SQL, etc. via l’attribution de rôles.

## 🌐 Sécurisation des ressources
- Stocker secrets/certificats dans **Azure Key Vault** ; accès via RBAC ou policies.
- Pour Storage : choisir entre **SAS** ou **Azure AD** (user delegation SAS).
- Restreindre l’accès réseau : pare-feu, VNet, Private Endpoint.

## ✅ Pour l'examen
- Protéger une API avec Azure AD et scopes/roles.
- Utiliser une Managed Identity pour accéder à une ressource (ex. Key Vault).
- Connaître la différence entre user-assigned et system-assigned et la gestion des tokens.
## 📚 Resources
- [Azure Active Directory pour les développeurs](https://learn.microsoft.com/azure/active-directory/develop/)
- [Identités managées pour ressources Azure](https://learn.microsoft.com/azure/active-directory/managed-identities-azure-resources/overview)
- [Contrôle d'accès basé sur les rôles](https://learn.microsoft.com/azure/role-based-access-control/overview)
