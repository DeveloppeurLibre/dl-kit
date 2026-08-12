# CONTEXTE — DL Kit

Fichier de référence pour le développement du produit.
À lire au début de toute session de travail sur ce repo.
Ne fait PAS partie du plugin distribué.

---

## Le produit

**Nom** : DL Kit
**Titre commercial** : Claude Code : la Méthode pour Finir une App (pas Juste la Commencer)
**Auteur** : Quentin Cornu — chaîne YouTube Développeur Libre

Un plugin Claude Code qui transforme l'agent en coach personnel. L'utilisateur
arrive avec une idée d'app ; le coach le questionne, calibre son niveau, et
l'accompagne phase par phase jusqu'à la publication.

**Promesse** : un coach personnel dans Claude Code qui t'accompagne de ton idée
jusqu'à ton app publiée.

**Différenciateur** : les arbitrages réels de Quentin (développeur iOS, 10 ans
d'expérience) sont encodés dans les fichiers. Ce n'est pas un kit générique de
prompts — c'est une méthode qui pilote l'agent.

## La cible

Des particuliers semi-techniques :
- Ont déjà bricolé avec Claude Code, Cursor ou ChatGPT
- Ont quelques notions techniques ou une vraie curiosité
- N'ont jamais terminé ce qu'ils ont commencé, faute de méthode

Reconversion, side-project, freelances, petits entrepreneurs. B2C, pas B2B.

**Phrase d'accroche qui les identifie** :
« Tu as déjà commencé une app avec l'IA. Tu ne l'as jamais finie. »

## La limite assumée

Le kit s'arrête à l'app publiée et fonctionnelle. Trouver des utilisateurs,
monétiser, faire vivre le produit : hors périmètre.

Cette limite est annoncée dès la phase 0 et rappelée à la clôture. Elle est
volontaire : elle ouvre la porte à une offre suivante (~300 €).

## Modèle économique

- Bêta : gratuit, en échange de retours
- Ensuite : 69 € (49 € en lancement) — modèle de distribution payante non
  encore tranché, car un dépôt de marketplace GitHub est public
- Offre suivante prévue : ~300 €, via masterclass, sur la partie traction

---

## Architecture technique

### Distribution : plugin Claude Code

```
dl-kit/
├── .claude-plugin/
│   └── plugin.json          ← SEULE chose dans ce dossier
├── skills/
│   └── coach/
│       ├── SKILL.md         ← point d'entrée du coach
│       ├── phases/
│       │   ├── 00-onboarding.md
│       │   ├── 01-challenge-idee.md
│       │   ├── 02-features.md
│       │   ├── 03-stack.md
│       │   ├── 04-architecture.md
│       │   ├── 05-setup.md
│       │   ├── 06-construction.md
│       │   ├── 07-verification.md
│       │   └── 08-publication.md
│       ├── quentin/
│       │   ├── principes.md
│       │   ├── pieges.md
│       │   ├── securite.md
│       │   ├── stack-ios.md
│       │   └── stack-web.md
│       └── templates/
│           ├── CLAUDE-md-ios.md
│           ├── CLAUDE-md-web.md
│           └── PRD.md
├── CONTEXTE.md              ← ce fichier, non distribué
└── README.md
```

⚠️ Erreur la plus fréquente : mettre `skills/`, `agents/` ou `hooks/` dans
`.claude-plugin/`. Le plugin se charge alors sans erreur mais ne fait rien.

### Où vivent les fichiers de l'utilisateur

Le plugin porte le SAVOIR (phases, principes, templates) : versionné, mis à jour.
Le dossier de travail de l'utilisateur porte l'ÉTAT :

```
son-projet/
├── projet/
│   ├── progression.md
│   ├── profil.md
│   ├── idee.md
│   ├── features.md
│   ├── stack.md
│   ├── architecture.md
│   └── verification.md
├── CLAUDE.md                ← celui de SON app, < 80 lignes
└── [le code de l'app]
```

L'utilisateur lance Claude Code dans son propre dossier de projet. Le coach est
disponible parce que le plugin est installé au scope utilisateur.

⚠️ Historique : une version antérieure imbriquait le projet dans le kit
(`dl-kit/projet/app/`). ABANDONNÉ avec le passage au plugin. Si une instruction
mentionne encore `projet/app/`, un changement de dossier, ou un `base directory`
Netlify lié à l'imbrication : c'est périmé, à supprimer.

---

## Règles de conception non négociables

### 1. Chargement progressif
Le `SKILL.md` reste court (règles + table des phases). Les fichiers de phases
ne sont lus qu'au moment où on y arrive. Ne JAMAIS relire une phase terminée.

C'est la règle la plus importante : un contexte saturé dégrade la qualité de
toutes les réponses. Le produit enseigne ce principe — il doit l'appliquer.

### 2. Une phase = un livrable écrit
On ne passe pas à la phase suivante sans que le fichier de `projet/` soit écrit.
C'est ce qui rend la reprise de session possible.

### 3. Une question à la fois
Le coach questionne, il n'enchaîne pas les questions groupées.

### 4. Le niveau pilote le ton
`projet/profil.md` est lu avant chaque réponse. Trois niveaux : débutant
(expliquer chaque commande), intermédiaire (expliquer les décisions), avancé
(aller droit au but).

### 5. Verrouillage par l'absence de fichier
Si `projet/profil.md` n'existe pas → phase 0 obligatoire, même si l'utilisateur
demande directement de coder.

### 6. Reprise de session
`progression.md` est mis à jour en continu, à chaque étape — pas à la fin de
session. L'utilisateur peut fermer son ordinateur à tout moment sans prévenir.

### 7. Le coach ne flatte pas
Ton direct, sans complaisance. Si une idée ou un choix pose problème, le dire
et expliquer pourquoi. Jamais de validation par politesse.

---

## Les arbitrages encodés (contenu de `quentin/`)

Ce dossier est le cœur du produit — la seule partie qu'un concurrent ne peut
pas copier. Il doit être écrit à la main, jamais généré.

- **Web app par défaut.** Natif seulement si notifications push, capteurs, ou
  vente App Store indispensables dès la v1.
- **Une seule fonctionnalité cœur en v1.** Trois maximum.
- **Pas d'authentification en v1** si l'app est mono-utilisateur.
- **Jamais d'API non officielle**, même si elle fonctionne. Vérifier les
  sources de données AVANT de coder.
- **CLAUDE.md du projet : moins de 80 lignes, jamais généré par `/init`.**
  Un fichier généré est trop verbeux et dégrade tous les prompts suivants.
- **Aucune règle de style dans un CLAUDE.md** : linter et hooks à la place.
- **Supabase** : publishable key OK côté client SI la RLS est activée. Secret
  key et connection string : jamais. Une publishable key sans RLS est une
  faille, pas une protection.
- **Construire dans l'ordre de valeur**, pas dans l'ordre du parcours
  utilisateur. L'écran d'accueil se construit en dernier.
- **Reporter une feature n'est pas un échec.** Un projet fini à 3 features vaut
  mieux qu'un projet abandonné à 5.

---

## État d'avancement

### Écrit
- Phases 00 à 08 (contenu rédigé)
- `quentin/pieges.md` (10 pièges du choix de projet)
- `quentin/securite.md` (référence sécurité pour le coach)

### À écrire
- `SKILL.md` (adaptation du CLAUDE.md coach, avec frontmatter)
- `quentin/principes.md`
- `quentin/stack-ios.md` et `quentin/stack-web.md`
- Les templates
- `plugin.json` et `marketplace.json`
- `README.md` (installation, mise à jour, prérequis)

### À corriger dans les fichiers existants
- **Chevauchement phases 4 et 5** : les étapes 4.2 (structure des dossiers) et
  4.5 (Git, filet de sécurité) sont des actions de setup. Elles doivent passer
  en phase 5. La phase 4 ne produit que des décisions sur papier.
- **Références à `projet/app/`** et aux changements de dossier : périmées,
  à supprimer partout.
- **Instruction d'initialisation via `/init`** : contraire aux principes,
  à supprimer si elle traîne encore.

---

## Points d'attention pour la suite

- **Cohérence croisée** : une règle modifiée doit être cherchée dans TOUS les
  fichiers, pas seulement celui qu'on édite. Les incohérences entre fichiers
  produisent des comportements erratiques difficiles à diagnostiquer.
- **Coût en contexte** : `/plugin` affiche aux utilisateurs le coût en tokens
  du plugin. Garder `SKILL.md` court est visible commercialement.
- **Mises à jour** : l'auto-update est désactivé par défaut pour les
  marketplaces tierces. À documenter dans le README.
- **Doc Claude Code volatile** : les specs de plugins évoluent vite. Vérifier
  sur code.claude.com avant de figer `plugin.json` ou `marketplace.json`.
- **Tester avec 3 personas** : un débutant sous Windows visant iOS (test du
  garde-fou), un intermédiaire avec une idée saine, un résistant qui refuse
  tous les recadrages.