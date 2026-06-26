Correction – KM-LAB-002

## Objectifs atteints

- Installation de Kyverno avec Helm.
- Vérification des composants installés.
- Création d'une ValidatingPolicy.
- Création d'une ClusterPolicy de validation.
- Création d'une MutatingPolicy.
- Création d'une ClusterPolicy de génération.
- Validation du mécanisme de nettoyage automatique.

---

## Corrections apportées

### Validate

- Correction de l'expression CEL.
- Suppression de l'utilisation incorrecte de `string(map)`.
- Vérification du label `owner`.

### Validation des images

- Remplacement de la policy de vérification Cosign.
- Mise en place d'une policy limitant les images à Docker Hub.

### Mutation

- Ajout automatique du label :

```yaml
team: production
Génération

Création automatique de :

ConfigMap company-info

dans chaque nouveau namespace.

Cleanup

Le mécanisme TTL ne fonctionnait pas.

L'analyse a montré que le Cleanup Controller ne disposait pas des permissions RBAC nécessaires.

Après ajout d'un ClusterRole et d'un ClusterRoleBinding autorisant la suppression des Pods, le nettoyage automatique a fonctionné.

Compétences acquises
Installer Kyverno.
Comprendre les Admission Controllers.
Écrire une ValidatingPolicy.
Écrire une ClusterPolicy.
Diagnostiquer une erreur CEL.
Diagnostiquer un problème RBAC.
Lire les logs Kyverno.
Tester les policies.
