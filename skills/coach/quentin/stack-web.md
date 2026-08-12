# Stack web — référence pour le coach

Fichier destiné à toi, l'agent. Sert en phase 3 (annoncer la stack) et
en phase 4 (caveats du CLAUDE.md du projet). Pas un cours à donner tel
quel — tu en extrais ce qui sert au moment où ça sert.

---

## La stack par défaut

- Interface : **Next.js** (React)
- Style : **Tailwind CSS**
- Hébergement : **Netlify**
- Données : locales par défaut, **Supabase** si accès multi-appareils
  (voir critère de l'étape 2.5/3.3)

**Pourquoi ce choix, pas un autre** : c'est la stack la mieux représentée
dans les données d'entraînement des modèles actuels. Moins d'hallucination
d'API, moins de blocages sur des erreurs obscures. Ce n'est pas un choix
d'élégance technique, c'est un choix de probabilité de réussite pour
quelqu'un qui code avec l'IA.

Ne t'écarte de ce défaut que si une contrainte réelle de `features.md`
l'exige (ex : besoin explicite d'un rendu temps réel complexe). Ne
propose jamais une alternative « plus moderne » sans raison concrète.

---

## Pièges de génération de code sur cette stack

### Variables d'environnement côté client vs serveur

**Détection** : une clé ou une variable d'env est utilisée dans un
composant qui s'exécute dans le navigateur.
**Pourquoi ça bloque** : dans Next.js, seules les variables préfixées
`NEXT_PUBLIC_` sont envoyées au navigateur. Une variable sans ce préfixe
utilisée côté client vaut `undefined` en production — souvent invisible
en développement local, ça casse au déploiement.
**Comment gérer** : vérifie systématiquement le préfixe selon l'usage.
Rappelle le point de sécurité : `NEXT_PUBLIC_` rend la valeur publique,
donc jamais un secret derrière ce préfixe (voir `securite.md`).

### Confusion Server Components / Client Components

**Détection** : erreur mentionnant les hooks React (`useState`,
`useEffect`) dans un composant qui n'a pas `"use client"` en haut du
fichier, ou l'inverse — une API serveur utilisée dans un composant
client.
**Pourquoi ça bloque** : App Router traite tout composant comme un
Server Component par défaut. Une bibliothèque IA qui génère du code
« React classique » oublie souvent cette directive.
**Comment gérer** : si le composant a de l'interactivité (état, effets,
événements), il a besoin de `"use client"`. Sinon, laisse-le côté
serveur — c'est plus rapide et ça évite d'exposer du code inutilement.

### Server Actions vs routes API

**Détection** : hésitation ou mélange entre les deux approches pour une
même fonctionnalité de mutation de données (formulaire, écriture DB).
**Pourquoi ça bloque** : les deux fonctionnent, mais mélanger les
approches dans un petit projet complique la lecture pour rien.
**Comment gérer** : par défaut, Server Actions pour les mutations
simples liées à un formulaire. Route API seulement si un service
externe doit appeler ce endpoint (webhook).

### Erreurs d'hydratation

**Détection** : erreur console mentionnant « hydration failed » ou un
contenu qui clignote au chargement de la page.
**Pourquoi ça bloque** : le rendu serveur et le rendu client ne
correspondent pas — souvent une valeur non déterministe (date, nombre
aléatoire, accès à `window`) utilisée pendant le rendu serveur.
**Comment gérer** : déplace ce genre de valeur dans un `useEffect` côté
client, pas dans le corps du composant.

### Dépendances inventées ou mal choisies

Rappel du principe général (`securite.md`, section dépendances) : vérifie
qu'un paquet proposé existe vraiment avant de l'installer. Sur cette
stack, l'écosystème npm est immense — c'est justement là que les noms de
paquets approximatifs ou inventés sont les plus fréquents.

---

## Déploiement Netlify

- Les variables d'environnement de production se configurent dans
  l'interface Netlify, jamais dans un fichier commité. Rappelle ce point
  au premier déploiement.
- Un build qui réussit en local peut échouer sur Netlify si une variable
  d'env manque côté hébergeur — c'est l'erreur de déploiement la plus
  fréquente sur cette stack. Vérifie les logs de build avant de chercher
  ailleurs.
- Le plan gratuit suffit largement pour une v1 (bande passante et minutes
  de build très au-dessus du besoin d'un side-project). Ne pas
  sur-anticiper une limite qui ne sera pas atteinte.

## Supabase côté web

- Le client Supabase s'initialise avec l'URL du projet et la
  **publishable key** — les deux sont publiques, elles vont dans
  `NEXT_PUBLIC_*`.
- Avant de considérer une table « prête », vérifie la RLS (voir
  `securite.md`, section 2). Ce rappel doit être systématique, pas
  seulement à la demande.
- Plan gratuit Supabase : suffisant pour une v1, y compris avec un usage
  réel modéré. Ne pas annoncer de coût tant que ce seuil n'est pas
  concrètement en vue.
