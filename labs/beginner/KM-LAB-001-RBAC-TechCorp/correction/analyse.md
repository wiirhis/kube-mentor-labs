# Analyse du laboratoire

## Objectif

Mettre en place une politique RBAC permettant à l'utilisateur `jdupont` de gérer les applications du namespace `production` tout en respectant le principe du moindre privilège.

---

## Analyse du besoin

Le besoin métier a été correctement identifié.

Les permissions ont été limitées au namespace `production` à l'aide d'un `Role` et d'un `RoleBinding`.

Le choix d'un `Role` est adapté puisque les droits ne doivent pas s'appliquer à l'ensemble du cluster.

---

## Points positifs

* Bonne identification des ressources Kubernetes.
* API Groups correctement utilisés.
* Séparation des permissions par ressource.
* Utilisation du principe du moindre privilège.
* Validation des permissions par des tests fonctionnels.
* Vérification des restrictions (Secrets, RBAC, suppression).

---

## Difficultés rencontrées

* Configuration initiale du kubeconfig.
* Gestion des certificats utilisateur.
* Compréhension des sous-ressources Kubernetes (`pods/log`, `deployments/scale`).
* Différence entre les verbes `update` et `patch`.

---

## Enseignements

Ce laboratoire montre que la conception d'une politique RBAC nécessite :

* une bonne compréhension du besoin métier ;
* la connaissance des ressources Kubernetes ;
* la maîtrise des API Groups ;
* la validation systématique des permissions accordées et refusées.

---

## Conclusion

Les objectifs du laboratoire sont atteints. La politique RBAC répond au besoin exprimé tout en limitant les privilèges accordés à l'utilisateur.

