# Pack de publication — chaîne COMMENT (TikTok · Reels · Shorts)

> Préparé le 2026-08-11. Tout est prêt-à-planifier : il ne manque QUE la connexion des comptes
> de la chaîne (étape OAuth que seul Maxime peut faire — voir « Activation » en bas).

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

## Activation — ce qu'il te reste à faire (5 min)

Deux chemins, au choix (le premier est celui du pipeline prévu) :

1. **Metricool (recommandé, multi-réseaux)** : créer la marque « COMMENT » dans Metricool
   (compte contact@oteaproduction.com) et connecter le TikTok + Instagram + YouTube de la chaîne.
   → Dis-moi ensuite « la marque COMMENT est créée » et je planifie tout le calendrier d'un coup
   (vidéos 1 et 2, 12:00 Paris, avec correction du bug de fuseau).
2. **TikTok direct via Higgsfield** : connecter le compte TikTok de la chaîne
   (outil de connexion TikTok dans l'interface Higgsfield). → Je peux alors préparer le post
   (brouillon TikTok ou publication directe avec label IA) sans passer par Metricool.

État vérifié le 2026-08-11 : 9 marques Metricool connectées (aucune pour COMMENT), 0 compte TikTok
connecté côté Higgsfield.
