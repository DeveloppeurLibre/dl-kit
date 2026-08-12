# Gabarit CLAUDE.md — projet Android

Usage interne, destiné à toi l'agent (phase 4, étape 4.3). Copie tout ce
qui suit le séparateur dans le `CLAUDE.md` du projet, remplace chaque
`[placeholder]`, retire les lignes qui ne s'appliquent pas au projet.
Le résultat final doit rester sous 80 lignes — ce gabarit en fait déjà
partie, ne rajoute pas de sections.

Ordre imposé, ne pas réorganiser : scope, commandes, exclusions,
anti-dérive, caveats, niveau utilisateur.

---

# [Nom de l'app]

[Une phrase : ce que fait l'app, pour qui. Reprise de la phrase de scope
de `idee.md`, complétée par la stack — ex : "App de suivi de dépenses
solo, en Kotlin + Jetpack Compose + Room, pour un seul utilisateur."]

## Commandes
- Lancer : `[Run dans Android Studio, ou ./gradlew installDebug]`
- Tester : `[./gradlew test]`
- Construire : `[./gradlew assembleDebug]`

## Hors scope v1
[Liste copiée telle quelle depuis les exclusions de `idee.md`. Ne pas
reformuler — c'est ce qui protège du scope creep.]
- [...]
- [...]

## IMPORTANT — Anti-dérive
N'ajoute AUCUNE fonctionnalité non listée ci-dessus sans demander
confirmation explicite d'abord, même si elle paraît évidente ou utile.

## Caveats
[Uniquement des points non devinables par une IA générique. Piocher
dans `quentin/securite.md` et `quentin/stack-android.md` ce qui
s'applique réellement à CE projet — pas une liste générique copiée
telle quelle.]
- [ex : après tout ajout de dépendance dans build.gradle.kts, une
  synchronisation Gradle est nécessaire avant de continuer]
- [ex : compte développeur Google Play (~25$, paiement unique) requis
  seulement à la phase de publication, pas avant]
- [ex : la publishable key Supabase peut aller dans le projet, jamais
  la secret key]
- [point spécifique à ce projet, ex : contrainte métier non évidente]

## Niveau utilisateur
[débutant / intermédiaire / avancé] — adapte tes explications pendant
la construction en conséquence.
