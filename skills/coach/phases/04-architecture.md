# Phase 4 — Organiser le projet

Objectif : poser une structure de fichiers claire et créer le CLAUDE.md
du projet, qui tiendra le cadre pendant toute la construction.
Livrable : projet créé + `CLAUDE.md` du projet + `projet/architecture.md`

## Règles pour cette phase
- Lis `projet/profil.md`, `idee.md`, `features.md`, `stack.md`.
- Lis `quentin/principes.md` et le template correspondant dans
  `templates/`.
- Ne fais PAS un cours d'architecture logicielle. On pose une
  organisation simple et on avance.
- Le CLAUDE.md du projet doit rester COURT : moins de 80 lignes.
  C'est une règle stricte, pas une indication.
- Ne passe pas à la phase 5 tant que le projet n'existe pas sur
  la machine avec son CLAUDE.md.

## Message d'ouverture

« Dernière étape avant de construire. On va créer ton projet et
surtout un fichier qui va servir de garde-fou : c'est lui qui
empêchera l'IA de partir dans tous les sens pendant qu'on construit. »

---

## Étape 4.1 — Créer le projet

Crée le projet avec l'outil adapté à la stack de `stack.md`.

- Demande d'abord où le créer sur la machine (chemin).
- Explique ce que fait la commande AVANT de la lancer si niveau
  débutant.
- Vérifie que le projet démarre correctement avant de continuer :
  lance-le et fais confirmer à l'utilisateur qu'il voit bien
  quelque chose s'afficher.

⚠️ Ne continue pas si le projet ne démarre pas. Un problème
d'installation non résolu ici deviendra un blocage bien plus
coûteux en phase 6.

## Étape 4.2 — L'organisation des fichiers

Présente l'organisation retenue, sans la faire choisir.

Explique-la en une phrase par dossier, en langage simple. Exemple :
« Les écrans que tu vois vont ici. Les données vont là. Ce qui sert
à plusieurs endroits va dans un troisième dossier. »

Règle : au maximum 4 ou 5 dossiers pour une v1. Une organisation
trop fine est du temps perdu à un stade où le projet est petit.

Ne crée pas des dossiers vides « au cas où ». On crée quand on
en a besoin.

## Étape 4.3 — Le CLAUDE.md du projet

C'est la pièce maîtresse de cette phase. Explique à l'utilisateur
à quoi il sert avant de l'écrire :

« Ce fichier est lu par l'IA au début de chaque session. Il contient
ce qu'elle doit savoir sur ton projet et ce qu'elle n'a pas le droit
de faire. Sans lui, elle repart de zéro à chaque fois et finit par
ajouter des choses que tu n'as pas demandées. »

Construis-le à partir des fichiers de `projet/`, en reprenant
le template de `templates/`.

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
   pièges connus de la plateforme (`quentin/stack-ios.md` ou
   `stack-web.md`).
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

## Étape 4.4 — Le filet de sécurité

Mets en place le moyen de revenir en arrière.

- Vérifie que les points de sauvegarde sont actifs.
- Fais un premier point de sauvegarde maintenant, avec le projet
  vide qui fonctionne. C'est le point de retour de référence.
- Explique en une phrase : « Si l'IA casse quelque chose pendant la
  construction, on peut revenir à un état qui marchait. »

Si niveau débutant : ne rentre pas dans le détail de Git. L'essentiel
est de savoir qu'un retour arrière est possible et comment le demander.

## Étape 4.5 — Le test de démarrage à froid

Test important, à ne pas sauter :

Demande à l'utilisateur de fermer la session en cours et d'en ouvrir
une nouvelle dans le dossier du projet. Puis de poser une question
simple sur le projet.

Objectif : vérifier que le CLAUDE.md est bien lu et que l'IA sait
de quoi il s'agit sans qu'on lui réexplique.

Si ce n'est pas le cas : le fichier est mal placé ou mal formé.
Corrige maintenant — c'est bien plus coûteux à découvrir en pleine
construction.

---

## Écriture du livrable

Crée `projet/architecture.md` :

```markdown
# Organisation du projet

## Emplacement
[chemin du projet sur la machine]

## Structure
- `[dossier]/` : [rôle en une phrase]
- `[dossier]/` : [rôle en une phrase]

## Commandes
- Lancer : `[...]`
- Tester : `[...]`
- Construire : `[...]`

## Filet de sécurité
Point de sauvegarde initial créé le [date].

## CLAUDE.md du projet
Créé et vérifié. Contient : scope, exclusions, règle anti-dérive,
caveats de la stack.
```

Puis mets à jour `projet/progression.md` et annonce la phase 5 :
« Tout est en place. On peut commencer à construire la première
fonctionnalité. »