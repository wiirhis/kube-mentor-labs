# Résultats attendus

## Vérification des permissions

| Action                  | Résultat attendu |
| ----------------------- | ---------------- |
| Lister les Pods         | ✅ Autorisé       |
| Créer un Pod            | ✅ Autorisé       |
| Modifier un Pod         | ✅ Autorisé       |
| Consulter les logs      | ✅ Autorisé       |
| Créer un Deployment     | ✅ Autorisé       |
| Modifier un Deployment  | ✅ Autorisé       |
| Créer un StatefulSet    | ✅ Autorisé       |
| Modifier un StatefulSet | ✅ Autorisé       |
| Créer un CronJob        | ✅ Autorisé       |
| Modifier un CronJob     | ✅ Autorisé       |

---

## Vérification des restrictions

| Action                   | Résultat attendu |
| ------------------------ | ---------------- |
| Lire un Secret           | ❌ Forbidden      |
| Lister les Secrets       | ❌ Forbidden      |
| Supprimer un Pod         | ❌ Forbidden      |
| Supprimer un Deployment  | ❌ Forbidden      |
| Supprimer un StatefulSet | ❌ Forbidden      |
| Supprimer un CronJob     | ❌ Forbidden      |
| Créer un Role            | ❌ Forbidden      |
| Modifier un Role         | ❌ Forbidden      |
| Créer un RoleBinding     | ❌ Forbidden      |
| Modifier un RoleBinding  | ❌ Forbidden      |

---

## Validation opérationnelle

Le laboratoire est validé lorsque :

* le `Role` est créé ;
* le `RoleBinding` est créé ;
* `jdupont` peut administrer les applications du namespace `production` ;
* `jdupont` ne peut pas accéder aux Secrets ;
* `jdupont` ne peut pas modifier la configuration RBAC ;
* toutes les restrictions sont appliquées conformément au besoin métier.

---

## Conclusion

La politique RBAC respecte le principe du moindre privilège et répond au besoin métier de l'équipe **Application Delivery**.

