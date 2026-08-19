# Pack de publication — chaîne ExpliqueMoi (TikTok · Reels · Shorts)

> **État au 2026-08-17.** Le correctif `privacyOption` est validé sur le terrain : les vidéos #4, #5 et #6 sont toutes sorties automatiquement, sans intervention manuelle.
>
> **État initial au 2026-08-13.** Compte TikTok **@expliquemoien40sec**, marque Metricool « ExpliqueMoi »
> (blogId **6704763**, userId **3689627**). Publication automatique, 12:00 Europe/Paris.
>
> | Post | Date | Réseau | ID Metricool | Statut |
> |---|---|---|---|---|
> | Vidéo #1 — otite | 2026-08-12 12:00 | TikTok | 360947537 | ❌ **ERROR — jamais publiée** |
> | Vidéo #2 — hoquet | 2026-08-12 18:00 | TikTok | 361250005 | ✅ PUBLIÉE |
> | Vidéo #3 — bâillements | 2026-08-13 10:00 | TikTok | 361250091 | ✅ PUBLIÉE |
> | Vidéo #4 — frissons | 2026-08-14 12:00 | TikTok | 361610915 | ✅ PUBLIÉE |
> | Vidéo #5 — nez bouché | 2026-08-15 12:00 | TikTok | 361610981 | ✅ PUBLIÉE |
> | Vidéo #6 — courbatures | 2026-08-16 12:00 | TikTok | 361608460 | ✅ PUBLIÉE |
> | Vidéo #7 — gargouillis | 2026-08-17 21:00 | TikTok | 363188030 | ✅ PUBLIÉE |
> | Vidéo #8 — doigts fripés | 2026-08-19 12:00 | TikTok | 363865699 | PENDING, autoPublish, 1080p |
>
> Vidéos publiées :
> [#2 hoquet](https://www.tiktok.com/@expliquemoien40sec/video/7673176927527652640) ·
> [#3 bâillements](https://www.tiktok.com/@expliquemoien40sec/video/7673423975707413792) ·
> [#4 frissons](https://www.tiktok.com/@expliquemoien40sec/video/7673825642026175777) ·
> [#5 nez bouché](https://www.tiktok.com/@expliquemoien40sec/video/7674196601761516833) ·
> [#6 courbatures](https://www.tiktok.com/@expliquemoien40sec/video/7674567610926648608) ·
> [#7 gargouillis](https://www.tiktok.com/@expliquemoien40sec/video/7675078078611098912)
>
> Bio, avatar et réglages du compte : `publication/bio-tiktok.md`.

## ⚠️ Le bug qui a coûté la vidéo #1 — corrigé

Le post de la vidéo #1 a été **accepté par l'API Metricool** (statut PENDING, tout paraissait normal)
puis **rejeté par TikTok** à l'heure de publication :

```
providers[0].status        = ERROR
providers[0].detailedStatus = "Publish Tiktok video error: does not specified privacy options"
```

Cause : le payload ne contenait pas `tiktokData.privacyOption`. Les vidéos #2 et #3 ne sont sorties
que parce qu'elles ont été recréées à la main dans l'interface Metricool, qui remplit ce champ.

**Correctif appliqué le 13/08** : l'action Zapier `schedule_reel_with_providers` envoie désormais
systématiquement `tiktokData: {privacyOption: "PUBLIC_TO_EVERYONE", photoCoverIndex: 0}`.
Les posts #4, #5 et #6 ont été relus après création : le champ est bien stocké.

**Réflexe à garder** : après chaque planification, relire le post avec `list_scheduled_posts` et
vérifier que `tiktokData.privacyOption` est présent. Un post sans ce champ passera l'heure dite
sans rien publier et sans alerte.

## Note technique — action Zapier

L'action standard `schedule_post` refuse les posts (« You need to include at least one provider »)
quel que soit le format des booléens. Utiliser `schedule_reel_with_providers`, qui envoie
`providers: [{"network":"tiktok"}]` explicitement **et** le bloc `tiktokData`.

## Vidéo #1 — Comment on attrape une otite ❌ NON PUBLIÉE

- **Fichier vidéo (URL publique, 1080×1920, 40 s)** :
  https://d8j0ntlcm91z4.cloudfront.net/user_2zae6klRfE97hlBWhyQP6j7d9cR/hf_20260810_113842_f31ff67a-95af-411b-b70d-7eca60e602ef.mp4
- **Cover/poster** :
  https://d2ol7oe51mr4n9.cloudfront.net/user_2zae6klRfE97hlBWhyQP6j7d9cR/fe68b739-d22a-4f6d-9090-771af94c8f6c.jpg
- **Créneau recommandé** : aujourd'hui ou demain, **12:00 Europe/Paris** (créneau reel du moteur CM),
  puis vidéo #2 le lendemain 12:00 pour honorer le « demain » du CTA.
- **Titre (TikTok ≤150 car.)** : `Pourquoi tu attrapes une otite (et non, c'est pas la piscine) 👂`
- **Légende (TikTok/Reels/Shorts)** :

```
8 enfants sur 10 font une otite avant 3 ans. Et non, la piscine n'y est pour rien 🏊
Le vrai coupable : un tube de 3 cm caché derrière ton tympan.
👉 Abonne-toi — demain : pourquoi tu as le hoquet.
#otite #corpshumain #anatomie #lesavaistu #apprendresurtiktok #santé
```

## Vidéo #2 — Pourquoi tu as le hoquet ✅ LIVRÉE

- **Fichier vidéo (URL publique, 1080×1920, 40 s)** :
  https://d8j0ntlcm91z4.cloudfront.net/user_2zae6klRfE97hlBWhyQP6j7d9cR/hf_20260811_084252_3b07f079-4c24-4a1a-b26c-c8ecbb0269da.mp4
- **Cover/poster** :
  https://d2ol7oe51mr4n9.cloudfront.net/user_2zae6klRfE97hlBWhyQP6j7d9cR/daa062b0-d837-4137-abfb-fadbd8fd29d1.jpg
- **Créneau recommandé** : lendemain de la vidéo #1, **12:00 Europe/Paris**.
- **Titre** : `Pourquoi tu as le hoquet (la vraie raison) 🫁`
- **Légende** :

```
Un homme a eu le hoquet pendant 68 ans 😳
Le vrai responsable : ton diaphragme… et une porte qui claque dans ta gorge.
👉 Abonne-toi — demain : les bâillements contagieux.
#hoquet #corpshumain #anatomie #lesavaistu #apprendresurtiktok #science
```

Payload Metricool vidéo #2 (mêmes règles que la #1) :

```json
{
  "blogId": "BLOGID_COMMENT",
  "type": "REEL",
  "tiktok": true, "instagram": true, "youtube": true,
  "date": "2026-08-13T12:00:00",
  "text": "Un homme a eu le hoquet pendant 68 ans 😳\nLe vrai responsable : ton diaphragme… et une porte qui claque dans ta gorge.\n👉 Abonne-toi — demain : les bâillements contagieux.\n#hoquet #corpshumain #anatomie #lesavaistu #apprendresurtiktok #science",
  "mediaUrls": ["https://d8j0ntlcm91z4.cloudfront.net/user_2zae6klRfE97hlBWhyQP6j7d9cR/hf_20260811_084252_3b07f079-4c24-4a1a-b26c-c8ecbb0269da.mp4"],
  "draft": false, "autoPublish": true
}
```

## Vidéo #3 — Pourquoi les bâillements sont contagieux ✅ LIVRÉE

- **Fichier vidéo (1080×1920, 40 s)** :
  https://d8j0ntlcm91z4.cloudfront.net/user_2zae6klRfE97hlBWhyQP6j7d9cR/hf_20260811_203005_71967cb6-06cf-41b3-96a3-b70e64aa50e1.mp4
- **Cover/poster** :
  https://d2ol7oe51mr4n9.cloudfront.net/user_2zae6klRfE97hlBWhyQP6j7d9cR/f1b2ea85-14aa-421c-8698-d8c448a1ac7d.jpg
- **Titre** : `Pourquoi les bâillements sont contagieux 🐶`
- **Légende** :

```
Ton chien bâille quand tu bâilles 🐶
Le coupable : de minuscules neurones qui copient ce qu'ils voient. Et plus tu aimes la personne, plus tu attrapes son bâillement.
👉 Abonne-toi — demain : les frissons.
#baillement #corpshumain #cerveau #empathie #lesavaistu #apprendresurtiktok
```

## Vidéo #4 — Pourquoi tu as des frissons ✅ LIVRÉE

- **Fichier vidéo (1080×1920, 40 s)** :
  https://d8j0ntlcm91z4.cloudfront.net/user_2zae6klRfE97hlBWhyQP6j7d9cR/hf_20260813_081032_b9d189fb-a840-4cd5-a767-ee4bdbead584.mp4
- **Poster** :
  https://d2ol7oe51mr4n9.cloudfront.net/user_2zae6klRfE97hlBWhyQP6j7d9cR/9348ab84-8776-42dc-a383-954c082e3e2d.jpg
- **Légende** :

```
Ta peau se hérisse sur une musique, alors que tu n'as pas froid 🎧
Le coupable : un muscle minuscule planté au pied de chaque poil — un chauffage hérité de l'époque où on avait de la fourrure.
👉 Abonne-toi — demain : pourquoi ton nez se bouche d'un seul côté.
#frissons #chairdepoule #corpshumain #lesavaistu #apprendresurtiktok #science
```

## Vidéo #5 — Pourquoi ton nez se bouche d'un seul côté ✅ LIVRÉE

- **Fichier vidéo (1080×1920, 40 s)** :
  https://d8j0ntlcm91z4.cloudfront.net/user_2zae6klRfE97hlBWhyQP6j7d9cR/hf_20260813_082701_5a9cb4f6-fd28-4851-8de1-fa86e533f1ed.mp4
- **Poster** :
  https://d2ol7oe51mr4n9.cloudfront.net/user_2zae6klRfE97hlBWhyQP6j7d9cR/7df679fd-8704-4bef-b557-307d72b1dc35.jpg
- **Légende** :

```
Ton nez n'est jamais bouché des deux côtés en même temps 🫢
Tes narines se relèvent toutes les quelques heures : pendant que l'une bosse, l'autre se repose. Le rhume ne crée pas ce cycle, il le rend juste impossible à ignorer.
👉 Abonne-toi — demain : pourquoi les courbatures arrivent deux jours après.
#nezbouche #cyclenasal #corpshumain #lesavaistu #apprendresurtiktok #sante
```

## Vidéo #6 — Pourquoi les courbatures arrivent deux jours après ✅ LIVRÉE

- **Fichier vidéo (1080×1920, 40 s)** :
  https://d8j0ntlcm91z4.cloudfront.net/user_2zae6klRfE97hlBWhyQP6j7d9cR/hf_20260813_085327_7f19750c-8b31-4d5a-b5e2-ecc3bffa10e8.mp4
- **Poster** :
  https://d2ol7oe51mr4n9.cloudfront.net/user_2zae6klRfE97hlBWhyQP6j7d9cR/13875f2c-1d3d-46fb-a3e6-87c582e61d8c.jpg
- **Légende** :

```
Non, ce ne sont pas les courbatures d'acide lactique 💪
Il a disparu depuis deux heures. Ce qui te fait mal, c'est le chantier de réparation : des milliers de micro-déchirures que ton corps recoud pendant deux jours.
👉 Abonne-toi — demain : pourquoi ton ventre gargouille.
#courbatures #sport #corpshumain #lesavaistu #apprendresurtiktok #science
```

## Vidéo #7 — Pourquoi ton ventre gargouille ✅ LIVRÉE

- **Fichier vidéo (1080×1920, 40 s)** :
  https://d8j0ntlcm91z4.cloudfront.net/user_2zae6klRfE97hlBWhyQP6j7d9cR/hf_20260817_172831_6029978b-bf66-4d16-8657-468f0fb502f6.mp4
- **Poster** :
  https://d2ol7oe51mr4n9.cloudfront.net/user_2zae6klRfE97hlBWhyQP6j7d9cR/b493ef37-ac7c-4bc4-89c9-92ff704d03fc.jpg
- **Légende** :

```
Ton ventre gargouille, et tout le monde croit que tu as faim 🫠
En fait ça n'a presque rien à voir : c'est une bulle d'air écrasée dans un tube étroit. Le bruit existe aussi après manger, sauf qu'à ce moment-là la nourriture l'étouffe.
👉 Abonne-toi — demain : pourquoi tes doigts se rident dans l'eau.
#gargouillis #digestion #corpshumain #lesavaistu #apprendresurtiktok #science
```

## Vidéo #8 — Pourquoi tes doigts se rident dans l'eau ✅ LIVRÉE

- **Fichier vidéo (1080×1920, 40 s)** :
  https://d8j0ntlcm91z4.cloudfront.net/user_2zae6klRfE97hlBWhyQP6j7d9cR/hf_20260819_052302_927c095b-cb89-4d50-8aa5-36cbaf597733.mp4
- **Note** : d'abord programmée en 720p (Topaz engorgé), puis passée en 1080p. ⚠️ L'action
  `swap_post_media_verified` ne remplace pas le média — elle crée un SECOND post au même créneau en
  annonçant `unchanged`. Toujours recompter les posts avec `list_scheduled_posts` après un swap et
  supprimer le doublon. Voir `regle_swap_media_metricool` dans `channel_dna.json`.
- **Légende** :

```
Non, tes doigts ne gonflent pas en absorbant l'eau 🛁
C'est ton système nerveux qui serre les vaisseaux sous la peau et creuse des sillons. La preuve : un doigt dont le nerf est abîmé ne se ride plus jamais. Ce sont des rainures antidérapantes, comme sur un pneu.
👉 Abonne-toi — demain : pourquoi le soleil te fait éternuer.
#doigtsfripes #corpshumain #systemenerveux #lesavaistu #apprendresurtiktok #science
```

## Règles de chaîne (à reconduire chaque jour)

- 1 vidéo/jour, 12:00 Paris, formats identiques (REEL/TikTok vidéo/Short).
- La légende reprend le hook chiffré + 1 seule question + CTA abonnement vers le sujet du lendemain.
- 6 hashtags max : 4 fixes (#corpshumain #lesavaistu #apprendresurtiktok + le sujet du jour) + 2 tournants.
- **Déclaration IA** : contenu généré par IA → activer le label « contenu généré par IA » de TikTok
  (flag AIGC dans le flux Higgsfield ; toggle manuel côté Reels/Shorts si demandé).

## Payloads Metricool prêts (dès que la marque existe)

Action Zapier `schedule_post` — remplacer `BLOGID_COMMENT` :

```json
{
  "blogId": "BLOGID_COMMENT",
  "type": "REEL",
  "tiktok": true, "instagram": true, "youtube": true,
  "date": "2026-08-12T12:00:00",
  "text": "8 enfants sur 10 font une otite avant 3 ans. Et non, la piscine n'y est pour rien 🏊\nLe vrai coupable : un tube de 3 cm caché derrière ton tympan.\n👉 Abonne-toi — demain : pourquoi tu as le hoquet.\n#otite #corpshumain #anatomie #lesavaistu #apprendresurtiktok #santé",
  "mediaUrls": ["https://d8j0ntlcm91z4.cloudfront.net/user_2zae6klRfE97hlBWhyQP6j7d9cR/hf_20260810_113842_f31ff67a-95af-411b-b70d-7eca60e602ef.mp4"],
  "draft": false, "autoPublish": true
}
```

⚠️ Après création : vérifier les heures avec `list_scheduled_posts` (bug de fuseau connu),
corriger via `bulk_update_post_times`, puis `bulk_set_draft` si on veut rester en brouillon.

## Ce qu'il reste à faire côté compte

- [x] ~~Passer le compte TikTok en Business~~ — **fait** : les vidéos #2 et #3 sont sorties en
      publication automatique (statut PUBLISHED avec URL publique), ce qui prouve que le compte
      est bien en Business et que Metricool a le droit de publier seul.
- [ ] **Mettre la bio et l'avatar** (`publication/bio-tiktok.md`).
- [x] ~~Activer le label « contenu généré par IA »~~ — automatique : les fichiers Higgsfield portent
      leurs métadonnées C2PA, TikTok appose le label seul à l'ingestion. À vérifier une fois à l'œil
      sur une publication réelle.
- [ ] Optionnel : ouvrir Instagram + la chaîne YouTube de marque, les connecter à la même marque
      Metricool → je planifierai alors les 3 réseaux en un seul appel.

## Élargir à Instagram / YouTube plus tard

Ajouter simplement les réseaux dans `networks` de l'action `schedule_reel_with_providers` :
`"tiktok,instagram,youtube"`. Les URLs des vidéos et les légendes ne changent pas.
