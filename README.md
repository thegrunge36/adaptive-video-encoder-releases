> 🇫🇷 **Français** ci-dessous — 🇬🇧 **English** follows below
>
> *La version française est en premier. / The French version comes first.*

---

# 🎬 Adaptive Video Encoder

> **L'encodeur H.265 qui ne casse pas votre Dolby Vision.**

[![Discord](https://img.shields.io/badge/Discord-Rejoindre-5865F2?logo=discord&logoColor=white)](https://discord.gg/UHrEn2H6jD)

---

## Réencodez votre vidéothèque sans compromis de qualité

Vous avez une vidéothèque pleine de remux Blu-ray 1080p, de rips Dolby Vision 4K, de sources HDR10, HDR10+ ou HLG. Vous voulez réencoder en H.265 pour récupérer des téraoctets — sans détruire les métadonnées qui font s'afficher vos films correctement sur votre OLED.

**Le problème :** La plupart des outils H.265 suppriment les métadonnées Dolby Vision Profil 7, ignorent les HDR10+ dynamiques, ou utilisent les mêmes paramètres pour toutes les vidéos. ffmpeg en manuel nécessite des heures de tests pour trouver les bons paramètres — et ces paramètres changent pour chaque source (grain, bruit, mouvement, complexité).

**La solution :** Adaptive Video Encoder analyse chaque vidéo image par image *avant* l'encodage, choisit automatiquement les meilleurs paramètres x265, et préserve intégralement votre Dolby Vision (Profil 5, 7, 8.x), HDR10+ (SMPTE 2094-40), HDR10 et HLG.

> 💡 **Philosophie :** Adaptive Video Encoder privilégie la **préservation du détail et des métadonnées HDR** sur la compression agressive. L'objectif est une qualité proche du remux, pas le meilleur ratio taille/qualité absolu.

---

## 🎯 Fait pour vous si...

**Bibliothèques Blu-ray 1080p :**
- Vous archivez des remux Blu-ray 1080p et voulez une qualité maximale
- Vous avez des sources HDR10 1080p que les encodeurs génériques gèrent mal
- Vous voulez préserver le détail des scènes complexes (action, fantastique, sci-fi)

**Bibliothèques UHD 4K :**
- Vous archivez des Blu-rays UHD avec Dolby Vision ou HDR10+ et voulez une qualité maximale
- Vous gérez des sources HDR10 ou HLG sans calibrer chaque film manuellement

**Tous formats :**
- Vous privilégiez la qualité d'image sur les économies d'espace disque
- Vous en avez marre de régler les paramètres x265 et de comparer 12 versions du même film

## ⚠️ Pas pour vous si...

- Vous cherchez une compression maximale pour économiser l'espace disque
- Vous avez besoin d'un encodage rapide (l'outil privilégie la qualité, pas la vitesse)

---

## ⚡ Pourquoi un encodeur adaptatif dédié ?

| | Encodeurs génériques | ffmpeg manuel | **Adaptive Video Encoder** |
|---|---|---|---|
| Dolby Vision Profil 7 | ❌ Cassé | ⚠️ Possible avec `dovi_tool` + scripts | ✅ Automatique (downgrade 7→8.1) |
| HDR10+ dynamique | ❌ Ignoré | ⚠️ Si vous extrayez le JSON à la main | ✅ Auto-détecté et réinjecté |
| Paramètres adaptés *par vidéo* | ❌ Préréglages fixes | ⚠️ Si vous testez vous-même | ✅ Analyse image par image |
| HDR10 / HLG préservé | ⚠️ Parfois | ⚠️ Si vous savez quoi activer | ✅ Toujours |
| Débruitage adaptatif | ❌ Force fixe ou absent | ⚠️ Manuel, force globale | ✅ Force calibrée selon les métriques, ou moteur forcé par l'utilisateur |
| Normalisation EBU R128 | ❌ Absent ou approximatif | ⚠️ Mesure puis ré-encodage manuel | ✅ Two-pass automatique |
| Détection des bandes noires | ✅ | ⚠️ Manuel | ✅ Automatique |
| Temps de configuration | 5 min | 1-3 h par film | **0 min** |

---

## 🎞️ Particulièrement excellent sur les Blu-rays 1080p

Beaucoup d'utilisateurs pensent à tort que cet outil est réservé à la 4K. **Ce n'est pas le cas.** Adaptive Video Encoder brille particulièrement sur les remux Blu-ray 1080p pour 3 raisons :

**1. Préréglages x265 finement adaptés à la 1080p.** L'outil ajuste automatiquement la taille des blocs (`ctu=32`, `qg-size=8`) sur le contenu sub-1440p, ce qui suit mieux le détail psy-visuel que les défauts x265 conçus pour 4K. Sur du 1440p et plus, il bascule sur les blocs plus grands (`ctu=64`, `qg-size=16`) attendus à cette échelle.

**2. Détection adaptative des scènes complexes.** Sur un film d'action 1080p, les scènes de combat ont une complexité radicalement différente des dialogues. L'analyse image par image ajuste les paramètres x265 (preset, CRF, psy-rd, AQ-mode) en conséquence, là où les encodeurs génériques utilisent les mêmes réglages du début à la fin.

**3. Préservation des métadonnées HDR10 / HDR10+ 1080p.** Certains Blu-rays récents ont du HDR10 voire du HDR10+ en 1080p. Adaptive Encoder préserve tout : master display, MaxCLL/MaxFALL, primaires de couleur, et métadonnées dynamiques.

---

## 🧠 Pourquoi l'encodage CPU plutôt que GPU ?

Réponse courte : **NVENC, QuickSync et AMF sont conçus pour la vitesse, pas la qualité.**

| | GPU (NVENC / QSV / AMF) | **CPU (x265)** |
|---|---|---|
| Vitesse d'encodage | ⚡⚡⚡ Rapide | 🐢 Lent |
| Qualité par bit | ⚠️ Correct | ✅ Excellent |
| Taille finale du fichier | ⚠️ Plus lourde | ✅ Plus légère |
| Cas d'usage idéal | Streaming live, capture temps réel | **Archivage, vidéothèque** |

**Pour archiver une bibliothèque, la vitesse n'a pas d'importance — vous encodez une fois, vous regardez 100 fois.**

---

## ✨ Ce que ça fait

- 🔍 **Analyse adaptative image par image** — détecte le bruit, le grain, la complexité spatiale, la densité de contours, l'activité temporelle, la fraction de pixels sombres
- 🎚️ **Paramètres x265 calibrés sur les métriques** — preset (entre `medium` et `veryslow`), CRF, psy-rd, psy-rdoq, aq-mode, aq-strength, deblock, SAO, ref, bframes, me, rdoq-level — tous ajustés au contenu réel
- 📐 **Adaptation à la résolution** — `ctu`, `qg-size` et cap VBV auto-réglés selon les pixels effectifs (post-crop)
- 📺 **Dolby Vision Profil 5, 7, 8.x** — métadonnées extraites via `dovi_tool`, préservées, réinjectées. Profil 7 converti en 8.1 par défaut (compatible avec la majorité des lecteurs DV). Option `--preserve-dv-profile` pour sortir en HDR10 plutôt qu'accepter la conversion.
- 🌟 **HDR10+ (SMPTE 2094-40)** — métadonnées dynamiques auto-détectées via `hdr10plus_tool`, extraites en JSON puis réinjectées dans le bitstream HEVC via le paramètre x265 `dhdr10-info`. DV et HDR10+ coexistent dans le même bitstream HEVC : les afficheurs Dolby Vision utilisent le RPU, les afficheurs HDR10+ (ex. Samsung) utilisent les SEI SMPTE 2094-40.
- 🎨 **HDR10 et HLG** — primaires de couleur, transferts, master display, MaxCLL/MaxFALL préservés
- 🌑 **Débruitage adaptatif** — force calibrée automatiquement à partir du bruit/grain mesurés. En mode `auto` (défaut), si le score combiné est sous le seuil (~0.08), aucun filtre n'est appliqué. Choisir un moteur explicitement (`nlmeans`, `bm3d`, `hybrid`) **garantit que le débruitage est toujours appliqué**, même sur une source propre — seul `auto` peut décider de ne rien faire. Option `--denoise-preserve-grain` pour ne lisser qu'une fraction de la texture.
- 🔊 **Normalisation audio EBU R128** — mode `single-pass` (loudnorm dynamique) ou `two-pass` (mesure puis correction linéaire — recommandé). Cible LUFS configurable.
- ✂️ **Recadrage intelligent** — détecte les bandes noires sans couper accidentellement le contenu
- 🎞️ **Toutes les pistes audio et sous-titres** copiées par défaut, zéro perte (sauf si normalisation ou downmix actif)
- 🎞️ **Formats supportés** — MKV, MP4, MOV, AVI, MXF, WebM, M4V, TS
- 📐 **Résolutions** — 480p à 8K

---

## 💻 Plateformes supportées

| Plateforme | Interface graphique | Ligne de commande | Notes |
|---|---|---|---|
| 🪟 Windows 10/11 (x64) | ✅ GUI incluse | ✅ CLI disponible | Tous les outils inclus dans le zip |
| 🐧 Linux (x64) | ✅ GUI incluse | ✅ CLI disponible | Ubuntu 22.04+, Debian 12+, Fedora 40+ |
| 🍎 macOS (Apple Silicon) | ✅ GUI incluse | ✅ CLI disponible | M1, M2, M3 — binaire natif arm64 |

---

## 💰 Tarif

## **$49.99 USD**
**Paiement unique. Licence à vie. Essai gratuit 7 jours.**

Pas d'abonnement. Pas de DRM agressif. Testez l'outil pendant 7 jours avant de décider.

👉 **[Essayer gratuitement 7 jours](https://adaptive-encoder.com)** | **[Acheter — $49.99 USD](https://adaptive-encoder.com)**

💬 **Questions ou retours ? Rejoignez le [Discord](https://discord.gg/UHrEn2H6jD)** — avec plaisir.

---

## ⚙️ Installation

Tous les outils nécessaires (`ffmpeg`, `ffprobe`, `dovi_tool`, `hdr10plus_tool`, `mkvmerge`) sont **inclus dans le zip** sur toutes les plateformes. Extrayez le zip et gardez tous les fichiers dans le même dossier — aucun téléchargement supplémentaire requis.

### 🪟 Windows

Extrayez le zip, puis lancez `adaptive-encoder-gui.exe`. Tous les outils sont inclus.

### 🐧 Linux

Extrayez le zip, puis lancez l'interface graphique :
```bash
chmod +x ./adaptive-encoder-gui
./adaptive-encoder-gui
```

### 🍎 macOS (premier lancement uniquement)

macOS bloque les binaires non signés. Exécutez ceci **une seule fois** :
```bash
xattr -d com.apple.quarantine ./adaptive-encoder-gui
chmod +x ./adaptive-encoder-gui
```

---

## 🚀 Démarrage rapide

### Interface graphique (recommandé)

Lancez l'application, sélectionnez votre fichier vidéo, ajustez les options si nécessaire, et lancez l'encodage. L'interface affiche l'analyse adaptative en temps réel et la progression de l'encodage.

Toutes les options disponibles en ligne de commande sont accessibles depuis l'interface graphique.

### Ligne de commande

Pour les utilisateurs avancés ou l'automatisation en batch :

```bash
./adaptive-encoder "mon_film.mkv"
```

Le fichier de sortie sera créé à côté, nommé `mon_film_adaptive.mkv`.

**Mode test — analyser sans encoder (recommandé sur un nouveau type de source) :**
```bash
./adaptive-encoder "mon_film.mkv" --dry-run
```

---

## 📖 Toutes les options (ligne de commande)

```
-h, --help                        Affiche l'aide et quitte
-o, --output OUTPUT               Fichier vidéo de sortie (défaut : <entrée>_adaptive.mkv)
--auto-rename                     Si le fichier de sortie est verrouillé, utilise automatiquement
                                  un nom alternatif (_v2, _v3, ...) au lieu d'abandonner.

[ Paramètres vidéo ]
--force-fps FORCE_FPS             Force la conversion de fréquence d'images (ex. 23.976)
--max-samples MAX_SAMPLES         Nombre max d'images à échantillonner pour l'analyse
--target-hours TARGET_HOURS       Durée de secours (h) si ffprobe ne peut pas la déterminer
--crop-samples CROP_SAMPLES       Nombre de points temporels pour la détection de recadrage
--no-crop-detect                  Désactive la détection automatique des bandes noires
--base-crf BASE_CRF               Décale la base du CRF adaptatif (défaut : 22.0)
--downscale-1080p-sdr             Réduit la source à 1080p et convertit en SDR via
                                  libplacebo (BT.2390) ou zscale+tonemap=mobius en fallback

[ Débit & Préréglages ]
--max-bitrate MAX_BITRATE         Force le débit max VBV (kbps)
--vbv-bufsize VBV_BUFSIZE         Taille optionnelle du buffer VBV (kbits)
--vbv                             Active le plafonnement automatique du débit VBV
--no-veryslow                     Limite les préréglages à 'slower' au lieu de 'veryslow'
--force-tune {grain,animation}    Force le preset tune x265

[ Dolby Vision & HDR ]
--no-dolby-vision                 Ignore les métadonnées Dolby Vision, encode en HDR10 seul
--preserve-dv-profile             Ignore le Dolby Vision si le profil source ne peut pas être
                                  reproduit par x265, au lieu de dégrader en 8.1
--temp-dir TEMP_DIR               Dossier pour les fichiers temporaires DV
--no-hdr10plus                    Ignore les métadonnées dynamiques HDR10+

[ Réduction du bruit ]
--no-denoise                      Désactive la réduction de bruit adaptative
--denoise-strength STRENGTH       Force la force du débruitage (0.0=off, 1.0=max)
--denoise-preserve-grain          Débruitage 40% plus doux qui préserve le grain
--denoise-engine {auto,nlmeans,bm3d,hybrid}
                                  Choisit le moteur de débruitage (défaut : auto)

[ Audio & Sous-titres ]
--no-audio                        Supprime les pistes audio (copiées par défaut)
--no-subs                         Supprime les sous-titres (copiés par défaut)
--audio-lang AUDIO_LANG           Garde uniquement certaines langues audio (ex. 'fre,eng')
--downmix-audio                   Mixe les pistes 7.1/Atmos en 5.1 ou 2.0
--normalize-audio {off,single-pass,two-pass}
                                  Normalisation EBU R128 (off par défaut)
--normalize-audio-target LUFS     Cible de loudness en LUFS (défaut : -16.0)

[ Système ]
--verbose                         Affiche les détails techniques de l'analyse adaptative
--dry-run                         Affiche l'analyse et la commande sans encoder
```

---

## 🎯 Exemples de combinaisons utiles (ligne de commande)

**📼 Archive 35mm grenu, fidélité au master maximale**
```bash
./adaptive-encoder "western_1970.mkv" --no-denoise --force-tune grain --base-crf 20.0
```

**🎌 Anime / dessin animé optimisé**
```bash
./adaptive-encoder "anime_serie_s01e01.mkv" --force-tune animation --audio-lang "jpn,fre"
```

**💾 Réduction de taille pour serveur de streaming personnel**
```bash
./adaptive-encoder "film.mkv" --base-crf 24.0 --max-bitrate 8000 --downmix-audio --audio-lang "fre,eng" --no-veryslow
```

**📺 Blu-ray UHD Dolby Vision Profil 7 — qualité maximale**
```bash
./adaptive-encoder "uhd_dv_profil7.mkv" --force-fps 23.976 --temp-dir /mnt/ssd/temp --base-crf 20.0
```

**📺 Conversion 4K HDR → 1080p SDR pour TV ancienne**
```bash
./adaptive-encoder "4k_hdr10plus.mkv" --downscale-1080p-sdr --downmix-audio --normalize-audio two-pass --normalize-audio-target -23.0
```

**🎞️ Capture VHS/DVD restaurée — débruitage agressif**
```bash
./adaptive-encoder "vhs_concert.mkv" --denoise-engine bm3d --denoise-strength 0.7 --base-crf 22.0
```

---

## 🛠️ Dépannage

**Le Dolby Vision ou le HDR10+ ne fonctionne pas.**
Vérifiez que vous avez bien extrait *tous* les fichiers du zip — pas seulement l'exécutable. `dovi_tool`, `hdr10plus_tool` et `mkvmerge` doivent se trouver dans le même dossier. Si un fichier manque, le DV et le HDR10+ sont ignorés silencieusement.

**L'encodage prend des heures par film — c'est normal ?**
Oui. `veryslow` est intentionnellement lent pour maximiser la qualité. Utilisez l'option `--no-veryslow` (ou l'équivalent dans la GUI) pour basculer sur `slower` (env. 2× plus rapide).

**Espace disque saturé pendant l'encodage Dolby Vision.**
Utilisez l'option `--temp-dir` pour rediriger les fichiers temporaires vers un disque avec de l'espace libre.

**Le débruitage semble ignoré malgré un forçage.**
Vérifiez la ligne `denoise:` affichée dans `▶ Selecting parameters…` : préfixe `auto→` = le mode auto a choisi pour vous ; pas de préfixe = votre choix est appliqué ; `disabled` = le débruitage est désactivé.

**macOS bloque le lancement.**
Exécutez `xattr -d com.apple.quarantine ./adaptive-encoder-gui` une seule fois après le téléchargement.

---

## ❓ FAQ

**Quelles plateformes sont supportées ?**
Windows 10/11 (x64), Linux (x64), et macOS Apple Silicon (M1/M2/M3). Interface graphique et ligne de commande disponibles sur les trois plateformes. Tous les outils sont inclus dans le zip.

**C'est seulement pour la 4K ?**
Non, l'outil est excellent en 1080p aussi. Les paramètres x265 (`ctu`, `qg-size`, preset) sont adaptés automatiquement à la résolution effective.

**Le Dolby Vision et le HDR10+ fonctionnent automatiquement ?**
Oui. Le binaire détecte automatiquement les sources Dolby Vision (Profil 5/7/8.x) et HDR10+ (SMPTE 2094-40) puis préserve les métadonnées. Si la source contient les deux, les deux métadonnées coexistent dans le bitstream HEVC.

**Le débruitage est-il actif par défaut ? Mon grain va-t-il être touché ?**
Le débruitage adaptatif est activé par défaut en mode `auto`. Si le score combiné est sous ~0.08, aucun filtre n'est appliqué. Pour garantir zéro filtre, utilisez `--no-denoise`. Pour un compromis, utilisez `--denoise-preserve-grain`.

**Pourquoi mes fichiers sont-ils plus lourds qu'avec d'autres encodeurs ?**
Choix de conception délibéré — préservation du détail et des métadonnées HDR. Pour limiter la taille, utilisez `--vbv`, `--max-bitrate`, ou augmentez `--base-crf`.

**Échelle CRF rapide :**

| `--base-crf` | Effet | Cas d'usage |
|---|---|---|
| 18 | Quasi-transparent, fichier très lourd | Archivage maximal |
| 20 | Excellent, légèrement plus léger | Archivage qualité, proche-remux |
| 22 (défaut) | Bon compromis qualité/taille | Usage général |
| 24 | Visible sur scènes complexes | Réduction de taille, streaming perso |
| 26+ | Artefacts visibles | À éviter sauf contrainte espace |

Règle empirique : **chaque +1 sur le CRF réduit la taille d'environ 20-25 %**.

---

## 📧 Support

- 💬 **Discord** (réponses rapides) : [https://discord.gg/UHrEn2H6jD](https://discord.gg/UHrEn2H6jD)
- 📧 **Email** : [osx300@gmail.com](mailto:osx300@gmail.com)

---
---

# 🎬 Adaptive Video Encoder — English

> **The H.265 encoder that doesn't break your Dolby Vision.**

[![Discord](https://img.shields.io/badge/Discord-Join-5865F2?logo=discord&logoColor=white)](https://discord.gg/UHrEn2H6jD)

---

## Re-encode your video library without quality compromise

You have a video library full of 1080p Blu-rays, 4K Dolby Vision rips, HDR10, HDR10+ or HLG sources. You want to re-encode to H.265 to reclaim terabytes — without destroying the metadata that makes your movies display correctly on your OLED.

**The problem:** Most H.265 tools strip out Dolby Vision Profile 7, ignore HDR10+ dynamic metadata, or use identical parameters for every video. Manual ffmpeg requires hours of testing to find the right parameters — and those parameters change for every source (grain, noise, motion, complexity).

**The solution:** Adaptive Video Encoder analyzes each video frame by frame *before* encoding, automatically picks the best x265 parameters, and fully preserves your Dolby Vision (Profile 5, 7, 8.x), HDR10+ (SMPTE 2094-40), HDR10 and HLG metadata.

> 💡 **Philosophy:** Adaptive Video Encoder prioritizes **preservation of detail and HDR metadata** over aggressive compression. The goal is near-remux quality, not the absolute best size/quality ratio.

---

## 🎯 Built for you if...

**1080p Blu-ray libraries:**
- You archive 1080p Blu-ray remuxes and want maximum quality
- You have HDR10 1080p sources that generic encoders handle poorly
- You want to preserve detail in complex scenes (action, fantasy, sci-fi)

**4K UHD libraries:**
- You archive UHD Blu-rays with Dolby Vision or HDR10+ and want maximum quality
- You handle HDR10 or HLG without manually calibrating each film

**All formats:**
- You value image quality over disk space savings
- You're tired of tweaking x265 parameters and comparing 12 versions of the same film

## ⚠️ Not for you if...

- You're looking for maximum compression to save disk space
- You need fast encoding (the tool prioritizes quality, not speed)

---

## ⚡ Why a dedicated adaptive encoder?

| | Generic encoders | Manual ffmpeg | **Adaptive Video Encoder** |
|---|---|---|---|
| Dolby Vision Profile 7 | ❌ Broken | ⚠️ Possible with `dovi_tool` + scripting | ✅ Automatic (7→8.1 downgrade) |
| HDR10+ dynamic metadata | ❌ Stripped | ⚠️ If you extract the JSON manually | ✅ Auto-detected and reinjected |
| Settings adapted *per video* | ❌ Fixed presets | ⚠️ If you test yourself | ✅ Frame-by-frame analysis |
| HDR10 / HLG preserved | ⚠️ Sometimes | ⚠️ If you know what to flag | ✅ Always |
| Adaptive denoising | ❌ Fixed strength or absent | ⚠️ Manual, global strength | ✅ Strength calibrated from detected metrics, or engine forced by user |
| EBU R128 normalization | ❌ Absent or approximate | ⚠️ Measure then manual re-encode | ✅ Two-pass automatic |
| Black bar detection | ✅ | ⚠️ Manual | ✅ Automatic |
| Setup time | 5 min | 1-3 h per film | **0 min** |

---

## 🎞️ Particularly excellent on 1080p Blu-rays

Many users mistakenly think this tool is only for 4K. **It's not.** Adaptive Video Encoder shines particularly well on 1080p Blu-ray remuxes for 3 reasons:

**1. x265 parameters finely tuned for 1080p.** The tool automatically adjusts block sizes (`ctu=32`, `qg-size=8`) on sub-1440p content, which tracks psy-visual detail better than the x265 defaults designed for 4K. On 1440p and above, it switches to the larger blocks (`ctu=64`, `qg-size=16`) expected at that scale.

**2. Adaptive complex scene detection.** On a 1080p action film, fight scenes have radically different complexity than dialogue. Frame-by-frame analysis adjusts x265 parameters (preset, CRF, psy-rd, AQ-mode) accordingly, where generic encoders use the same settings start to finish.

**3. 1080p HDR10 / HDR10+ metadata preservation.** Some recent Blu-rays have HDR10 or even HDR10+ in 1080p. Adaptive Encoder preserves everything: master display, MaxCLL/MaxFALL, color primaries, and dynamic metadata.

---

## 🧠 Why CPU encoding instead of GPU?

Short answer: **NVENC, QuickSync and AMF are designed for speed, not quality.**

| | GPU (NVENC / QSV / AMF) | **CPU (x265)** |
|---|---|---|
| Encoding speed | ⚡⚡⚡ Fast | 🐢 Slow |
| Quality per bit | ⚠️ Decent | ✅ Excellent |
| Final file size | ⚠️ Larger | ✅ Smaller |
| Ideal use case | Live streaming, real-time capture | **Archival, video library** |

**For archiving a library, speed doesn't matter — you encode once, watch 100 times.**

---

## ✨ What it does

- 🔍 **Frame-by-frame adaptive analysis** — measures noise, grain, spatial complexity, edge density, temporal activity, dark-pixel fraction
- 🎚️ **x265 parameters tuned to the metrics** — preset (between `medium` and `veryslow`), CRF, psy-rd, psy-rdoq, aq-mode, aq-strength, deblock, SAO, ref, bframes, me, rdoq-level — all adjusted to the actual content
- 📐 **Resolution-aware** — `ctu`, `qg-size` and VBV cap auto-tuned from effective pixels (post-crop)
- 📺 **Dolby Vision Profile 5, 7, 8.x** — metadata extracted via `dovi_tool`, preserved, reinjected. Profile 7 converted to 8.1 by default. `--preserve-dv-profile` outputs HDR10 instead of accepting the conversion.
- 🌟 **HDR10+ (SMPTE 2094-40)** — dynamic metadata auto-detected via `hdr10plus_tool`, extracted to JSON then reinjected into the HEVC bitstream. DV and HDR10+ coexist in the same HEVC bitstream.
- 🎨 **HDR10 and HLG** — color primaries, transfers, master display, MaxCLL/MaxFALL preserved
- 🌑 **Adaptive denoising** — strength auto-calibrated from measured noise/grain. In `auto` mode (default), if the combined score is below threshold (~0.08), no filter is applied. Picking an engine explicitly (`nlmeans`, `bm3d`, `hybrid`) **guarantees denoising is always applied**, even on clean sources.
- 🔊 **EBU R128 audio normalization** — `single-pass` or `two-pass` (recommended). Configurable LUFS target.
- ✂️ **Smart crop** — detects black bars without accidentally cutting content
- 🎞️ **All audio and subtitle tracks** copied by default, zero loss (unless normalization or downmix active)
- 🎞️ **Supported formats** — MKV, MP4, MOV, AVI, MXF, WebM, M4V, TS
- 📐 **Resolutions** — 480p to 8K

---

## 💻 Platform support

| Platform | GUI | CLI | Notes |
|---|---|---|---|
| 🪟 Windows 10/11 (x64) | ✅ Included | ✅ Available | All tools included in the zip |
| 🐧 Linux (x64) | ✅ Included | ✅ Available | Ubuntu 22.04+, Fedora 40+ |
| 🍎 macOS (Apple Silicon) | ✅ Included | ✅ Available | M1, M2, M3 — native arm64 binary |

---

## 💰 Pricing

## **$49.99 USD**
**One-time payment. Lifetime license. Free 7-day trial.**

No subscription. No aggressive DRM. Try the tool for 7 days before you decide.

👉 **[Try free for 7 days](https://adaptive-encoder.com)** | **[Buy — $49.99 USD](https://adaptive-encoder.com)**

💬 **Questions or feedback? Join the [Discord](https://discord.gg/UHrEn2H6jD)** — happy to help.

---

## ⚙️ Installation

All required tools (`ffmpeg`, `ffprobe`, `dovi_tool`, `hdr10plus_tool`, `mkvmerge`) are **bundled in the zip** on all platforms. Extract the zip and keep all files in the same folder — no additional downloads needed.

### 🪟 Windows

Extract the zip, then launch `adaptive-encoder-gui.exe`. All tools are included.

### 🐧 Linux

Extract the zip, then launch the GUI:
```bash
chmod +x ./adaptive-encoder-gui
./adaptive-encoder-gui
```

### 🍎 macOS (first launch only)

macOS blocks unsigned binaries. Run this **once** after downloading:
```bash
xattr -d com.apple.quarantine ./adaptive-encoder-gui
chmod +x ./adaptive-encoder-gui
```

---

## 🚀 Quick start

### GUI (recommended)

Launch the application, select your video file, adjust options as needed, and start encoding. The interface displays the adaptive analysis in real time along with encoding progress.

All options available on the command line are also accessible from the GUI.

### Command line

For advanced users or batch automation:

```bash
./adaptive-encoder "my_movie.mkv"
```

The output file will be created next to it, named `my_movie_adaptive.mkv`.

**Test mode — analyze without encoding (recommended on a new source type):**
```bash
./adaptive-encoder "my_movie.mkv" --dry-run
```

---

## 📖 All options (command line)

```
-h, --help                        Display this help message and exit
-o, --output OUTPUT               Output video file (default: <input>_adaptive.mkv)
--auto-rename                     If the output file is locked, automatically pick an
                                  alternative name (_v2, _v3, ...) instead of aborting.

[ Video Settings ]
--force-fps FORCE_FPS             Force video frame rate conversion (e.g., 23.976)
--max-samples MAX_SAMPLES         Max number of frames to sample for analysis
--target-hours TARGET_HOURS       Fallback duration (h) if ffprobe cannot determine it
--crop-samples CROP_SAMPLES       Number of time points for crop detection
--no-crop-detect                  Disable automatic black bar detection
--base-crf BASE_CRF               Shift the adaptive CRF baseline (default: 22.0)
--downscale-1080p-sdr             Downscale source to 1080p and convert to SDR via
                                  libplacebo (BT.2390) or zscale+tonemap=mobius fallback

[ Bitrate & Presets ]
--max-bitrate MAX_BITRATE         Force VBV max bitrate (kbps)
--vbv-bufsize VBV_BUFSIZE         Optional VBV buffer size (kbits)
--vbv                             Enable automatic VBV bitrate cap
--no-veryslow                     Limit presets to 'slower' instead of 'veryslow'
--force-tune {grain,animation}    Force x265 tune preset

[ Dolby Vision & HDR ]
--no-dolby-vision                 Ignore Dolby Vision metadata, encode as HDR10 only
--preserve-dv-profile             Skip Dolby Vision if the source profile cannot be reproduced
--temp-dir TEMP_DIR               Directory for DV temp files
--no-hdr10plus                    Ignore HDR10+ dynamic metadata

[ Noise Reduction ]
--no-denoise                      Disable the adaptive noise reduction
--denoise-strength STRENGTH       Override denoise strength (0.0=off, 1.0=max)
--denoise-preserve-grain          40% gentler denoise that preserves film grain texture
--denoise-engine {auto,nlmeans,bm3d,hybrid}
                                  Pick the denoising engine (default: auto)

[ Audio & Subtitles ]
--no-audio                        Remove audio tracks (copied by default)
--no-subs                         Remove subtitle tracks (copied by default)
--audio-lang AUDIO_LANG           Keep only specific audio languages (e.g., 'eng,fre')
--downmix-audio                   Downmix heavy 7.1/Atmos tracks to standard 5.1 or 2.0
--normalize-audio {off,single-pass,two-pass}
                                  Apply EBU R128 loudness normalization (off by default)
--normalize-audio-target LUFS     Integrated loudness target in LUFS (default: -16.0)

[ System ]
--verbose                         Display technical details of adaptive analysis
--dry-run                         Display analysis and command without encoding
```

---

## 🎯 Useful combinations (command line)

**📼 Grainy 35mm archive, maximum master fidelity**
```bash
./adaptive-encoder "western_1970.mkv" --no-denoise --force-tune grain --base-crf 20.0
```

**🎌 Anime / cartoon optimized**
```bash
./adaptive-encoder "anime_series_s01e01.mkv" --force-tune animation --audio-lang "jpn,eng"
```

**💾 Aggressive size reduction for personal streaming server**
```bash
./adaptive-encoder "film.mkv" --base-crf 24.0 --max-bitrate 8000 --downmix-audio --audio-lang "eng,fre" --no-veryslow
```

**📺 UHD Blu-ray Dolby Vision Profile 7 — max quality**
```bash
./adaptive-encoder "uhd_dv_profile7.mkv" --force-fps 23.976 --temp-dir /mnt/ssd/temp --base-crf 20.0
```

**📺 4K HDR → 1080p SDR for an older TV**
```bash
./adaptive-encoder "4k_hdr10plus.mkv" --downscale-1080p-sdr --downmix-audio --normalize-audio two-pass --normalize-audio-target -23.0
```

**🎞️ Restored VHS/DVD — aggressive denoising**
```bash
./adaptive-encoder "vhs_concert.mkv" --denoise-engine bm3d --denoise-strength 0.7 --base-crf 22.0
```

---

## 🛠️ Troubleshooting

**Dolby Vision or HDR10+ doesn't work.**
Make sure you extracted *all* the files from the zip — not just the executable. `dovi_tool`, `hdr10plus_tool` and `mkvmerge` must be in the same folder. If any file is missing, DV and HDR10+ are silently ignored.

**Encoding takes hours per film — is that normal?**
Yes. `veryslow` is intentionally slow to maximize quality. Use `--no-veryslow` (or the equivalent option in the GUI) to switch to `slower` (about 2× faster).

**Disk space saturated during Dolby Vision encoding.**
Use `--temp-dir` to redirect temp files to a drive with free space.

**Denoising seems ignored despite forcing it.**
Check the `denoise:` line in `▶ Selecting parameters…`: `auto→` prefix = auto picked; no prefix = your choice applied; `disabled` = denoising is off.

**macOS blocks the launch.**
Run `xattr -d com.apple.quarantine ./adaptive-encoder-gui` once after downloading.

---

## ❓ FAQ

**What platforms are supported?**
Windows 10/11 (x64), Linux (x64), and macOS Apple Silicon (M1/M2/M3). GUI and command line available on all three platforms. All tools are included in the zip.

**Is this only for 4K?**
No, the tool is excellent for 1080p too. x265 parameters (`ctu`, `qg-size`, preset) are automatically tuned to the effective resolution.

**Do Dolby Vision and HDR10+ work automatically?**
Yes. The binary auto-detects Dolby Vision (Profile 5/7/8.x) and HDR10+ (SMPTE 2094-40) sources. If a source carries both, they coexist in the HEVC bitstream.

**Is denoising active by default? Will my grain be touched?**
Adaptive denoising is enabled in `auto` mode. If the combined score is below ~0.08, no filter is applied. To guarantee zero filtering, use `--no-denoise`. For a compromise, use `--denoise-preserve-grain`.

**Why are my files larger than with other encoders?**
Intentional design choice — detail and HDR metadata preservation. Use `--vbv`, `--max-bitrate`, or raise `--base-crf` to reduce size.

**CRF quick reference:**

| `--base-crf` | Effect | Use case |
|---|---|---|
| 18 | Near-transparent, very large file | Maximum archival |
| 20 | Excellent, slightly lighter | Quality archival, near-remux |
| 22 (default) | Good quality/size balance | General use |
| 24 | Visible on complex scenes | Size reduction, personal streaming |
| 26+ | Visible artifacts | Avoid unless space-constrained |

Rule of thumb: **each +1 on the CRF reduces file size by roughly 20-25%**.

---

## 📧 Support

- 💬 **Discord** (fast replies): [https://discord.gg/UHrEn2H6jD](https://discord.gg/UHrEn2H6jD)
- 📧 **Email**: [osx300@gmail.com](mailto:osx300@gmail.com)
