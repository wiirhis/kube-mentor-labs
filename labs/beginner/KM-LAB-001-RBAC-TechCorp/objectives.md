# Objectifs du laboratoire

## Objectif principal

Mettre en œuvre une politique **RBAC (Role-Based Access Control)** permettant de sécuriser l'accès à un cluster Kubernetes en appliquant le principe du moindre privilège.

---

# Objectifs pédagogiques

À l'issue de ce laboratoire, vous devrez être capable de :

## Comprendre RBAC

* Expliquer le rôle de RBAC dans Kubernetes.
* Comprendre pourquoi RBAC est indispensable dans un cluster partagé.
* Identifier les différents objets RBAC.

---

## Analyser un besoin métier

À partir d'un cahier des charges :

* identifier les ressources Kubernetes concernées ;
* identifier les API Groups ;
* déterminer les verbes RBAC nécessaires ;
* choisir entre un `Role` et un `ClusterRole`.

---

## Concevoir une politique RBAC

Être capable de :

* créer un `Role` ;
* créer un `RoleBinding` ;
* associer un utilisateur à un rôle ;
* limiter les permissions à un namespace.

---

## Vérifier les permissions

Savoir utiliser :

```bash
kubectl auth can-i
```

pour vérifier :

* les autorisations ;
* les restrictions ;
* le périmètre des permissions.

---

## Réaliser une validation opérationnelle

Être capable de démontrer que :

* les ressources autorisées peuvent être créées et modifiées ;
* les ressources interdites sont correctement protégées ;
* les règles RBAC fonctionnent conformément au besoin métier.

---

# Compétences techniques acquises

À la fin du laboratoire, les compétences suivantes doivent être maîtrisées :

* RBAC Kubernetes
* Role
* RoleBinding
* API Groups
* Resources
* Verbs
* Namespace
* kubectl auth can-i
* Validation des permissions
* Validation des restrictions

---

# Bonnes pratiques mises en œuvre

* Application du principe du moindre privilège.
* Limitation des droits au namespace concerné.
* Séparation des responsabilités.
* Validation systématique des autorisations.
* Vérification des restrictions de sécurité.

---

# Critères de réussite

Le laboratoire est considéré comme réussi lorsque :

* toutes les permissions fonctionnent conformément au besoin métier ;
* toutes les restrictions sont effectivement appliquées ;
* les commandes de validation sont exécutées avec succès ;
* l'utilisateur ne peut pas obtenir davantage de privilèges que ceux prévus.

---

# Ce qu'il faut retenir

À l'issue de ce laboratoire, vous devez être capable de concevoir et de mettre en œuvre une politique RBAC répondant à un besoin métier concret, tout en garantissant un niveau de sécurité adapté à un environnement de production.

