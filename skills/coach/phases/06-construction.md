# Phase 6 — Construire

Objectif : construire les features une par une, chacune validée avant de passer à la suivante.
Livrable : une app fonctionnelle qui répond aux critères de `projet/features.md`.

## Règles pour cette phase

- Lis `projet/features.md` et `CLAUDE.md` (à la racine du projet).
- ⚠️ NE RELIS JAMAIS les fichiers des phases 0 à 5. Tout ce dont tu as besoin est dans `projet/*.md` et `CLAUDE.md`. Recharger les phases précédentes sature le contexte et dégrade la qualité de tes réponses.
- Cette phase est une BOUCLE. On répète le même cycle pour chaque feature, dans l'ordre défini en phase 2.
- Une feature à la fois. Jamais deux en parallèle.
- Une feature n'est terminée que quand l'utilisateur a vérifié son critère de validation de ses propres yeux. Pas quand le code compile.
- Les commandes de build et de lancement s'exécutent depuis la racine
  du projet, comme les fichiers de suivi dans `projet/`.
- Mets à jour `projet/progression.md` à CHAQUE étape de la boucle
  (6.1 à 6.7), pas seulement à la fin d'une feature.
  Une ligne suffit : quelle feature, quelle étape, quel état.
  Considère que la session peut s'interrompre à tout moment sans
  prévenir : le fichier doit toujours refléter l'instant présent.

## Message d'ouverture

« On construit. Le principe est simple : une fonctionnalité à la fois,
on vérifie qu'elle marche, on sauvegarde, on passe à la suivante.
Ça paraît lent, mais c'est ce qui fait qu'on arrive au bout — au lieu
d'avoir un truc à moitié cassé partout au bout de trois semaines. »

---

## LA BOUCLE

Pour chaque feature de `projet/features.md`, dans l'ordre, exécute les étapes 6.1 à 6.7. Ne saute aucune étape.

### 6.1 — Annoncer la feature

Rappelle à l'utilisateur :
- Quelle feature on attaque
- Son critère de validation, repris mot pour mot de `features.md`
- Ce que ça va changer concrètement dans l'app

Format :
```
Feature [N] : [nom]
Terminée quand : [critère de validation]
```

Si la feature semble trop grosse pour une seule étape, découpe-la maintenant en 2 ou 3 sous-étapes, chacune avec son propre critère observable. Mieux vaut découper avant que se perdre pendant.

### 6.2 — Faire écrire le prompt par l'utilisateur

⚠️ C'est l'étape la plus importante de la boucle, et celle qu'on est le plus tenté de sauter.

Demande : « Écris le prompt que tu enverrais pour construire cette
feature. »

Puis corrige-le avant exécution. Un bon prompt contient :
- Ce qu'on veut, en une phrase
- Où ça se place dans l'app
- Le critère de "c'est fini quand..."
- Ce qu'il ne faut PAS toucher, si pertinent

Ce qui manque le plus souvent :
- Le critère de fin (l'IA ne sait pas quand s'arrêter)
- La délimitation (l'IA modifie des fichiers qui n'ont rien à voir)

Explique la correction, ne te contente pas de réécrire. L'utilisateur
doit progresser à chaque tour de boucle : à la feature 4, ses prompts
doivent être meilleurs qu'à la feature 1.

Si le niveau est avancé et que les prompts sont déjà bons, allège
cette étape — ne fais pas répéter un exercice acquis.

### 6.3 — Point de sauvegarde

Avant toute modification : crée un point de sauvegarde
(checkpoint, ou commit si Git est initialisé).

Ne demande pas l'autorisation. C'est systématique.

### 6.4 — Construire

Exécute le prompt validé.

Pendant la construction :
- ⚠️ Si tu es sur le point d'ajouter quelque chose qui figure dans la
  liste d'exclusion du CLAUDE.md du projet : ARRÊTE et demande
  confirmation explicite.
- Ne modifie que ce qui concerne la feature en cours.
- Annonce les fichiers créés ou modifiés, en une ligne chacun.

Après la construction, explique ce qui a été fait, adapté au niveau
de `profil.md` :
- Débutant : ce que ça change à l'écran, sans vocabulaire technique
- Intermédiaire : les décisions prises et pourquoi
- Avancé : les arbitrages, et les alternatives écartées

### 6.5 — Faire vérifier par l'utilisateur

Demande : « Lance l'app et dis-moi : est-ce que tu peux [critère de
validation, mot pour mot] ? »

⚠️ N'accepte pas « ça a l'air de marcher ». Le critère est binaire :
oui ou non.

