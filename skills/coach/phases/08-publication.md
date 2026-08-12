# Phase 8 — Publier

Objectif : mettre l'app en ligne, accessible par une autre personne
que son créateur.
Livrable : une URL ou une app publiée + `projet/publication.md`.

## Règles pour cette phase

- Lis `projet/stack.md`, `projet/profil.md`, `projet/verification.md`.
- ⚠️ NE RELIS PAS les fichiers des phases 0 à 6.
- Ne publie pas si la phase 7 n'est pas terminée, en particulier le
  contrôle de sécurité.
- Suis UNIQUEMENT la section correspondant à la plateforme choisie.
  Ne lis pas les autres.
- Sois honnête sur les délais. Ne laisse pas croire qu'une publication
  App Store est instantanée.

## Message d'ouverture

« Dernière étape. Publier, c'est ce qui transforme un projet perso en
quelque chose de réel : une adresse que tu peux envoyer à quelqu'un.
C'est aussi l'étape où beaucoup de gens s'arrêtent, souvent à cause
d'un détail administratif. On y va tranquillement. »

---

# A — PUBLIER UNE WEB APP

C'est le chemin le plus court : pas de validation externe, pas de
frais, publication en quelques minutes.

## A.1 — Vérifier que la version de production fonctionne

⚠️ Point critique et souvent ignoré : une app qui tourne en
développement peut échouer en production. C'est la cause n°1 des
échecs de publication.

Lance la commande de build depuis la racine du projet et vérifie
qu'elle se termine sans erreur.

Si le build échoue :
- Lis le message d'erreur en entier avant d'agir
- Les causes fréquentes : une variable d'environnement manquante, un
  fichier importé qui n'existe pas, une erreur de type ignorée en
  développement
- Corrige, puis relance le build. Ne publie jamais avec un build cassé.

## A.2 — Créer le dépôt de code

Si Git n'est pas encore initialisé (niveau débutant), c'est le moment.

- Initialise le dépôt à la racine du projet
- ⚠️ Vérifie le `.gitignore` AVANT le premier envoi : les fichiers de
  configuration contenant des secrets ne doivent pas partir
- Crée le dépôt distant et envoie le code

⚠️ Si un secret part par erreur dans un dépôt public : le retirer ne
suffit pas, il reste dans l'historique. Il faut le régénérer.
Préviens avant, pas après.

## A.3 — Déployer sur Netlify

Connecte le dépôt à Netlify.

Renseigne, si nécessaire :
- La commande de build
- Le dossier de publication
- Les variables d'environnement (les mêmes qu'en local)

## A.4 — Vérifier en ligne

Une fois l'URL générée :
- Ouvre-la sur l'ordinateur
- Ouvre-la sur un téléphone
- Refais passer les critères de validation de `features.md` sur la
  version en ligne

⚠️ Une app peut marcher en local et être cassée en ligne, le plus
souvent à cause d'une variable d'environnement absente. Ne considère
pas la publication faite tant que l'URL n'a pas été testée pour de
vrai.

## A.5 — Partager

« Envoie l'adresse à la personne qui avait testé ton app en phase 7. »

C'est le vrai moment de fin : quelqu'un d'autre utilise l'app depuis
son propre appareil.

---

# B — PUBLIER SUR L'APP STORE (iOS)

⚠️ AVERTISSEMENT À DONNER DÈS LE DÉBUT DE CETTE SECTION :

« Publier sur l'App Store n'est pas instantané. Il faut un compte
développeur payant (environ 99 $/an), et la validation par Apple prend
du temps — cela peut aller de quelques jours à plusieurs semaines, et
les refus sont fréquents pour des raisons administratives.

Si tu veux que ton app soit accessible rapidement, on peut aussi la
laisser accessible en test sans passer par la validation publique.
Tu veux qu'on prenne cette voie d'abord ? »

Laisse l'utilisateur décider en connaissance de cause.

## B.1 — Le compte développeur

- Compte Apple Developer payant requis pour toute publication
- Compte gratuit : suffisant pour tester sur son propre appareil,
  insuffisant pour publier
- L'inscription peut prendre 24 à 48 h à être validée

Si l'utilisateur n'a pas de compte : ne le laisse pas payer sans
avoir compris. Repropose la voie web une dernière fois.

## B.2 — Préparer l'app

- Nom de l'app (celui qui sera visible)
- Icône de l'app, dans toutes les tailles requises
- Numéro de version
- Identifiant unique (bundle identifier)

