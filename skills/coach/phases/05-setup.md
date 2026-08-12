# Phase 5 — Initialiser le projet

Objectif : créer le projet dans `projet/app/`, vérifier qu'il tourne,
poser le CLAUDE.md du projet.
Livrable : un projet qui démarre et affiche quelque chose à l'écran.

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

⚠️ RÈGLE STRUCTURANTE : le code de l'app va dans `projet/app/`,
à l'intérieur du kit. Pas ailleurs.

Structure finale :

```
dl-kit/
├── CLAUDE.md          ← le coach (reste chargé en permanence)
├── phases/
├── quentin/
└── projet/
    ├── progression.md
    ├── profil.md
    ├── idee.md
    ├── features.md
    ├── stack.md
    ├── architecture.md
    └── app/           ← le code de l'app, avec son propre CLAUDE.md
```

Explication à donner à l'utilisateur :
« Ton app se construit dans `projet/app/`, à l'intérieur du kit. C'est
volontaire : ça me permet de rester ton coach pendant toute la
construction, avec tout ce qu'on a décidé ensemble. Tu ne repars pas
de zéro dans un dossier vide. »

⚠️ Ne lance JAMAIS une nouvelle session Claude Code depuis
`projet/app/`. Tout se fait depuis la racine `dl-kit/`, comme depuis
le début. C'est ce qui garde le coach actif.

⚠️ Le nom du dossier `app/` ne change pas, quel que soit le nom de
l'application. Le nom de l'app est défini dans son CLAUDE.md et dans
sa configuration, pas dans le nom du dossier.

## Étape 5.2 — Créer le projet

Toutes les commandes de création s'exécutent depuis `dl-kit/`, en
ciblant `projet/app`.

**Web** : crée le projet Next.js dans `projet/app`. Attends la fin de
l'installation, qui peut prendre plusieurs minutes — préviens
l'utilisateur avant, pour qu'il ne pense pas que c'est bloqué.

**iOS** : guide la création du projet dans Xcode, écran par écran.
Xcode ne se pilote pas en ligne de commande pour cette étape : donne
les clics exacts (nom du projet, interface SwiftUI, langage Swift), et
indique comme emplacement le dossier `projet/app` du kit.

⚠️ Si iOS : vérifie que les dossiers synchronisés au système de fichiers
sont utilisés (voir `quentin/stack-ios.md`). Sans ça, chaque fichier
créé par l'IA en ligne de commande ne sera pas pris en compte par
Xcode, et l'utilisateur aura des erreurs de compilation
incompréhensibles pendant toute la phase 6.

**Android** : guide la création du projet dans Android Studio, écran par
écran (nom du projet, langage Kotlin, template Empty Activity avec
Jetpack Compose), en ciblant `projet/app`. Une fois créé, toute
modification du fichier `build.gradle.kts` faite en ligne de commande
nécessite une synchronisation Gradle avant de continuer (voir
`quentin/stack-android.md`) — sans elle, les nouvelles dépendances ne
sont pas reconnues et l'IA risque de « corriger » du code qui n'a en
réalité pas encore été synchronisé.

## Étape 5.3 — Premier lancement

Lance le projet et fais constater le résultat à l'utilisateur.

⚠️ La commande de lancement s'exécute depuis `projet/app/`, pas depuis
la racine du kit. C'est la seule chose qui change de dossier : les
commandes du projet ciblent le projet.

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

**Commande lancée depuis le mauvais dossier** → erreur fréquente avec
cette structure. Vérifie systématiquement le répertoire courant avant
de conclure à autre chose.

**Xcode : erreur de signature / compte développeur** → un compte Apple
gratuit suffit pour le simulateur. Ne fais pas payer les 99 $ à ce
stade, c'est seulement nécessaire pour publier.

**Android Studio : dépendance non reconnue après modification de
build.gradle.kts** → une synchronisation Gradle manuelle est nécessaire
(« Sync Project with Gradle Files »). Ne cherche pas une erreur de code
avant d'avoir vérifié ce point.

Règle générale : si une erreur persiste après deux tentatives, ne
répète pas la même approche. Change de méthode, ou propose une
alternative (par exemple : basculer sur le web si l'installation iOS
est bloquée par la machine).

## Étape 5.5 — Poser le CLAUDE.md du projet

Copie le `CLAUDE.md` rédigé en phase 4 dans `projet/app/`.

⚠️ Il y a maintenant DEUX fichiers CLAUDE.md, et c'est normal :
- `dl-kit/CLAUDE.md` → ton rôle de coach, la méthode
- `dl-kit/projet/app/CLAUDE.md` → le contexte technique de l'app

Explique-le à l'utilisateur en une phrase : « Le premier me dit comment
t'accompagner, le second décrit ton app. Les deux sont lus
automatiquement quand on travaille. »

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

## Étape 5.7 — Vérifier le filet de sécurité

Avant d'entrer en construction, un dernier contrôle :

- Les checkpoints Claude Code fonctionnent (testé en phase 4)
- Si Git est initialisé : fais un commit avec le projet propre.
  C'est le point de retour « projet neuf qui marche ».

Dis explicitement : « Si tout part en vrille en phase 6, tu peux
toujours revenir ici. »

## Étape 5.8 — Vérifications avant construction

Passe en revue, en une ligne chacun :
- [ ] Le projet est bien dans `projet/app/`
- [ ] Le projet démarre
- [ ] L'utilisateur voit son app à l'écran
- [ ] `projet/app/CLAUDE.md` est en place, moins de 80 lignes
- [ ] Le point de sauvegarde initial existe
- [ ] Aucune erreur non résolue

Si un point n'est pas coché : ne passe pas à la phase 6. Règle-le.

---

## Écriture du livrable

Mets à jour `projet/architecture.md` avec une section :

```markdown
## Setup

- Projet créé le : [date]
- Emplacement : projet/app/
- Commande de lancement : [commande] (depuis projet/app/)
- Premier lancement validé : oui
- Point de sauvegarde initial : [checkpoint / commit]

### Problèmes rencontrés
[Ex : Node 18 → mise à jour vers Node 22]
```

Puis mets à jour `projet/progression.md` et annonce la phase 6 :
« Le projet tourne. Maintenant on construit la première fonctionnalité :
[reprendre la feature 1 de features.md]. »