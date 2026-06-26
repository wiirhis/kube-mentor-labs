# Analyse du laboratoire

## Résumé

Le laboratoire a permis de mettre en œuvre les principaux mécanismes de Kyverno :

- Installation avec Helm
- Validation
- Mutation
- Génération
- Nettoyage automatique (TTL)

## Points forts

- Bonne compréhension du fonctionnement général de Kyverno.
- Bonne utilisation de la documentation officielle.
- Démarche de diagnostic cohérente.
- Vérification systématique des policies.

## Difficultés rencontrées

### Policy Validate

Une erreur dans une expression CEL empêchait la validation.

### Image Policy

Le template choisi vérifiait une signature Cosign alors que le besoin concernait le registre d'images.

### Generate

Le template sélectionné mutait les Pods au lieu de générer une ConfigMap.

### Cleanup

Le Cleanup Controller détectait correctement le label TTL mais ne possédait pas les permissions RBAC nécessaires pour supprimer les Pods.

Le diagnostic a été réalisé avec :

- kubectl logs
- kubectl auth can-i
- analyse des ClusterRole
- analyse des ClusterRoleBinding

La correction consistait à ajouter un ClusterRole autorisant la suppression des Pods.

## Conclusion

Tous les objectifs du laboratoire ont finalement été atteints après correction.
