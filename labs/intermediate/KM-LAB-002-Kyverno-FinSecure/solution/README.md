# Solution – KM-LAB-002 Kyverno FinSecure

Cette solution présente une implémentation complète et validée du laboratoire **KM-LAB-002** consacré à Kyverno.

## Objectifs

Le laboratoire avait pour objectif de découvrir les principaux mécanismes de Kyverno en mettant en œuvre plusieurs types de policies.

Les fonctionnalités implémentées sont :

* installation de Kyverno avec Helm ;
* validation des ressources ;
* restriction des registres d'images ;
* mutation automatique des ressources ;
* génération automatique de ressources ;
* nettoyage automatique via le mécanisme TTL.

## Policies créées

### ValidatingPolicy

Une **ValidatingPolicy** impose la présence du label :

```yaml
owner
```

Tout Pod ne possédant pas ce label est refusé.

---

### ClusterPolicy – Restriction des images

Une **ClusterPolicy** limite les images autorisées au registre :

```text
docker.io
```

Les images provenant d'autres registres sont refusées.

---

### MutatingPolicy

Une **MutatingPolicy** ajoute automatiquement le label :

```yaml
team: production
```

Aucune intervention de l'utilisateur n'est nécessaire.

---

### Generate

Une **ClusterPolicy** génère automatiquement une ConfigMap :

```text
company-info
```

dans chaque nouveau namespace créé.

---

### Cleanup

Le mécanisme TTL de Kyverno est utilisé pour supprimer automatiquement les Pods temporaires.

Au cours du laboratoire, un problème RBAC a été identifié sur le Cleanup Controller.

Après ajout des permissions nécessaires, le nettoyage automatique fonctionne correctement.

## Démarche de diagnostic

Le laboratoire a également permis d'apprendre à diagnostiquer un dysfonctionnement Kyverno en utilisant :

* les logs des contrôleurs ;
* les commandes `kubectl auth can-i` ;
* l'analyse des ClusterRoles et ClusterRoleBindings ;
* les tests unitaires de chaque policy.

## Compétences acquises

À l'issue du laboratoire, les compétences suivantes sont acquises :

* installer Kyverno ;
* comprendre l'architecture des Admission Controllers ;
* écrire des policies de validation ;
* écrire des policies de mutation ;
* écrire des policies de génération ;
* utiliser le nettoyage automatique (TTL) ;
* diagnostiquer un problème de permissions RBAC ;
* tester et valider une policy avant son déploiement.

