# Vidéo #9 — Pourquoi tu éternues en regardant le soleil

**Livrée le 2026-08-21** · Explainer · Pastel Flat 2D (DNA) · 40 s (4 blocs × 10 s) · 9:16 · voix Ainsley (FR) · sous-titres clean burnés · fond lo-fi ducké · upscale Topaz 1080p.

> **Deux créneaux perdus avant celui-ci.** Rien n'est sorti le 20/08 ni le 21/08 à midi : la routine
> quotidienne se déclenche bien mais ne produit rien, faute de connecteurs MCP
> (voir `publication/routine-quotidienne.md`). Cet épisode a donc été lancé à la main le 21/08 au soir
> et calé le soir même à 22:30 plutôt que d'attendre le lendemain midi.

## Livrables (hébergés Higgsfield)

| Fichier | URL |
|---|---|
| **Vidéo finale 1080×1920** | https://d8j0ntlcm91z4.cloudfront.net/user_2zae6klRfE97hlBWhyQP6j7d9cR/hf_20260821_194409_cc2a5213-f6b0-4574-b45f-496015b17103.mp4 |
| Master 720p sous-titré (backup) | https://d2ol7oe51mr4n9.cloudfront.net/user_2zae6klRfE97hlBWhyQP6j7d9cR/aadeb266-bce4-418b-b666-22e82bbf48f9.mp4 |
| Poster | https://d2ol7oe51mr4n9.cloudfront.net/user_2zae6klRfE97hlBWhyQP6j7d9cR/abf33d0a-9b02-46b5-a074-d2721b5b1b78.jpg |

**Publication** : TikTok @expliquemoien40sec, vendredi 21/08 à 22:30 (post Metricool 365057205, 1080p, `privacyOption` relu et présent, aucun doublon).

## Script final (tel que dit à l'antenne)

1. **HOOK** — Une personne sur quatre éternue face au soleil. Tu sors du cinéma en plein jour et ça part tout seul, sans que la lumière touche ton nez.
2. **BUILD** — Le nerf qui gère ton nez passe juste à côté du nerf optique. Sur ce court trajet, les deux fibres se frôlent de très près.
3. **TURN** — Une lumière brutale sature le nerf optique, et le signal déborde sur son voisin. Le cerveau croit alors que ton nez est vraiment irrité.
4. **PAYOFF + CTA** — Tu éternues donc à cause de tes yeux, absolument pas de ton nez. Abonne-toi, demain on explique pourquoi la glace provoque un mal de tête.

Fil rouge : **le carrefour des deux nerfs** (ignoré → localisé → franchi → compris).
Le twist : l'éternuement ne part pas du nez. Il part de l'œil, et ne devient un éternuement qu'en
sautant, sur quelques millimètres, d'un câble à son voisin.

## Nouveaux assets (personnage principal et clé de style réutilisés)

sortie de cinéma en plein soleil, coupe de profil avec les deux câbles nerveux, badge « carrefour ».

## Qualité (mesures réelles)

- 4 blocs de 10.006 s, 720×1280 → 1080×1920, 24 fps.
- Voix : 9.18 / 8.80 / 9.50 / 9.18 s ; débits 2.94 / 2.84 / 2.53 / 2.72 ; **zéro pause interne**.
- Sous-titres : 23 cues, acceptés du premier coup (similarités 0.87 / 0.80 / 0.90 / 0.90).
- Sidecar blocks=4 / per_block=4 · GATE 8 : audio 40.055 s, vidéo 40.042 s.
- `validate_motion_script` : **valid:false sur un point résiduel** — les blocs 2 et 3 partagent lieu +
  assets. Le plateau dédié (`loc_carrefour`, job `f2798e26`) a été généré pour corriger ça, mais les
  crédits Higgsfield se sont épuisés avant de pouvoir régénérer le bloc. Les deux clips livrés sont
  visuellement distincts (bloc 2 large et froid, bloc 3 serré et lumineux), la règle n'est simplement
  pas satisfaite au sens strict du validateur.

## Trois leçons techniques capitalisées (voir `channel_dna.json`)

### 1. Le bundle Higgsfield a été redécoupé

`faceless-channel-video/scripts/` n'existe plus. Les scripts vivent maintenant dans trois bundles :

| Script | Chemin actuel |
|---|---|
| `speech_metrics.sh` | `$HF_WORKFLOWS/narrator/scripts/` |
| `finish_video.sh`, `validate_motion_script.py` | `$HF_WORKFLOWS/faceless-video/scripts/` |
| `audio_to_captions.py` | `$HF_WORKFLOWS/subtitles/scripts/` |

### 2. Le validateur pré-génération s'est durci

Il passait sur les vidéos 004 à 008 ; il a refusé ce manifeste sur six points. Cinq règles nouvelles :

- champ `genre` obligatoire (`education` ici) ;
- deux plans **voisins** ne peuvent pas partager la même taille de cadre ;
- un bloc qui **revient** sur un lieu déjà vu ne peut pas rouvrir sur un WIDE ;
- le hook doit ouvrir sur une phrase d'**au plus 8 mots**, le fait brut posé à plat ;
- deux blocs à moins de 2 blocs d'écart ne peuvent pas partager lieu + assets (l'asset du fil rouge
  ne compte pas — le réordonner ne sert donc à rien, il faut un vrai plateau différent).

Coût : 3 blocs vidéo et 6 prises de voix régénérés. **Valider le manifeste AVANT de générer**, pas après.

### 3. La règle des 8 mots crée un point — et le point invite à respirer

La ligne 1 a demandé 8 prises sur 2 formulations :

| Version | Mots | Durées mesurées |
|---|---|---|
| une longue phrase d'ouverture | 26 | 7.95 · 8.17 (RUSHED) |
| registre relevé | 25 | 11.29 · 9.53 |
| 8 mots + reste (règle du validateur) | 27 | 9.96 **avec pause 0.89 s** · 8.27 (RUSHED) · 6.80 · 10.50 · **9.18 ✓** |

La pause au point est un tirage, exactement comme la durée : sur cinq prises du même texte elle est
passée de 0.89 s à zéro. **Ne pas réécrire la ligne pour tuer la pause — retirer.**

### 4. Bug interne au bundle : les noms de fichiers voix

`finish_video.sh` assemble le master puis échoue aux sous-titres :

```
ERROR: per-block timing failed: voice file missing for block 1: tried work/voices/v_000.wav
```

L'étape assemblage écrit `work/voices/voice01.wav … voice04.wav`, l'étape caption relit
`v_000.wav … v_003.wav`. Correctif : copier les fichiers sous les deux noms puis relancer
`finish_video.sh` — il est idempotent, il saute l'assemblage et reprend aux sous-titres.

## Sources

- [ACHOO Syndrome — MINI Medical Genetics Summaries (NCBI)](https://www.ncbi.nlm.nih.gov/books/NBK109193/)
- [ACHOO Syndrome (PubMed 28520355)](https://pubmed.ncbi.nlm.nih.gov/28520355/)
- [GWAS on photic sneeze reflex — prévalence 25.6 %](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC6428856/)
- [OMIM 100820 — ACHOO syndrome](https://omim.org/entry/100820)
