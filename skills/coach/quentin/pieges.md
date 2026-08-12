# Les 10 pièges du choix de projet

Référence pour la phase 1. Chaque piège : comment le détecter,
pourquoi il bloque, comment recadrer.

Rappel : signaler 3 pièges maximum à l'utilisateur, les plus bloquants.
Toujours proposer un recadrage, jamais un simple verdict.

---

## 1. Le projet à plusieurs faces

**Détection** : l'idée contient « et aussi », « et en plus », ou décrit
plusieurs usages distincts. Trois apps déguisées en une.
**Pourquoi ça bloque** : chaque fonctionnalité est faisable seule, mais
l'ensemble ne se termine jamais.
**Recadrage** : « Si tu enlèves deux de ces trois choses, est-ce que ça
reste utile ? » Garder la plus utilisée, pas la plus impressionnante.

## 2. Le clone d'une app connue

**Détection** : « un Notion mais plus simple », « un Strava pour X ».
**Pourquoi ça bloque** : pas un problème technique — un problème de
comparaison mentale. La personne se compare à un produit fait par 200
développeurs, rien ne lui paraît assez bien, elle abandonne par
découragement plutôt que par blocage.
**Recadrage** : identifier LE cas d'usage précis que l'app de référence
gère mal, et ne faire que celui-là.

## 3. Le projet qui a besoin de monde pour être utile

**Détection** : réseau social, marketplace, app collaborative, système
de matching.
**Pourquoi ça bloque** : une app vide n'est pas testable. Aucun retour
possible, donc aucune motivation à continuer.
**Recadrage** : version mono-utilisateur d'abord. Le multi-utilisateur
est une évolution, pas une v1.

## 4. La dépendance à une donnée qu'on n'a pas

**Détection** : l'app a besoin de prix, horaires, catalogue, lieux,
stocks, ou toute donnée qui ne vient pas de l'utilisateur.
**Pourquoi ça bloque** : on découvre au bout de trois jours que l'API
est payante, limitée, ou inexistante. Tout est à refaire.
**Recadrage** : vérifier la source AVANT de coder. Trois options si elle
manque : source alternative officielle (ex. OpenStreetMap plutôt qu'un
service fermé), saisie manuelle en v1, ou changement d'idée.
**Règle absolue** : jamais d'API non officielle, même si elle fonctionne.
Ça casse sans prévenir et ça expose juridiquement.

## 5. L'authentification en v1

**Détection** : « il faut que les gens puissent créer un compte ».
**Pourquoi ça bloque** : comptes, mots de passe, réinitialisation,
sessions — beaucoup de complexité, zéro retour utilisateur en échange.
**Recadrage** : si l'app est pour une seule personne, aucun compte n'est
nécessaire. Les données restent sur l'appareil.

## 6. La dépendance à une validation externe pour tester

**Détection** : le seul moyen de voir si ça marche est de publier sur
l'App Store ou le Play Store.
**Pourquoi ça bloque** : plusieurs jours à plusieurs semaines entre chaque
itération. Tueur de motivation.
**Recadrage** : web app par défaut (voir `principes.md`). Le natif se
justifie seulement si notifications push, capteurs, ou vente App Store
sont indispensables dès la v1.

## 7. L'idée qu'on n'utilisera pas soi-même

**Détection** : la personne parle des autres (« ça pourrait servir à... »)
avant de parler d'elle. Ou ne trouve pas d'exemple récent où elle a
rencontré le problème.
**Pourquoi ça bloque** : ce qui fait reprendre un projet un mardi soir
sans envie, c'est d'en avoir personnellement besoin. Rien d'autre.
**Recadrage** : chercher un problème que la personne vit vraiment,
même plus petit et moins ambitieux.

## 8. Le projet qui vise l'argent d'abord

**Détection** : « une app qui rapporte », « un truc qui peut se vendre ».
**Pourquoi ça bloque** : c'est un objectif de business, pas un critère de
choix de premier projet. Ça pousse vers des idées plus grosses et plus
risquées.
**Recadrage** : le premier projet a un seul but — aller au bout.
Monétiser vient après et relève d'un autre travail que la construction.

## 9. Le projet trop gros « parce que l'IA va le faire »

**Détection** : périmètre justifié par la vitesse de l'IA, pas par le
besoin réel.
**Pourquoi ça bloque** : l'IA a accéléré la production de code, pas la
capacité humaine à comprendre, tester et décider. Le goulot
d'étranglement est l'attention de la personne, pas la génération.
**Recadrage** : dimensionner le projet sur le temps disponible déclaré
en phase 0, pas sur la vitesse de l'outil.

## 10. Le projet flou

**Détection** : impossible de décrire l'app en une phrase avec un seul
verbe d'action. « Un truc autour de la productivité. »
**Pourquoi ça bloque** : ce que la personne ne précise pas, l'IA le
comblera à sa place. C'est le point de départ exact de la dérive de scope.
**Recadrage** : ne pas quitter la phase 1 tant que la phrase de scope
n'est pas nette.