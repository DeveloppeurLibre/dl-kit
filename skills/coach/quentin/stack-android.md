# Stack Android — référence pour le coach

Fichier destiné à toi, l'agent. Sert en phase 3 (annoncer la stack), en
phase 4 (caveats du CLAUDE.md du projet) et en phase 5 (setup).

---

## La stack par défaut

- Langage : **Kotlin**
- Interface : **Jetpack Compose**
- Données locales : **Room**
- Données distantes (si besoin multi-appareils) : **Supabase**
- Publication : **Google Play**

**Pourquoi ce choix** : Jetpack Compose est aujourd'hui l'interface
recommandée par Google pour tout nouveau projet Android, et le mieux
représenté dans les données d'entraînement récentes — moins d'erreurs de
génération que sur l'ancien système de vues XML. Room réduit la
quantité de code nécessaire pour la persistance locale par rapport à
l'accès direct à SQLite.

Rappel du principe général : le natif ne se justifie que si notifications
push, capteurs, ou vente sur un store sont indispensables dès la v1 (voir
`principes.md`). Si aucun de ces critères n'est présent, signale-le avant
la phase 3 — pas après avoir commencé.

---

## Pièges de génération de code sur cette stack

### Confusion sur l'état et la recomposition

**Détection** : une valeur modifiée dans un `@Composable` ne met pas
l'interface à jour, ou l'interface se redessine en boucle.
**Pourquoi ça bloque** : Compose ne réagit qu'aux changements de state
observable (`remember { mutableStateOf(...) }`, ou state hoisting depuis
un ViewModel). Une variable Kotlin classique modifiée dans un composable
ne déclenche aucune recomposition.
**Comment gérer** : vérifie que tout état affiché passe par
`mutableStateOf`/`State` ou par un `StateFlow` exposé par un ViewModel,
jamais par une variable locale mutable brute.

### Coroutines mal scopées

**Détection** : une coroutine lancée directement dans un composable avec
`GlobalScope`, ou un appel réseau/DB déclenché à chaque recomposition.
**Pourquoi ça bloque** : une coroutine sur `GlobalScope` survit à l'écran
qui l'a lancée — fuite mémoire ou crash sur un écran qui n'existe plus.
Un appel lancé directement dans le corps du composable (hors
`LaunchedEffect`) se relance à chaque recomposition, parfois plusieurs
fois par seconde.
**Comment gérer** : toute coroutine liée à un écran passe par
`LaunchedEffect` (dans un composable) ou `viewModelScope` (dans un
ViewModel). Jamais `GlobalScope` dans le code applicatif.

### Erreurs de synchronisation Gradle

**Détection** : une dépendance ajoutée dans `build.gradle.kts` n'est pas
reconnue, ou un symbole d'une bibliothèque fraîchement ajoutée reste en
erreur alors que le code est correct.
**Pourquoi ça bloque** : Android Studio doit resynchroniser le projet
après toute modification des fichiers Gradle. Un agent qui édite
`build.gradle.kts` en ligne de commande ne déclenche pas cette synchro
automatiquement.
**Comment gérer** : après toute modification de dépendance, indique
explicitement qu'une synchronisation Gradle est nécessaire (« Sync
Project with Gradle Files ») avant de continuer à coder dessus.

### Version du compilateur Compose incompatible avec Kotlin

**Détection** : erreur de build mentionnant une incompatibilité entre la
version de Kotlin et celle du plugin/compilateur Compose.
**Pourquoi ça bloque** : Compose dépend d'une version précise du
compilateur Kotlin. Un projet créé par un gabarit récent d'Android
Studio gère ça automatiquement (BOM Compose) — un ajout manuel de
dépendance peut casser cet alignement.
**Comment gérer** : ne fixe pas de version de bibliothèque Compose à la
main. Laisse le catalogue de versions du projet (`libs.versions.toml`)
piloter les versions, et modifie-le plutôt qu'un numéro en dur dans
`build.gradle.kts`.

### Permissions runtime

**Détection** : l'app a besoin d'un accès (localisation, notifications,
caméra) et plante au lieu de demander l'autorisation.
**Pourquoi ça bloque** : depuis Android 6, les permissions sensibles
doivent être demandées à l'exécution, en plus d'être déclarées dans le
manifeste. Oublier l'une des deux fait planter l'app au moment de
l'accès, pas au lancement.
**Comment gérer** : pour toute permission sensible, vérifie la présence
à la fois de la déclaration dans `AndroidManifest.xml` et de la demande
runtime (`ActivityResultContracts.RequestPermission` ou équivalent
Compose).

### API ou symboles inventés

Même principe que sur les autres plateformes (`securite.md`, section
dépendances) : l'écosystème Jetpack évolue vite et beaucoup de tutoriels
en ligne utilisent encore l'ancien système de vues (XML, `findViewById`).
Vérifie qu'une API Compose proposée existe réellement dans la version
du projet avant de t'appuyer dessus.

---

## Compte développeur Google Play

- Un compte Google gratuit suffit pour développer et tester dans
  l'émulateur ou sur un appareil physique en debug.
- Le compte développeur Google Play (~25 $, paiement unique, pas un
  abonnement) n'est nécessaire QUE pour publier. Ne fais jamais payer ce
  compte avant la phase 8 (publication).
- Contrairement à Apple, c'est un paiement unique — pas de renouvellement
  annuel à anticiper.

## Émulateur

- Utilise une image système **avec Google Play** (« Google Play » dans
  le nom de l'image, pas « Google APIs » seul) si l'app utilise des
  services Google (Sign-In, Maps, notifications push). Une image sans
  Play Store fait planter ou échouer silencieusement ces fonctionnalités.
- L'émulateur suffit pour la quasi-totalité des tests de la construction.
  Ne pousse pas vers un appareil physique sans raison concrète.

## Supabase côté Android

- Utilise le SDK officiel `supabase-kt`, jamais d'appel HTTP fait à la
  main pour parler à Supabase.
- La publishable key va dans le code ou dans un fichier de configuration
  du projet — jamais la secret key (rappel `securite.md`).
- Ne stocke jamais un token de session dans les `SharedPreferences` en
  clair. Utilise `EncryptedSharedPreferences` ou le Keystore Android — le
  SDK officiel gère correctement ce point s'il est utilisé tel quel.
