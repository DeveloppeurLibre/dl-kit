# Phase 7 — Vérifier

Objectif : s'assurer que l'app tient debout quand ce n'est pas son
créateur qui l'utilise.
Livrable : `projet/verification.md` + les corrections bloquantes faites.

## Règles pour cette phase

- Lis `projet/features.md` et `projet/profil.md`.
- ⚠️ NE RELIS PAS les fichiers des phases 0 à 5.
- Cette phase n'ajoute AUCUNE fonctionnalité. On vérifie et on corrige,
  on ne construit pas.
- Ne corrige pas tout. On corrige ce qui bloque, on note le reste.
- Ne passe pas à la phase 8 tant que les points bloquants ne sont pas
  réglés.

## Message d'ouverture

« Ton app fait ce que tu voulais. Maintenant on vérifie qu'elle tient
quand ce n'est pas toi qui l'utilises. C'est là qu'on découvre 90 %
des problèmes : pas quand ça marche, mais quand quelqu'un clique là
où tu n'avais pas prévu. »

---

## Étape 7.1 — Repasser les critères de validation

Reprends chaque critère de `projet/features.md`, un par un, et fais-les
tester à nouveau par l'utilisateur.

Pourquoi les retester alors qu'ils ont déjà été validés : chaque
feature construite après a pu casser une feature précédente. C'est le
problème le plus fréquent et le plus invisible.

Format :
```
Feature 1 : est-ce que tu peux toujours [critère] ?
Feature 2 : est-ce que tu peux toujours [critère] ?
```

Note tout ce qui ne passe plus. Ces régressions sont prioritaires sur
tout le reste.

## Étape 7.2 — Les cas limites

Fais tester ces situations, une par une. Ce sont celles qui cassent
le plus souvent une app construite avec l'IA :

**L'app vide**
« Ouvre l'app comme si c'était la première fois, sans aucune donnée.
Qu'est-ce que tu vois ? »
Un écran blanc ou une erreur = problème bloquant. Il faut un message
qui explique quoi faire.

**La fermeture / réouverture**
« Ferme complètement l'app, rouvre-la. Tes données sont toujours là ? »
Si les données disparaissent, c'est bloquant.

**Les données bizarres**
« Essaie d'entrer : rien du tout, un texte très long, un nombre
négatif, des caractères spéciaux (é, ç, emoji). »
L'app ne doit pas planter. Elle peut refuser, mais pas casser.

**Le désordre**
« Clique dans un ordre inattendu : reviens en arrière au milieu d'une
action, appuie deux fois rapidement sur un bouton. »

**Le petit écran**
Web : réduire la fenêtre du navigateur à la taille d'un téléphone.
iOS : tester sur le plus petit simulateur disponible.
Le contenu doit rester lisible et utilisable.

Pour chaque test : ✅ passe / ⚠️ à améliorer / ❌ bloquant.

## Étape 7.3 — Le test par quelqu'un d'autre

⚠️ Étape obligatoire. Ne la présente pas comme optionnelle.

« Fais tester ton app à quelqu'un — un proche, un collègue, peu
importe. Ne lui explique RIEN. Regarde-le faire sans intervenir. »

Consignes à donner à l'utilisateur :
- Ne pas commenter, ne pas aider, ne pas justifier
- Noter chaque hésitation, chaque question posée
- Une hésitation = un problème d'interface, pas un problème
  d'utilisateur

Puis : « Qu'est-ce qu'il a compris tout seul ? Où est-ce qu'il a
hésité ? Qu'est-ce qu'il a essayé de faire que tu n'avais pas prévu ? »

C'est l'étape qui rapporte le plus d'informations de toute la phase.
Le créateur d'une app est structurellement incapable de la juger :
il sait où cliquer.

## Étape 7.4 — Trier les problèmes

Classe tout ce qui a été relevé en trois catégories :

**❌ Bloquant** — l'app plante, une feature ne marche plus, les données
se perdent, un utilisateur ne peut pas accomplir l'action principale.
→ À corriger maintenant.

**⚠️ Gênant** — c'est utilisable mais confus, moche, ou hésitant.
→ À noter. Corriger seulement si c'est rapide.

**💭 Amélioration** — une idée qui rendrait l'app meilleure.
→ Ne pas corriger. Noter dans « Idées pour plus tard » de
`features.md`.

⚠️ Le piège de cette phase : vouloir tout corriger. Une liste de 20
corrections avant publication, c'est une app jamais publiée. Sois
strict sur le tri, et dis-le à l'utilisateur.

## Étape 7.5 — Corriger les bloquants

Pour chaque problème bloquant, applique la même boucle qu'en phase 6 :

1. Point de sauvegarde
2. Correction ciblée, sans toucher au reste
3. L'utilisateur revérifie le critère de ses propres yeux
4. Point de sauvegarde après validation

⚠️ Après chaque correction, refais un passage rapide sur les critères
de validation des autres features. Une correction peut en casser une
autre.

## Étape 7.6 — Le contrôle de sécurité

Non négociable, quel que soit le niveau. Consulte
`quentin/securite.md`.

Vérifie et annonce le résultat de chaque point :

- [ ] Aucune clé secrète, mot de passe ou chaîne de connexion dans le
      code de l'app
- [ ] Si une base de données distante est utilisée : seule la clé
      publique est présente côté client, et les règles d'accès sont
      activées
- [ ] Les fichiers de configuration contenant des secrets sont exclus
      du dépôt (`.gitignore`)

⚠️ Si un secret est présent dans le code : c'est bloquant, on ne
publie pas. Explique pourquoi simplement (« n'importe qui pourra le
lire et s'en servir »), puis corrige. Si le secret a déjà été
publié quelque part, il doit être régénéré, pas seulement retiré.

## Étape 7.7 — Le dernier contrôle avant publication

Récapitule :
- [ ] Tous les critères de validation passent
- [ ] Aucun problème bloquant restant
- [ ] Le test par une personne extérieure a été fait
- [ ] Le contrôle de sécurité est passé
- [ ] L'app démarre proprement depuis zéro

Si tout est coché : « Ton app est prête à être publiée. »

---

## Écriture du livrable

Crée `projet/verification.md` :

```markdown
# Vérification

Date : [date]

## Critères de validation
- Feature 1 : ✅ / ❌
- Feature 2 : ✅ / ❌

## Cas limites
- App vide : ✅ / ⚠️ / ❌
- Fermeture / réouverture : ✅ / ⚠️ / ❌
- Données inhabituelles : ✅ / ⚠️ / ❌
- Ordre inattendu : ✅ / ⚠️ / ❌
- Petit écran : ✅ / ⚠️ / ❌

## Test utilisateur externe
Testeur : [qui]
- A compris seul : [...]
- A hésité sur : [...]
- A essayé de faire : [...]

## Corrections faites
- [problème] → [correction]

## Non corrigé (assumé)
- [problème] → reporté après publication

## Sécurité
- Secrets dans le code : aucun ✅
- Règles d'accès base de données : [activées / sans objet]
- Fichiers sensibles exclus du dépôt : ✅
```

Puis mets à jour `projet/progression.md` et annonce la phase 8 :
« On publie. »