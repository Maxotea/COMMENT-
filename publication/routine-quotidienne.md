# Routine quotidienne — ExpliqueMoi

**État : `trig_01Lq7k3wegKAPMTyduScXyJj`, tous les jours à 06:00 heure de Paris (04:00 UTC).**
Recréée le 2026-08-19 (l'ancienne, `trig_01Mu7zmXeawv4pQeyfkReSM7`, a été supprimée).

> ## ⛔ La routine ne peut PAS fonctionner en l'état — et c'est prouvé
>
> Elle a tiré le **18/08 à 06:04** et n'a rien produit. Aucune vidéo, aucun post, aucun commit.
> La chaîne des CTA a glissé d'un jour et la vidéo 008 a dû être rattrapée à la main.
>
> **Cause :** la routine ne stocke aucun connecteur MCP. Sans Higgsfield elle ne peut rien générer,
> sans Zapier elle ne peut rien planifier. La session se réveille, ne trouve pas ses outils, et s'arrête.
>
> **Ce que j'ai essayé et qui ne marche pas :** le paramètre `connectors` de `create_trigger` renvoie
> `the connectors parameter is not available for this organization`. L'API refuse donc d'attacher les
> connecteurs, quelle que soit la formulation.
>
> **Le seul correctif possible, et il n'appartient qu'à Maxime (2 min) :**
> ouvrir **claude.ai → Routines → « ExpliqueMoi — vidéo quotidienne »**, attacher les connecteurs
> **HIGGSFIELD** et **Zapier**, enregistrer. Si l'entrée n'est pas modifiable, la supprimer et la recréer
> depuis cette interface en collant le prompt ci-dessous.
>
> **Comment vérifier que c'est réglé :** une routine correctement configurée porte un bloc
> `mcp_connections` listant ses connecteurs. Les routines *POST CM-OTEA* et *CR client Publi Hebdo*
> l'ont (elles ont été créées depuis l'interface, `created_via: http_api`) ; celle-ci ne l'a pas
> (`created_via: meta_mcp`). C'est exactement la différence entre une routine qui tourne et une qui
> se réveille pour rien.
>
> Tant que ce n'est pas fait, il suffit de demander « lance la vidéo du jour » pour que je la produise.

## Garde-fou ajouté au prompt

Le prompt commence désormais par une étape 0 : la session vérifie que Higgsfield et Zapier répondent
**avant** de commencer, et s'arrête net en le disant si l'un manque. Elle ne fera plus semblant d'avancer.

## Pourquoi 06:00

La routine produit la vidéo le matin et la programme pour **le premier créneau libre à 12:00**,
pas forcément le jour même. Il y a donc toujours au moins une vidéo d'avance : si un matin la
production échoue, la publication du jour part quand même et il reste une journée pour rattraper.

## Prompt de la routine (à coller tel quel)

