# Routine quotidienne — ExpliqueMoi

**État : créée le 2026-08-13, id `trig_01Mu7zmXeawv4pQeyfkReSM7`, tous les jours à 06:00 heure de Paris (04:00 UTC).**

> ⚠️ **Action requise avant qu'elle serve à quelque chose.** Le planificateur a créé la routine
> **sans les connecteurs** Higgsfield et Zapier/Metricool. Une session qui démarre sans eux ne peut
> ni générer la vidéo ni la planifier : elle se réveillerait pour rien.
>
> **Correctif (2 min)** : ouvrir claude.ai → **Routines** → « ExpliqueMoi — vidéo quotidienne » →
> attacher les connecteurs **Higgsfield** et **Zapier** (et GitHub si proposé), puis enregistrer.
> Si la routine n'est pas modifiable, la recréer depuis cette même interface en collant le prompt
> ci-dessous — c'est le seul chemin qui attache les connecteurs de façon fiable.
>
> Tant que ce n'est pas fait, la production quotidienne reste manuelle (il suffit de me demander
> « lance la vidéo du jour »).

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

Deux pièges déjà rencontrés, à respecter sans exception :
- Débit voix : la voix Ainsley lit vite en français. Vise 24-28 mots par ligne de 10 s, pas la bande nominale du workflow. Mesure chaque prise avec speech_metrics.sh ; vise rate=ok et zéro pause interne >= 0,8 s. Budget de 3 essais par ligne, ensuite garde la meilleure et signale-le.
- Sous-titres : l'aligneur casse sur les élisions françaises (voir regle_sous_titres_fr dans channel_dna.json). Maximum 1 à 2 apostrophes ou traits d'union par ligne, surtout sur la ligne du CTA. Si le burn est refusé pour cause de similarité, ne change pas de modèle Whisper — réécris la ligne avec moins d'apostrophes.

Le sandbox Higgsfield est éphémère : enchaîne téléchargements, assemblage et upload dans un seul appel, et relance depuis les URLs si tu perds les fichiers.

## 3. Planifier la publication

- Liste d'abord les posts déjà programmés : action Zapier Metricool code_action_metricoolcliapi__list_scheduled_posts, blogId 6704763 (marque ExpliqueMoi), sur les 10 prochains jours.
- Choisis le premier jour libre après le dernier post programmé, à 12:00 heure de Paris. Ne double jamais un créneau déjà pris.
- Planifie avec l'action code_action_metricoolcliapi__schedule_reel_with_providers (paramètres : blog_id 6704763, user_id 3689627, networks tiktok, date_time AAAA-MM-JJT12:00:00, auto_publish true, draft false, media_url = l'URL de la vidéo 1080p, text = la légende). N'utilise pas l'action schedule_post standard : elle échoue avec « You need to include at least one provider ».
- Légende : hook de la vidéo reformulé + le mécanisme en une ligne + « Abonne-toi — demain : [sujet suivant] » + 6 hashtags maximum dont #corpshumain #lesavaistu #apprendresurtiktok.
- Revérifie ensuite avec list_scheduled_posts que la date enregistrée est bien celle voulue (bug de fuseau connu).

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
| Débit de la voix française | `rate=RUSHED` malgré une durée correcte | 24-28 mots par ligne, pas 27-32 |
| Élisions et sous-titres | burn refusé, similarité ~0,63 | max 1-2 apostrophes par ligne |
| Action Metricool standard | « at least one provider » | utiliser `schedule_reel_with_providers` |
| Recommandeur de preset vidéo | `submission_failed` sur les 4 blocs | `declined_preset_id` pré-appliqué |
| Sandbox éphémère | fichiers disparus entre deux appels | tout enchaîner dans un seul appel |
| Modération sur l'anatomie | faux positifs `nsfw` sur le thorax | reformuler (« breathing system » plutôt que « chest ») |

## Surveillance

La routine envoie une notification push à chaque exécution. En cas d'échec elle s'arrête proprement
et laisse le travail committé — il suffit alors de reprendre en demandant « reprends la vidéo du jour ».
