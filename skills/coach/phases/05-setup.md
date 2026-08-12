# Phase 5 — Initialiser le projet

Objectif : créer le projet, installer le CLAUDE.md rédigé en phase 4,
vérifier que tout tourne, et poser le filet de sécurité.
Livrable : un projet qui démarre et affiche quelque chose à l'écran,
avec son CLAUDE.md en place et un premier point de sauvegarde.

## Règles pour cette phase
- Lis `projet/profil.md`, `projet/stack.md`, `projet/architecture.md`.
- C'est la première phase où on exécute des commandes. Si le niveau est
  débutant : annonce CHAQUE commande avant de la lancer, en une phrase,
  et dis ce qui va se passer.
- Ne lance jamais plusieurs commandes d'un coup. Une commande, on
  vérifie le résultat, on continue.
- Si quelque chose échoue : traite l'erreur immédiatement, ne passe pas
  à la suite en espérant que ça se règle.
- Ne passe pas à la phase 6 tant que l'utilisateur n'a pas vu son
  projet tourner de ses propres yeux.

## Message d'ouverture

« On installe le projet. C'est la partie la moins intéressante mais
c'est là que beaucoup de gens abandonnent, souvent à cause d'un
problème d'installation qui n'a rien à voir avec leur app. Si quelque
chose coince, dis-le-moi tout de suite, on règle. »

---

## Étape 5.1 — L'emplacement du projet

Le code de l'app se construit à la racine du dossier où l'utilisateur
a lancé Claude Code — le même dossier que `projet/`. Il n'y a qu'un
seul dossier de travail.

Structure finale :

```
mon-projet/
├── projet/
│   ├── progression.md
│   ├── profil.md
│   ├── idee.md
│   ├── features.md
│   ├── stack.md
│   ├── architecture.md
│   └── CLAUDE.md      ← brouillon rédigé en phase 4, installé ici-bas
├── CLAUDE.md           ← une fois installé (étape 5.5)
└── [le code de l'app]
```

Explication à donner à l'utilisateur : « Ton app se construit ici,
dans ce même dossier. Les fichiers de `projet/` restent à côté : ils
gardent la trace de tout ce qu'on a décidé ensemble. »

## Étape 5.2 — Créer le projet

Crée le projet avec l'outil adapté à la stack de `stack.md`,
**directement à la racine du dossier de travail** — pas dans un
sous-dossier créé par l'outil. La plupart des outils de scaffolding
créent un nouveau sous-dossier par défaut ; vérifie l'option qui cible
le dossier courant avant de lancer la commande (ex. `.` en argument).

Explique ce que fait la commande AVANT de la lancer si niveau débutant.

**Web** : crée le projet Next.js en ciblant le dossier courant.
Attends la fin de l'installation, qui peut prendre plusieurs minutes —
préviens l'utilisateur avant, pour qu'il ne pense pas que c'est
bloqué.

**iOS** : guide la création du projet dans Xcode, écran par écran.
Xcode ne se pilote pas en ligne de commande pour cette étape : donne
les clics exacts (nom du projet, interface SwiftUI, langage Swift), et
indique comme emplacement le dossier de travail courant.

⚠️ Si iOS : vérifie que les dossiers synchronisés au système de
fichiers sont utilisés (voir `quentin/stack-ios.md`). Sans ça, chaque
fichier créé par l'IA en ligne de commande ne sera pas pris en compte
par Xcode, et l'utilisateur aura des erreurs de compilation
incompréhensibles pendant toute la phase 6.

**Android** : guide la création du projet dans Android Studio, écran
par écran (nom du projet, langage Kotlin, template Empty Activity avec
Jetpack Compose), en ciblant le dossier de travail courant. Une fois
créé, toute modification du fichier `build.gradle.kts` faite en ligne
de commande nécessite une synchronisation Gradle avant de continuer
(voir `quentin/stack-android.md`) — sans elle, les nouvelles
dépendances ne sont pas reconnues et l'IA risque de « corriger » du
code qui n'a en réalité pas encore été synchronisé.

Vérifie que le projet démarre correctement avant de continuer : lance-
le et fais confirmer à l'utilisateur qu'il voit bien quelque chose
s'afficher.

⚠️ Ne continue pas si le projet ne démarre pas. Un problème
d'installation non résolu ici deviendra un blocage bien plus coûteux
en phase 6.

## Étape 5.3 — Premier lancement

Lance le projet et fais constater le résultat à l'utilisateur.

**Web** : commande de démarrage, puis « ouvre ton navigateur sur
l'adresse affichée. Tu dois voir la page d'accueil par défaut. »
**iOS** : lancement dans le simulateur.
**Android** : lancement dans l'émulateur. Vérifie que l'image système
utilisée inclut Google Play si l'app en aura besoin plus tard (voir
`quentin/stack-android.md`) — plus simple à corriger maintenant qu'en
phase 6.

Ne continue PAS tant que l'utilisateur n'a pas confirmé qu'il voit
quelque chose. C'est le premier moment de victoire concrète du
parcours — marque-le : « Ton projet tourne. C'est vide, mais c'est
à toi. »

