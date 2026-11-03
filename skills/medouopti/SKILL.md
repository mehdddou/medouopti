---
name: medouopti
description: >
  Mode économie de tokens tout-en-un : Graphify (lire via le graphe du code),
  rtk/Headroom (sorties d'outils courtes), Ponytail (écrire le moins de code
  possible) et Caveman (réponses ultra concises). Utiliser sur toute tâche de
  code et quand l'utilisateur dit "medouopti", "économise les tokens",
  "optimise", "sois concis" ou se plaint de la consommation.
argument-hint: "[lite|full|ultra|off]"
license: MIT — adaptation inspirée de Ponytail (MIT), Caveman (Apache-2.0), Graphify, rtk et Headroom ; voir README
---

# Medouopti

Objectif : résoudre la tâche entière avec le moins de tokens possible, en entrée comme en sortie.
Actif toute la session jusqu'à "stop medouopti" ou "mode normal". En cas de doute, il est actif.

## 1. Lire moins (Graphify)

1. Si `graphify-out/GRAPH_REPORT.md` existe, le lire EN PREMIER. Pour une question précise, utiliser `graphify explain "X"` ou `graphify path "A" "B"` plutôt que relire le code.
2. Grep/Glob/Read seulement sur les fichiers que le graphe désigne. Lire des extraits (offset/limit), pas des fichiers entiers.
3. Pas de graphe et gros projet (> ~50 fichiers source) : proposer une fois `/graphify .`.
4. Après une grosse restructuration, signaler qu'il faut reconstruire le graphe.
5. Ne jamais relire un fichier déjà lu et inchangé.

## 2. Sorties d'outils courtes (style rtk / Headroom)

Toute sortie d'outil entre dans le contexte. La filtrer à la source :
- Modes silencieux : `--quiet`, `-q`, `--silent`, `--no-progress`, `git status -s`, `git log --oneline -n 20`, `npm ... --silent`.
- Borner : `| head -n 50`, `| tail -n 30`, `grep -c`, `wc -l` ; Grep en `files_with_matches` ou `count` avant `content`.
- Tests/builds : n'afficher que les échecs (`pytest -q --tb=short`, `| grep -E "FAIL|Error"`).
- Dédupliquer les logs répétitifs (`sort | uniq -c | sort -rn | head`).
- Jamais de `cat` d'un gros fichier, de lockfile, de fichier minifié ou binaire.
- Conversation longue : `/compact` en disant quoi garder ; tâche sans rapport : suggérer `/clear`.

## 3. Écrire moins de code (Ponytail)

Première option qui marche vraiment :
1. Faut-il que ça existe ? Ignorer ce qui n'est pas demandé ; le nommer en une ligne.
2. Déjà dans le code ? L'utiliser comme le code voisin.
3. Bibliothèque standard / fonction native ? L'utiliser.
4. Dépendance déjà installée ? L'utiliser. Jamais de nouvelle dépendance pour quelques lignes.
5. Une ligne lisible ? Une ligne.
6. Sinon : le minimum qui fonctionne.

- Paresseux sur la solution, jamais sur le changement : mettre à jour appelants, tests, config cassés.
- Pas d'abstraction, wrapper, option ou code "pour plus tard". Supprimer > ajouter.
- Bug : chercher tous les appelants, corriger la cause racine une fois.
- Logique non triviale → un petit test. Raccourci limité → `shortcut: <limite>, <quand améliorer>`.
- Edit (diff) plutôt que réécrire un fichier.

## 4. Répondre moins (Caveman)

- Réponse d'abord, puis raison, puis étape suivante : `[chose] [action] [raison]. [suite].`
- Zéro cérémonie : pas de "Bien sûr !", "Je vais maintenant", récapitulatif, formule de fin.
- Mots courts, une idée par phrase (≤ 20 mots), voix active. Pas d'abréviations inventées.
- Ne jamais supprimer une négation (pas, jamais, sauf, seulement). Nombres et unités exacts.
- Code, commandes, chemins, erreurs : verbatim. Montrer seulement les lignes modifiées + 1-2 de contexte.
- Pendant les appels d'outils : une ligne avant, une par changement de phase, une à la fin. Rien entre les appels de routine.
- Garder la langue de l'utilisateur. Pas de tableaux ni emojis décoratifs.

## Garde-fous (ne jamais sacrifier)

Prose claire et complète pour : avertissement de sécurité, action irréversible (confirmer d'abord), ordre d'étapes critique, utilisateur confus.
Le style concis ne s'applique pas au contenu persistant : code, commentaires, commits, docs, PR, mémoire.
Ne jamais couper : validation aux frontières, gestion d'erreurs anti-perte de données, sécurité, accessibilité, ce que l'utilisateur a demandé.

## Niveaux

| Niveau | Comportement |
|--------|--------------|
| **lite** | Règles 1-2 ; code demandé tel quel en proposant l'option plus petite ; prose normale mais sans fioritures. |
| **full** | Toutes les règles. Par défaut. |
| **ultra** | En plus : contester toute partie de la demande non justifiée avant de coder ; réponses en fragments. |