Sur l'icône : c'est le point qui bloque le plus souvent les débutants.
Génère les tailles nécessaires plutôt que de laisser l'utilisateur les
créer une par une à la main.

## B.3 — La fiche App Store

À préparer avant l'envoi :
- Description de l'app
- Captures d'écran aux formats demandés
- Catégorie
- Politique de confidentialité (⚠️ obligatoire, même pour une app
  simple, même sans collecte de données)
- Déclaration sur la collecte de données

La politique de confidentialité est un motif de refus très fréquent.
Aide l'utilisateur à en produire une adaptée à son app — et si son
app ne collecte rien, dis-le explicitement dedans.

## B.4 — Envoyer

- Archive depuis Xcode
- Envoi vers App Store Connect
- Test interne avant soumission publique

⚠️ Après l'envoi, dis clairement : « À partir de maintenant, ce n'est
plus entre tes mains. Apple examine ton app. Ça peut prendre du temps.
Un refus n'est pas un échec : c'est très courant, souvent pour un
détail de fiche, et ça se corrige. »

## B.5 — En cas de refus

Motifs de refus les plus fréquents pour une première app :
- Politique de confidentialité absente ou incomplète
- Description ne correspondant pas à l'app
- App jugée trop simple ou sans intérêt propre
- Captures d'écran non conformes

Ne dramatise pas. Lis le motif exact, corrige, renvoie.

---

# C — PUBLIER SUR GOOGLE PLAY (ANDROID)

## C.1 — Le compte développeur

- Compte Google Play Console : environ 25 $, paiement unique
- La validation du compte peut prendre plusieurs jours
- Google impose des exigences de test pour les nouveaux comptes avant
  publication publique — vérifie les conditions en vigueur au moment
  de la publication, elles évoluent

## C.2 — Préparer et envoyer

- Icône et captures d'écran
- Description
- Politique de confidentialité (obligatoire)
- Déclaration sur la collecte de données
- Génération du fichier de publication signé

⚠️ La clé de signature doit être conservée précieusement. Sans elle,
il devient impossible de publier des mises à jour de l'app.
Dis-le explicitement et fais sauvegarder la clé avant de continuer.

---

## Écriture du livrable

Crée `projet/publication.md` :

```markdown
# Publication

Date : [date]
Plateforme : [web / iOS / Android]

## Accès
- URL / lien : [...]
- Statut : [en ligne / en attente de validation / refusé]

## Configuration
- Dépôt : [...]
- Répertoire de base : [...]
- Variables d'environnement : [renseignées / sans objet]

## Vérification post-publication
- Testé sur ordinateur : ✅
- Testé sur mobile : ✅
- Critères de validation repassés en ligne : ✅

## Coûts engagés
- [poste] : [montant]

## Notes
[Ex : refusé une fois pour politique de confidentialité manquante]
```

---

## CLÔTURE DU PARCOURS

Une fois l'app publiée, fais le bilan avec l'utilisateur.

Reprends `projet/progression.md` et rappelle le chemin parcouru :
l'idée de départ, ce qui a été recadré, les features construites,
ce qui a été reporté, le temps écoulé.

Puis dis ceci, sans le déguiser :

« Ton app est en ligne. C'est la partie que la plupart des gens ne
finissent jamais.

Maintenant, sois lucide sur une chose : construire est devenu la
partie facile. L'IA t'a permis de faire en quelques semaines ce qui
prenait des mois. Mais avoir des utilisateurs, comprendre ce qu'ils
veulent vraiment, faire vivre le produit et éventuellement le
monétiser — ça, l'IA ne le fait pas à ta place. C'est un travail
différent, qui n'a rien à voir avec le code.

Ce parcours s'arrête ici, comme annoncé au départ : tu as une app qui
marche et qui est publiée. La suite est un autre métier. »

Ne vends rien de plus à cet endroit. Reste factuel.

## Prochaines étapes concrètes à proposer

- Faire utiliser l'app par 5 personnes et écouter leurs retours
- Ne rien ajouter avant d'avoir écouté ces retours
- Reprendre la liste « Idées pour plus tard » de `features.md`
  seulement après, et la retrier selon ce qui a été entendu

⚠️ Insiste sur le deuxième point. Le réflexe naturel après publication
est d'ajouter des fonctionnalités. Le bon réflexe est d'écouter
d'abord.