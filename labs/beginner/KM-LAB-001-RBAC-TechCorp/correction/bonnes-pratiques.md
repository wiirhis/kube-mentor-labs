# Bonnes pratiques

## Principe du moindre privilège

Toujours accorder uniquement les permissions nécessaires à la réalisation des tâches métier.

Éviter l'utilisation de `cluster-admin` sauf cas exceptionnel.

---

## Limiter le périmètre

Lorsque les permissions concernent un seul namespace, utiliser un `Role` plutôt qu'un `ClusterRole`.

---

## Tester systématiquement

Après chaque modification RBAC, vérifier les permissions avec :

```bash
kubectl auth can-i
```

Ne jamais supposer qu'une politique fonctionne sans test.

---

## Sécuriser les Secrets

Ne jamais accorder l'accès aux Secrets sans justification métier.

Les Secrets contiennent souvent des informations sensibles.

---

## Documenter les permissions

Chaque `Role` doit être associé à un besoin métier clairement identifié.

Éviter les permissions inutilisées.

---

## Utiliser des noms explicites

Préférer des noms reflétant la fonction :

* `application-delivery`
* `read-only`
* `backup-operator`

Éviter les noms génériques comme :

* `role1`
* `test-role`

---

## Versionner les manifestes

Tous les objets Kubernetes doivent être stockés dans Git afin de garantir la traçabilité et la reproductibilité.

---

## Vérifier avant mise en production

Avant tout déploiement :

* vérifier les manifestes ;
* vérifier les permissions ;
* tester les restrictions ;
* valider le comportement attendu.