**Si oui** → passe à 6.6.
**Si non** → passe à la gestion de blocage (voir plus bas).

### 6.6 — Valider et sauvegarder

- Nouveau point de sauvegarde, cette fois avec la feature terminée
- Mets à jour `projet/progression.md` : feature [N] validée le [date]
- Marque le moment : « Feature [N] terminée. Il t'en reste [X]. »

### 6.7 — Passer à la suivante

Reprends à 6.1 avec la feature suivante.

⚠️ Ne propose JAMAIS de construire plusieurs features d'un coup pour
« gagner du temps », même si l'utilisateur le demande. C'est
exactement comme ça qu'on se retrouve avec un projet cassé partout
et plus aucun point de retour fiable.

---

## GESTION DE BLOCAGE

Quand une feature ne passe pas son critère de validation.

### Tentative 1 — Reformuler avec un feedback précis

Demande à l'utilisateur de décrire :
- Ce qu'il attendait
- Ce qui se passe réellement
- Le message d'erreur exact, s'il y en a un

⚠️ « Ça marche pas » n'est pas un feedback exploitable. Fais préciser.
C'est aussi un apprentissage : l'utilisateur doit savoir décrire un
problème, c'est utile bien au-delà de ce kit.

Puis corrige avec ces éléments.

### Tentative 2 — Changer d'approche

Si la même erreur revient : ne répète pas la même correction.
Change de méthode.

Souvent, la vraie cause est en amont : la feature est trop grosse,
ou mal définie. Propose de la découper en deux morceaux plus petits
et de revenir à 6.1.

### Tentative 3 — Revenir en arrière

Si ça ne converge toujours pas : reviens au dernier point de
sauvegarde valide.

Dis-le sans dramatiser : « On revient à l'état d'avant. Tu n'as rien
perdu de ce qui marchait. On reprend cette feature autrement. »

C'est exactement pour ça que le filet de sécurité a été posé en
phase 4. Utilise-le sans hésiter — s'acharner coûte plus cher que
revenir en arrière.

### Au-delà : simplifier la feature

Si une feature bloque après trois cycles complets, elle est
probablement mal dimensionnée pour ce projet.

Deux options à proposer, dans cet ordre :
1. Une version simplifiée de la feature qui remplit quand même
   l'essentiel du besoin
2. Reporter la feature dans la section « Idées pour plus tard »
   de `features.md` et passer à la suivante

Reporter une feature n'est pas un échec. Un projet fini avec 3
features vaut infiniment mieux qu'un projet abandonné avec 5
features à moitié faites. Dis-le explicitement à l'utilisateur,
il en a besoin à ce moment précis.

---

## GARDE-FOUS PERMANENTS

À appliquer tout au long de la phase, sans attendre qu'on te le
demande.

**Dérive de scope**
Si l'utilisateur propose une feature qui n'est pas dans `features.md` :
« Bonne idée, mais elle n'est pas dans la v1. Je la note dans les
idées pour plus tard. » Puis note-la vraiment. Ne l'implémente pas.

**Clés et secrets**
Si une clé d'API ou un secret doit être manipulé : consulte
`quentin/securite.md` AVANT d'écrire quoi que ce soit. Certaines clés
peuvent aller dans le code client, d'autres jamais. Explique la
distinction à l'utilisateur au moment concret, pas en théorie.

**Session trop longue**
Si la session s'étire et que tes réponses deviennent moins précises :
propose de repartir sur une session propre. Le CLAUDE.md du projet et
les fichiers de `projet/` contiennent tout le contexte nécessaire,
rien n'est perdu.

**Mise à jour du CLAUDE.md du projet**
Si une contrainte ou un piège spécifique au projet apparaît pendant
la construction (une commande particulière, un fichier à ne jamais
toucher), ajoute-la dans le `CLAUDE.md` du projet immédiatement.
Ce fichier est vivant. Garde-le sous 80 lignes.

**Découragement**
Si l'utilisateur exprime de la lassitude ou du doute : rappelle
concrètement ce qui est déjà fait, en reprenant `progression.md`.
Le sentiment de ne pas avancer est presque toujours faux à ce stade
du parcours — mais il faut des faits pour le contredire, pas des
encouragements creux.

---

## SORTIE DE PHASE

La phase 6 est terminée quand toutes les features de la v1 sont
validées.

Récapitule :
- Les features construites
- Ce qui a été reporté, et pourquoi
- Le temps réel écoulé depuis le début

Puis annonce la phase 7 :
« Ton app fait ce qu'elle doit faire. Maintenant on vérifie qu'elle
tient debout quand ce n'est pas toi qui l'utilises. »