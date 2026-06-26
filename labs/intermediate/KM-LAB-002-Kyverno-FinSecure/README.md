# KM-LAB-002 – Kyverno FinSecure

## Présentation

Dans ce laboratoire, vous incarnez un administrateur Kubernetes chargé de renforcer la sécurité et la gouvernance d'un cluster utilisé par l'entreprise **FinSecure**.

L'objectif est de découvrir **Kyverno** en mettant en œuvre plusieurs mécanismes de contrôle et d'automatisation directement au niveau du cluster Kubernetes.

Ce laboratoire s'appuie sur des cas d'usage réalistes inspirés de situations rencontrées en environnement de production.

---

# Niveau

**Intermédiaire**

---

# Durée estimée

**2 à 3 heures**

---

# Prérequis

Avant de commencer ce laboratoire, il est recommandé de maîtriser :

* Kubernetes (Pods, Namespaces, Labels)
* RBAC
* `kubectl`
* Helm

Le **KM-LAB-001 – RBAC TechCorp** est considéré comme un prérequis.

---

# Objectifs

À l'issue de ce laboratoire, vous serez capable de :

* Installer Kyverno avec Helm.
* Comprendre le rôle des Admission Controllers.
* Écrire une ValidatingPolicy.
* Écrire une MutatingPolicy.
* Générer automatiquement des ressources.
* Restreindre les registres d'images.
* Configurer le nettoyage automatique des Pods.
* Diagnostiquer un problème RBAC.
* Interpréter les logs des différents contrôleurs Kyverno.

---

# Contenu du laboratoire

Le laboratoire couvre les thèmes suivants :

* Validation des ressources.
* Restriction des registres d'images.
* Mutation automatique.
* Génération de ressources.
* Cleanup Controller.
* RBAC.
* Troubleshooting.
* Bonnes pratiques.
* Références officielles.

---

# Structure

```text
KM-LAB-002-Kyverno-FinSecure
├── README.md
├── metadata.md
├── scenario.md
├── objectives.md
├── validation.md
├── troubleshooting.md
├── references.md
├── lessons-learned.md
├── manifests/
├── solution/
├── correction/
├── assets/
└── scripts/
```

---

# Résultat attendu

À la fin du laboratoire, vous aurez déployé une plateforme Kyverno capable de :

* refuser les Pods ne respectant pas les règles définies ;
* limiter les registres d'images autorisés ;
* enrichir automatiquement les ressources ;
* générer des ConfigMaps lors de la création de nouveaux namespaces ;
* supprimer automatiquement les Pods temporaires après expiration de leur TTL.

---

# Ce que vous apprendrez

Au-delà de la création de policies, ce laboratoire met l'accent sur une démarche de diagnostic inspirée des pratiques d'administration système :

* observer les symptômes ;
* analyser les événements Kubernetes ;
* consulter les logs des contrôleurs Kyverno ;
* vérifier les permissions RBAC ;
* identifier la cause racine ;
* appliquer une correction adaptée ;
* valider le retour à un fonctionnement nominal.

---

# Références

Les exemples utilisés dans ce laboratoire sont basés sur la documentation officielle de :

* Kubernetes
* Kyverno
* Helm

Les liens vers les ressources officielles sont regroupés dans le fichier `references.md`.

---

# Version

**KM-LAB-002 – Version 1.0**
