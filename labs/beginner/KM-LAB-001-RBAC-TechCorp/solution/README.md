# Solution – KM-LAB-001 RBAC TechCorp

Cette solution décrit la mise en œuvre validée du laboratoire RBAC.

## Objets créés

- Namespace `production`
- Role `application-delivery`
- RoleBinding `jdupont-application-delivery`
- Contexte kubectl `ApplicationDelivery-context`

## Principe retenu

Le besoin est limité au namespace `production`.

Le choix correct est donc un `Role` associé à un `RoleBinding`, et non un `ClusterRole`.

## Permissions accordées

L'utilisateur `jdupont` peut consulter, créer et modifier :

- Pods
- Deployments
- StatefulSets
- CronJobs

Il peut aussi consulter les logs des Pods via `pods/log`.

## Restrictions

L'utilisateur `jdupont` ne peut pas :

- supprimer des ressources ;
- lire les Secrets ;
- modifier RBAC ;
- accéder aux autres namespaces.
