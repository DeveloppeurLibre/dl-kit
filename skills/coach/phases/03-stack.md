# Phase 3 — Choisir les outils

Objectif : verrouiller la stack technique en quelques minutes,
sans comparatif ni exploration.
Livrable : `projet/stack.md`

## Règles pour cette phase
- Lis `projet/profil.md`, `projet/idee.md` et `projet/features.md`.
- Lis `quentin/principes.md`, puis `quentin/stack-web.md` OU
  `quentin/stack-ios.md` selon la plateforme (pas les deux).
- Tu RECOMMANDES, tu ne présentes pas d'options à comparer.
  Une recommandation + une justification courte. Pas de tableau
  comparatif, pas de « ça dépend ».
- Presque tout est déjà déterminé par les phases 0 et 2. Cette phase
  doit prendre 5 minutes, pas 30.
- Ne passe pas à la phase 4 tant que `projet/stack.md` n'est pas écrit.

## Message d'ouverture

« On passe aux outils. Je vais te faire des recommandations directes
plutôt que te présenter dix options — le but n'est pas de choisir la
stack parfaite, c'est d'en choisir une qui marche et d'avancer. Tu
pourras toujours changer plus tard si ton projet le justifie. »

---

## Étape 3.1 — Confirmer la plateforme

La plateforme a été choisie en phase 0. Confirme-la, ne la rouvre pas :

« On part sur [web / iOS / Android], comme décidé au départ. »

⚠️ Vérifie la cohérence avec `profil.md` :
- Machine Windows ou Linux + cible iOS → impossible. Ça aurait dû être
  bloqué en phase 0. Si ça arrive ici, arrête et recadre maintenant :
  web app ou Android.
- Aucune contrainte native identifiée en phase 2 + cible native →
  signale-le une fois : « Rien dans tes features ne nécessite une app
  native. Le web serait plus rapide à construire et à tester. Tu veux
  qu'on bascule ? » Si l'utilisateur maintient, avance sans insister.

## Étape 3.2 — Annoncer la stack

Présente la stack complète d'un bloc, sans la faire choisir.

**Si web** (voir `quentin/stack-web.md`) :

- Interface : Next.js (React)
- Style : Tailwind CSS
- Hébergement : Netlify
- Base de données : [selon étape 2.5]

**Si iOS** (voir `quentin/stack-ios.md`) :

- Interface : SwiftUI
- Outil : Xcode
- Données locales : SwiftData
- Base de données distante : [selon étape 2.5]
- Publication : App Store

**Si Android** (voir `quentin/stack-android.md`) :

- Langage : Kotlin
- Interface : Jetpack Compose
- Outil : Android Studio
- Données locales : Room
- Base de données distante : [selon étape 2.5]
- Publication : Google Play

Puis une justification courte, adaptée au niveau :
- Débutant : « C'est ce qui est le mieux compris par l'IA, donc tu
  auras moins de blocages. »
- Intermédiaire / avancé : justification technique en 2 lignes max.

Ne détaille pas chaque outil. L'utilisateur n'a pas besoin de comprendre
Next.js pour commencer — il le découvrira en construisant.

## Étape 3.3 — Le stockage des données

Reprends la réponse de l'étape 2.5.

**Données locales uniquement** → aucun service externe en v1.
Dis-le explicitement : « Tes données restent sur ton appareil.
Pas de base de données à configurer, pas de compte à créer.
C'est un vrai avantage pour démarrer. »

**Données accessibles depuis plusieurs endroits** → Supabase.

Dans ce cas, préviens dès maintenant, quel que soit le niveau :
« Ça implique de créer un compte Supabase et de gérer des clés d'accès.
Je t'accompagnerai, mais retiens un point de sécurité dès maintenant :
certaines clés peuvent aller dans ton code, d'autres jamais. On y
reviendra au moment de la configuration — voir `quentin/securite.md`. »

## Étape 3.4 — Les coûts réels

Annonce les coûts avant de commencer, jamais après. Adapte à la stack :

- Claude Code : abonnement en cours (déjà en place)
- Hébergement web (Netlify) : gratuit pour un projet de cette taille
- Supabase : gratuit jusqu'à un certain volume, suffisant pour une v1
- Compte développeur Apple : ~99 $/an, obligatoire pour publier sur
  l'App Store
- Compte Google Play : ~25 $ une fois

Puis : « Est-ce que ces coûts te vont ? Si le compte Apple est un
blocage, on peut partir sur une web app qui fonctionne aussi sur
iPhone, sans frais ni délai de validation. »

C'est le dernier moment pour basculer sans perdre de travail.

## Étape 3.5 — Vérifier ce qui est installé

Liste ce qui doit être présent sur la machine et vérifie un par un :

**Web** : Node.js, un éditeur de code, Git
**iOS** : Xcode, un compte Apple (gratuit suffit pour tester)
**Android** : Android Studio, un JDK (installé avec Android Studio), un
compte Google (gratuit suffit pour tester)

Pour chaque élément manquant : donne la commande ou le lien
d'installation, adapté au système d'exploitation de `profil.md`.

Si niveau débutant : explique ce que fait chaque outil en une phrase
avant de l'installer. Ne lance jamais une commande sans dire ce qu'elle
fait.

Ne passe pas à la suite tant que tout n'est pas installé et vérifié.

## Étape 3.6 — Verrouiller

« On ne changera plus de stack à partir d'ici. Si tu veux changer
quelque chose, c'est maintenant. »

Ce verrouillage est important : changer d'outil en cours de
construction est une des causes les plus fréquentes de projet
abandonné. Une fois `stack.md` écrit, la question est close.

---

## Écriture du livrable

Crée `projet/stack.md` :

```markdown
# Stack technique

## Plateforme
[web / iOS / Android]

## Outils
- Interface : [...]
- Style : [...]
- Données locales : [...]
- Base de données distante : [aucune / Supabase]
- Hébergement / publication : [...]

## Installé et vérifié
- [ ] [outil] — version [...]
- [ ] [outil] — version [...]

## Coûts
- [poste] : [montant]

## Notes
[Ex : basculé de iOS vers web à cause du compte Apple]
```

Puis mets à jour `projet/progression.md` et annonce la phase 4 :
« Les outils sont posés. Maintenant on organise le projet avant
d'écrire la première ligne de code. »