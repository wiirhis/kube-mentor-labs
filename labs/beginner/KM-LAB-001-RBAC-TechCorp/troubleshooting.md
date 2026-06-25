# Guide de dépannage (Troubleshooting)

## Objectif

Ce document recense les incidents rencontrés durant la réalisation du laboratoire, leurs causes ainsi que les méthodes de résolution.

---

# Incident n°1

## Symptôme

Lors de l'utilisation du contexte `ApplicationDelivery-context`, la commande :

```bash
kubectl get pods
```

retourne une erreur indiquant que les certificats client sont introuvables.

Exemple :

```text
unable to read client-cert
no such file or directory
```

### Cause

Les chemins vers `jdupont.crt` et `jdupont.key` configurés dans le kubeconfig ne correspondent pas à leur emplacement réel.

### Diagnostic

```bash
kubectl config view
```

ou

```bash
kubectl config view --raw
```

### Résolution

Vérifier :

* l'existence des fichiers ;
* les chemins configurés dans le kubeconfig ;
* les permissions des fichiers.

Puis mettre à jour les chemins avec :

```bash
kubectl config set-credentials
```

---

# Incident n°2

## Symptôme

La commande :

```bash
kubectl scale deployment ...
```

retourne :

```text
Forbidden
User "jdupont" cannot patch resource "deployments/scale"
```

### Cause

Le sous-ressource `deployments/scale` n'est pas autorisée par le `Role`.

### Explication

La commande `kubectl scale` n'agit pas directement sur l'objet `Deployment`.

Elle utilise la sous-ressource :

```text
deployments/scale
```

Cette sous-ressource nécessite une autorisation RBAC spécifique.

### Contournement

Modifier le nombre de réplicas avec :

```bash
kubectl patch deployment ...
```

### Solution

Ajouter les permissions sur :

```yaml
resources:
- deployments/scale
```

si l'utilisation de `kubectl scale` est souhaitée.

---

# Incident n°3

## Symptôme

La commande :

```bash
kubectl apply -f role.yaml
```

échoue avec :

```text
Forbidden
```

### Cause

`kubectl apply` effectue d'abord une lecture (`GET`) de la ressource.

L'utilisateur ne possède pas les permissions RBAC permettant de lire ou modifier les `Role`.

### Résolution

Exécuter cette opération avec un compte administrateur.

---

# Vérifications utiles

## Vérifier le contexte courant

```bash
kubectl config current-context
```

---

## Vérifier les permissions

```bash
kubectl auth can-i ...
```

---

## Décrire un Role

```bash
kubectl describe role
```

---

## Décrire un RoleBinding

```bash
kubectl describe rolebinding
```

---

## Vérifier les événements

```bash
kubectl get events
```

---

# Bonnes pratiques

* Vérifier le contexte Kubernetes avant toute opération.
* Tester les permissions avec `kubectl auth can-i`.
* Ne jamais attribuer plus de privilèges que nécessaire.
* Documenter les erreurs rencontrées afin de faciliter les interventions futures.
* Vérifier les sous-ressources (`pods/log`, `deployments/scale`, etc.) lors de la conception des politiques RBAC.

---

# Enseignements

Ce laboratoire montre que la majorité des problèmes RBAC proviennent :

* d'un mauvais périmètre de permissions ;
* de l'oubli des sous-ressources Kubernetes ;
* d'une mauvaise configuration du kubeconfig ;
* d'une mauvaise compréhension du fonctionnement de certaines commandes `kubectl`.

