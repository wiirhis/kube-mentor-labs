# Commandes de validation – KM-LAB-002 Kyverno

## Installation Kyverno

```bash
helm repo add kyverno https://kyverno.github.io/kyverno/
helm repo update

helm install kyverno kyverno/kyverno \
  -n kyverno \
  --create-namespace \
  --set admissionController.replicas=3 \
  --set backgroundController.replicas=2 \
  --set cleanupController.replicas=2 \
  --set reportsController.replicas=2
Vérification installation
kubectl get all -n kyverno
kubectl get crd | grep kyverno
kubectl get validatingwebhookconfigurations,mutatingwebhookconfigurations | grep kyverno
Application des policies
kubectl apply -f manifests/01-require-owner-label.yaml
kubectl apply -f manifests/02-allow-only-dockerhub-images.yaml
kubectl apply -f manifests/03-add-team-label.yaml
kubectl apply -f manifests/04-generate-company-info-configmap.yaml
kubectl apply -f manifests/05-cleanup-controller-rbac.yaml
Tests validate owner
kubectl run test-no-owner --image=nginx
kubectl run test-with-owner --image=nginx --labels owner=rhisland
Tests registre d'images
kubectl run img-ok-nginx --image=nginx --labels owner=rhisland
kubectl run img-ok-dockerio --image=docker.io/library/nginx --labels owner=rhisland
kubectl run img-ko-ghcr --image=ghcr.io/nginx/nginx --labels owner=rhisland
kubectl run img-ko-quay --image=quay.io/prometheus/prometheus --labels owner=rhisland
Test mutation
kubectl run mutate-test --image=nginx --labels owner=rhisland
kubectl get pod mutate-test --show-labels
kubectl get pod mutate-test -o jsonpath='{.metadata.labels.team}{"\n"}'
Test generate
kubectl create ns kyverno-generate-test
kubectl get configmap company-info -n kyverno-generate-test -o yaml
Test cleanup TTL
kubectl auth can-i delete pods \
  --as=system:serviceaccount:kyverno:kyverno-cleanup-controller

kubectl run temp-pod \
  --image=nginx \
  --labels owner=rhisland,temporary=true,cleanup.kyverno.io/ttl=2m

watch kubectl get pod temp-pod --show-labels

