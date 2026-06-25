# Validation du laboratoire

## Objectif

Cette checklist permet de vérifier que le laboratoire a été réalisé conformément aux exigences fonctionnelles et de sécurité.

Le laboratoire est considéré comme validé uniquement lorsque tous les critères ci-dessous sont satisfaits.

---

# 1. Préparation

## Namespace

* [ ] Le namespace `production` existe.

## Utilisateur

* [ ] L'utilisateur `jdupont` est créé.
* [ ] Les certificats utilisateur sont générés.
* [ ] Le contexte Kubernetes `ApplicationDelivery-context` fonctionne.

---

# 2. RBAC

## Role

* [ ] Le `Role` est créé.
* [ ] Les API Groups sont corrects.
* [ ] Les ressources sont correctes.
* [ ] Les verbes sont conformes au besoin métier.

## RoleBinding

* [ ] Le `RoleBinding` associe correctement `jdupont`.
* [ ] Les permissions sont limitées au namespace `production`.

---

# 3. Vérification des permissions

## Pods

* [ ] Consultation des Pods.
* [ ] Création d'un Pod.
* [ ] Modification d'un Pod.
* [ ] Consultation des logs.

## Deployments

* [ ] Consultation.
* [ ] Création.
* [ ] Modification.

## StatefulSets

* [ ] Consultation.
* [ ] Création.
* [ ] Modification.

## CronJobs

* [ ] Consultation.
* [ ] Création.
* [ ] Modification.

---

# 4. Vérification des restrictions

L'utilisateur ne peut pas :

* [ ] Lire un Secret.
* [ ] Lister les Secrets.
* [ ] Supprimer un Pod.
* [ ] Supprimer un Deployment.
* [ ] Supprimer un StatefulSet.
* [ ] Supprimer un CronJob.
* [ ] Créer un Role.
* [ ] Modifier un Role.
* [ ] Créer un RoleBinding.
* [ ] Modifier un RoleBinding.
* [ ] Accéder aux ressources d'un autre namespace.

---

# 5. Validation opérationnelle

En utilisant le contexte `ApplicationDelivery-context` :

* [ ] Déploiement d'une application de test.
* [ ] Modification de cette application.
* [ ] Consultation des logs.
* [ ] Vérification du refus d'accès aux Secrets.
* [ ] Vérification de l'interdiction de suppression.
* [ ] Vérification du refus de création d'objets RBAC.

---

# 6. Questions de réflexion

Les questions suivantes doivent pouvoir être expliquées :

* [ ] Pourquoi éviter `cluster-admin` ?
* [ ] Différence entre `Role` et `ClusterRole`.
* [ ] Différence entre `update` et `patch`.
* [ ] Pourquoi autoriser explicitement `pods/log` ?
* [ ] Principe du moindre privilège.
* [ ] Risques liés à l'accès aux Secrets.
* [ ] Cas d'utilisation d'un `ClusterRole`.

---

# Résultat final

| Élément                       | Statut |
| ----------------------------- | ------ |
| Analyse des besoins           | ☐      |
| Création des objets RBAC      | ☐      |
| Vérification des permissions  | ☐      |
| Vérification des restrictions | ☐      |
| Validation opérationnelle     | ☐      |
| Questions de réflexion        | ☐      |

---

# Validation du mentor

**Date :** ........................................

**Version du laboratoire :** 1.0

**Résultat :**

* ☐ Validé
* ☐ À corriger

**Commentaires :**

........................................................................

........................................................................

........................................................................

