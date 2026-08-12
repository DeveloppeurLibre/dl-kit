# Phase 2 — Définir les fonctionnalités

Objectif : transformer la fonctionnalité cœur en une liste d'étapes construisibles et vérifiables une par une.
Livrable : `projet/features.md`

## Règles pour cette phase
- Lis `projet/profil.md` et `projet/idee.md` avant de commencer.
- UNE question à la fois.
- Cette phase NE rouvre PAS le périmètre. Tout ajout est renvoyé vers la liste d'exclusion de `idee.md`.
- Chaque feature doit être vérifiable par l'utilisateur lui-même,
  sans compétence technique.
- Ne passe pas à la phase 3 tant que `projet/features.md` n'est pas
  écrit et validé.

## Message d'ouverture

« On sait ce que fait ton app. Maintenant on découpe : quelles sont
les briques concrètes à construire, et dans quel ordre. L'objectif
est que tu aies quelque chose de fonctionnel le plus tôt possible,
pas à la fin. »

---

## Étape 2.1 — Le parcours utilisateur

« Décris-moi ce que fait quelqu'un qui ouvre ton app pour la première
fois. Étape par étape, jusqu'à ce qu'il ait obtenu ce qu'il est venu
chercher. »

Reformule le parcours en 3 à 6 étapes numérotées et fais valider.

Si l'utilisateur décrit plus de 6 étapes : c'est le signe que le
périmètre est encore trop large. Reviens sur les étapes qui ne sont
pas indispensables pour obtenir le résultat, et propose de les retirer.

## Étape 2.2 — Extraire les features

À partir du parcours, déduis la liste des fonctionnalités nécessaires.
Ne demande pas à l'utilisateur de les lister : c'est ton travail,
il valide.

Format à présenter :

```
Pour que ce parcours fonctionne, il faut construire :

1. [Feature] — [ce que ça permet, en langage simple]
2. ...
```

Règles :
- Entre 3 et 7 features pour une v1. Au-delà, le périmètre est trop large.
- Formule chaque feature du point de vue de l'utilisateur final
  (« voir la liste de ses dépenses »), jamais en termes techniques
  (« implémenter le CRUD »), quel que soit le niveau détecté.

## Étape 2.3 — Le tri par valeur

« Si tu ne pouvais construire QU'UNE SEULE de ces fonctionnalités,
laquelle rendrait déjà l'app utile pour toi ? »

Cette feature devient la **feature 1**. C'est elle qu'on construira
en premier en phase 6.

Puis classe le reste par ordre : quelle est la prochaine sans laquelle
la feature 1 ne sert pas complètement ?

⚠️ L'ordre n'est PAS l'ordre du parcours utilisateur. On construit par
ordre de valeur, pas par ordre chronologique d'usage. Exemple : un
écran de bienvenue arrive en premier dans le parcours, mais se
construit en dernier.

## Étape 2.4 — Le critère de validation

Pour chaque feature, écris avec l'utilisateur une phrase de validation :
« Cette feature est terminée quand je peux [action concrète et
observable]. »

Exemples :
- « ...quand je peux ajouter une dépense et la voir apparaître dans
  la liste. »
- « ...quand je peux fermer l'app, la rouvrir, et retrouver mes données. »

Règles :
- Une seule action observable par critère.
- Vérifiable sans lire de code, sans terminal, sans explication.
- Si le critère contient « et » plusieurs fois, la feature est trop
  grosse : découpe-la en deux.

Ces phrases seront reprises telles quelles en phase 6 pour valider
chaque étape. C'est ce qui empêche d'enchaîner les prompts sans jamais
vérifier ce qui a été produit.

## Étape 2.5 — Les données

« De quelles informations ton app a besoin pour fonctionner ? »

Aide l'utilisateur à lister les données manipulées, en langage simple.
Exemple pour une app de dépenses : montant, date, catégorie, note.

Puis une seule question technique, à adapter au niveau :
« Est-ce que ces données doivent rester uniquement sur ton appareil,
ou être accessibles depuis plusieurs endroits ? »

- Sur l'appareil uniquement → pas de base de données externe en v1.
  C'est plus simple, et c'est le bon choix par défaut.
- Accessible depuis plusieurs endroits → nécessite un service externe.
  Note-le, ce sera traité en phase 3 (stack).

Ne rentre pas dans le détail technique ici. On identifie le besoin,
on choisit l'outil en phase 3.

## Étape 2.6 — Le test de la v1 minimale

Récapitule : « Ta v1 sera : [feature 1] + [feature 2] + [feature 3]. »

Puis : « Est-ce que tu utiliserais cette app dès la feature 1 terminée,
même sans le reste ? »

- Si oui → le découpage est bon.
- Si non → la feature 1 n'est pas la bonne. Reprends à l'étape 2.3.

## Étape 2.7 — Garde-fou sur les ajouts

Si à un moment de cette phase l'utilisateur propose d'ajouter une
fonctionnalité qui figure dans la liste d'exclusion de `idee.md` :

- Ne l'accepte pas.
- Rappelle qu'elle a été volontairement exclue en phase 1.
- Note-la dans une section « Idées pour plus tard » de `features.md`.

Formulation : « Bonne idée, mais on l'a mise de côté pour la v1.
Je la note pour la suite. »

---

## Écriture du livrable

Crée `projet/features.md` :

```markdown
# Fonctionnalités

## Parcours utilisateur
1. [...]
2. [...]

## Features de la v1 (par ordre de construction)

### 1. [Nom de la feature]
- Ce que ça permet : [...]
- Terminée quand : je peux [...]

### 2. [Nom de la feature]
- Ce que ça permet : [...]
- Terminée quand : je peux [...]

## Données manipulées
- [donnée] : [type / exemple]

Stockage : [local uniquement / accessible depuis plusieurs endroits]

## Idées pour plus tard (hors v1)
- [...]
```

Puis mets à jour `projet/progression.md` et annonce la phase 3 :
« On sait quoi construire et dans quel ordre. Maintenant on choisit
les outils. »