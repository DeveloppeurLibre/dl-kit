# Phase 4 — Organiser le projet

Objectif : décider de l'organisation des fichiers et rédiger le
CLAUDE.md du projet, qui tiendra le cadre pendant toute la
construction. Cette phase ne produit que des décisions écrites — le
projet lui-même est créé en phase 5.
Livrable : `projet/architecture.md` + un brouillon `projet/CLAUDE.md`,
prêt à être installé dans le projet en phase 5.

## Règles pour cette phase
- Lis `projet/profil.md`, `idee.md`, `features.md`, `stack.md`.
- Lis `quentin/principes.md` et le template correspondant dans
  `templates/`.
- Ne fais PAS un cours d'architecture logicielle. On pose une
  organisation simple et on avance.
- Le CLAUDE.md du projet doit rester COURT : moins de 80 lignes.
  C'est une règle stricte, pas une indication.
- Aucune commande n'est exécutée dans cette phase. Ce sont des
  décisions sur papier ; l'exécution vient en phase 5.
- Ne passe pas à la phase 5 tant que `projet/architecture.md` et le
  brouillon `projet/CLAUDE.md` ne sont pas écrits.

## Message d'ouverture

« Avant-dernière étape avant de construire pour de vrai. On va décider
comment organiser le projet et rédiger un fichier qui va servir de
garde-fou : c'est lui qui empêchera l'IA de partir dans tous les sens
pendant qu'on construit. »

---

## Étape 4.1 — L'organisation des fichiers

Décide l'organisation à adopter, sans encore rien créer sur la machine
— la création physique se fait en phase 5.

Présente l'organisation retenue, sans la faire choisir. Explique-la en
une phrase par dossier, en langage simple. Exemple : « Les écrans que
tu vois vont ici. Les données vont là. Ce qui sert à plusieurs
endroits va dans un troisième dossier. »

Règle : au maximum 4 ou 5 dossiers pour une v1. Une organisation trop
fine est du temps perdu à un stade où le projet est petit.

Ne planifie pas de dossiers vides « au cas où ». On crée quand on en a
besoin.

## Étape 4.2 — Le CLAUDE.md du projet

C'est la pièce maîtresse de cette phase. Explique à l'utilisateur
à quoi il sert avant de l'écrire :

« Ce fichier est lu par l'IA au début de chaque session de travail sur
ton projet. Il contient ce qu'elle doit savoir et ce qu'elle n'a pas
le droit de faire. Sans lui, elle repart de zéro à chaque fois et
finit par ajouter des choses que tu n'as pas demandées. »

Rédige-le maintenant dans `projet/CLAUDE.md` — un brouillon, puisque le
projet n'existe pas encore sur la machine. Il sera installé à la
racine du projet en phase 5.

Construis-le à partir des fichiers de `projet/`, en reprenant le
template de `templates/`.

Contenu obligatoire, dans cet ordre :

1. **Une ligne décrivant le projet** — reprise de la phrase de scope
   de `idee.md`, complétée par la stack.
2. **Les commandes essentielles** — lancer, tester, construire.
   Uniquement celles utilisées au quotidien.
3. **Ce qui NE rentre PAS dans la v1** — copie la liste d'exclusion
   de `idee.md`.
4. **La règle anti-dérive** — instruction explicite à l'IA de demander
   confirmation avant d'ajouter toute fonctionnalité non listée.
5. **Les caveats du projet** — spécificités non devinables :
   contraintes de la stack, points de sécurité (`quentin/securite.md`),
   pièges connus de la plateforme (`quentin/stack-web.md`,
   `quentin/stack-ios.md` ou `quentin/stack-android.md` selon le cas).
6. **Une ligne sur le niveau de l'utilisateur** — pour que l'IA adapte
   ses explications pendant la construction.

Règles strictes :
- Moins de 80 lignes au total.
- AUCUNE règle de style de code (indentation, nommage, guillemets).
  Un linter fait ça mieux et ça gaspille des instructions.
- Ne génère JAMAIS ce fichier avec `/init`. Un fichier généré
  automatiquement est trop long et contient des instructions vagues
  qui dégradent toutes les réponses futures.
- Les instructions les plus importantes en HAUT du fichier.
- Utilise IMPORTANT ou JAMAIS en majuscules pour les règles critiques
  (clés d'API, fichiers à ne pas toucher).

Après écriture : montre le fichier à l'utilisateur et explique
chaque section en une phrase. Il doit comprendre ce qu'il contient,
c'est lui qui devra le maintenir.

---

## Écriture du livrable

Crée `projet/architecture.md` :

```markdown
# Organisation du projet

## Structure prévue
- `[dossier]/` : [rôle en une phrase]
- `[dossier]/` : [rôle en une phrase]

## CLAUDE.md du projet
Brouillon rédigé dans `projet/CLAUDE.md`. Contient : scope, exclusions,
règle anti-dérive, caveats de la stack. À installer à la racine du
projet en phase 5.
```

Puis mets à jour `projet/progression.md` et annonce la phase 5 :
« L'organisation est décidée et le garde-fou est rédigé. Maintenant on
crée le projet pour de vrai. »
