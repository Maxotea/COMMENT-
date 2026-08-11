# Pack de publication — chaîne ExpliqueMoi (TikTok · Reels · Shorts)

> ✅ **PLANIFIÉ le 2026-08-11.** Marque Metricool « ExpliqueMoi » (blogId **6704763**),
> compte TikTok @ExpliqueMoi connecté. Les deux vidéos sont en file d'attente TikTok,
> publication automatique, 12:00 Europe/Paris — horaires vérifiés après création.
>
> | Post | Date | Réseau | ID Metricool | Statut |
> |---|---|---|---|---|
> | Vidéo #1 — otite | 2026-08-12 12:00 | TikTok | 360947537 | PENDING, autoPublish |
> | Vidéo #2 — hoquet | 2026-08-13 12:00 | TikTok | 360947612 | PENDING, autoPublish |
>
> Bio, avatar et réglages du compte : `publication/bio-tiktok.md`.
>
> **Note technique importante** : l'action Zapier standard `schedule_post` refuse les posts
> (« You need to include at least one provider ») quel que soit le format des booléens.
> Contournement en place : l'action `schedule_reel_with_providers` (créée pour ce compte),
> qui envoie `providers: [{"network":"tiktok"}]` explicitement. C'est elle qu'il faut utiliser
> pour les prochaines vidéos.

## Vidéo #1 — Comment on attrape une otite

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

- [ ] **Passer le compte TikTok en Business** (Paramètres → Gérer le compte → Passer à un compte
      Business, catégorie Éducation). La publication automatique Metricool ne fonctionne que sur un
      compte Business — sans ça, les deux posts basculeront en simple rappel de publication manuelle.
- [ ] **Mettre la bio et l'avatar** (`publication/bio-tiktok.md`).
- [ ] **Activer le label « contenu généré par IA »** sur chaque publication.
- [ ] Optionnel : ouvrir Instagram + la chaîne YouTube de marque, les connecter à la même marque
      Metricool → je planifierai alors les 3 réseaux en un seul appel.

## Élargir à Instagram / YouTube plus tard

Ajouter simplement les réseaux dans `networks` de l'action `schedule_reel_with_providers` :
`"tiktok,instagram,youtube"`. Les URLs des vidéos et les légendes ne changent pas.
