# Vidéo #8 — Pourquoi tes doigts se rident dans l'eau

**Livrée le 2026-08-19** · Explainer · Pastel Flat 2D (DNA) · 40 s (4 blocs × 10 s) · 9:16 · voix Ainsley (FR) · sous-titres clean burnés · fond lo-fi ducké · upscale Topaz 1080p.

> **Épisode rattrapé à la main.** La routine quotidienne a bien tiré le 18/08 à 06:04 mais n'a rien produit,
> faute de connecteurs MCP (voir `publication/routine-quotidienne.md`). La chaîne des CTA a donc glissé d'un jour :
> la vidéo 007, sortie le 17/08, annonçait « demain ».

## Script final (tel que dit à l'antenne)

1. **HOOK** — Après un long bain, tes doigts se couvrent de petits plis. On croit généralement que la peau absorbe l'eau et gonfle, mais c'est entièrement faux.
2. **BUILD** — C'est ton système nerveux qui commande. Il serre les vaisseaux sous la peau du doigt, et la surface, tirée par en dessous, se creuse en sillons.
3. **TURN** — La preuve : un doigt dont le nerf est abîmé ne se ride plus jamais. Ces sillons agissent comme les rainures d'un pneu sous la pluie.
4. **PAYOFF + CTA** — Ce sont donc des rainures utiles, pas un accident : elles aident à agripper les objets mouillés. Abonne-toi, demain on regarde pourquoi le soleil fait éternuer.

Fil rouge : **le sillon sur la pulpe** (constaté → expliqué → prouvé → utilisé).
Le twist : le pli n'est pas subi mais fabriqué — le système nerveux creuse des rainures antidérapantes à la demande. Le doigt dont le nerf est abîmé, qui ne se ride plus, est la preuve décisive.

## Nouveaux assets (personnage principal et clé de style réutilisés)

salle de bain, coupe de pulpe de doigt avec vaisseaux et nerf, badge pulpe-à-sillons.

## Qualité (mesures réelles)

- 4 blocs de 10.006 s, 720×1280 → 1080×1920, 24 fps ; coupes 4/3/3/4.
- Voix : 8.78 / 8.75 / 9.50 / 9.76 s ; débits 2.85 / 2.97 / 2.63 / 2.56 ; zéro pause interne.
- Sous-titres : 27 cues, acceptés du premier coup (similarités 0.89 / 0.85 / 0.81 / 0.91).
- Validateurs : validate_motion_script valid:true · sidecar blocks=4/per_block=4 · GATE 8 : audio 40.055 s.

## Leçon technique capitalisée (voir `channel_dna.json`)

**La structure de la phrase compte autant que le registre.** La ligne 1 a demandé 13 prises et 5 formulations.
Elle oscillait d'un extrême à l'autre sans jamais se poser :

| Version | Mots | Durées mesurées |
|---|---|---|
| familière | 27 | 6.43 / 7.17 s — `RUSHED` |
| soutenue | 24 | 10.35 / 10.29 / 10.18 s |
| intermédiaire **avec apposition** | 25 | 10.80 / 10.43 / **8.88 s mais 1 pause de 0.92 s** |
| simplifiée | 24 | 6.82 / 8.08 / 8.12 s |
| simplifiée **+ 2 mots polysyllabiques** | 25 | 9.45 / **8.78 s** / 9.45 s |

La version à apposition (« L'explication habituelle, celle de la peau qui absorbe l'eau, est fausse ») tombait
dans la bonne durée, mais la voix respirait au milieu de l'incise — 0,92 s, au-dessus du seuil de 0,8 s.
**Une incise invite le modèle à respirer ; deux propositions simples ne le font pas.**

La méthode qui a fini par marcher : partir d'une phrase **simple**, sans incise, pour éliminer les pauses,
puis régler la durée en échangeant deux mots courants contre deux mots polysyllabiques
(« croit » → « croit généralement », « faux » → « entièrement faux »). Le registre devient un réglage fin
sur une structure déjà saine, au lieu d'un pansement sur une phrase mal bâtie.
