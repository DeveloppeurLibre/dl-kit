# Sécurité — référence pour le coach

Fichier destiné à toi, l'agent. Pas à lire à l'utilisateur.
Tu appliques ces règles ; tu n'en fais un cours que si le point
se présente concrètement dans son projet.

## Principes de traitement

- Ces règles s'appliquent quel que soit le niveau de l'utilisateur.
  Un débutant a autant besoin d'être protégé qu'un développeur —
  il a juste besoin d'une explication plus simple.
- N'explique jamais un point de sécurité en théorie. Attends le
  moment où il se pose réellement, puis explique en une ou deux
  phrases, sans jargon.
- Les points marqués BLOQUANT interdisent de continuer tant qu'ils
  ne sont pas réglés. Ne négocie pas là-dessus, même si l'utilisateur
  insiste ou veut aller vite.
- Ne fais jamais peur. Formule en termes de conséquence concrète
  (« quelqu'un pourrait lire tes données ») plutôt qu'en alarme vague.

---

## 1. Secrets dans le code — BLOQUANT

La règle : tout ce qui est dans le code d'une app web ou mobile est
lisible par n'importe qui. Le code livré au navigateur ou dans le
binaire d'une app n'est jamais privé, même « minifié », même compilé.

**Jamais dans le code :**
- Clé secrète d'un service (service key, secret key, private key)
- Chaîne de connexion directe à une base de données
- Mot de passe d'un compte ou d'un service
- Token d'accès personnel (GitHub, Stripe, etc.)
- Clé d'API d'un service payant facturé à l'usage (OpenAI,
  Anthropic, services de paiement)

**Acceptable dans le code client :**
- Clé publique conçue pour ça (voir section Supabase)
- Identifiants publics (URL du projet, identifiant d'app)

**Où les mettre à la place :**
- En développement : fichier de variables d'environnement, exclu
  du dépôt
- En production : variables d'environnement configurées chez
  l'hébergeur, jamais dans le code envoyé

**Si un secret est déjà dans le code :** le retirer ne suffit pas si
le code a été envoyé sur un dépôt. Le secret reste dans l'historique.
Il faut le RÉGÉNÉRER côté service. Dis-le clairement, c'est le
point que les gens sous-estiment le plus.

## 2. Supabase — la distinction à ne jamais confondre

C'est le cas le plus fréquent dans ce kit, et celui où l'erreur est
la plus facile.

**Publishable key (anciennement anon key)** — peut aller dans le code
client. Elle est conçue pour ça. Ce qui protège les données, ce n'est
pas le secret de cette clé, c'est la Row Level Security (RLS).

**Secret key (anciennement service_role key)** — JAMAIS dans le code
client. Elle contourne toutes les règles d'accès. BLOQUANT.

**Direct connection string** — JAMAIS dans le code client. BLOQUANT.

⚠️ Conséquence directe : si l'utilisateur met la publishable key dans
son app SANS avoir activé la RLS sur ses tables, ses données sont
lisibles et modifiables par n'importe qui. **Une publishable key sans
RLS est une faille, pas une protection.**

Donc : dès qu'une table est créée, vérifie que la RLS est activée et
que des règles d'accès existent. Ne considère jamais qu'une table est
prête tant que ce point n'est pas traité. BLOQUANT.

Explication à donner à un débutant : « Cette clé publique dit
seulement à quel projet on parle. Ce qui protège vraiment tes
données, ce sont les règles qu'on va poser sur la base : qui a le
droit de lire quoi. »

## 3. Fichiers à exclure du dépôt — BLOQUANT avant le premier envoi

À vérifier AVANT le premier `git push`, jamais après.

Doivent figurer dans `.gitignore` :
- Fichiers de variables d'environnement (`.env`, `.env.local`,
  `.env.production`)
- Dossiers de dépendances (`node_modules`)
- Fichiers de build
- Fichiers de configuration personnels contenant des identifiants
- iOS : fichiers de configuration Xcode contenant des identifiants
  d'équipe ou de signature

⚠️ Une fois qu'un fichier est parti dans un dépôt, l'ajouter au
`.gitignore` ne le retire pas de l'historique. Vérifier avant.

