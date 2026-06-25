# Scénario métier

## Contexte

La société **TechCorp** est un éditeur de logiciels SaaS qui héberge plusieurs applications critiques sur un cluster Kubernetes.

Afin d'assurer la séparation des responsabilités, les équipes sont organisées par domaine :

* Infrastructure
* Sécurité
* Application Delivery
* Développement
* Exploitation

L'équipe **Application Delivery** est chargée de déployer les applications, d'effectuer les mises à jour et de superviser les workloads du namespace `production`.

Pour renforcer la sécurité du cluster, l'équipe Infrastructure souhaite appliquer le principe du **moindre privilège** (*Least Privilege*). Chaque collaborateur doit disposer uniquement des droits nécessaires à ses missions.

---

## Situation

Un nouvel ingénieur, **jdupont**, rejoint l'équipe Application Delivery.

Avant de lui donner accès au cluster, l'administrateur Kubernetes doit définir précisément les permissions qui lui seront accordées.

L'objectif est de permettre à `jdupont` de gérer les applications du namespace `production`, tout en empêchant toute action pouvant compromettre la sécurité ou la stabilité du cluster.

---

## Besoins fonctionnels

L'utilisateur `jdupont` doit pouvoir :

* consulter les Pods ;
* créer des Pods ;
* modifier des Pods ;
* consulter les logs des Pods ;
* gérer les Deployments ;
* gérer les StatefulSets ;
* gérer les CronJobs.

---

## Contraintes de sécurité

Pour limiter les risques, `jdupont` ne doit pas pouvoir :

* supprimer des ressources ;
* consulter les Secrets ;
* modifier les objets RBAC ;
* accéder aux autres namespaces ;
* obtenir des privilèges administrateur.

---

## Objectif du laboratoire

Concevoir et mettre en œuvre une politique RBAC répondant à ce besoin métier.

Le laboratoire devra démontrer que les autorisations accordées correspondent exactement aux besoins exprimés et que toutes les restrictions sont correctement appliquées.

---

## Résultat attendu

À l'issue du laboratoire :

* `jdupont` peut administrer les applications du namespace `production` dans le périmètre défini ;
* toutes les opérations non autorisées sont refusées par Kubernetes ;
* les permissions respectent le principe du moindre privilège.

---

## Compétences mises en œuvre

* Analyse d'un besoin métier
* Conception d'une politique RBAC
* Création d'un Role
* Création d'un RoleBinding
* Vérification des permissions
* Validation opérationnelle
* Application des bonnes pratiques de sécurité Kubernetes

