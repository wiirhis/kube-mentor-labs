# Lessons Learned – KM-LAB-002

## 1. Toujours partir du besoin métier

Le nom d'une policy ou d'un template peut être trompeur.

Avant de choisir un exemple, il faut répondre à la question :

> Quel problème dois-je résoudre ?

Puis seulement rechercher une policy adaptée.

---

## 2. Tester une policy à la fois

La bonne démarche est :

- créer la policy ;
- l'appliquer ;
- la tester ;
- seulement ensuite passer à la suivante.

Cela simplifie énormément le diagnostic.

---

## 3. Les messages d'erreur sont précieux

L'erreur :

```
no such overload: string(map)
```

indiquait directement un problème dans l'expression CEL.

Le problème n'était pas Kubernetes ni Kyverno.

---

## 4. Vérifier les permissions

Le Cleanup Controller détectait correctement les Pods à supprimer.

Le problème venait du RBAC.

La commande suivante a permis de confirmer le diagnostic :

```bash
kubectl auth can-i delete pods \
  --as=system:serviceaccount:kyverno:kyverno-cleanup-controller
```

---

## 5. Ne pas modifier les exemples sans comprendre

Les templates officiels constituent un excellent point de départ.

Ils doivent être adaptés au besoin du laboratoire et non copiés aveuglément.

---

## 6. Toujours privilégier la documentation officielle

Les templates doivent provenir en priorité :

- Documentation Kyverno
- Policies officielles
- Documentation Kubernetes

L'IA sert à expliquer et adapter, pas à remplacer la documentation officielle.
