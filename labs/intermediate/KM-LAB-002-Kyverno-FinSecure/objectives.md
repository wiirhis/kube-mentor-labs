# Objectifs – KM-LAB-002 Kyverno FinSecure

# Objectif général

Découvrir Kyverno et mettre en œuvre les principaux mécanismes de gouvernance d'un cluster Kubernetes afin d'automatiser les contrôles de sécurité, de conformité et de gestion des ressources.

---

# Objectifs pédagogiques

À l'issue de ce laboratoire, l'apprenant sera capable de :

* comprendre le rôle de Kyverno dans Kubernetes ;
* distinguer les différents types de policies ;
* choisir la policy adaptée à un besoin métier ;
* interpréter les messages d'erreur retournés par Kyverno ;
* diagnostiquer un dysfonctionnement lié à une policy.

---

# Objectifs techniques

Le laboratoire doit permettre de savoir :

## Installer Kyverno

* installer Kyverno avec Helm ;
* vérifier le bon fonctionnement des différents contrôleurs.

---

## Mettre en œuvre une policy de validation

Créer une policy imposant la présence du label :

```text id="ncmgcv"
owner
```

sur tous les Pods.

---

## Restreindre les registres d'images

Autoriser uniquement les images provenant du registre :

```text id="9c3e1j"
docker.io
```

---

## Mettre en œuvre une mutation

Ajouter automatiquement le label :

```yaml id="qef4ij"
team: production
```

lors de la création d'un Pod.

---

## Générer automatiquement une ressource

Créer automatiquement une ConfigMap :

```text id="0q4grm"
company-info
```

dans chaque nouveau namespace.

---

## Mettre en œuvre le nettoyage automatique

Configurer Kyverno afin de supprimer automatiquement les Pods temporaires après expiration de leur durée de vie.

---

## Diagnostiquer un problème

Être capable d'utiliser :

* les logs Kyverno ;
* les événements Kubernetes ;
* les commandes `kubectl auth can-i` ;
* les objets RBAC ;

pour identifier l'origine d'un dysfonctionnement.

---

# Critères de réussite

Le laboratoire est considéré comme réussi lorsque :

* Kyverno est correctement installé ;
* toutes les policies sont appliquées sans erreur ;
* chaque fonctionnalité est validée par un test ;
* le nettoyage automatique fonctionne ;
* les problèmes rencontrés sont expliqués et corrigés.

---

# Compétences développées

À l'issue du laboratoire, les compétences suivantes sont acquises :

* Installation de Kyverno.
* Administration de policies Kubernetes.
* Gouvernance d'un cluster.
* Validation, mutation et génération de ressources.
* Utilisation du Cleanup Controller.
* Diagnostic RBAC.
* Analyse des logs Kubernetes.
* Méthodologie de troubleshooting.

---

# Niveau

**Intermédiaire**

Ce laboratoire suppose que les notions fondamentales de Kubernetes (Pods, Namespaces, RBAC, API Server et Admission Controllers) sont déjà acquises.
