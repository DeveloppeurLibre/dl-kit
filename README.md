# DL Kit

**Claude Code : la Méthode pour Finir une App (pas Juste la Commencer)**

> Tu as déjà commencé une app avec l'IA. Tu ne l'as jamais finie.

DL Kit transforme Claude Code en coach personnel : il te questionne,
calibre son niveau d'explication sur le tien, et t'accompagne phase par
phase — de l'idée à l'app publiée.

## Ce que le kit fait, et ce qu'il ne fait pas

Le coach t'accompagne jusqu'à une app **publiée et fonctionnelle**.
Trouver des utilisateurs, monétiser, faire vivre le produit ensuite :
hors périmètre, volontairement. C'est un autre métier, qui commence
une fois l'app en ligne.

## Prérequis

- [Claude Code](https://code.claude.com/docs/en/setup) installé et à
  jour — le système de plugins nécessite une version récente.
- Rien d'autre pour démarrer. Les outils spécifiques à ta stack
  (Node.js, Xcode, Android Studio...) sont vérifiés et installés avec
  toi pendant le parcours, en phase 3.

## Installation

Dans un terminal Claude Code :

```
/plugin marketplace add DeveloppeurLibre/dl-kit
/plugin install dl-kit@dl-kit
```

Si l'installation affiche « Run /reload-plugins to activate. », lance :

```
/reload-plugins
```

⚠️ Un plugin peut exécuter du code sur ta machine. N'installe que des
marketplaces en qui tu as confiance.

## Utilisation

Ouvre Claude Code dans le dossier où tu veux construire ton app (un
dossier vide convient) et dis simplement que tu veux construire une
application. Le coach démarre automatiquement, en phase 0.

Si tu reprends une session déjà commencée, dis-le : le coach relit
`projet/progression.md` et reprend là où vous en étiez.

## Mise à jour

Par défaut, une marketplace tierce (celle-ci comprise) ne se met **pas**
à jour toute seule — c'est le comportement standard de Claude Code, pas
une limite de ce kit.

Pour vérifier si une nouvelle version est disponible :

```
/plugin marketplace update dl-kit
```

Puis mets à jour le plugin depuis le panneau interactif : `/plugin` →
onglet **Installed** → sélectionne DL Kit → **Update**.

Si tu préfères des mises à jour automatiques : `/plugin` → onglet
**Marketplaces** → sélectionne `dl-kit` → **Enable auto-update**.

## Bêta

Ce kit est actuellement en bêta gratuite, en échange de retours. Un
bug, un blocage, une idée ? Ouvre une
[issue sur ce dépôt](https://github.com/DeveloppeurLibre/dl-kit/issues).

---

Fait par Quentin Cornu — chaîne YouTube Développeur Libre.
