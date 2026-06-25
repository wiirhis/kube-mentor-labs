# Commandes utilisées

## Appliquer les manifestes

```bash
kubectl apply -f manifests/namespace-production.yaml
kubectl apply -f manifests/role-techcorp.yaml
kubectl apply -f manifests/rolebinding-jdupont.yaml
```

## Vérifier les objets RBAC

```bash
kubectl get role -n production
kubectl describe role application-delivery -n production

kubectl get rolebinding -n production
kubectl describe rolebinding jdupont-application-delivery -n production
```

## Changer de contexte

```bash
kubectl config use-context ApplicationDelivery-context
```

## Vérifier le contexte courant

```bash
kubectl config current-context
```

## Tester les permissions

```bash
kubectl auth can-i get pods -n production
kubectl auth can-i create deployments.apps -n production
kubectl auth can-i get secrets -n production
kubectl auth can-i delete pods -n production
```

## Déployer une application de test

```bash
kubectl create deployment app-test-rbac \
  --image=nginx \
  --replicas=2 \
  -n production
```

## Modifier un Deployment

```bash
kubectl patch deployment app-test-rbac \
  -n production \
  -p '{"spec":{"replicas":3}}'
```

## Vérifier le résultat

```bash
kubectl get deploy,pods -n production
```

