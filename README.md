# medouopti

Skill Claude Code qui réduit la consommation de tokens en entrée comme en sortie.

| Étape | Inspiré de | Effet |
|---|---|---|
| Lire moins | Graphify | Consulter le graphe du code avant de lire des fichiers ; extraits ciblés |
| Sorties courtes | rtk, Headroom | Modes silencieux, sorties bornées, tests limités aux échecs |
| Écrire moins | Ponytail | Code minimal, réutiliser l'existant, pas d'abstraction inutile |
| Répondre moins | Caveman | Réponse d'abord, zéro politesse, code et erreurs verbatim |

Niveaux : `lite`, `full` (défaut), `ultra`. Arrêt : « stop medouopti ».

## Installation

```
/plugin marketplace add mehdddou/medouopti
/plugin install medouopti@medouopti
```

Puis `/medouopti` dans Claude Code.

Pour profiter pleinement de l'étape « Lire moins », installer Graphify : `pip install graphifyy && graphify install`, puis `/graphify .` dans le projet.

## Crédits

Ce skill est une adaptation en français, réécrite et condensée, des idées de :
- [Ponytail](https://github.com/DietrichGebert/ponytail) — Dietrich Gebert, licence MIT
- [Caveman](https://github.com/JuliusBrussee/caveman) — Julius Brussee, licence Apache-2.0
- [Graphify](https://github.com/Graphify-Labs/graphify)
- rtk et Headroom (principes de filtrage des sorties d'outils)

Aucun de ces projets n'est affilié à medouopti ni ne le cautionne.

## Licence

MIT — voir [LICENSE](LICENSE).
