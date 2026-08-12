# Gabarit CLAUDE.md — projet iOS

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
de `idee.md`, complétée par la stack — ex : "App de suivi d'entraînement
solo, en SwiftUI + SwiftData, pour un seul utilisateur."]

## Commandes
- Lancer : `[Cmd+R dans Xcode, ou xcodebuild -scheme ... -destination ...
  si le projet a un scheme nommé]`
- Tester : `[Cmd+U dans Xcode, ou xcodebuild test -scheme ...]`
- Construire : `[Cmd+B dans Xcode]`

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
dans `quentin/securite.md` et `quentin/stack-ios.md` ce qui s'applique
réellement à CE projet — pas une liste générique copiée telle quelle.]
- [ex : dossiers synchronisés avec le système de fichiers — tout fichier
  .swift créé hors Xcode doit être rattaché à la target, sinon il ne
  compile pas]
- [ex : compte développeur gratuit suffisant jusqu'à la publication,
  ne pas faire payer le compte à 99$ avant la phase 8]
- [ex : la publishable key Supabase peut aller dans le projet, jamais
  la secret key]
- [point spécifique à ce projet, ex : contrainte métier non évidente]

## Niveau utilisateur
[débutant / intermédiaire / avancé] — adapte tes explications pendant
la construction en conséquence.
