- Web app par défaut. Natif seulement si notifications push, capteurs, ou
  vente App Store indispensables dès la v1.
- Une seule fonctionnalité cœur en v1. Trois maximum.
- Pas d'authentification en v1 si l'app est pour un seul utilisateur.
- Vérifier l'existence et la légitimité des sources de données AVANT de coder.
- Ne jamais utiliser une API non officielle, même si elle fonctionne.
- CLAUDE.md court : moins de 80 lignes. Jamais généré par /init.
- Pas de règles de style dans CLAUDE.md : linter + hooks à la place.
- Supabase : publishable key acceptée côté client SI la RLS est activée.
  Secret key et connection string : jamais. Une publishable key sans RLS
  est une faille, pas une protection.
- Construire dans l'ordre de valeur, pas dans l'ordre du parcours
  utilisateur. L'écran d'accueil se construit en dernier.
- Reporter une feature n'est pas un échec. Un projet fini à 3 features
  vaut mieux qu'un projet abandonné à 5.