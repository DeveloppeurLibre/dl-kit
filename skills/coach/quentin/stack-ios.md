# Stack iOS — référence pour le coach

Fichier destiné à toi, l'agent. Sert en phase 3 (annoncer la stack), en
phase 4 (caveats du CLAUDE.md du projet) et surtout en phase 5 (setup) —
c'est là que le piège des dossiers synchronisés se déclenche concrètement.

---

## La stack par défaut

- Interface : **SwiftUI**
- Outil : **Xcode**
- Données locales : **SwiftData**
- Données distantes (si besoin multi-appareils) : **Supabase**
- Publication : **App Store**

**Pourquoi ce choix** : SwiftUI est aujourd'hui le framework d'interface
recommandé par Apple et le mieux représenté dans les données
d'entraînement récentes, ce qui réduit les erreurs de génération par
rapport à UIKit. SwiftData réduit la quantité de code nécessaire pour la
persistance locale par rapport à Core Data.

Rappel du principe général : le natif ne se justifie que si notifications
push, capteurs, ou vente App Store sont indispensables dès la v1 (voir
`principes.md`). Si aucun de ces critères n'est présent, signale-le avant
la phase 3 — pas après avoir commencé.

---

## Le piège des dossiers synchronisés Xcode — BLOQUANT en phase 5

**Détection** : le projet Xcode a été créé sans l'option de dossier
synchronisé avec le système de fichiers (« folder reference » / groupe
synchronisé), ou tu ne sais pas laquelle des deux options a été utilisée
à la création.

**Pourquoi ça bloque** : Xcode a historiquement deux façons de référencer
des fichiers — des groupes qui vivent uniquement dans le fichier projet
(`.pbxproj`), et des dossiers synchronisés avec le système de fichiers.
Quand un fichier `.swift` est créé par l'IA en ligne de commande (donc
directement sur le disque, hors de l'interface Xcode), il n'apparaît dans
le projet QUE si le dossier parent est synchronisé. Sinon, le fichier
existe sur le disque, compile pour personne, et Xcode continue de dire
« Cannot find X in scope » comme si le fichier n'existait pas — une
erreur incompréhensible pour quelqu'un qui voit le fichier dans son
éditeur.

**Comment gérer** :
- Vérifie ce point dès la création du projet en phase 5, pas quand
  l'erreur apparaît en phase 6.
- Dans les projets Xcode récents (créés avec Xcode 16+), les dossiers
  sont synchronisés par défaut — mais vérifie-le explicitement plutôt
  que de le supposer.
- Si un fichier créé par l'IA ne compile pas et que le message évoque un
  symbole introuvable alors que le fichier existe visiblement : c'est le
  premier réflexe à avoir, avant de chercher une erreur de syntaxe.
- Explique le point à l'utilisateur en une phrase, même débutant : « Sur
  iOS, un fichier créé en dehors d'Xcode doit être rattaché au projet,
  sinon il n'existe pas pour le compilateur. »

---

## Compte développeur Apple : gratuit vs payant

- Un compte Apple **gratuit** suffit pour développer et tester dans le
  simulateur, et même pour installer l'app sur un appareil physique en
  développement.
- Le compte payant (~99 $/an) n'est nécessaire QUE pour publier sur
  l'App Store (TestFlight inclus). Ne fais jamais payer ce compte avant
  la phase 8 (publication).
- Si une erreur de signature apparaît avant la phase 8 : c'est presque
  toujours un problème de compte gratuit mal sélectionné dans les
  réglages de signature du projet, pas un besoin réel de compte payant.

## Pièges de génération de code Swift

### Fichiers créés par l'IA non ajoutés à la target

Conséquence directe du piège des dossiers synchronisés ci-dessus. Si ce
n'est pas le cas et que le fichier n'apparaît toujours pas : vérifie
manuellement que le fichier est coché dans la target de l'app (panneau
File Inspector, section Target Membership).

### Previews SwiftUI cassés par SwiftData

**Détection** : la preview Xcode plante ou reste vide sur une vue qui
utilise un `@Query` ou un `modelContext` SwiftData.
**Pourquoi ça bloque** : la preview a besoin d'un conteneur SwiftData en
mémoire, distinct du conteneur réel de l'app. Sans ça, elle cherche un
contexte qui n'existe pas dans l'environnement de preview.
**Comment gérer** : fournis systématiquement un `.modelContainer` en
mémoire (`isStoredInMemoryOnly: true`) dans le code de preview des vues
qui dépendent de SwiftData.

### API ou symboles inventés

Même principe que sur le web (`securite.md`, section dépendances) : les
frameworks Apple évoluent vite d'une version d'Xcode à l'autre. Vérifie
qu'une API SwiftUI ou SwiftData proposée existe réellement dans la
version d'Xcode installée avant de t'appuyer dessus — les hallucinations
de symboles sont fréquentes sur les API récentes (moins de deux ans).

## Supabase côté iOS

- Utilise le SDK officiel `supabase-swift`, jamais d'appel HTTP fait à la
  main pour parler à Supabase.
- La publishable key va dans le code ou dans un fichier de configuration
  du projet — jamais la secret key (rappel `securite.md`).
- Ne stocke jamais un token de session dans `UserDefaults`. Utilise le
  Keychain (le SDK officiel le fait automatiquement si utilisé
  correctement) — `UserDefaults` n'est pas chiffré sur le disque.

## Simulateur vs appareil physique

- Le simulateur suffit pour la quasi-totalité des tests de la
  construction. Ne pousse pas vers un appareil physique sans raison
  (capteur, performance réelle) — ça ajoute une étape de configuration
  de signature pour peu de bénéfice à ce stade.
- Si l'utilisateur veut tester sur son propre iPhone : ça reste possible
  avec un compte gratuit, mais l'app expire au bout de 7 jours et doit
  être réinstallée. Précise-le pour éviter la confusion « mon app a
  disparu ».
