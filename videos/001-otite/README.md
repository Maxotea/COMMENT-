# Vidéo #1 — Comment on attrape une otite

**Livrée le 2026-08-10** · Explainer · Pastel Flat 2D · 40 s (4 blocs × 10 s) · 9:16 · voix Ainsley (FR) · sous-titres clean burnés · fond musical lo-fi discret (ducké sous la voix) · upscale Topaz 1080p.

## Livrables (hébergés Higgsfield)

| Fichier | URL |
|---|---|
| **Vidéo finale 1080×1920** | https://d8j0ntlcm91z4.cloudfront.net/user_2zae6klRfE97hlBWhyQP6j7d9cR/hf_20260810_113842_f31ff67a-95af-411b-b70d-7eca60e602ef.mp4 |
| Poster 1080 | https://d2ol7oe51mr4n9.cloudfront.net/user_2zae6klRfE97hlBWhyQP6j7d9cR/fe68b739-d22a-4f6d-9090-771af94c8f6c.jpg |
| Master 720p sous-titré (pré-upscale, backup) | https://d2ol7oe51mr4n9.cloudfront.net/user_2zae6klRfE97hlBWhyQP6j7d9cR/bbc23708-e9bf-4975-968d-e13d85075c73.mp4 |

## Script final (tel que dit à l'antenne)

1. **HOOK** — Huit enfants sur dix font une otite. Et non, la piscine n'y est pour rien : le vrai coupable se cache juste derrière ton tympan.
2. **BUILD** — Ton oreille abrite une petite pièce reliée à ta gorge par un tunnel : la trompe d'Eustache. Sa mission : aérer la cavité et évacuer les liquides.
3. **TURN** — Attrape un rhume : ce tunnel gonfle et se bouche, le liquide reste coincé à l'intérieur. Les bactéries adorent cette piscine tiède, s'y multiplient : voilà l'otite.
4. **PAYOFF + CTA** — Mais pourquoi surtout les enfants ? Leur trompe est plus courte et presque horizontale, alors le liquide stagne au chaud — abonne-toi, demain on t'explique pourquoi tu as le hoquet.

Fil rouge : **la trompe d'Eustache** (teasée → saine → bouchée/envahie → comparée enfant/adulte).
Le « twist piscine » : l'eau accusée au hook devient la piscine tiède intérieure du bloc 3.

## Qualité (mesures réelles)

- 4 blocs vidéo, 10.006 s chacun, 720×1280→1080×1920, 24 fps, 4 cuts/bloc (= 5 plans).
- Voix : 9.00 / 9.00 / 8.94 / 9.00 s de parole (fenêtre 8.6–10.0), débit 2.78–3.11 mots/s (rate=ok), 0 pause interne, centrées dans leurs blocs (sidecar).
- Note pace : la voix Ainsley lit vite en français — la bande nominale 27–32 mots donnait un débit >3.2 mots/s ; lignes recalibrées à ~24–28 tokens (la fenêtre prime sur le compte de mots, cf. workflow).
- Mix : loudnorm −16 LUFS, SFX sous la voix, bed mesuré à −21.8 dB puis ducké.
- Sous-titres : Whisper sur les prises propres + wording auteur (`final.srt`), burn clean, vérifié à l'image.
- Sidecar assembleur : `final.mp4.assembly.json` (blocks=4, aucun freeze, full decode).
- Validateurs : `validate_motion_script` valid:true · `validate_result_manifests` valid:true.

## Fichiers

- `script_manifest.json` — manifeste canonique (wording final, plans, arc, sources)
- `asset_manifest.json` — roster des 9 assets générés (clé de style incluse)
- `final.srt` — sous-titres (cues réels du burn)
- `final.mp4.assembly.json` — sidecar de l'assembleur (preuve de pipeline)
- `run.json` — état complet du run (ids de jobs, notes d'exploitation)

La **CHANNEL DNA** (pour que la vidéo #2 garde le même look/voix sans refaire l'intake ni le style) est à la racine : `channel_dna.json`.
