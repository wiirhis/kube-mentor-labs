# Scénario – KM-LAB-002 Kyverno FinSecure

# Contexte

Vous venez d'intégrer l'équipe **Plateforme Kubernetes** de **FinSecure**, une entreprise spécialisée dans les services financiers.

L'entreprise exploite plusieurs clusters Kubernetes hébergeant des applications critiques.

Après plusieurs incidents de sécurité et de conformité, l'équipe Architecture décide de renforcer les contrôles directement au niveau du cluster.

Votre mission consiste à déployer et configurer **Kyverno** afin d'automatiser l'application des règles de gouvernance.

---

# Contexte technique

Le cluster Kubernetes est déjà opérationnel.

Les développeurs disposent aujourd'hui d'une totale liberté pour déployer leurs applications.

Cette situation entraîne plusieurs problèmes :

* certains Pods sont créés sans propriétaire identifié ;
* des images provenant de registres publics non approuvés sont utilisées ;
* les labels de production ne sont pas homogènes ;
* certaines ressources communes doivent être créées manuellement dans chaque namespace ;
* des Pods temporaires restent présents pendant plusieurs jours et consomment inutilement des ressources.

L'équipe Sécurité souhaite automatiser ces contrôles à l'aide de Kyverno.

---

# Votre mission

En tant qu'administrateur Kubernetes, vous devez mettre en place plusieurs policies permettant de renforcer la gouvernance du cluster.

Les exigences sont les suivantes :

## 1. Validation

Tout Pod doit obligatoirement posséder le label :

```text id="qzz9ur"
owner
```

Les Pods ne respectant pas cette règle doivent être refusés.

---

## 2. Restriction des registres

Les développeurs sont uniquement autorisés à utiliser des images provenant de :

```text id="wqftjg"
docker.io
```

Toute autre provenance doit être interdite.

---

## 3. Mutation automatique

Tous les Pods doivent recevoir automatiquement le label :

```yaml id="h2pdce"
team: production
```

Aucune intervention des développeurs ne doit être nécessaire.

---

## 4. Génération automatique

Lorsqu'un nouveau namespace est créé, une ConfigMap nommée :

```text id="6w0d0o"
company-info
```

doit être générée automatiquement avec les informations de l'entreprise.

---

## 5. Nettoyage automatique

Les Pods temporaires identifiés par un label TTL doivent être supprimés automatiquement après expiration de leur durée de vie.

---

# Contraintes

Vous devez :

* utiliser exclusivement Kyverno ;
* privilégier les policies officielles lorsque cela est possible ;
* tester chaque policy individuellement ;
* documenter les résultats obtenus ;
* diagnostiquer les éventuels dysfonctionnements avant toute correction.

---

# Livrables attendus

À la fin du laboratoire, vous devrez être capable de démontrer que :

* les Pods sans label `owner` sont refusés ;
* seuls les registres autorisés peuvent être utilisés ;
* les labels sont ajoutés automatiquement ;
* les ConfigMaps sont générées automatiquement ;
* les Pods temporaires sont supprimés automatiquement ;
* les problèmes rencontrés ont été diagnostiqués et corrigés.

---

# Compétences visées

À l'issue de ce laboratoire, vous serez capable de :

* installer Kyverno ;
* comprendre les Admission Controllers Kubernetes ;
* créer des policies de validation, de mutation, de génération et de nettoyage ;
* diagnostiquer un dysfonctionnement Kyverno ;
* analyser les logs des différents contrôleurs ;
* identifier et corriger un problème RBAC.
