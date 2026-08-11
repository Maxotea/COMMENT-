# Vidéo #3 — Pourquoi les bâillements sont contagieux

**Livrée le 2026-08-11** · Explainer · Pastel Flat 2D (DNA) · 40 s (4 blocs × 10 s) · 9:16 · voix Ainsley (FR) · sous-titres clean burnés · fond lo-fi ducké · upscale Topaz 1080p.

## Livrables (hébergés Higgsfield)

| Fichier | URL |
|---|---|
| **Vidéo finale 1080×1920** | https://d8j0ntlcm91z4.cloudfront.net/user_2zae6klRfE97hlBWhyQP6j7d9cR/hf_20260811_203005_71967cb6-06cf-41b3-96a3-b70e64aa50e1.mp4 |
| Poster 1080 | https://d2ol7oe51mr4n9.cloudfront.net/user_2zae6klRfE97hlBWhyQP6j7d9cR/f1b2ea85-14aa-421c-8698-d8c448a1ac7d.jpg |
| Master 720p sous-titré (backup) | https://d2ol7oe51mr4n9.cloudfront.net/user_2zae6klRfE97hlBWhyQP6j7d9cR/c535f6fe-d9e3-4591-af3d-a76dbbddd3f9.mp4 |

**Publication** : TikTok @ExpliqueMoi, vendredi 14/08 à 12:00 (post Metricool 360968512).

## Script final (tel que dit à l'antenne)

1. **HOOK** — Ton chien bâille quand tu bâilles. Ce réflexe saute d'un cerveau à l'autre sans un mot, et personne ne décide vraiment de le déclencher.
2. **BUILD** — Dans ton cerveau vit un petit groupe de cellules, les neurones miroirs. Ils s'allument quand tu fais un geste, mais aussi quand tu le vois chez quelqu'un.
3. **TURN** — Voir un bâillement suffit donc à activer le circuit qui le déclenche. Ton cerveau imite avant que tu décides : tu bâilles déjà quand tu comprends pourquoi.
4. **PAYOFF + CTA** — Plus tu es proche de la personne, plus tu attrapes son bâillement. Ce petit réflexe mesure donc ton empathie : abonne-toi, demain on regarde les frissons.

Fil rouge : **les neurones miroirs** (invisibles → révélés → en action → transformés en jauge d'empathie).
Le twist : le bâillement n'est pas une histoire de fatigue mais de lien social — ce qui répond au chien du hook.

## Nouveaux assets (le personnage principal et la clé de style sont réutilisés)

salon (+ angle de couverture), cerveau/neurones miroirs, second personnage (cheveux foncés, pull rose), chien, badge amas de neurones.

## Qualité (mesures réelles)

- 4 blocs de 10.006 s, 720×1280 → 1080×1920, 24 fps, tous acceptés du premier coup.
- Voix : 8.95 / 8.87 / 9.00 / 9.00 s ; débits 3.13 / 3.04 / 3.33 / 3.00.
- Réserve assumée : le bloc 1 conserve une pause interne de 0.87 s (seuil 0.80). Trois prises testées ; les alternatives étaient soit sous le plancher de 8.6 s, soit plus rapides. La meilleure a été conservée, conformément au budget de 3 essais par ligne.
- Mix : loudnorm −16 LUFS, bed mesuré à −22.7 dB puis ducké.
- Sous-titres : Whisper sur les prises propres + wording auteur, 25 cues, vérifiés à l'image.
- Validateurs : validate_motion_script valid:true · sidecar blocks=4/per_block=4 · GATE 8 : 1080×1920, audio 40.064 s.

## Leçon technique capitalisée (voir `channel_dna.json`)

Les sous-titres ont été refusés trois fois sur le bloc 4 (similarité 0.63 < 0.75). Cause réelle, trouvée en comparant les tokens : **l'aligneur découpe les élisions de Whisper** (`c'est` → `c` + `est`) alors que le script les garde soudées après normalisation (`cest`). Chaque apostrophe compte donc comme une erreur — la ligne 4 en avait six. Changer de modèle Whisper ne corrige rien (ratio identique en `small` et `medium`). La réécriture à un seul trait d'union est passée immédiatement. Règle ajoutée à la DNA : **1 à 2 apostrophes maximum par ligne, surtout sur le CTA**.
