# Vidéo #4 — Pourquoi tu as des frissons

**Livrée le 2026-08-13** · Explainer · Pastel Flat 2D (DNA) · 40 s (4 blocs × 10 s) · 9:16 · voix Ainsley (FR) · sous-titres clean burnés · fond lo-fi ducké · upscale Topaz 1080p.

## Livrables (hébergés Higgsfield)

| Fichier | URL |
|---|---|
| **Vidéo finale 1080×1920** | https://d8j0ntlcm91z4.cloudfront.net/user_2zae6klRfE97hlBWhyQP6j7d9cR/hf_20260813_081032_b9d189fb-a840-4cd5-a767-ee4bdbead584.mp4 |
| Poster | https://d2ol7oe51mr4n9.cloudfront.net/user_2zae6klRfE97hlBWhyQP6j7d9cR/9348ab84-8776-42dc-a383-954c082e3e2d.jpg |
| Master 720p sous-titré (backup) | https://d2ol7oe51mr4n9.cloudfront.net/user_2zae6klRfE97hlBWhyQP6j7d9cR/2fc7160b-0247-45a7-a515-0284673728fe.mp4 |

**Publication** : TikTok @expliquemoien40sec, vendredi 14/08 à 12:00 (post Metricool 361594247).

## Script final (tel que dit à l'antenne)

1. **HOOK** — Ta peau se hérisse devant une musique, alors que tu n'as pas froid. Le coupable est un muscle minuscule, planté au pied de chaque poil.
2. **BUILD** — Ce petit muscle arrecteur se contracte et redresse le poil d'un coup sec. La peau se plisse autour de la racine : voilà la chair de poule.
3. **TURN** — Chez un animal à fourrure, ce réflexe gonfle tout le pelage et emprisonne une couche d'air chaud. Toi, tu hérisses trois poils pour rien.
4. **PAYOFF + CTA** — Une émotion forte libère la même adrénaline que le grand froid, et le circuit se déclenche pareil : abonne-toi, demain on regarde le nez bouché.

Fil rouge : **le muscle arrecteur** (caché → révélé → comparé chez l'animal → résolu par l'émotion).
Le twist : le frisson est un chauffage hérité d'ancêtres à fourrure, devenu inutile sur nous — ce qui explique pourquoi une musique le déclenche aussi bien que le froid.

## Nouveaux assets (le personnage principal, le salon et la clé de style sont réutilisés)

coupe de peau avec poils et rubans-muscles, clairière enneigée, badge poil-et-muscle. Le chien vient de la vidéo 003.

## Qualité (mesures réelles)

- 4 blocs de 10.006 s, 720×1280 → 1080×1920, 24 fps, tous acceptés du premier coup, 5 plans chacun (coupes à 2.0 / 3.9 / 6.0 / 8.0 s).
- Voix : 8.85 / 8.89 / 9.14 / 9.00 s ; débits 2.71 / 2.92 / 2.63 / 2.78 ; **zéro pause interne** sur les quatre lignes.
- Mix : loudnorm −16 LUFS, bed mesuré puis ducké sous la voix.
- Sous-titres : 24 cues, **acceptés du premier coup** sur les 4 blocs (similarités 0.78 / 0.85 / 0.77 / 0.90) — la règle des apostrophes établie sur la vidéo 003 a tenu.
- Validateurs : validate_motion_script valid:true · sidecar blocks=4/per_block=4 · GATE 8 : audio 40.055 s.

## Leçons techniques capitalisées (voir `channel_dna.json`)

**1. Le nombre de mots ne détermine pas la durée.** À texte identique, la voix Ainsley a lu entre 2.30 et 2.97 mots/seconde selon la prise : 26 mots ont donné 8.89 s, 28 mots 12.18 s. Écrire « 26 mots » ne garantit donc rien. La méthode qui marche : **soumettre deux prises du même texte en un seul appel**, mesurer les deux, garder celle qui tombe entre 8.6 et 9.2 s. Même coût qu'un aller-retour séquentiel, une seule attente. Appliqué à la vidéo 005 dès le premier essai, 3 lignes sur 4 étaient bonnes immédiatement.

**2. Piège d'outillage.** La détection de coupes doit lire le champ ffprobe `pts_time`, pas `pkt_pts_time` (retiré des ffmpeg récents). Avec l'ancien nom la commande renvoie `0 coupe` **sans erreur** sur des blocs pourtant parfaits — un faux négatif silencieux qui pousse à regénérer des blocs corrects.
