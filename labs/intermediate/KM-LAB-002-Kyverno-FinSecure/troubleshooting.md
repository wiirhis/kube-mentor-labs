# Troubleshooting – KM-LAB-002 Kyverno FinSecure

# Objectif

Ce document présente une méthodologie de diagnostic applicable aux principaux problèmes rencontrés avec Kyverno.

L'objectif n'est pas seulement de résoudre un incident, mais d'apprendre à identifier sa cause.

---

# 1. Vérifier que Kyverno est installé

## Contrôleurs

```bash
kubectl get pods -n kyverno
```

Tous les Pods doivent être à l'état :

```text
Running
```

---

## Helm

```bash
helm list -n kyverno
```

Vérifier que la release est déployée.

---

# 2. Vérifier les CRD

```bash
kubectl get crd | grep kyverno
```

Les principales CRD doivent être présentes.

Exemples :

* clusterpolicies
* validatingpolicies
* mutatingpolicies
* cleanuppolicies

---

# 3. Vérifier les Policies

Lister toutes les policies :

```bash
kubectl get cpol
```

ou

```bash
kubectl get validatingpolicy
```

Puis contrôler :

```bash
kubectl describe <policy>
```

---

# 4. Vérifier les logs

Admission Controller

```bash
kubectl logs -n kyverno deploy/kyverno-admission-controller
```

Background Controller

```bash
kubectl logs -n kyverno deploy/kyverno-background-controller
```

Cleanup Controller

```bash
kubectl logs -n kyverno deploy/kyverno-cleanup-controller
```

Reports Controller

```bash
kubectl logs -n kyverno deploy/kyverno-reports-controller
```

Les logs constituent toujours la première source d'information.

---

# 5. Vérifier les évènements Kubernetes

```bash
kubectl get events -A --sort-by=.lastTimestamp
```

ou

```bash
kubectl describe pod <pod>
```

---

# 6. Vérifier les permissions RBAC

Tester les permissions du contrôleur :

```bash
kubectl auth can-i <verbe> <ressource> \
--as=system:serviceaccount:kyverno:<serviceaccount>
```

Exemple :

```bash
kubectl auth can-i delete pods \
--as=system:serviceaccount:kyverno:kyverno-cleanup-controller
```

---

# 7. Vérifier les webhooks

```bash
kubectl get validatingwebhookconfigurations
```

```bash
kubectl get mutatingwebhookconfigurations
```

Le webhook Kyverno doit être présent.

---

# 8. Vérifier les ressources créées

Pour une policy Generate :

```bash
kubectl get configmap -A
```

Pour une policy Mutate :

```bash
kubectl get pod <pod> --show-labels
```

Pour une policy Validate :

Créer volontairement une ressource invalide.

---

# 9. Tester une seule policy à la fois

Toujours :

1. appliquer une policy ;
2. la tester ;
3. la corriger ;
4. passer à la suivante.

Ne jamais diagnostiquer plusieurs policies simultanément.

---

# 10. Erreurs fréquentes

## CEL

Symptômes :

* expression invalide
* type incompatible

Diagnostic :

* relire l'expression CEL ;
* vérifier les types manipulés.

---

## Mutation

Symptôme :

La ressource est créée mais aucune modification n'est visible.

Diagnostic :

* vérifier le webhook ;
* vérifier la règle `match`.

---

## Generate

Symptôme :

La ressource attendue n'est pas créée.

Diagnostic :

* vérifier le namespace ;
* vérifier les logs du Background Controller.

---

## Cleanup

Symptôme :

Les Pods ne sont jamais supprimés.

Diagnostic :

1. vérifier le label TTL ;
2. vérifier les logs du Cleanup Controller ;
3. vérifier le RBAC ;
4. tester avec :

```bash
kubectl auth can-i delete pods \
--as=system:serviceaccount:kyverno:kyverno-cleanup-controller
```

---

# Méthodologie recommandée

Toujours appliquer le même ordre :

1. Observer.
2. Lire les messages d'erreur.
3. Vérifier les événements.
4. Vérifier les logs.
5. Vérifier les permissions.
6. Corriger.
7. Rejouer le test.
