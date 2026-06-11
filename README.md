> 🇫🇷 **Français** ci-dessous — 🇬🇧 **English** follows below
>
> *La version française est en premier. / The French version comes first.*
---

# 🎬 Adaptive Video Encoder

> **L'encodeur H.265 qui ne casse pas votre Dolby Vision.**

[![Site web](https://img.shields.io/badge/Site%20web-adaptive--encoder.com-2D8CFF?logo=googlechrome&logoColor=white)](https://adaptive-encoder.com) [![Essai gratuit](https://img.shields.io/badge/Essai%20gratuit-7%20jours-22C55E)](https://adaptive-video-encoder.lemonsqueezy.com) [![Licence à vie](https://img.shields.io/badge/Licence%20%C3%A0%20vie-%2449.99-004577)](https://adaptive-video-encoder.lemonsqueezy.com) [![Discord](https://img.shields.io/badge/Discord-Rejoindre-5865F2?logo=discord&logoColor=white)](https://discord.gg/UHrEn2H6jD)

---

## Réencodez votre vidéothèque sans compromis de qualité

Vous avez une vidéothèque pleine de remux Blu-ray 1080p, de rips Dolby Vision 4K, de sources HDR10 ou HLG. Vous voulez réencoder en H.265 pour récupérer des téraoctets — sans détruire les métadonnées qui font s'afficher vos films correctement sur votre OLED.

**Le problème :** La plupart des outils H.265 suppriment les métadonnées Dolby Vision Profil 7 ou lissent le grain par défaut. ffmpeg en manuel nécessite des heures de tests pour trouver les bons paramètres — et ces paramètres changent pour chaque vidéo (grain, bruit, mouvement, complexité).

**La solution :** Adaptive Video Encoder analyse chaque vidéo image par image *avant* l'encodage, choisit automatiquement les meilleurs paramètres x265, et préserve intégralement votre Dolby Vision (Profil 5, 7, 8.x), ainsi que les métadonnées HDR10 et HLG. Disponible avec une **interface graphique** sur Windows, Linux et macOS — et en ligne de commande pour l'automatisation.

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
- Vous voulez une interface graphique simple — ou la ligne de commande pour automatiser vos encodages
- Vous en avez marre de régler les paramètres x265 et de comparer 12 versions du même film

## ⚠️ Pas pour vous si...

- Vous cherchez une compression maximale pour économiser l'espace disque
- Vous encodez surtout du contenu SDR simple sans grain (comédies récentes en intérieur, animation fluide, talking heads) — dans ces cas, des outils plus simples donnent souvent de meilleurs taux de compression
- Vous avez besoin d'un encodage rapide (l'outil privilégie la qualité, pas la vitesse)

---

## 💰 Essai gratuit 7 jours · Licence à vie $49.99

Adaptive Video Encoder est disponible avec un **essai gratuit de 7 jours**, sans engagement. Ensuite, une **licence à vie à $49.99** débloque l'outil définitivement — pas d'abonnement, mises à jour incluses.

👉 **[Démarrer l'essai gratuit](https://adaptive-video-encoder.lemonsqueezy.com)** · **[Acheter — $49.99](https://adaptive-video-encoder.lemonsqueezy.com)**

💬 **Questions avant d'acheter ? Rejoignez le [Discord](https://discord.gg/UHrEn2H6jD)** — avec plaisir.

---

## ⚡ Pourquoi un encodeur adaptatif dédié ?

|  | Encodeurs génériques | ffmpeg manuel | **Adaptive Video Encoder** |
| --- | --- | --- | --- |
| Dolby Vision Profil 7 | ❌ Cassé | ⚠️ Possible avec `dovi_tool` + scripts | ✅ Automatique |
| Préservation du grain | ❌ Lissé par défaut | ⚠️ Si vous savez quoi activer | ✅ Préservé automatiquement |
| Paramètres adaptés *par vidéo* | ❌ Préréglages fixes | ⚠️ Si vous testez vous-même | ✅ Analyse image par image |
| HDR10 / HLG préservé | ⚠️ Parfois | ⚠️ Si vous savez quoi activer | ✅ Toujours |
| Détection des bandes noires | ✅ | ⚠️ Manuel | ✅ Automatique |
| Interface graphique | ✅ | ❌ | ✅ Windows · Linux · macOS |
| Temps de configuration | 5 min | 1-3 h par film | **0 min** |

---

## 🎞️ Particulièrement excellent sur les Blu-rays 1080p

Beaucoup d'utilisateurs pensent à tort que cet outil est réservé à la 4K. **Ce n'est pas le cas.** Adaptive Video Encoder brille particulièrement sur les remux Blu-ray 1080p pour 3 raisons :

**1. Préservation du grain cinématique.** Les films classiques, les films d'horreur, les films d'auteur récents en 35mm ont un grain qui fait partie de leur identité visuelle. La plupart des encodeurs le lissent par défaut. Adaptive Encoder le détecte et le préserve.

**2. Détection adaptative des scènes complexes.** Sur un film d'action 1080p, les scènes de combat ont une complexité radicalement différente des dialogues. L'analyse image par image ajuste les paramètres x265 en conséquence, là où les encodeurs génériques utilisent les mêmes réglages du début à la fin.

**3. Préservation des métadonnées HDR10 1080p.** Certains Blu-rays récents ont le HDR10 en 1080p. Adaptive Encoder préserve tout : master display, MaxCLL/MaxFALL, primaires de couleur.

**Moins pertinent pour :** le contenu numérique récent avec une image propre (comédies romantiques, sitcoms, documentaires en intérieur). Ces sources n'ont ni grain ni détail complexe à préserver.

---

## 🧠 Pourquoi l'encodage CPU plutôt que GPU ?

Réponse courte : **NVENC, QuickSync et AMF sont conçus pour la vitesse, pas la qualité.**

|  | GPU (NVENC / QSV / AMF) | **CPU (x265)** |
| --- | --- | --- |
| Vitesse d'encodage | ⚡⚡⚡ Rapide | 🐢 Lent |
| Qualité par bit | ⚠️ Correct | ✅ Excellent |
| Taille finale du fichier | ⚠️ Plus lourde | ✅ Plus légère |
| Cas d'usage idéal | Streaming live, capture temps réel | **Archivage, vidéothèque** |

**Pour archiver une bibliothèque, la vitesse n'a pas d'importance — vous encodez une fois, vous regardez 100 fois.**

---

## ✨ Ce que ça fait

- 🖥️ **Interface graphique native** — Windows, Linux et macOS (Apple Silicon)
- 🔍 **Analyse adaptative** — détecte le bruit, le grain, la complexité, la densité de contours pour régler x265
- 📺 **Dolby Vision Profil 5, 7, 8.x** — métadonnées extraites, préservées, réinjectées
- 🎨 **HDR10 et HLG** — primaires de couleur, transferts, master display, MaxCLL/MaxFALL préservés
- 🎞️ **Préservation du grain** — pellicule 35mm, films d'horreur, sources granuleuses gérées automatiquement
- ✂️ **Recadrage intelligent** — détecte les bandes noires sans couper accidentellement le contenu
- 🔊 **Toutes les pistes audio et sous-titres** copiées par défaut, zéro perte
- 🎞️ **Formats supportés** — MKV, MP4, MOV, AVI, MXF, WebM, M4V, TS
- 📐 **Résolutions** — 480p à 8K (excellent pour 1080p ET 4K)
- 📦 **Binaire unique** — ffmpeg et ffprobe intégrés. Aucune dépendance à installer.

---

## 💻 Plateformes supportées

| Plateforme | Statut | Notes |
| --- | --- | --- |
| 🐧 Linux (x64) | ✅ Supporté | Ubuntu 22.04+, Debian 12+, Fedora 40+ |
| 🪟 Windows 10/11 (x64) | ✅ Supporté | Interface graphique · PowerShell ou CMD |
| 🍎 macOS (Apple Silicon) | ✅ Supporté | M1, M2, M3 — binaire natif arm64 |

---

## ⚙️ Installation et prérequis

ffmpeg et ffprobe sont intégrés — inutile de les installer séparément. Cependant, **deux outils doivent être installés** avant d'utiliser l'encodeur :

### 1. mkvmerge — requis pour la sortie MKV

| Plateforme | Installation |
| --- | --- |
| 🐧 Linux | `sudo apt-get install mkvtoolnix` |
| 🍎 macOS | `brew install mkvtoolnix` |
| 🪟 Windows | Téléchargez [MKVToolNix](https://mkvtoolnix.download/downloads.html), installez-le, puis copiez `mkvmerge.exe` depuis `C:\Program Files\MKVToolNix\` dans le **même dossier** que `adaptive-encoder.exe` |

### 2. dovi_tool — requis pour le Dolby Vision

| Plateforme | Installation |
| --- | --- |
| 🐧 Linux | `wget https://github.com/quietvoid/dovi_tool/releases/download/2.3.1/dovi_tool-2.3.1-x86_64-unknown-linux-musl.tar.gz && tar -xzf dovi_tool-*.tar.gz && chmod +x dovi_tool && sudo mv dovi_tool /usr/local/bin/` |
| 🍎 macOS | Téléchargez depuis [github.com/quietvoid/dovi_tool/releases](https://github.com/quietvoid/dovi_tool/releases), puis `chmod +x dovi_tool && sudo mv dovi_tool /usr/local/bin/` |
| 🪟 Windows | Téléchargez `dovi_tool-x86_64-pc-windows-msvc.zip` depuis [github.com/quietvoid/dovi_tool/releases](https://github.com/quietvoid/dovi_tool/releases), extrayez et placez `dovi_tool.exe` dans le **même dossier** que `adaptive-encoder.exe` |

Sans `dovi_tool`, l'encodeur bascule sur HDR10 uniquement.

### 3. Premier lancement — macOS uniquement

macOS bloque les binaires non signés. Exécutez ceci **une seule fois** après le téléchargement :

    xattr -d com.apple.quarantine ./adaptive-encoder
    chmod +x ./adaptive-encoder

Après ça, macOS ne vous avertira plus jamais pour ce fichier.

### 4. Activation

Au premier lancement, démarrez votre **essai gratuit de 7 jours** ou entrez votre **clé de licence** reçue par email après l'achat sur [adaptive-video-encoder.lemonsqueezy.com](https://adaptive-video-encoder.lemonsqueezy.com).

---

## 🚀 Démarrage rapide

**Interface graphique :** lancez simplement l'application, glissez-déposez votre fichier vidéo, et démarrez l'encodage.

**Ligne de commande :**

    # 🐧 Linux / 🍎 macOS
    chmod +x ./adaptive-encoder
    ./adaptive-encoder "mon_film.mkv"

    # 🪟 Windows (PowerShell ou CMD)
    .\adaptive-encoder.exe "mon_film.mkv"

> 💡 **Astuce Windows :** Shift + clic droit dans le dossier → "Ouvrir la fenêtre PowerShell ici"

**Mode test — analyser sans encoder :**

    ./adaptive-encoder "mon_film.mkv" --dry-run

---

## 🗂️ Encoder une bibliothèque entière

    # 🐧 Linux / 🍎 macOS
    for file in *.mkv; do
        ./adaptive-encoder "$file"
    done

    # 🪟 Windows
    Get-ChildItem *.mkv | ForEach-Object {
        .\adaptive-encoder.exe $_.FullName
    }

> 💡 **Conseil :** lancez d'abord avec `--dry-run` sur un seul fichier pour vérifier que le Dolby Vision et le HDR sont correctement détectés.

---

## 📖 Toutes les options (ligne de commande)

    -h, --help                        Affiche l'aide et quitte
    -o, --output OUTPUT               Fichier vidéo de sortie (défaut : <entrée>_adaptive.mkv)

    [ Paramètres vidéo ]
    --force-fps FORCE_FPS             Force la conversion de fréquence d'images (ex. 23.976).
                                      Assure une sync A/V parfaite lors du remux Dolby Vision.
    --max-samples MAX_SAMPLES         Nombre max d'images à échantillonner pour l'analyse
    --target-hours TARGET_HOURS       Durée de secours (h) si ffprobe ne peut pas la déterminer
    --crop-samples CROP_SAMPLES       Nombre de points temporels pour la détection de recadrage
    --no-crop-detect                  Désactive la détection automatique des bandes noires
    --downscale-1080p-sdr             Réduit la source à 1080p et convertit en SDR.
                                      Applique un tone mapping pour les écrans non-HDR.
    --base-crf BASE_CRF               Décale la base CRF adaptative (défaut : 22.0).
                                      Plus bas = meilleure qualité, plus haut = fichier plus petit.

    [ Débit & Préréglages ]
    --max-bitrate MAX_BITRATE         Force le débit max VBV (kbps)
    --vbv-bufsize VBV_BUFSIZE         Taille optionnelle du buffer VBV (kbits)
    --no-vbv                          Désactive le plafonnement automatique VBV
    --no-veryslow                     Limite les préréglages à 'slower' au lieu de 'veryslow'
    --force-tune {grain,animation}    Force le preset tune x265. 'grain' préserve la structure
                                      du grain (psy-rd plus élevé). 'animation' optimise pour
                                      les zones plates et les bords nets.

    [ Dolby Vision & HDR ]
    --no-dolby-vision                 Ignore les métadonnées Dolby Vision, encode en HDR10 seul
    --preserve-dv-profile             Ignore le Dolby Vision si le profil source ne peut pas être
                                      reproduit par x265 (ex. profil 7.x), au lieu de dégrader
                                      silencieusement en 8.1. Sort en HDR10 dans ce cas.
    --temp-dir TEMP_DIR               Dossier pour les fichiers temporaires DV pour éviter la
                                      saturation RAM de /tmp. Crucial sur Linux avec tmpfs.

    [ Réduction du bruit ]
    --no-denoise                      Désactive la réduction de bruit adaptative
    --denoise-strength DENOISE_STRENGTH  Force la force du débruitage (0.0=off, 1.0=max). Défaut : auto
    --denoise-preserve-grain          Débruitage plus doux qui préserve une partie de la texture du grain
    --denoise-engine {nlmeans,bm3d,hybrid}
                                      Force un moteur de débruitage spécifique. bm3d pour la qualité
                                      maximale (3-5x plus lent), nlmeans pour la vitesse, hybrid pour
                                      le grain cinématique.

    [ Audio & Sous-titres ]
    --no-audio                        Supprime les pistes audio (copiées par défaut)
    --no-subs                         Supprime les sous-titres (copiés par défaut)
    --audio-lang AUDIO_LANG           Garde uniquement certaines langues audio (ex. 'fre,eng').
                                      Supprime les doublages indésirables pour économiser de l'espace.
    --downmix-audio                   Mixe les pistes 7.1/Atmos lourdes en 5.1 ou 2.0 standard.

    [ Système ]
    --verbose                         Affiche les détails techniques de l'analyse adaptative
    --dry-run                         Affiche l'analyse et la commande sans encoder

---

## ❓ FAQ

**Combien ça coûte ?** L'outil est disponible avec un essai gratuit de 7 jours. Ensuite, une licence à vie coûte $49.99 — paiement unique, pas d'abonnement. Achat sur [adaptive-video-encoder.lemonsqueezy.com](https://adaptive-video-encoder.lemonsqueezy.com).

**Comment fonctionne l'essai gratuit ?** Téléchargez l'application et essayez toutes les fonctionnalités pendant 7 jours, sans engagement.

**Y a-t-il une interface graphique ?** Oui ! Une interface graphique native est disponible sur Windows, Linux et macOS. La ligne de commande reste disponible pour l'automatisation et les scripts.

**Quelles plateformes sont supportées ?** Windows 10/11 (x64), Linux (x64), et macOS Apple Silicon (M1/M2/M3). ffmpeg et ffprobe sont intégrés — seuls mkvmerge et dovi_tool doivent être installés séparément.

**C'est seulement pour la 4K ?** Non, l'outil est excellent en 1080p aussi. Particulièrement sur les remux Blu-ray avec grain cinématique (classiques, horreur, films d'auteur 35mm) ou les scènes complexes (action, sci-fi).

**Dois-je installer ffmpeg séparément ?** Non. ffmpeg et ffprobe sont intégrés dans le binaire. Téléchargez, lancez, c'est tout.

**Le Dolby Vision ne fonctionne pas — pourquoi ?** `dovi_tool` doit être installé séparément (voir Installation ci-dessus). Sans lui, l'encodeur bascule sur HDR10 uniquement.

**La conversion Profil 7 → 8.1 fonctionne ?** Oui, c'est le comportement par défaut. Le Profil 7 (FEL/MEL) est extrait et réinjecté en 8.1, compatible avec la plupart des lecteurs Dolby Vision modernes.

**Pourquoi mes fichiers sont-ils plus lourds qu'avec d'autres encodeurs ?** Choix de conception délibéré — préservation maximale du détail et des métadonnées HDR. Pour limiter la taille du fichier, utilisez `--max-bitrate`.

**Vitesse d'encodage ?** L'outil utilise les préréglages x265 `slower` ou `veryslow` — pas un encodeur rapide, un *bon* encodeur. Pour un encodage plus rapide, utilisez `--no-veryslow`.

**Et si ça ne fonctionne pas sur mes fichiers ?** Ouvrez une issue sur GitHub ou posez la question sur Discord — avec plaisir.

---

## 📧 Support

- 🌐 **Site web** : <https://adaptive-encoder.com>
- 💬 **Discord** (réponses rapides) : <https://discord.gg/UHrEn2H6jD>
- 📧 **Email** : <osx300@gmail.com>

---

---

# 🎬 Adaptive Video Encoder — English

> **The H.265 encoder that doesn't break your Dolby Vision.**

[![Website](https://img.shields.io/badge/Website-adaptive--encoder.com-2D8CFF?logo=googlechrome&logoColor=white)](https://adaptive-encoder.com) [![Free trial](https://img.shields.io/badge/Free%20trial-7%20days-22C55E)](https://adaptive-video-encoder.lemonsqueezy.com) [![Lifetime license](https://img.shields.io/badge/Lifetime%20license-%2449.99-004577)](https://adaptive-video-encoder.lemonsqueezy.com) [![Discord](https://img.shields.io/badge/Discord-Join-5865F2?logo=discord&logoColor=white)](https://discord.gg/UHrEn2H6jD)

---

## Re-encode your video library without quality compromise

You have a video library full of 1080p Blu-rays, 4K Dolby Vision rips, HDR10 or HLG sources. You want to re-encode to H.265 to reclaim terabytes — without destroying the metadata that makes your movies display correctly on your OLED.

**The problem:** Most H.265 tools strip out Dolby Vision Profile 7 metadata or smooth grain by default. Manual ffmpeg requires hours of testing to find the right parameters — and those parameters change for every video (grain, noise, motion, complexity).

**The solution:** Adaptive Video Encoder analyzes each video frame by frame *before* encoding, automatically picks the best x265 parameters, and fully preserves your Dolby Vision (Profile 5, 7, 8.x), HDR10 and HLG metadata. Available with a **graphical interface** on Windows, Linux and macOS — plus a command line for automation.

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
- You want a simple graphical interface — or the command line to automate your encodes
- You're tired of tweaking x265 parameters and comparing 12 versions of the same film

## ⚠️ Not for you if...

- You're looking for maximum compression to save disk space
- You mostly encode simple SDR content without grain (recent indoor comedies, smooth animation, talking heads) — for those cases, simpler tools often give better compression ratios
- You need fast encoding (the tool prioritizes quality, not speed)

---

## 💰 7-day free trial · Lifetime license $49.99

Adaptive Video Encoder comes with a **7-day free trial**, no commitment. After that, a **$49.99 lifetime license** unlocks the tool forever — no subscription, updates included.

👉 **[Start the free trial](https://adaptive-video-encoder.lemonsqueezy.com)** · **[Buy — $49.99](https://adaptive-video-encoder.lemonsqueezy.com)**

💬 **Questions before buying? Join the [Discord](https://discord.gg/UHrEn2H6jD)** — happy to help.

---

## ⚡ Why a dedicated adaptive encoder?

|  | Generic encoders | Manual ffmpeg | **Adaptive Video Encoder** |
| --- | --- | --- | --- |
| Dolby Vision Profile 7 | ❌ Broken | ⚠️ Possible with `dovi_tool` + scripting | ✅ Automatic |
| Grain preservation | ❌ Smoothed by default | ⚠️ If you know what to flag | ✅ Preserved automatically |
| Settings adapted *per video* | ❌ Fixed presets | ⚠️ If you test yourself | ✅ Frame-by-frame analysis |
| HDR10 / HLG preserved | ⚠️ Sometimes | ⚠️ If you know what to flag | ✅ Always |
| Black bar detection | ✅ | ⚠️ Manual | ✅ Automatic |
| Graphical interface | ✅ | ❌ | ✅ Windows · Linux · macOS |
| Setup time | 5 min | 1-3 h per film | **0 min** |

---

## 🎞️ Particularly excellent on 1080p Blu-rays

Many users mistakenly think this tool is only for 4K. **It's not.** Adaptive Video Encoder shines particularly well on 1080p Blu-ray remuxes for 3 reasons:

**1. Film grain preservation.** Classic films, horror movies, recent 35mm auteur films have grain that's part of their visual identity. Most encoders smooth it by default. Adaptive Encoder detects and preserves it.

**2. Adaptive complex scene detection.** On a 1080p action film, fight scenes have radically different complexity than dialogue. Frame-by-frame analysis adjusts x265 parameters accordingly, where generic encoders use the same settings start to finish.

**3. 1080p HDR10 metadata preservation.** Some recent Blu-rays have HDR10 in 1080p. Adaptive Encoder preserves everything: master display, MaxCLL/MaxFALL, color primaries.

**Less relevant for:** recently-shot digital content with clean image (romantic comedies, sitcoms, indoor documentaries). Those sources have neither grain nor complex detail to preserve.

---

## 🧠 Why CPU encoding instead of GPU?

Short answer: **NVENC, QuickSync and AMF are designed for speed, not quality.**

|  | GPU (NVENC / QSV / AMF) | **CPU (x265)** |
| --- | --- | --- |
| Encoding speed | ⚡⚡⚡ Fast | 🐢 Slow |
| Quality per bit | ⚠️ Decent | ✅ Excellent |
| Final file size | ⚠️ Larger | ✅ Smaller |
| Ideal use case | Live streaming, real-time capture | **Archival, video library** |

**For archiving a library, speed doesn't matter — you encode once, watch 100 times.**

---

## ✨ What it does

- 🖥️ **Native graphical interface** — Windows, Linux and macOS (Apple Silicon)
- 🔍 **Adaptive analysis** — detects noise, grain, complexity, edge density to tune x265
- 📺 **Dolby Vision Profile 5, 7, 8.x** — metadata extracted, preserved, reinjected
- 🎨 **HDR10 and HLG** — color primaries, transfers, master display, MaxCLL/MaxFALL preserved
- 🎞️ **Grain preservation** — 35mm film, horror movies, grainy sources handled automatically
- ✂️ **Smart crop** — detects black bars without accidentally cutting content
- 🔊 **All audio and subtitle tracks** copied by default, zero loss
- 🎞️ **Supported formats** — MKV, MP4, MOV, AVI, MXF, WebM, M4V, TS
- 📐 **Resolutions** — 480p to 8K (excellent for 1080p AND 4K)
- 📦 **Single binary** — ffmpeg and ffprobe bundled. No dependencies to install.

---

## 💻 Platform support

| Platform | Status | Notes |
| --- | --- | --- |
| 🐧 Linux (x64) | ✅ Supported | Ubuntu 22.04+, Debian 12+, Fedora 40+ |
| 🪟 Windows 10/11 (x64) | ✅ Supported | Graphical interface · PowerShell or CMD |
| 🍎 macOS (Apple Silicon) | ✅ Supported | M1, M2, M3 — native arm64 binary |

---

## ⚙️ Installation & requirements

ffmpeg and ffprobe are bundled — no need to install them separately. However, **two tools must be installed** before using the encoder:

### 1. mkvmerge — required for MKV output

| Platform | Install |
| --- | --- |
| 🐧 Linux | `sudo apt-get install mkvtoolnix` |
| 🍎 macOS | `brew install mkvtoolnix` |
| 🪟 Windows | Download [MKVToolNix](https://mkvtoolnix.download/downloads.html), install it, then copy `mkvmerge.exe` from `C:\Program Files\MKVToolNix\` into the **same folder** as `adaptive-encoder.exe` |

### 2. dovi_tool — required for Dolby Vision

| Platform | Install |
| --- | --- |
| 🐧 Linux | `wget https://github.com/quietvoid/dovi_tool/releases/download/2.3.1/dovi_tool-2.3.1-x86_64-unknown-linux-musl.tar.gz && tar -xzf dovi_tool-*.tar.gz && chmod +x dovi_tool && sudo mv dovi_tool /usr/local/bin/` |
| 🍎 macOS | Download from [github.com/quietvoid/dovi_tool/releases](https://github.com/quietvoid/dovi_tool/releases), then `chmod +x dovi_tool && sudo mv dovi_tool /usr/local/bin/` |
| 🪟 Windows | Download `dovi_tool-x86_64-pc-windows-msvc.zip` from [github.com/quietvoid/dovi_tool/releases](https://github.com/quietvoid/dovi_tool/releases), extract and place `dovi_tool.exe` in the **same folder** as `adaptive-encoder.exe` |

Without `dovi_tool`, the encoder falls back to HDR10 only.

### 3. First launch — macOS only

macOS blocks unsigned binaries. Run this **once** after downloading:

    xattr -d com.apple.quarantine ./adaptive-encoder
    chmod +x ./adaptive-encoder

After that, macOS will never warn about this file again.

### 4. Activation

On first launch, start your **7-day free trial** or enter the **license key** you received by email after purchasing on [adaptive-video-encoder.lemonsqueezy.com](https://adaptive-video-encoder.lemonsqueezy.com).

---

## 🚀 Quick start

**Graphical interface:** just launch the app, drag and drop your video file, and start encoding.

**Command line:**

    # 🐧 Linux / 🍎 macOS
    chmod +x ./adaptive-encoder
    ./adaptive-encoder "my_movie.mkv"

    # 🪟 Windows (PowerShell or CMD)
    .\adaptive-encoder.exe "my_movie.mkv"

> 💡 **Windows tip:** Shift + right-click in the folder → "Open PowerShell window here"

**Test mode — analyze without encoding:**

    ./adaptive-encoder "my_movie.mkv" --dry-run

---

## 🗂️ Batch encode an entire library

    # 🐧 Linux / 🍎 macOS
    for file in *.mkv; do
        ./adaptive-encoder "$file"
    done

    # 🪟 Windows
    Get-ChildItem *.mkv | ForEach-Object {
        .\adaptive-encoder.exe $_.FullName
    }

> 💡 **Tip:** run with `--dry-run` on a single file first to verify Dolby Vision and HDR are correctly detected.

---

## 📖 All options (command line)

    -h, --help                        Display this help message and exit
    -o, --output OUTPUT               Output video file (default: <input>_adaptive.mkv)

    [ Video Settings ]
    --force-fps FORCE_FPS             Force video frame rate conversion (e.g., 23.976).
                                      Ensures perfect A/V sync during Dolby Vision remux.
    --max-samples MAX_SAMPLES         Max number of frames to sample for analysis
    --target-hours TARGET_HOURS       Fallback duration (h) if ffprobe cannot determine it
    --crop-samples CROP_SAMPLES       Number of time points for crop detection
    --no-crop-detect                  Disable automatic black bar detection
    --downscale-1080p-sdr             Downscale source to 1080p and convert to SDR.
                                      Applies tone mapping for non-HDR display compatibility.
    --base-crf BASE_CRF               Shift the adaptive CRF baseline (default: 22.0).
                                      Lower is better quality, higher is smaller file size.

    [ Bitrate & Presets ]
    --max-bitrate MAX_BITRATE         Force VBV max bitrate (kbps)
    --vbv-bufsize VBV_BUFSIZE         Optional VBV buffer size (kbits)
    --no-vbv                          Disable automatic VBV bitrate capping
    --no-veryslow                     Limit presets to 'slower' instead of 'veryslow'
    --force-tune {grain,animation}    Force x265 tune preset. 'grain' preserves film grain
                                      structure (higher psy-rd). 'animation' optimizes for
                                      flat areas and sharp edges.

    [ Dolby Vision & HDR ]
    --no-dolby-vision                 Ignore Dolby Vision metadata, encode as HDR10 only
    --preserve-dv-profile             Skip Dolby Vision if the source profile cannot be
                                      reproduced by x265 (e.g. profile 7.x), instead of
                                      silently downgrading to 8.1. Outputs HDR10 in that case.
    --temp-dir TEMP_DIR               Directory for DV temp files to avoid /tmp RAM exhaustion.
                                      Crucial for Linux systems using tmpfs for /tmp.

    [ Noise Reduction ]
    --no-denoise                      Disable adaptive noise reduction (auto-enabled for noisy sources)
    --denoise-strength DENOISE_STRENGTH  Override denoise strength (0.0=off, 1.0=max). Default: auto
    --denoise-preserve-grain          Gentler denoise that preserves some film grain texture
    --denoise-engine {nlmeans,bm3d,hybrid}
                                      Force a specific denoise engine instead of automatic
                                      selection. bm3d for maximum quality (3-5x slower),
                                      nlmeans for speed, hybrid for film grain

    [ Audio & Subtitles ]
    --no-audio                        Remove audio tracks (copied by default)
    --no-subs                         Remove subtitle tracks (copied by default)
    --audio-lang AUDIO_LANG           Keep only specific audio languages (e.g., 'fre,eng').
                                      Removes unwanted dubs to save space.
    --downmix-audio                   Downmix heavy 7.1/Atmos tracks to standard 5.1 or 2.0.

    [ System ]
    --verbose                         Display technical details of adaptive analysis
    --dry-run                         Display analysis and command without encoding

---

## ❓ FAQ

**How much does it cost?** The tool comes with a 7-day free trial. After that, a lifetime license costs $49.99 — one-time payment, no subscription. Purchase at [adaptive-video-encoder.lemonsqueezy.com](https://adaptive-video-encoder.lemonsqueezy.com).

**How does the free trial work?** Download the app and try all features for 7 days, no commitment.

**Is there a graphical interface?** Yes! A native graphical interface is available on Windows, Linux and macOS. The command line remains available for automation and scripting.

**What platforms are supported?** Windows 10/11 (x64), Linux (x64), and macOS Apple Silicon (M1/M2/M3). ffmpeg and ffprobe are bundled — only mkvmerge and dovi_tool need to be installed separately.

**Is this only for 4K?** No, the tool is excellent for 1080p too. Particularly on Blu-ray remuxes with film grain (classics, horror, 35mm auteur films) or complex scenes (action, sci-fi).

**Do I need to install ffmpeg separately?** No. ffmpeg and ffprobe are bundled inside the binary. Download, run, done.

**Dolby Vision doesn't work — why?** `dovi_tool` must be installed separately (see Installation above). Without it, the encoder falls back to HDR10 only.

**Does Profile 7 → 8.1 conversion work?** Yes, it's the default. Profile 7 (FEL/MEL) is extracted and reinjected as 8.1, compatible with most modern Dolby Vision players.

**Why are my files larger than with other encoders?** Intentional design choice — maximum detail and HDR metadata preservation. To cap file size, use `--max-bitrate`.

**Encoding speed?** The tool uses x265 `slower` or `veryslow` presets — not a fast encoder, a *good* one. For faster encoding use `--no-veryslow`.

**What if it doesn't work for my files?** Open an issue on GitHub or ask on Discord — happy to help.

---

## 📧 Support

- 🌐 **Website**: <https://adaptive-encoder.com>
- 💬 **Discord** (fast replies): <https://discord.gg/UHrEn2H6jD>
- 📧 **Email**: <osx300@gmail.com>
