# Correction

## Éléments attendus

Le laboratoire devait aboutir à la mise en place des objets suivants :

* Namespace `production`
* Role `application-delivery`
* RoleBinding `jdupont-application-delivery`

---

## Validation des permissions

Les actions suivantes doivent être autorisées :

* Consultation des Pods
* Création des Pods
* Modification des Pods
* Consultation des logs
* Gestion des Deployments
* Gestion des StatefulSets
* Gestion des CronJobs

---

## Validation des restrictions

Les actions suivantes doivent être refusées :

* Lecture des Secrets
* Liste des Secrets
* Suppression des ressources
* Création ou modification des objets RBAC
* Accès aux autres namespaces

---

## Remarques

### `kubectl scale`

La commande :

```bash
kubectl scale deployment ...
```

a échoué car elle utilise la sous-ressource :

```text
deployments/scale
```

Cette permission n'était pas présente dans le `Role`.

L'utilisation de :

```bash
kubectl patch deployment ...
```

a permis d'obtenir le résultat attendu.

---

### Secrets

L'accès aux Secrets est correctement refusé.

Cette restriction est essentielle car les Secrets peuvent contenir :

* mots de passe ;
* clés API ;
* certificats ;
* jetons d'authentification.

---

### RBAC

La création d'un `Role` par `jdupont` est correctement refusée.

Cela empêche toute élévation de privilèges.

---

## Conclusion

Le laboratoire est conforme aux exigences. Les permissions accordées répondent au besoin métier tout en respectant le principe du moindre privilège.