```
Tu produis et planifies l'épisode du jour de la chaîne éducative TikTok ExpliqueMoi (vidéos verticales de 40 s expliquant le corps humain). Cette tâche est autonome et complète : tu vas du sujet jusqu'au post planifié, sans demander de validation.

## 1. Charger le contexte (obligatoire, dans cet ordre)

- Le dépôt Maxotea/COMMENT-, branche claude/educational-channel-otite-video-hh0qdc. Clone-le si nécessaire.
- channel_dna.json à la racine : c'est le contrat visuel et sonore de la chaîne (clé de style Pastel Flat 2D, personnage principal, voix Ainsley, aspect 9:16, sous-titres clean FR, bed musical). Réutilise ces ids tels quels — ne regénère JAMAIS la clé de style ni le personnage principal, et ne refais pas l'intake du workflow.
- publication/file-attente-sujets.md : prends le premier sujet non coché. C'est le sujet du jour, il est déjà annoncé par le CTA de la vidéo précédente.
- videos/003-baillements/run.json et son README : exemple complet de ce qui est attendu en sortie.
- Charge le workflow Higgsfield avec get_workflow_instructions(workflow="faceless-channel-video") et suis ses phases 1 à 9 (l'intake est déjà tranché par la DNA).

## 2. Produire la vidéo

Format verrouillé : 4 blocs de 10 s, 9:16, 5 plans cutés par bloc, voix Ainsley en français, sous-titres clean burnés, bed lo-fi ducké, upscale Topaz 1080p pour finir.

Structure narrative : hook chiffré ou contre-intuitif en une phrase courte -> un mécanisme expliqué -> un twist qui renverse l'idée reçue -> payoff qui referme le hook, suivi du CTA « abonne-toi, demain on … » annonçant le sujet suivant de la file.

Fil rouge obligatoire : un objet physique unique présent dans les 4 blocs, qui évolue et se résout au dernier (donne-lui son propre asset).

Trois pièges déjà rencontrés, à respecter sans exception :
- Débit voix : soumets TOUJOURS deux prises du même texte dans le même appel generate_audio_batch, mesure-les avec speech_metrics.sh et garde celle dont la parole tombe entre 8,6 et 9,2 s (rate=ok, zéro pause interne >= 0,8 s). À texte identique la même voix varie de 1,9 à 4,1 mots/s : le tirage compte plus que le nombre de mots, donc tire deux fois plutôt que de réécrire.
- Si les DEUX prises ratent la fenêtre du même côté, ce n'est plus le hasard : c'est le registre de langue. Une phrase familière faite de mots courts est lue vite (jusqu'à 4,1 mots/s) et l'allonger ne sert à rien — elle sera lue encore plus vite. Une phrase à vocabulaire soutenu est lue lentement (jusqu'à 1,9 mots/s). Trop court -> remplace un ou deux mots familiers par des tournures plus soutenues ; trop long -> fais l'inverse. Voir regle_debit_voix_fr dans channel_dna.json.
- Sous-titres : l'aligneur casse sur les élisions françaises (voir regle_sous_titres_fr dans channel_dna.json). Maximum 1 à 2 apostrophes ou traits d'union par ligne, surtout sur la ligne du CTA. Si le burn est refusé pour cause de similarité, ne change pas de modèle Whisper — réécris la ligne avec moins d'apostrophes.

Le sandbox Higgsfield est éphémère : enchaîne téléchargements, assemblage et upload dans un seul appel, et relance depuis les URLs si tu perds les fichiers.

## 3. Planifier la publication

- Liste d'abord les posts déjà programmés : action Zapier Metricool code_action_metricoolcliapi__list_scheduled_posts, blogId 6704763 (marque ExpliqueMoi), sur les 10 prochains jours.
- Choisis le premier jour libre après le dernier post programmé, à 12:00 heure de Paris. Ne double jamais un créneau déjà pris.
- Planifie avec l'action code_action_metricoolcliapi__schedule_reel_with_providers (paramètres : blog_id 6704763, user_id 3689627, networks tiktok, date_time AAAA-MM-JJT12:00:00, auto_publish true, draft false, privacy_option PUBLIC_TO_EVERYONE, ai_generated true, media_url = l'URL de la vidéo 1080p, text = la légende). N'utilise pas l'action schedule_post standard : elle échoue avec « You need to include at least one provider ».
- Légende : hook de la vidéo reformulé + le mécanisme en une ligne + « Abonne-toi — demain : [sujet suivant] » + 6 hashtags maximum dont #corpshumain #lesavaistu #apprendresurtiktok.
- Revérifie ensuite avec list_scheduled_posts DEUX choses : que la date enregistrée est bien celle voulue (bug de fuseau connu), et que tiktokData.privacyOption est bien présent sur le post. Un post sans ce champ est accepté par Metricool puis rejeté par TikTok à l'heure dite, sans aucune alerte — c'est ce qui a fait perdre la vidéo 001.

## 4. Archiver et livrer

Dans videos/NNN-motcle/ : script_manifest.json, final.srt, final.mp4.assembly.json, run.json (ids de jobs, mesures de voix, incidents rencontrés) et un README.md sur le modèle de la vidéo 003. Coche le sujet dans publication/file-attente-sujets.md, ajoute la ligne du post dans le tableau de publication/pack-publication.md, et si tu découvres un nouveau piège technique, écris la règle dans channel_dna.json — c'est ce qui fait que la chaîne s'améliore.

Commit et push sur la branche. Termine par un message court : le lien de la vidéo, la date de publication, et tout point qui mérite l'attention de Maxime.

## Si ça bloque

Ne livre jamais une vidéo à moitié faite. Si une étape échoue après des essais raisonnables (modération qui refuse un asset, assemblage impossible, Metricool indisponible), arrête-toi, explique précisément ce qui a échoué et ce que tu as tenté, et laisse le travail déjà fait committé pour qu'on puisse reprendre. Les sous-titres sont la seule exception : si le burn est vraiment impossible, livre la vidéo sans sous-titres et signale-le.
```

## Ce que la routine sait déjà éviter

Ces règles sont dans le prompt parce qu'elles ont coûté du temps en production :

| Piège | Symptôme | Correctif inscrit |
|---|---|---|
| Débit de la voix française | prise hors fenêtre alors que `rate=ok` | deux prises par ligne, on garde la bonne |
| Registre de langue | les deux prises ratent du même côté | phrase familière = lue vite, soutenue = lue lentement |
| Publication TikTok | post PENDING puis `ERROR` silencieux | `privacyOption` obligatoire + relecture après création |
| Élisions et sous-titres | burn refusé, similarité ~0,63 | max 1-2 apostrophes par ligne |
| Action Metricool standard | « at least one provider » | utiliser `schedule_reel_with_providers` |
| Recommandeur de preset vidéo | `submission_failed` sur les 4 blocs | `declined_preset_id` pré-appliqué |
| Sandbox éphémère | fichiers disparus entre deux appels | tout enchaîner dans un seul appel |
| Modération sur l'anatomie | faux positifs `nsfw` sur le thorax | reformuler (« breathing system » plutôt que « chest ») |

## Surveillance

La routine envoie une notification push à chaque exécution. En cas d'échec elle s'arrête proprement
et laisse le travail committé — il suffit alors de reprendre en demandant « reprends la vidéo du jour ».
