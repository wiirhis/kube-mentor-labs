# Validation – KM-LAB-002 Kyverno FinSecure

## Objectif

Valider que toutes les fonctionnalités mises en œuvre dans ce laboratoire fonctionnent conformément aux attentes.

---

# Critères de validation

## 1. Installation de Kyverno

### Vérification

```bash
kubectl get pods -n kyverno
```

### Résultat attendu

* Tous les Pods sont à l'état **Running**.
* Aucun contrôleur n'est en erreur.

---

## 2. Validation des labels

### Test

Créer un Pod sans le label `owner`.

```bash
kubectl run test-no-owner --image=nginx
```

### Résultat attendu

Le Pod est refusé par Kyverno.

---

Créer un Pod avec le label `owner`.

```bash
kubectl run test-with-owner \
  --image=nginx \
  --labels owner=rhisland
```

### Résultat attendu

Le Pod est créé avec succès.

---

## 3. Restriction des registres d'images

### Test

Déployer une image provenant de Docker Hub.

```bash
kubectl run img-ok \
  --image=nginx \
  --labels owner=rhisland
```

### Résultat attendu

Le Pod est créé.

---

Déployer une image provenant d'un autre registre.

```bash
kubectl run img-ko \
  --image=ghcr.io/nginx/nginx \
  --labels owner=rhisland
```

### Résultat attendu

Le Pod est refusé.

---

## 4. Mutation automatique

### Test

Créer un Pod valide.

```bash
kubectl run mutate-test \
  --image=nginx \
  --labels owner=rhisland
```

Afficher les labels.

```bash
kubectl get pod mutate-test --show-labels
```

### Résultat attendu

Le label suivant est automatiquement ajouté :

```text
team=production
```

---

## 5. Génération automatique

### Test

Créer un namespace.

```bash
kubectl create namespace kyverno-generate-test
```

Vérifier la ConfigMap.

```bash
kubectl get configmap company-info \
-n kyverno-generate-test
```

### Résultat attendu

La ConfigMap `company-info` existe automatiquement.

---

## 6. Nettoyage automatique

### Vérification des permissions

```bash
kubectl auth can-i delete pods \
--as=system:serviceaccount:kyverno:kyverno-cleanup-controller
```

### Résultat attendu

```text
yes
```

---

Créer un Pod temporaire.

```bash
kubectl run temp-pod \
--image=nginx \
--labels owner=rhisland,cleanup.kyverno.io/ttl=2m
```

Attendre environ deux minutes puis vérifier :

```bash
kubectl get pod temp-pod
```

### Résultat attendu

```text
Error from server (NotFound)
```

Le Pod a été supprimé automatiquement.

---

# Validation finale

Le laboratoire est considéré comme réussi lorsque les conditions suivantes sont réunies :

* ✅ Kyverno est correctement installé.
* ✅ Les Pods sans label `owner` sont refusés.
* ✅ Les Pods avec le label `owner` sont acceptés.
* ✅ Seules les images Docker Hub sont autorisées.
* ✅ Le label `team=production` est ajouté automatiquement.
* ✅ La ConfigMap `company-info` est générée automatiquement.
* ✅ Le Cleanup Controller supprime automatiquement les Pods temporaires après expiration du TTL.
* ✅ Aucun composant Kyverno n'est en erreur.

---

# Compétences validées

À l'issue de ce laboratoire, les compétences suivantes sont validées :

* Installation de Kyverno avec Helm.
* Utilisation des principales familles de policies (Validate, Mutate, Generate).
* Restriction des registres d'images.
* Génération automatique de ressources.
* Nettoyage automatique via le Cleanup Controller.
* Diagnostic d'un problème RBAC.
* Analyse des logs Kyverno.
* Validation fonctionnelle des policies.
