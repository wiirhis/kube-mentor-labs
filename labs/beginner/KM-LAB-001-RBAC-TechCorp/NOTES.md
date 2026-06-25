# NOTES – KM-LAB-001

## À retenir

RBAC signifie **Role-Based Access Control**.

Son objectif est de contrôler précisément qui peut faire quoi dans Kubernetes.

---

# Les objets RBAC

| Objet              | Rôle                                                                                     |
| ------------------ | ---------------------------------------------------------------------------------------- |
| Role               | Définit des permissions dans un namespace.                                               |
| ClusterRole        | Définit des permissions au niveau du cluster ou réutilisables dans plusieurs namespaces. |
| RoleBinding        | Associe un utilisateur, un groupe ou un ServiceAccount à un Role.                        |
| ClusterRoleBinding | Associe un ClusterRole à l'échelle du cluster.                                           |

---

# Les verbes les plus courants

| Verbe  | Action                               |
| ------ | ------------------------------------ |
| get    | Lire une ressource                   |
| list   | Lister plusieurs ressources          |
| watch  | Observer les changements             |
| create | Créer une ressource                  |
| update | Remplacer une ressource              |
| patch  | Modifier partiellement une ressource |
| delete | Supprimer une ressource              |

---

# API Groups utilisés

| Ressource    | API Group   |
| ------------ | ----------- |
| Pods         | `""` (core) |
| Pods Logs    | `""` (core) |
| Deployments  | `apps`      |
| StatefulSets | `apps`      |
| CronJobs     | `batch`     |

---

# Commandes utiles

## Vérifier le contexte

```bash
kubectl config current-context
```

---

## Changer de contexte

```bash
kubectl config use-context <nom-contexte>
```

---

## Tester une permission

```bash
kubectl auth can-i get pods
```

---

## Tester une permission dans un namespace

```bash
kubectl auth can-i create deployment -n production
```

---

## Décrire un Role

```bash
kubectl describe role <nom> -n production
```

---

## Décrire un RoleBinding

```bash
kubectl describe rolebinding <nom> -n production
```

---

# Les pièges classiques

* Oublier le namespace.
* Confondre `Role` et `ClusterRole`.
* Oublier `pods/log`.
* Penser que `update` autorise automatiquement `patch`.
* Oublier les sous-ressources comme `deployments/scale`.
* Tester avec le mauvais contexte Kubernetes.

---

# Les bonnes pratiques

* Toujours appliquer le principe du moindre privilège.
* Tester les permissions avec `kubectl auth can-i`.
* Vérifier le contexte avant toute opération.
* Documenter les incidents rencontrés.
* Donner uniquement les droits nécessaires au métier.

---

# Ce que je dois être capable d'expliquer

* Pourquoi utiliser RBAC ?
* Quand choisir un Role ?
* Quand choisir un ClusterRole ?
* Pourquoi les Secrets doivent-ils être protégés ?
* Pourquoi `pods/log` est-il une ressource distincte ?
* Pourquoi `kubectl scale` nécessite `deployments/scale` ?

---

# Niveau atteint

À l'issue de ce laboratoire, je suis capable de :

* concevoir une politique RBAC ;
* créer un Role et un RoleBinding ;
* attribuer des permissions à un utilisateur ;
* vérifier les droits accordés ;
* identifier les principales erreurs de configuration RBAC.

