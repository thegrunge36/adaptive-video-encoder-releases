> 🇫🇷 **Français** ci-dessous · 🇬🇧 **English** follows below
>
> *La version française est en premier. / The French version comes first.*
---

# 🎬 Adaptive Video Encoder

> **L'encodeur H.265 qui ne casse pas votre Dolby Vision.**

[![Site web](https://img.shields.io/badge/Site%20web-adaptive--encoder.com-2D8CFF?logo=googlechrome&logoColor=white)](https://adaptive-encoder.com) [![Essai gratuit](https://img.shields.io/badge/Essai%20gratuit-7%20jours-22C55E)](https://adaptive-video-encoder.lemonsqueezy.com/checkout/buy/7f26ba5d-c99c-4af7-8a08-63258326a38a) [![Licence à vie](https://img.shields.io/badge/Licence%20%C3%A0%20vie-%2449.99%20CAD-004577)](https://adaptive-video-encoder.lemonsqueezy.com/checkout/buy/27660616-8926-4588-b00d-fe9a7c48e9da) [![Discord](https://img.shields.io/badge/Discord-Rejoindre-5865F2?logo=discord&logoColor=white)](https://discord.gg/UHrEn2H6jD)

> ⚠️ **Logiciel propriétaire, licence requise.**
>
> Ce dépôt **ne contient pas de code source** : seules les versions compilées (binaires) sont distribuées. L'application **ne fonctionne pas sans clé de licence valide** (ou un essai gratuit de 7 jours actif) ; l'activation se fait au lancement. Procurez-vous une clé sur **[adaptive-video-encoder.lemonsqueezy.com](https://adaptive-video-encoder.lemonsqueezy.com/checkout/buy/27660616-8926-4588-b00d-fe9a7c48e9da)**.

---

## Réencodez votre vidéothèque sans compromis de qualité

Vous avez une vidéothèque pleine de remux Blu-ray 1080p, de rips Dolby Vision 4K, de sources HDR10 ou HLG. Vous voulez réencoder en H.265 pour récupérer des téraoctets, sans détruire les métadonnées qui font s'afficher vos films correctement sur votre OLED.

**Le problème :** La plupart des outils H.265 suppriment les métadonnées Dolby Vision Profil 7 ou lissent le grain par défaut. Trouver les bons réglages demande des heures de tests, et ces réglages changent pour chaque vidéo (grain, bruit, mouvement, complexité).

**La solution :** Adaptive Video Encoder analyse chaque vidéo image par image *avant* l'encodage, choisit automatiquement les meilleurs paramètres, et préserve intégralement votre Dolby Vision (Profil 5, 7, 8.x), ainsi que les métadonnées HDR10 et HLG. Le tout depuis une **interface graphique simple**, sur Windows, Linux et macOS.

> 💡 **Philosophie :** Adaptive Video Encoder privilégie la **préservation maximale du détail, du grain et des métadonnées HDR** sur la compression agressive. L'objectif est une qualité proche du remux, pas le meilleur ratio taille/qualité absolu.

---

## 🎯 Fait pour vous si...

**Bibliothèques Blu-ray 1080p :**

- Vous archivez des remux Blu-ray 1080p et voulez préserver le grain cinématique (films d'horreur, classiques, films d'auteur en 35mm)
- Vous avez des sources HDR10 1080p que les encodeurs génériques gèrent mal
- Vous voulez préserver chaque détail des scènes complexes (action, fantastique, sci-fi)

**Bibliothèques UHD 4K :**

- Vous archivez des Blu-rays UHD avec Dolby Vision et voulez une qualité maximale
- Vous gérez des sources HDR10 ou HLG sans calibrer chaque film manuellement

**Tous formats :**

- Vous privilégiez la qualité d'image sur les économies d'espace disque
- Vous voulez une interface graphique simple, sans paramètres à mémoriser
- Vous en avez marre de régler les paramètres x265 et de comparer 12 versions du même film

## ⚠️ Pas pour vous si...

- Vous cherchez une compression maximale pour économiser l'espace disque
- Vous encodez surtout du contenu SDR simple sans grain (comédies récentes en intérieur, animation fluide, talking heads) ; dans ces cas, des outils plus simples donnent souvent de meilleurs taux de compression
- Vous avez besoin d'un encodage rapide (l'outil privilégie la qualité, pas la vitesse)

---

## 💰 Essai gratuit 7 jours · Licence à vie

Adaptive Video Encoder est disponible avec un **essai gratuit de 7 jours**, sans engagement. Ensuite, une **licence à vie débloque l'outil définitivement : pas d'abonnement, mises à jour incluses.

👉 **[Démarrer l'essai gratuit](https://adaptive-video-encoder.lemonsqueezy.com/checkout/buy/7f26ba5d-c99c-4af7-8a08-63258326a38a)** · **[Acheter ·](https://adaptive-video-encoder.lemonsqueezy.com/checkout/buy/27660616-8926-4588-b00d-fe9a7c48e9da)**

💬 **Questions avant d'acheter ? Rejoignez le [Discord](https://discord.gg/UHrEn2H6jD)**, avec plaisir.

---

## ⚡ Pourquoi un encodeur adaptatif dédié ?

|  | Encodeurs génériques | Réglage manuel | **Adaptive Video Encoder** |
| --- | --- | --- | --- |
| Dolby Vision Profil 7 | ❌ Cassé | ⚠️ Possible, mais complexe | ✅ Automatique |
| Préservation du grain | ❌ Lissé par défaut | ⚠️ Si vous savez quoi activer | ✅ Préservé automatiquement |
| Paramètres adaptés *par vidéo* | ❌ Préréglages fixes | ⚠️ Si vous testez vous-même | ✅ Analyse image par image |
| Qualité garantie (VMAF) | ❌ | ⚠️ Scripts à monter soi-même | ✅ En un clic |
| HDR10 / HLG préservé | ⚠️ Parfois | ⚠️ Si vous savez quoi activer | ✅ Toujours |
| Détection des bandes noires | ✅ | ⚠️ Manuel | ✅ Automatique |
| Dépendances à installer | ⚠️ Souvent | ⚠️ Souvent | ✅ Aucune (tout intégré) |
| Temps de configuration | 5 min | 1-3 h par film | **0 min** |

---

## 📏 Nouveau : la qualité mesurée, pas devinée (Cible VMAF)

En un clic, la qualité passe de *prédite* à **mesurée**. L'outil encode des extraits répartis sur tout le film, note chaque essai avec **VMAF**, la métrique perceptuelle développée par Netflix, puis retient le réglage le plus économe qui atteint le score demandé. Le fichier livré ne « devrait pas » être bon : il l'est, mesure à l'appui.

- Repères : **93** = compact · **95** = élevé · **97** = quasi transparent
- La mesure reproduit l'encodage final à l'identique (recadrage, débruitage, tone mapping, réglages psychovisuels) : seule la compression réellement obtenue est notée
- Fonctionne avec les trois codecs et n'ajoute que quelques minutes par film

---

## 🎞️ Particulièrement excellent sur les Blu-rays 1080p

Beaucoup d'utilisateurs pensent à tort que cet outil est réservé à la 4K. **Ce n'est pas le cas.** Adaptive Video Encoder brille particulièrement sur les remux Blu-ray 1080p pour 3 raisons :

**1. Préservation du grain cinématique.** Les films classiques, les films d'horreur, les films d'auteur récents en 35mm ont un grain qui fait partie de leur identité visuelle. La plupart des encodeurs le lissent par défaut. Adaptive Encoder le détecte, le préserve et va jusqu'à adapter le budget de compression au grain mesuré.

**2. Détection adaptative des scènes complexes.** Sur un film d'action 1080p, les scènes de combat ont une complexité radicalement différente des dialogues. L'analyse image par image ajuste les paramètres en conséquence, là où les encodeurs génériques utilisent les mêmes réglages du début à la fin.

**3. Préservation des métadonnées HDR10 1080p.** Certains Blu-rays récents ont le HDR10 en 1080p. Adaptive Encoder préserve tout : master display, MaxCLL/MaxFALL, primaires de couleur.

**Moins pertinent pour :** le contenu numérique récent avec une image propre (comédies romantiques, sitcoms, documentaires en intérieur). Ces sources n'ont ni grain ni détail complexe à préserver.

---

## 🧠 Pourquoi l'encodage CPU plutôt que GPU ?

Réponse courte : **NVENC, QuickSync et AMF sont conçus pour la vitesse, pas la qualité.**

|  | GPU (NVENC / QSV / AMF) | **CPU (x265 / SVT-AV1)** |
| --- | --- | --- |
| Vitesse d'encodage | ⚡⚡⚡ Rapide | 🐢 Lent |
| Qualité par bit | ⚠️ Correct | ✅ Excellent |
| Taille finale du fichier | ⚠️ Plus lourde | ✅ Plus légère |
| Cas d'usage idéal | Streaming live, capture temps réel | **Archivage, vidéothèque** |

**Pour archiver une bibliothèque, la vitesse n'a pas d'importance : vous encodez une fois, vous regardez 100 fois.**

---

## ✨ Ce que ça fait

- 🖥️ **Interface graphique native** : Windows, Linux et macOS (Apple Silicon)
- 🎬 **Trois codecs** : HEVC (défaut), AV1 et H.264, avec une qualité visuelle alignée entre les trois
- 📏 **Cible VMAF** : qualité mesurée et garantie, en un clic
- 🔍 **Analyse adaptative** : détecte le bruit, le grain, la complexité, la densité de contours pour régler l'encodage
- 📺 **Dolby Vision Profil 5, 7, 8.x** : métadonnées extraites, préservées, réinjectées
- 🎨 **HDR10 et HLG** : primaires de couleur, transferts, master display, MaxCLL/MaxFALL préservés
- 🎞️ **Préservation du grain** : pellicule 35mm, films d'horreur, sources granuleuses gérées automatiquement ; le grain réel n'est plus lissé, même en AV1
- ✂️ **Recadrage intelligent** : détecte les bandes noires sans couper accidentellement le contenu
- 🔊 **Toutes les pistes audio et sous-titres** copiées par défaut, zéro perte
- 🎞️ **Formats supportés** : MKV, MP4, MOV, AVI, MXF, WebM, M4V, TS
- 📐 **Résolutions** : 480p à 8K (excellent pour 1080p ET 4K)
- 📦 **Tout intégré** : aucune dépendance à installer, aucune configuration. Téléchargez, lancez, encodez.

---

## 💻 Plateformes supportées

| Plateforme | Statut | Notes |
| --- | --- | --- |
| 🐧 Linux (x64) | ✅ Supporté | Ubuntu 22.04+, Debian 12+, Fedora 40+ |
| 🪟 Windows 10/11 (x64) | ✅ Supporté | Interface graphique native |
| 🍎 macOS (Apple Silicon) | ✅ Supporté | M1, M2, M3, binaire natif arm64 |

---

## ⚙️ Installation

**Aucune dépendance à installer.** Tout est intégré à l'application (ffmpeg, ffprobe et l'ensemble des outils nécessaires). Téléchargez la version correspondant à votre plateforme et lancez-la : c'est tout.

**macOS :** si un avertissement « éditeur non identifié » apparaît au premier lancement, faites un **clic droit (ou Ctrl-clic) sur l'application → Ouvrir → Ouvrir**. Une seule fois ; macOS ne vous redemandera plus.

**Activation :** au premier lancement, démarrez votre **essai gratuit de 7 jours** ou entrez la **clé de licence** reçue par email après l'achat sur [adaptive-video-encoder.lemonsqueezy.com](https://adaptive-video-encoder.lemonsqueezy.com/checkout/buy/27660616-8926-4588-b00d-fe9a7c48e9da).

---

## 🚀 Démarrage rapide

1. **Lancez l'application.**
2. **Glissez-déposez votre fichier vidéo** dans la fenêtre (ou parcourez pour le sélectionner).
3. **Ajustez les réglages** si vous le souhaitez ; sinon, les valeurs automatiques conviennent à la plupart des sources.
4. **Cliquez sur Encoder.** L'analyse de la vidéo s'affiche, puis l'encodage démarre avec la progression en temps réel.

> 💡 **Conseil :** le Dolby Vision et le HDR sont détectés et affichés avant l'encodage : vous voyez tout de suite ce qui sera préservé.

---

## 🎛️ Principaux réglages (dans l'interface)

Tout se règle visuellement ; aucune ligne de commande. Parmi les options disponibles :

- **Codec** : HEVC (défaut), AV1 ou H.264 selon la compatibilité visée
- **Cible VMAF** : score de qualité garanti, mesuré sur des extraits du film
- **Qualité cible** : plus haute pour une fidélité maximale, plus basse pour un fichier plus léger
- **Débit maximum** optionnel pour plafonner la taille des fichiers
- **Préréglage vitesse / qualité** : jusqu'au mode le plus lent et le plus précis
- **Tune** : préservation du grain, ou optimisation pour l'animation et les aplats
- **Dolby Vision** : activer / désactiver, avec option de préservation stricte du profil source
- **Réduction de bruit** : automatique, ajustable, avec préservation du grain et choix du moteur
- **Recadrage automatique** des bandes noires (activable / désactivable)
- **Downscale 1080p + conversion SDR** (tone mapping) pour les écrans non-HDR
- **Conversion de fréquence d'images** pour une synchronisation audio/vidéo parfaite
- **Audio** : tout conserver, filtrer par langue, ou downmix 7.1 / Atmos → 5.1 / 2.0
- **Sous-titres** : conserver ou retirer

---

## ❓ FAQ

**Combien ça coûte ?** L'outil est disponible avec un essai gratuit de 7 jours. Ensuite, une licence à vie coûte $49.99 CAD, soit environ 35 $ US ou 31 € selon le taux de change : paiement unique, pas d'abonnement. Achat sur [adaptive-video-encoder.lemonsqueezy.com](https://adaptive-video-encoder.lemonsqueezy.com/checkout/buy/27660616-8926-4588-b00d-fe9a7c48e9da).

**Comment fonctionne l'essai gratuit ?** Téléchargez l'application et essayez toutes les fonctionnalités pendant 7 jours, sans engagement.

**C'est quoi, la « Cible VMAF » ?** Un mode optionnel qui garantit la qualité au lieu de l'estimer : l'outil encode des extraits du film, mesure la qualité réelle de chaque essai avec VMAF (la métrique perceptuelle de Netflix) et retient le réglage le plus économe qui atteint le score demandé. Cochez la case, choisissez un score (95 par défaut), c'est tout.

**Le code source est-il disponible ?** Non. L'application est propriétaire ; seules les versions compilées sont distribuées sur GitHub (versions + issues). Elle nécessite une clé de licence valide (ou un essai actif) pour s'exécuter.

**Dois-je installer quelque chose d'autre ?** Non. Aucune dépendance : tout est intégré à l'application. Téléchargez, lancez, activez.

**Y a-t-il une interface graphique ?** Oui, c'est même la seule façon d'utiliser l'outil. Interface graphique native sur Windows, Linux et macOS.

**Quelles plateformes sont supportées ?** Windows 10/11 (x64), Linux (x64), et macOS Apple Silicon (M1/M2/M3). Tout est intégré, rien à installer en plus.

**C'est seulement pour la 4K ?** Non, l'outil est excellent en 1080p aussi. Particulièrement sur les remux Blu-ray avec grain cinématique (classiques, horreur, films d'auteur 35mm) ou les scènes complexes (action, sci-fi).

**Le Dolby Vision est-il géré automatiquement ?** Oui. L'extraction, la préservation et la réinjection des métadonnées sont automatiques et intégrées : rien à installer ni configurer.

**La conversion Profil 7 → 8.1 fonctionne ?** Oui, c'est le comportement par défaut. Le Profil 7 (FEL/MEL) est extrait et réinjecté en 8.1, compatible avec la plupart des lecteurs Dolby Vision modernes.

**Pourquoi mes fichiers sont-ils plus lourds qu'avec d'autres encodeurs ?** Choix de conception délibéré : préservation maximale du détail et des métadonnées HDR. Pour limiter la taille, un réglage de débit maximum est disponible dans l'interface, ou visez un score Cible VMAF plus bas (93) pour un résultat plus compact à qualité mesurée.

**Vitesse d'encodage ?** L'outil privilégie la qualité à la vitesse. Un réglage de préréglage plus rapide est disponible dans l'interface si vous préférez accélérer.

**Et si ça ne fonctionne pas sur mes fichiers ?** Ouvrez une issue sur GitHub ou posez la question sur Discord, avec plaisir.

---

## 📧 Support

- 🌐 **Site web** : <https://adaptive-encoder.com>
- 💬 **Discord** (réponses rapides) : <https://discord.gg/UHrEn2H6jD>
- 📧 **Email** : <osx300@gmail.com>

---

---

# 🎬 Adaptive Video Encoder (English)

> **The H.265 encoder that doesn't break your Dolby Vision.**

[![Website](https://img.shields.io/badge/Website-adaptive--encoder.com-2D8CFF?logo=googlechrome&logoColor=white)](https://adaptive-encoder.com) [![Free trial](https://img.shields.io/badge/Free%20trial-7%20days-22C55E)](https://adaptive-video-encoder.lemonsqueezy.com/checkout/buy/7f26ba5d-c99c-4af7-8a08-63258326a38a) [![Lifetime license](https://img.shields.io/badge/Lifetime%20license-%2449.99%20CAD-004577)](https://adaptive-video-encoder.lemonsqueezy.com/checkout/buy/27660616-8926-4588-b00d-fe9a7c48e9da) [![Discord](https://img.shields.io/badge/Discord-Join-5865F2?logo=discord&logoColor=white)](https://discord.gg/UHrEn2H6jD)

> ⚠️ **Proprietary software, license required.**
>
> This repository **contains no source code**: only compiled (binary) releases are distributed. The application **will not run without a valid license key** (or an active 7-day free trial); activation happens on launch. Get a key at **[adaptive-video-encoder.lemonsqueezy.com](https://adaptive-video-encoder.lemonsqueezy.com/checkout/buy/27660616-8926-4588-b00d-fe9a7c48e9da)**.

---

## Re-encode your video library without quality compromise

You have a video library full of 1080p Blu-rays, 4K Dolby Vision rips, HDR10 or HLG sources. You want to re-encode to H.265 to reclaim terabytes without destroying the metadata that makes your movies display correctly on your OLED.

**The problem:** Most H.265 tools strip out Dolby Vision Profile 7 metadata or smooth grain by default. Finding the right settings takes hours of testing, and those settings change for every video (grain, noise, motion, complexity).

**The solution:** Adaptive Video Encoder analyzes each video frame by frame *before* encoding, automatically picks the best parameters, and fully preserves your Dolby Vision (Profile 5, 7, 8.x), HDR10 and HLG metadata, all from a **simple graphical interface** on Windows, Linux and macOS.

> 💡 **Philosophy:** Adaptive Video Encoder prioritizes **maximum preservation of detail, grain, and HDR metadata** over aggressive compression. The goal is near-remux quality, not the absolute best size/quality ratio.

---

## 🎯 Built for you if...

**1080p Blu-ray libraries:**

- You archive 1080p Blu-ray remuxes and want to preserve film grain (horror movies, classics, 35mm auteur films)
- You have HDR10 1080p sources that generic encoders handle poorly
- You want to preserve every fine detail of complex scenes (action, fantasy, sci-fi)

**4K UHD libraries:**

- You archive UHD Blu-rays with Dolby Vision and want maximum quality
- You handle HDR10 or HLG without manually calibrating each film

**All formats:**

- You value image quality over disk space savings
- You want a simple graphical interface, with nothing to memorize
- You're tired of tweaking x265 parameters and comparing 12 versions of the same film

## ⚠️ Not for you if...

- You're looking for maximum compression to save disk space
- You mostly encode simple SDR content without grain (recent indoor comedies, smooth animation, talking heads); for those cases, simpler tools often give better compression ratios
- You need fast encoding (the tool prioritizes quality, not speed)

---

## 💰 7-day free trial · Lifetime license

Adaptive Video Encoder comes with a **7-day free trial**, no commitment. After that, a lifetime license unlocks the tool forever: no subscription, updates included.

👉 **[Start the free trial](https://adaptive-video-encoder.lemonsqueezy.com/checkout/buy/7f26ba5d-c99c-4af7-8a08-63258326a38a)** · **[Buy ·](https://adaptive-video-encoder.lemonsqueezy.com/checkout/buy/27660616-8926-4588-b00d-fe9a7c48e9da)**

💬 **Questions before buying? Join the [Discord](https://discord.gg/UHrEn2H6jD)**, happy to help.

---

## ⚡ Why a dedicated adaptive encoder?

|  | Generic encoders | Manual tuning | **Adaptive Video Encoder** |
| --- | --- | --- | --- |
| Dolby Vision Profile 7 | ❌ Broken | ⚠️ Possible, but complex | ✅ Automatic |
| Grain preservation | ❌ Smoothed by default | ⚠️ If you know what to flag | ✅ Preserved automatically |
| Settings adapted *per video* | ❌ Fixed presets | ⚠️ If you test yourself | ✅ Frame-by-frame analysis |
| Guaranteed quality (VMAF) | ❌ | ⚠️ DIY scripts | ✅ One click |
| HDR10 / HLG preserved | ⚠️ Sometimes | ⚠️ If you know what to flag | ✅ Always |
| Black bar detection | ✅ | ⚠️ Manual | ✅ Automatic |
| Dependencies to install | ⚠️ Often | ⚠️ Often | ✅ None (all bundled) |
| Setup time | 5 min | 1-3 h per film | **0 min** |

---

## 📏 New: quality that's measured, not guessed (Target VMAF)

With one click, quality goes from *predicted* to **measured**. The tool encodes clips sampled across the whole film, scores each attempt with **VMAF**, the perceptual metric developed by Netflix, then keeps the most economical setting that reaches the requested score. The delivered file isn't "supposed to" look good: it does, with the measurement to prove it.

- Reference points: **93** = compact · **95** = high · **97** = near-transparent
- The measurement reproduces the final encode exactly (crop, denoising, tone mapping, psychovisual settings): only the compression actually obtained is scored
- Works with all three codecs and only adds a few minutes per film

---

## 🎞️ Particularly excellent on 1080p Blu-rays

Many users mistakenly think this tool is only for 4K. **It's not.** Adaptive Video Encoder shines particularly well on 1080p Blu-ray remuxes for 3 reasons:

**1. Film grain preservation.** Classic films, horror movies, recent 35mm auteur films have grain that's part of their visual identity. Most encoders smooth it by default. Adaptive Encoder detects it, preserves it, and even adapts the compression budget to the measured grain.

**2. Adaptive complex scene detection.** On a 1080p action film, fight scenes have radically different complexity than dialogue. Frame-by-frame analysis adjusts parameters accordingly, where generic encoders use the same settings start to finish.

**3. 1080p HDR10 metadata preservation.** Some recent Blu-rays have HDR10 in 1080p. Adaptive Encoder preserves everything: master display, MaxCLL/MaxFALL, color primaries.

**Less relevant for:** recently-shot digital content with clean image (romantic comedies, sitcoms, indoor documentaries). Those sources have neither grain nor complex detail to preserve.

---

## 🧠 Why CPU encoding instead of GPU?

Short answer: **NVENC, QuickSync and AMF are designed for speed, not quality.**

|  | GPU (NVENC / QSV / AMF) | **CPU (x265 / SVT-AV1)** |
| --- | --- | --- |
| Encoding speed | ⚡⚡⚡ Fast | 🐢 Slow |
| Quality per bit | ⚠️ Decent | ✅ Excellent |
| Final file size | ⚠️ Larger | ✅ Smaller |
| Ideal use case | Live streaming, real-time capture | **Archival, video library** |

**For archiving a library, speed doesn't matter: you encode once, watch 100 times.**

---

## ✨ What it does

- 🖥️ **Native graphical interface**: Windows, Linux and macOS (Apple Silicon)
- 🎬 **Three codecs**: HEVC (default), AV1 and H.264, with visual quality aligned across all three
- 📏 **Target VMAF**: measured, guaranteed quality in one click
- 🔍 **Adaptive analysis**: detects noise, grain, complexity, edge density to tune the encode
- 📺 **Dolby Vision Profile 5, 7, 8.x**: metadata extracted, preserved, reinjected
- 🎨 **HDR10 and HLG**: color primaries, transfers, master display, MaxCLL/MaxFALL preserved
- 🎞️ **Grain preservation**: 35mm film, horror movies, grainy sources handled automatically; real grain is no longer smoothed away, even in AV1
- ✂️ **Smart crop**: detects black bars without accidentally cutting content
- 🔊 **All audio and subtitle tracks** copied by default, zero loss
- 🎞️ **Supported formats**: MKV, MP4, MOV, AVI, MXF, WebM, M4V, TS
- 📐 **Resolutions**: 480p to 8K (excellent for 1080p AND 4K)
- 📦 **Everything bundled**: no dependencies, no configuration. Download, launch, encode.

---

## 💻 Platform support

| Platform | Status | Notes |
| --- | --- | --- |
| 🐧 Linux (x64) | ✅ Supported | Ubuntu 22.04+, Debian 12+, Fedora 40+ |
| 🪟 Windows 10/11 (x64) | ✅ Supported | Native graphical interface |
| 🍎 macOS (Apple Silicon) | ✅ Supported | M1, M2, M3, native arm64 binary |

---

## ⚙️ Installation

**No dependencies to install.** Everything is bundled inside the app (ffmpeg, ffprobe and all required tools). Download the build for your platform and launch it: that's it.

**macOS:** if an "unidentified developer" warning appears on first launch, **right-click (or Ctrl-click) the app → Open → Open**. Once only; macOS won't ask again.

**Activation:** on first launch, start your **7-day free trial** or enter the **license key** you received by email after purchasing on [adaptive-video-encoder.lemonsqueezy.com](https://adaptive-video-encoder.lemonsqueezy.com/checkout/buy/27660616-8926-4588-b00d-fe9a7c48e9da).

---

## 🚀 Quick start

1. **Launch the app.**
2. **Drag and drop your video file** into the window (or browse to select it).
3. **Adjust the settings** if you like; otherwise the automatic values suit most sources.
4. **Click Encode.** The video analysis is shown, then encoding starts with real-time progress.

> 💡 **Tip:** Dolby Vision and HDR are detected and displayed before encoding: you immediately see what will be preserved.

---

## 🎛️ Key settings (in the app)

Everything is set visually; no command line. Available options include:

- **Codec**: HEVC (default), AV1 or H.264 depending on the compatibility you need
- **Target VMAF**: a guaranteed quality score, measured on clips from the film
- **Target quality**: higher for maximum fidelity, lower for a smaller file
- **Maximum bitrate** (optional) to cap file size
- **Speed / quality preset**: up to the slowest, most precise mode
- **Tune**: preserve film grain, or optimize for animation and flat areas
- **Dolby Vision**: enable / disable, with an option to strictly preserve the source profile
- **Noise reduction**: automatic, adjustable, with grain preservation and engine choice
- **Automatic crop** of black bars (toggle on / off)
- **1080p downscale + SDR conversion** (tone mapping) for non-HDR displays
- **Frame rate conversion** for perfect audio/video sync
- **Audio**: keep everything, filter by language, or downmix 7.1 / Atmos → 5.1 / 2.0
- **Subtitles**: keep or remove

---

## ❓ FAQ

**How much does it cost?** The tool comes with a 7-day free trial. After that, a lifetime license costs $49.99 CAD, about $35 USD or €31 depending on the exchange rate: one-time payment, no subscription. Purchase at [adaptive-video-encoder.lemonsqueezy.com](https://adaptive-video-encoder.lemonsqueezy.com/checkout/buy/27660616-8926-4588-b00d-fe9a7c48e9da).

**How does the free trial work?** Download the app and try all features for 7 days, no commitment.

**What is "Target VMAF"?** An optional mode that guarantees quality instead of estimating it: the tool encodes clips from the film, measures the real quality of each attempt with VMAF (Netflix's perceptual metric) and keeps the most economical setting that reaches the requested score. Tick the box, pick a score (95 by default), done.

**Is the source code available?** No. The application is proprietary; only compiled releases are distributed on GitHub (releases + issues). It requires a valid license key (or an active trial) to run.

**Do I need to install anything else?** No. Zero dependencies: everything is bundled inside the app. Download, launch, activate.

**Is there a graphical interface?** Yes, it's the only way to use the tool. Native graphical interface on Windows, Linux and macOS.

**What platforms are supported?** Windows 10/11 (x64), Linux (x64), and macOS Apple Silicon (M1/M2/M3). Everything is bundled, nothing extra to install.

**Is this only for 4K?** No, the tool is excellent for 1080p too. Particularly on Blu-ray remuxes with film grain (classics, horror, 35mm auteur films) or complex scenes (action, sci-fi).

**Is Dolby Vision handled automatically?** Yes. Metadata extraction, preservation and reinjection are automatic and built in: nothing to install or configure.

**Does Profile 7 → 8.1 conversion work?** Yes, it's the default. Profile 7 (FEL/MEL) is extracted and reinjected as 8.1, compatible with most modern Dolby Vision players.

**Why are my files larger than with other encoders?** Intentional design choice: maximum detail and HDR metadata preservation. To cap file size, a maximum-bitrate setting is available in the app, or aim for a lower Target VMAF score (93) for a more compact result at measured quality.

**Encoding speed?** The tool prioritizes quality over speed. A faster preset setting is available in the app if you'd rather speed things up.

**What if it doesn't work for my files?** Open an issue on GitHub or ask on Discord, happy to help.

---

## 📧 Support

- 🌐 **Website**: <https://adaptive-encoder.com>
- 💬 **Discord** (fast replies): <https://discord.gg/UHrEn2H6jD>
- 📧 **Email**: <osx300@gmail.com>
