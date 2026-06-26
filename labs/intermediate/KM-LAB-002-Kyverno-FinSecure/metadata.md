# Metadata – KM-LAB-002 Kyverno FinSecure

| Propriété                | Valeur                                       |
| ------------------------ | -------------------------------------------- |
| **Identifiant**          | KM-LAB-002                                   |
| **Titre**                | Kyverno – Gouvernance et Sécurité du Cluster |
| **Niveau**               | Intermédiaire                                |
| **Difficulté**           | ★★★☆☆                                        |
| **Durée estimée**        | 2 à 3 heures                                 |
| **Auteur**               | Rhisland OGAGNA                              |
| **Projet**               | Kube Mentor Labs                             |
| **Version**              | 1.0                                          |
| **Statut**               | Validé                                       |
| **Dernière mise à jour** | Juin 2026                                    |

---

# Technologies

* Kubernetes
* Kyverno
* Helm
* kubectl

---

# Versions utilisées

| Composant  | Version |
| ---------- | ------- |
| Kubernetes | v1.36.x |
| Kyverno    | v1.15+  |
| Helm       | v4.x    |

---

# Prérequis

Avant de commencer ce laboratoire, il est recommandé de maîtriser :

* les Pods ;
* les Namespaces ;
* les Labels ;
* les Admission Controllers Kubernetes ;
* le RBAC ;
* les commandes de base `kubectl`.

Le **KM-LAB-001 (RBAC)** est considéré comme un prérequis.

---

# Concepts abordés

Le laboratoire couvre les mécanismes suivants :

* ValidatingPolicy
* ClusterPolicy
* MutatingPolicy
* Generate
* Cleanup
* Admission Webhooks
* RBAC
* Helm

---

# Compétences développées

À l'issue de ce laboratoire, l'apprenant sera capable de :

* installer Kyverno avec Helm ;
* comprendre l'architecture de Kyverno ;
* créer des policies de validation ;
* créer des policies de mutation ;
* créer des policies de génération ;
* limiter les registres d'images autorisés ;
* automatiser le nettoyage des Pods temporaires ;
* diagnostiquer une policy en échec ;
* diagnostiquer un problème RBAC.

---

# Livrables

Le laboratoire contient :

* un scénario réaliste ;
* les objectifs pédagogiques ;
* les manifestes Kubernetes ;
* les commandes de validation ;
* les résultats attendus ;
* un guide de dépannage (*troubleshooting*) ;
* une correction détaillée ;
* une analyse pédagogique ;
* les bonnes pratiques ;
* les références officielles ;
* les leçons apprises.

---

# Critère de validation

Le laboratoire est validé lorsque :

* toutes les policies fonctionnent ;
* tous les tests sont concluants ;
* les erreurs rencontrées sont expliquées ;
* le mécanisme de nettoyage automatique est opérationnel.

---

# Références

Les exemples utilisés dans ce laboratoire sont adaptés à partir de la documentation officielle de :

* Kubernetes
* Kyverno
* Helm