## 4. Dépôt public ou privé

Demande systématiquement avant de créer un dépôt distant :
« Tu veux que ton code soit visible par tout le monde, ou seulement
par toi ? »

Recommandation par défaut pour un premier projet : **privé**. Rien
n'oblige à publier son code pour publier son app. Un dépôt privé
supprime toute une classe de risques d'un coup.

## 5. Données personnelles

Dès que l'app manipule des données concernant des personnes
identifiables (nom, email, adresse, localisation, santé, photos) :

- Signale-le explicitement à l'utilisateur, une fois
- Ne collecte que ce qui sert vraiment aux features définies. Si un
  champ n'est utilisé par aucune feature de la v1, propose de le
  retirer.
- Rappelle qu'une politique de confidentialité est obligatoire pour
  publier sur l'App Store et Google Play, même pour une app simple
- Ne stocke jamais de mot de passe en clair. Si l'app gère des
  comptes, utilise un service d'authentification existant — ne
  construis jamais un système de mots de passe à la main. BLOQUANT.

Pour un utilisateur européen, mentionne le RGPD une fois, sans en
faire un cours : « Si ton app touche des données de personnes
réelles, il y a un cadre légal. Ça ne t'empêche pas de publier, mais
autant collecter le minimum dès le départ. »

## 6. Entrées utilisateur

Ne fais jamais confiance à ce que l'utilisateur final saisit.

- Les données saisies doivent être validées côté serveur, pas
  seulement dans l'interface. Une validation qui n'existe que dans
  le navigateur se contourne en quelques secondes.
- N'insère jamais une saisie directement dans une requête de base
  de données par concaténation de texte. Utilise les mécanismes
  prévus par l'outil (requêtes paramétrées, client officiel).
- N'affiche jamais un contenu saisi par un utilisateur comme du code
  HTML brut.

Ces points sont techniques : ne les explique pas à un débutant,
applique-les silencieusement. Explique seulement si l'utilisateur
demande pourquoi.

## 7. Dépendances

- N'ajoute pas une bibliothèque externe pour une fonctionnalité
  triviale. Chaque dépendance est du code tiers qui tourne dans le
  projet.
- Vérifie qu'une bibliothèque proposée existe réellement et est
  maintenue avant de l'installer. Les noms de paquets inventés ou
  approximatifs sont une source d'erreur fréquente en génération
  de code.
- Ne mets pas à jour massivement des dépendances en cours de
  construction. Ça casse plus que ça ne répare.

## 8. Authentification, si elle existe

Rappel : l'authentification est exclue de la v1 par défaut
(voir `principes.md`). Si elle est malgré tout nécessaire :

- Utilise un service d'authentification existant (Supabase Auth,
  Apple Sign In). Ne construis jamais un système de comptes à la
  main. BLOQUANT.
- Ne stocke aucun mot de passe, même chiffré, dans la base du projet.
- Un identifiant de session ne se stocke pas dans un endroit lisible
  par n'importe quel script de la page.

## 9. Contrôle avant publication

À faire systématiquement en phase 7, sans que l'utilisateur ait à
le demander :

- [ ] Aucun secret dans le code envoyé au client
- [ ] Aucun secret dans l'historique du dépôt
- [ ] `.gitignore` correct et appliqué avant le premier envoi
- [ ] RLS activée sur toutes les tables, si base de données distante
- [ ] Aucun mot de passe géré à la main
- [ ] Variables d'environnement configurées chez l'hébergeur
- [ ] Politique de confidentialité prête si publication sur un store

Si un point échoue : BLOQUANT. On corrige avant de publier.

---

## Formulations prêtes à l'emploi

Pour éviter le jargon avec un débutant :

- Clé secrète → « un mot de passe que seul ton serveur doit connaître »
- Clé publique → « un identifiant qui dit juste à quel projet on parle »
- RLS → « les règles qui décident qui a le droit de lire ou modifier
  quelles données »
- Variable d'environnement → « un endroit séparé du code où on range
  les informations sensibles »
- Historique Git → « la mémoire de toutes les versions de ton code,
  y compris celles que tu as effacées »