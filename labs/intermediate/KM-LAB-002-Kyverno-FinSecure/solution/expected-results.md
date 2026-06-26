# Résultats attendus – KM-LAB-002

## Installation

```bash
kubectl get pods -n kyverno
```

Résultat attendu :

* Tous les contrôleurs sont à l'état **Running**.
* Aucun Pod n'est en erreur.

---

## Validation du label `owner`

### Sans label

```bash
kubectl run test-no-owner --image=nginx
```

Résultat attendu :

```text
Error from server: admission webhook denied the request
Policy require-owner-label failed
```

### Avec le label

```bash
kubectl run test-with-owner \
  --image=nginx \
  --labels owner=rhisland
```

Résultat attendu :

```text
pod/test-with-owner created
```

---

## Restriction des registres

### Docker Hub

```bash
kubectl run img-ok \
  --image=nginx \
  --labels owner=rhisland
```

Résultat attendu :

```text
pod/img-ok created
```

### GHCR

```bash
kubectl run img-ko \
  --image=ghcr.io/nginx/nginx \
  --labels owner=rhisland
```

Résultat attendu :

```text
validation failure:
Only images from docker.io are allowed.
```

---

## Mutation

```bash
kubectl get pod mutate-test --show-labels
```

Résultat attendu :

```text
owner=rhisland
team=production
```

---

## Génération

```bash
kubectl get configmap company-info \
-n kyverno-generate-test
```

Résultat attendu :

```text
company-info
```

Le contenu attendu est :

```yaml
data:
  company: FinSecure
  environment: production
```

---

## Nettoyage automatique

```bash
kubectl auth can-i delete pods \
--as=system:serviceaccount:kyverno:kyverno-cleanup-controller
```

Résultat attendu :

```text
yes
```

Création :

```bash
kubectl run temp-pod \
--image=nginx \
--labels owner=rhisland,cleanup.kyverno.io/ttl=2m
```

Après environ deux minutes :

```bash
kubectl get pod temp-pod
```

Résultat attendu :

```text
Error from server (NotFound)
```

---

## Conclusion

Si tous les résultats ci-dessus sont obtenus, le laboratoire est considéré comme validé.

