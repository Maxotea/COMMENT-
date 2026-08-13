# Vidéo #6 — Pourquoi les courbatures arrivent deux jours après

**Livrée le 2026-08-13** · Explainer · Pastel Flat 2D (DNA) · 40 s (4 blocs × 10 s) · 9:16 · voix Ainsley (FR) · sous-titres clean burnés · fond lo-fi ducké · upscale Topaz 1080p.

## Livrables (hébergés Higgsfield)

| Fichier | URL |
|---|---|
| **Vidéo finale 1080×1920** | https://d8j0ntlcm91z4.cloudfront.net/user_2zae6klRfE97hlBWhyQP6j7d9cR/hf_20260813_085327_7f19750c-8b31-4d5a-b5e2-ecc3bffa10e8.mp4 |
| Poster | https://d2ol7oe51mr4n9.cloudfront.net/user_2zae6klRfE97hlBWhyQP6j7d9cR/13875f2c-1d3d-46fb-a3e6-87c582e61d8c.jpg |
| Master 720p sous-titré (backup) | https://d2ol7oe51mr4n9.cloudfront.net/user_2zae6klRfE97hlBWhyQP6j7d9cR/ee6cf07b-aab4-4dff-ae9c-c5332ec4a271.mp4 |

**Publication** : TikTok @expliquemoien40sec, dimanche 16/08 à 12:00 (post Metricool 361608460).

## Script final (tel que dit à l'antenne)

1. **HOOK** — Hier soir tu as fait du sport sans ressentir la moindre gêne. Et pourtant demain matin, descendre un escalier va devenir une vraie épreuve.
2. **BUILD** — Un effort intense crée des milliers de micro-déchirures dans tes fibres musculaires. Elles sont minuscules, indolores, et ton corps ne réagit pas tout de suite.
3. **TURN** — Le fameux acide lactique disparaît en moins de deux heures. La vraie douleur vient de la réparation des fibres, un chantier qui met deux jours à monter.
4. **PAYOFF + CTA** — Ces fibres repoussent ensuite un peu plus solides. Ta courbature est le reçu de ta séance : abonne-toi, demain on regarde les gargouillis du ventre.

Fil rouge : **la fibre fendue** (intacte → fendue → assiégée par les blobs réparateurs → recousue plus épaisse).
Le twist : la douleur n'est pas la blessure mais le chantier de réparation — c'est ce qui explique le décalage de deux jours, et pourquoi l'acide lactique n'y est pour rien.

## Nouveaux assets (personnage principal et clé de style réutilisés)

coin sport, coupe de tissu musculaire, escalier intérieur, badge fibre-avec-encoche.

## Qualité (mesures réelles)

- 4 blocs de 10.006 s, 720×1280 → 1080×1920, 24 fps, acceptés du premier coup.
- Voix : 9.50 / 9.14 / 8.73 / 9.80 s ; débits 2.53 / 2.74 / 3.09 / 2.45 ; zéro pause interne.
- Sous-titres : 25 cues, acceptés du premier coup — meilleures similarités de la série (0.96 / 0.85 / 0.86 / 0.82), similarité globale 0.937.
- Validateurs : validate_motion_script valid:true · sidecar blocks=4/per_block=4 · GATE 8 : audio 40.055 s.

## Leçon technique capitalisée (voir `channel_dna.json`)

La ligne 1 est restée hors fenêtre sur **10 prises consécutives**, et le diagnostic a renversé une idée
qu'on croyait acquise. Version conversationnelle (24 mots) : 7.46 / 6.80 / 6.63 s, `rate=RUSHED` à chaque fois.
Allongée à 29 mots, elle a été lue **encore plus vite** (3.53 → 4.08 mots/s) pour ne gagner que 0,7 s.
Réécrite en vocabulaire lourd, elle est passée à 12.80 / 10.50 / 11.18 s, `rate=SLOW`.

Ce n'est donc pas le nombre de mots qui pilote la durée, c'est le **registre de langue**. Une phrase
familière faite de mots courts et fréquents déclenche une diction rapide et enjouée (jusqu'à 4,08 mots/s) ;
une phrase à vocabulaire soutenu et polysyllabique déclenche une diction lente et posée (jusqu'à 1,88 mots/s).
Sur une même voix, l'écart dépasse le double.

Le correctif est un **registre mixte** : une ou deux tournures soutenues insérées dans une phrase par
ailleurs simple. « Hier soir tu as fait du sport **sans ressentir la moindre gêne** […] va devenir
**une vraie épreuve** » → 9.50 s du premier coup.
