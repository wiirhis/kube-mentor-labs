# KM-LAB-001 – RBAC : Gestion des accès d'une équipe Application Delivery

## Présentation

Ce laboratoire met en œuvre le contrôle d'accès basé sur les rôles (RBAC) dans Kubernetes.

À partir d'un besoin métier réaliste, l'objectif est de concevoir puis de déployer une politique d'autorisation permettant à une équipe de gérer des applications dans un namespace donné, tout en respectant le principe du moindre privilège.

---

## Niveau

**Beginner**

---

## Durée estimée

2 à 3 heures

---

## Compétences visées

À l'issue de ce laboratoire, vous serez capable de :

* comprendre le fonctionnement de RBAC ;
* distinguer un `Role` d'un `ClusterRole` ;
* créer un `Role` ;
* créer un `RoleBinding` ;
* attribuer des permissions à un utilisateur ;
* vérifier les permissions avec `kubectl auth can-i` ;
* appliquer le principe du moindre privilège ;
* réaliser une validation fonctionnelle des droits accordés.

---

## Contexte métier

L'entreprise **TechCorp** exploite un cluster Kubernetes partagé entre plusieurs équipes.

L'équipe **Application Delivery** est responsable du déploiement et de la maintenance des applications dans le namespace `production`.

Un nouvel utilisateur, `jdupont`, rejoint cette équipe. Il doit disposer uniquement des permissions nécessaires à ses missions quotidiennes.

---

## Technologies utilisées

* Kubernetes
* RBAC
* kubectl
* OpenSSL
* YAML

---

## Architecture logique

```
Utilisateur (jdupont)
          │
          ▼
     RoleBinding
          │
          ▼
         Role
          │
          ▼
 Namespace production
          │
          ▼
 Pods / Deployments / StatefulSets / CronJobs
```

---

## Livrables

Ce laboratoire contient :

* les manifestes RBAC ;
* les commandes de validation ;
* les tests fonctionnels ;
* la correction détaillée ;
* les bonnes pratiques ;
* les notes de troubleshooting.

---

## Critères de réussite

Le laboratoire est considéré comme réussi lorsque :

* l'utilisateur `jdupont` peut gérer les ressources autorisées ;
* l'accès aux Secrets est refusé ;
* la suppression des ressources est interdite ;
* les objets RBAC ne peuvent pas être modifiés par `jdupont` ;
* les permissions sont limitées au namespace `production`.

---

## Structure du laboratoire

```
KM-LAB-001-RBAC-TechCorp/

├── manifests/
├── scripts/
├── assets/
├── solution/
├── correction/
├── metadata.md
├── scenario.md
├── objectives.md
├── validation.md
├── troubleshooting.md
└── README.md
```

---

## Références

* Documentation officielle Kubernetes – RBAC
* Documentation officielle kubectl