## Étape 5.4 — En cas d'échec

Les problèmes les plus fréquents, à traiter dans cet ordre :

**Commande introuvable** → l'outil n'est pas installé ou pas dans le
PATH. Renvoie à l'étape 3.5 et réinstalle.

**Erreur de version** → version de Node ou de Xcode trop ancienne.
Donne la version minimale requise et la procédure de mise à jour.

**Erreur de permissions** → n'utilise PAS `sudo` par réflexe pour
contourner. Explique le problème et propose la solution propre
(changer de dossier, corriger les droits).

**Port déjà utilisé (web)** → une autre application occupe le port.
Propose un autre port plutôt que de tuer un processus au hasard.

**Xcode : erreur de signature / compte développeur** → un compte Apple
gratuit suffit pour le simulateur. Ne fais pas payer les 99 $ à ce
stade, c'est seulement nécessaire pour publier.

**Android Studio : dépendance non reconnue après modification de
build.gradle.kts** → une synchronisation Gradle manuelle est
nécessaire (« Sync Project with Gradle Files »). Ne cherche pas une
erreur de code avant d'avoir vérifié ce point.

Règle générale : si une erreur persiste après deux tentatives, ne
répète pas la même approche. Change de méthode, ou propose une
alternative (par exemple : basculer sur le web si l'installation iOS
est bloquée par la machine).

## Étape 5.5 — Installer le CLAUDE.md du projet

Déplace le brouillon `projet/CLAUDE.md` (rédigé en phase 4) à la
racine du projet, à côté du code : il devient `CLAUDE.md`.

Il n'y a qu'un seul fichier CLAUDE.md pour ce projet — celui que tu
viens d'installer. Ton rôle de coach à toi vient du plugin installé
sur la machine de l'utilisateur, il n'a pas besoin d'un fichier séparé
dans le dossier du projet.

Explique-le en une phrase à l'utilisateur : « Ce fichier est lu
automatiquement à chaque session de travail sur ton projet. C'est lui
qui donne le contexte à l'IA. »

Vérifie deux points et dis-les à voix haute :
- Le CLAUDE.md du projet fait moins de 80 lignes
- Il n'a pas été généré par /init

## Étape 5.6 — Nettoyer le contenu par défaut

Le projet créé contient une page ou un écran de démonstration.
Fais-le remplacer par un écran minimal : le nom de l'app, rien d'autre.

Objectif : que l'utilisateur voie SON app, pas un template. C'est un
petit changement mais c'est le premier où il constate que le projet
lui appartient.

C'est aussi le premier vrai prompt de construction. Fais-le écrire
par l'utilisateur, pas par toi — il doit s'exercer sur quelque chose
de trivial avant la phase 6. Si son prompt est vague, corrige-le
maintenant : c'est le meilleur moment possible pour apprendre.

## Étape 5.7 — Le filet de sécurité

Mets en place le moyen de revenir en arrière.

- Vérifie que les points de sauvegarde sont actifs.
- Fais un premier point de sauvegarde maintenant, avec le projet qui
  démarre et son CLAUDE.md en place. C'est le point de retour de
  référence.
- Explique en une phrase : « Si l'IA casse quelque chose pendant la
  construction, on peut revenir à un état qui marchait. »

Si niveau débutant : ne rentre pas dans le détail de Git. L'essentiel
est de savoir qu'un retour arrière est possible et comment le demander.

## Étape 5.8 — Le test de démarrage à froid

Test important, à ne pas sauter :

Demande à l'utilisateur de fermer la session en cours et d'en ouvrir
une nouvelle dans le dossier du projet. Puis de poser une question
simple sur le projet.

Objectif : vérifier que le CLAUDE.md est bien lu et que l'IA sait de
quoi il s'agit sans qu'on lui réexplique.

Si ce n'est pas le cas : le fichier est mal placé ou mal formé.
Corrige maintenant — c'est bien plus coûteux à découvrir en pleine
construction.

## Étape 5.9 — Vérifications avant construction

Passe en revue, en une ligne chacun :
- [ ] Le projet démarre
- [ ] L'utilisateur voit son app à l'écran
- [ ] `CLAUDE.md` est à la racine du projet, moins de 80 lignes
- [ ] Le point de sauvegarde initial existe
- [ ] Le test de démarrage à froid est passé
- [ ] Aucune erreur non résolue

Si un point n'est pas coché : ne passe pas à la phase 6. Règle-le.

---

## Écriture du livrable

Mets à jour `projet/architecture.md` avec une section :

```markdown
## Setup

- Projet créé le : [date]
- Commande de lancement : [commande]
- Premier lancement validé : oui
- CLAUDE.md installé à la racine, vérifié
- Point de sauvegarde initial : [checkpoint / commit]

### Problèmes rencontrés
[Ex : Node 18 → mise à jour vers Node 22]
```

Puis mets à jour `projet/progression.md` et annonce la phase 6 :
« Le projet tourne. Maintenant on construit la première fonctionnalité :
[reprendre la feature 1 de features.md]. »
