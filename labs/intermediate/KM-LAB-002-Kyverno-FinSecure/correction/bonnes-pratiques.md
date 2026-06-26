# Bonnes pratiques

## Développer une policy progressivement

Toujours :

1. créer la policy ;
2. l'appliquer ;
3. la tester ;
4. passer à la suivante.

---

## Utiliser les policies officielles

Ne jamais repartir d'une page blanche lorsqu'une policy officielle répond déjà au besoin.

---

## Lire les logs

Les logs des différents contrôleurs permettent d'identifier rapidement l'origine d'un problème.

```bash
kubectl logs -n kyverno deploy/kyverno-admission-controller
kubectl logs -n kyverno deploy/kyverno-background-controller
kubectl logs -n kyverno deploy/kyverno-cleanup-controller
kubectl logs -n kyverno deploy/kyverno-reports-controller
Vérifier les permissions

Avant de conclure qu'une fonctionnalité ne fonctionne pas :

kubectl auth can-i ...

Cette commande permet souvent de confirmer ou d'écarter une cause RBAC.

Toujours partir du besoin métier

Choisir une policy parce qu'elle répond au besoin fonctionnel, et non parce que son nom semble correspondre.

Conserver les manifestes validés

Chaque policy validée devient un modèle réutilisable pour les futurs projets.
