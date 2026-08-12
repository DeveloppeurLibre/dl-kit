# Phase 0 — Onboarding

Objectif : calibrer ton accompagnement sur la personne réelle.
Livrable : `projet/profil.md`

## Règles pour cette phase
- UNE question à la fois. Attends la réponse avant la suivante.
- Ne juge jamais une réponse ("c'est peu", "tu devrais savoir ça").
- Reformule les réponses techniques en langage simple pour confirmer.
- Durée cible : 5 minutes. Ne rallonge pas.

## Message d'accueil

« Avant de commencer, quelques questions rapides pour que je m'adapte à toi.
Ça prend 2 minutes et ça change tout pour la suite. »

---

## Q1 — Expérience du code
« Est-ce que tu as déjà écrit du code toi-même ?
a) Jamais
b) Un peu (tutos, bidouille, cours en ligne)
c) Oui, régulièrement »

## Q2 — Terminal
« Est-ce que tu es à l'aise avec le terminal / la ligne de commande ?
a) Je ne sais pas ce que c'est
b) Je sais l'ouvrir et taper des commandes qu'on me donne
c) Oui, c'est mon quotidien »

## Q3 — Expérience de publication
« As-tu déjà publié une app ou un site en ligne ?
a) Jamais
b) Un site simple / une page
c) Oui, une vraie app en production »

## Q4 — Machine
« Tu travailles sur quel système ? Mac, Windows ou Linux ? »

⚠️ Si Windows ou Linux ET que la personne veut une app iOS : préviens
immédiatement qu'une app iOS ne peut pas être compilée ni publiée sans un Mac.
Ne la laisse pas découvrir ça en phase 5. Propose : web app (accessible
sur iPhone via le navigateur) ou Android.

## Q5 — Plateforme visée
« Où veux-tu que ton app soit accessible ?
a) Sur le web (navigateur, ordi + mobile)
b) Sur iPhone (App Store)
c) Sur Android (Play Store)
d) Je ne sais pas encore »

Si (d) ou hésitation : recommande le web par défaut
(voir `quentin/principes.md`). N'impose pas, explique le raisonnement.

Si (b) ou (c) : signale dès maintenant les coûts et délais réels —
compte développeur Apple ~99 $/an, compte Google Play ~25 $ une fois,
et un délai de validation qui peut prendre plusieurs jours à plusieurs
semaines. C'est mieux de le savoir maintenant qu'à la fin.

## Q6 — Temps disponible
« Combien de temps par semaine tu peux vraiment y consacrer ?
a) Moins de 3h
b) 3 à 8h
c) Plus de 8h »

Si (a) : préviens que le rythme sera plus lent, et que c'est OK —
mais qu'il faudra être encore plus strict sur le périmètre de la v1.

## Q7 — Contexte Claude Code
« Est-ce que Claude Code est déjà installé et fonctionnel chez toi ? »

Si non : accompagne l'installation avant d'aller plus loin.
Si oui : continue.

## Q8 — Objectif personnel
« Dernière question : c'est quoi ton objectif avec cette app ?
a) L'utiliser moi-même
b) Apprendre à construire quelque chose
c) La vendre / en faire un business »

Si (c) : dis clairement que ce parcours va jusqu'à une app publiée
et fonctionnelle, mais ne couvre pas la recherche de clients ni la
monétisation. Sois honnête sur cette limite dès maintenant.

---

## Calcul du niveau

- **Débutant** : Q1=a, ou (Q1=b ET Q2=a)
- **Intermédiaire** : Q1=b ET Q2≥b
- **Avancé** : Q1=c ET Q2=c

## Écriture du livrable

Crée `projet/profil.md` :

```markdown
# Profil

- Niveau : [débutant / intermédiaire / avancé]
- Code : [réponse Q1]
- Terminal : [réponse Q2]
- Publication : [réponse Q3]
- Machine : [Mac / Windows / Linux]
- Plateforme visée : [web / iOS / Android]
- Temps par semaine : [réponse Q6]
- Objectif : [réponse Q8]

## Consignes de communication
[Selon le niveau :]
- Débutant : expliquer chaque commande AVANT de la lancer. Aucun terme
  technique sans définition. Toujours proposer l'option la plus simple.
- Intermédiaire : expliquer les décisions, pas les commandes. Vocabulaire
  technique autorisé.
- Avancé : aller droit au but, proposer des alternatives, discuter
  les arbitrages.
```

Puis mets à jour `projet/progression.md` et annonce la phase 1.