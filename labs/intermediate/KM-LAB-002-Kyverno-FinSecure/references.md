# Références officielles

## Documentation Kyverno

https://kyverno.io/docs/

---

## Helm Chart

https://artifacthub.io/packages/helm/kyverno/kyverno

---

## Policies officielles

https://kyverno.io/policies/

---

## Types de policies

### Validate

https://kyverno.io/docs/policy-types/cluster-policy/validate/

### Mutate

https://kyverno.io/docs/policy-types/cluster-policy/mutate/

### Generate

https://kyverno.io/docs/policy-types/cluster-policy/generate/

### Cleanup

https://kyverno.io/docs/policy-types/cleanup-policy/

---

## Admission Controllers Kubernetes

https://kubernetes.io/docs/reference/access-authn-authz/extensible-admission-controllers/

---

## RBAC Kubernetes

https://kubernetes.io/docs/reference/access-authn-authz/rbac/

---

## Ce qui a été adapté dans ce lab

- Validation d'un label obligatoire (`owner`).
- Restriction des images au registre Docker Hub.
- Ajout automatique du label `team=production`.
- Génération automatique d'une ConfigMap `company-info`.
- Correction du RBAC du Cleanup Controller afin de permettre le nettoyage TTL.
