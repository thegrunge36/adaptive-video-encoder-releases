> 🇫🇷 **Français** ci-dessous — 🇬🇧 **English** follows below
>
> *La version française est en premier. / The French version comes first.*

---

# 🎬 Adaptive Video Encoder

> **L'encodeur H.265 qui ne casse pas votre Dolby Vision.**

[![Discord](https://img.shields.io/badge/Discord-Rejoindre-5865F2?logo=discord&logoColor=white)](https://discord.gg/UHrEn2H6jD) [![Buy me a coffee](https://img.shields.io/badge/Un%20café-PayPal-00457C?logo=paypal&logoColor=white)](https://paypal.me/thegrunge45)

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
- Vous êtes à l'aise avec la ligne de commande
- Vous en avez marre de régler les paramètres x265 et de comparer 12 versions du même film

## ⚠️ Pas pour vous si...

- Vous cherchez une compression maximale pour économiser l'espace disque
- Vous voulez une interface graphique
- Vous avez besoin d'un encodage rapide (l'outil privilégie la qualité, pas la vitesse)

---

## ⚡ Pourquoi un encodeur adaptatif dédié ?

| | Encodeurs génériques | ffmpeg manuel | **Adaptive Video Encoder** |
|---|---|---|---|
| Dolby Vision Profil 7 | ❌ Cassé | ⚠️ Possible avec `dovi_tool` + scripts | ✅ Automatique (downgrade 7→8.1) |
| HDR10+ dynamique | ❌ Ignoré | ⚠️ Si vous extrayez le JSON à la main | ✅ Auto-détecté et réinjecté |
| Paramètres adaptés *par vidéo* | ❌ Préréglages fixes | ⚠️ Si vous testez vous-même | ✅ Analyse image par image |
| HDR10 / HLG préservé | ⚠️ Parfois | ⚠️ Si vous savez quoi activer | ✅ Toujours |
| Débruitage adaptatif | ❌ Force fixe ou absent | ⚠️ Manuel, force globale | ✅ Force calibrée selon les métriques détectées |
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
- 🌟 **HDR10+ (SMPTE 2094-40)** — métadonnées dynamiques auto-détectées via `hdr10plus_tool`, extraites en JSON puis réinjectées dans le bitstream HEVC via le paramètre x265 `dhdr10-info`. DV prend priorité quand les deux sont présents.
- 🎨 **HDR10 et HLG** — primaires de couleur, transferts, master display, MaxCLL/MaxFALL préservés
- 🌑 **Débruitage adaptatif** — force calibrée automatiquement à partir du bruit/grain mesurés ; si le score combiné est sous le seuil (~0.08), aucun filtre n'est appliqué. Trois moteurs : `nlmeans`, `bm3d`, `hybrid` (hqdn3d+nlmeans), plus `auto`. Option `--denoise-preserve-grain` pour ne lisser qu'une fraction de la texture.
- 🔊 **Normalisation audio EBU R128** — mode `single-pass` (loudnorm dynamique) ou `two-pass` (mesure puis correction linéaire — recommandé). Cible LUFS configurable.
- ✂️ **Recadrage intelligent** — détecte les bandes noires sans couper accidentellement le contenu
- 🎞️ **Toutes les pistes audio et sous-titres** copiées par défaut, zéro perte (sauf si normalisation ou downmix actif)
- 🎞️ **Formats supportés** — MKV, MP4, MOV, AVI, MXF, WebM, M4V, TS
- 📐 **Résolutions** — 480p à 8K
- 📦 **Binaire unique, zéro dépendance** — `ffmpeg`, `ffprobe`, `dovi_tool`, `hdr10plus_tool` et `mkvmerge` intégrés sur les trois plateformes. Aucun outil externe à installer.

---

## 💻 Plateformes supportées

| Plateforme | Statut | Notes |
|---|---|---|
| 🐧 Linux (x64) | ✅ Supporté | Ubuntu 22.04+, Debian 12+, Fedora 40+ |
| 🪟 Windows 10/11 (x64) | ✅ Supporté | PowerShell ou CMD |
| 🍎 macOS (Apple Silicon) | ✅ Supporté | M1, M2, M3 — binaire natif arm64 |

---

## ☕ Cet outil est gratuit — offrez-moi un café si ça vous a aidé !

Adaptive Video Encoder est entièrement gratuit. Si il vous a fait gagner du temps ou amélioré votre bibliothèque, un petit café est toujours apprécié — mais jamais obligatoire.

👉 **[M'offrir un café](https://paypal.me/thegrunge45)** — totalement optionnel, toujours apprécié ☕

💬 **Questions ou retours ? Rejoignez le [Discord](https://discord.gg/UHrEn2H6jD)** — avec plaisir.

---

## ⚙️ Installation et prérequis

Tous les outils nécessaires (`ffmpeg`, `ffprobe`, `dovi_tool`, `hdr10plus_tool`, `mkvmerge`) sont intégrés dans le binaire — **aucune installation externe requise** sur Windows, Linux ou macOS.

### Premier lancement — macOS uniquement

macOS bloque les binaires non signés. Exécutez ceci **une seule fois** après le téléchargement :

```bash
xattr -d com.apple.quarantine ./adaptive-encoder
chmod +x ./adaptive-encoder
```

Après ça, macOS ne vous avertira plus jamais pour ce fichier.

---

## 🚀 Démarrage rapide

```bash
# 🐧 Linux / 🍎 macOS
chmod +x ./adaptive-encoder
./adaptive-encoder "mon_film.mkv"

# 🪟 Windows (PowerShell ou CMD)
.\adaptive-encoder.exe "mon_film.mkv"
```

> 💡 **Astuce Windows :** Shift + clic droit dans le dossier → "Ouvrir la fenêtre PowerShell ici"

**Mode test — analyser sans encoder :**
```bash
./adaptive-encoder "mon_film.mkv" --dry-run
```

**Préserver le grain — désactiver le débruitage :**
```bash
./adaptive-encoder "film_35mm.mkv" --no-denoise
```

**Plafonner le débit (utile pour cibler une taille) :**
```bash
./adaptive-encoder "film.mkv" --vbv
```

**Normaliser le loudness audio (recommandé pour mix hétérogène) :**
```bash
./adaptive-encoder "film.mkv" --normalize-audio two-pass
```

**Loudness pour broadcast EBU R128 (-23 LUFS) :**
```bash
./adaptive-encoder "film.mkv" --normalize-audio two-pass --normalize-audio-target -23.0
```

---

## 🗂️ Encoder une bibliothèque entière

```bash
# 🐧 Linux / 🍎 macOS
for file in *.mkv; do
    ./adaptive-encoder "$file"
done
```

```powershell
# 🪟 Windows
Get-ChildItem *.mkv | ForEach-Object {
    .\adaptive-encoder.exe $_.FullName
}
```

> 💡 **Conseil :** lancez d'abord avec `--dry-run` sur un seul fichier pour vérifier que le Dolby Vision et le HDR sont correctement détectés.

---

## 📖 Toutes les options

```
-h, --help                        Affiche l'aide et quitte
-o, --output OUTPUT               Fichier vidéo de sortie (défaut : <entrée>_adaptive.mkv)

[ Paramètres vidéo ]
--force-fps FORCE_FPS             Force la conversion de fréquence d'images (ex. 23.976).
                                  Assure une sync A/V parfaite lors du remux Dolby Vision.
--max-samples MAX_SAMPLES         Nombre max d'images à échantillonner pour l'analyse
--target-hours TARGET_HOURS       Durée de secours (h) si ffprobe ne peut pas la déterminer
--crop-samples CROP_SAMPLES       Nombre de points temporels pour la détection de recadrage
--no-crop-detect                  Désactive la détection automatique des bandes noires
--base-crf BASE_CRF               Décale la base du CRF adaptatif (défaut : 22.0).
                                  Augmenter réduit la taille du fichier au détriment
                                  de la qualité visuelle.
--downscale-1080p-sdr             Réduit la source à 1080p et convertit en SDR via
                                  libplacebo (BT.2390) ou zscale+tonemap=mobius en
                                  fallback. Sortie : couleurs BT.709, range TV, 10-bit.

[ Débit & Préréglages ]
--max-bitrate MAX_BITRATE         Force le débit max VBV (kbps). Utile pour cibler
                                  une taille de fichier précise.
--vbv-bufsize VBV_BUFSIZE         Taille optionnelle du buffer VBV (kbits)
--vbv                             Active le plafonnement automatique du débit VBV
                                  (désactivé par défaut). Quand activé, le max bitrate
                                  est calibré sur la résolution effective (post-crop)
                                  via la courbe continue 12000 × ratio^0.6, ancrée à
                                  1080p = 12 Mbps. Donne ~7 Mbps en 720p, ~17 Mbps en
                                  1440p, ~28 Mbps en 4K, capé à 35 Mbps. Par défaut
                                  l'encodeur fonctionne en CRF pur — les scènes
                                  complexes et granuleuses reçoivent tous les bits
                                  dont elles ont besoin.
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
--no-hdr10plus                    Ignore les métadonnées dynamiques HDR10+ même si présentes
                                  dans la source (encodé en HDR10 seul). HDR10+ est détecté
                                  et embarqué automatiquement via hdr10plus_tool quand aucun
                                  Dolby Vision n'est actif (le DV est prioritaire si les
                                  deux sont présents).

[ Réduction du bruit ]
--no-denoise                      Désactive la réduction de bruit adaptative. Par défaut
                                  le débruitage est activé et calibré automatiquement
                                  selon le niveau de bruit/grain détecté ; si la source
                                  est très propre (score combiné < 0.08), aucun filtre
                                  n'est appliqué de toute façon.
--denoise-strength STRENGTH       Force la force du débruitage (0.0=off, 1.0=max).
                                  Override le calibrage automatique.
--denoise-preserve-grain          Débruitage 40% plus doux qui préserve une partie de la
                                  texture du grain.
--denoise-engine {auto,nlmeans,bm3d,hybrid}
                                  Force un moteur de débruitage spécifique au lieu de la
                                  sélection automatique. 'nlmeans' rapide et général.
                                  'bm3d' qualité maximale sur bruit stationnaire (3-5×
                                  plus lent). 'hybrid' chaîne hqdn3d + nlmeans pour les
                                  sources mixtes. 'auto' choisit selon le profil bruit/grain.

[ Audio & Sous-titres ]
--no-audio                        Supprime les pistes audio (copiées par défaut)
--no-subs                         Supprime les sous-titres (copiés par défaut)
--audio-lang AUDIO_LANG           Garde uniquement certaines langues audio (ex. 'fre,eng').
                                  Supprime les doublages indésirables pour économiser de
                                  l'espace. La première langue listée devient la piste par
                                  défaut du player.
--downmix-audio                   Mixe les pistes 7.1/Atmos lourdes en 5.1 ou 2.0 standard.
--normalize-audio {off,single-pass,two-pass}
                                  Applique la normalisation de loudness EBU R128 sur les
                                  pistes audio conservées. 'single-pass' utilise une
                                  normalisation linéaire dynamique (rapide, légèrement
                                  moins précise — une seule passe ffmpeg). 'two-pass'
                                  mesure d'abord la loudness intégrée de tout le fichier,
                                  puis applique une correction linéaire (plus lent mais
                                  précis — recommandé). Quand actif, l'audio est ré-encodé
                                  en AC3 à 640 kbps pour 5.1 / 192 kbps pour stéréo.
                                  Off par défaut.
--normalize-audio-target LUFS     Cible de loudness intégrée en LUFS (défaut : -16.0, adapté
                                  TV/streaming. Utiliser -23.0 pour EBU R128 broadcast).

[ Système ]
--verbose                         Affiche les détails techniques de l'analyse adaptative
--dry-run                         Affiche l'analyse et la commande sans encoder
```

---

## ❓ FAQ

**Quelles plateformes sont supportées ?**
Windows 10/11 (x64), Linux (x64), et macOS Apple Silicon (M1/M2/M3). Tous les outils nécessaires (`ffmpeg`, `ffprobe`, `dovi_tool`, `hdr10plus_tool`, `mkvmerge`) sont intégrés dans le binaire — aucune installation externe requise.

**C'est seulement pour la 4K ?**
Non, l'outil est excellent en 1080p aussi. Les paramètres x265 (`ctu`, `qg-size`, preset) sont adaptés automatiquement à la résolution effective.

**Dois-je installer ffmpeg ou d'autres outils séparément ?**
Non. `ffmpeg`, `ffprobe`, `dovi_tool`, `hdr10plus_tool` et `mkvmerge` sont tous intégrés dans le binaire sur les trois plateformes. Téléchargez et lancez, c'est tout.

**Le Dolby Vision et le HDR10+ fonctionnent automatiquement ?**
Oui. Le binaire détecte automatiquement les sources Dolby Vision (Profil 5/7/8.x) et HDR10+ (SMPTE 2094-40) puis préserve les métadonnées sans configuration. Si la source contient les deux (rare), Dolby Vision prend la priorité car les deux portent du tone-mapping par frame et seul un peut être affiché à la fois sur la TV.

**La conversion Profil 7 → 8.1 fonctionne ?**
Oui, c'est le comportement par défaut. Le Profil 7 (FEL/MEL) est extrait et réinjecté en 8.1, compatible avec la plupart des lecteurs Dolby Vision modernes. Si vous préférez sortir en HDR10 plutôt qu'accepter la conversion, utilisez `--preserve-dv-profile`.

**Le débruitage est-il actif par défaut ? Mon grain va-t-il être touché ?**
Le débruitage **adaptatif** est activé par défaut, mais il n'est pas appliqué aveuglément. La force est auto-calibrée à partir des métriques de bruit et de grain : si le score combiné est sous ~0.08, aucun filtre n'est appliqué. Sur une source propre (Blu-ray récent sans grain marqué), vous n'aurez aucun traitement. Sur un film 35mm très grenu, vous aurez un débruitage modéré. Pour garantir zéro filtre quelle que soit la source, utilisez `--no-denoise`. Pour un compromis (préserver une partie de la texture du grain), utilisez `--denoise-preserve-grain`.

**Quand utiliser `--normalize-audio` ?**
Surtout pour les bibliothèques hétérogènes (films de décennies différentes, mix de sources, doublages enregistrés à des niveaux variables). Le mode `two-pass` mesure d'abord le loudness intégré de tout le fichier puis applique une correction linéaire — c'est la même approche que Netflix/Apple/YouTube utilisent côté plateforme. La cible par défaut `-16 LUFS` est calibrée TV/streaming ; pour la diffusion broadcast EBU R128 stricte, utilisez `-23.0`. Important : activer la normalisation force le ré-encodage audio (AC3), donc vous perdez l'audio bit-perfect d'origine. Sans `--normalize-audio`, les pistes audio sont copiées en bit-perfect.

**Pourquoi mes fichiers sont-ils plus lourds qu'avec d'autres encodeurs ?**
Choix de conception délibéré — préservation du détail et des métadonnées HDR. Pour limiter la taille du fichier, utilisez `--vbv` (active un plafond adapté à la résolution), `--max-bitrate` (force un plafond manuel), ou augmentez `--base-crf`.

**Vitesse d'encodage ?**
L'outil utilise les préréglages x265 `slower` ou `veryslow` selon la complexité du contenu — pas un encodeur rapide, un *bon* encodeur. Pour un encodage plus rapide, utilisez `--no-veryslow`. Note : le mode `--normalize-audio two-pass` ajoute une passe de mesure audio (proportionnelle à la durée du film, sans encodage vidéo).

**Et si ça ne fonctionne pas sur mes fichiers ?**
Ouvrez une issue sur GitHub ou posez la question sur Discord — avec plaisir.

---

## 📧 Support

- 💬 **Discord** (réponses rapides) : [https://discord.gg/UHrEn2H6jD](https://discord.gg/UHrEn2H6jD)
- 📧 **Email** : [osx300@gmail.com](mailto:osx300@gmail.com)
- ☕ **M'offrir un café** (optionnel) : [paypal.me/thegrunge45](https://paypal.me/thegrunge45)

---
---

# 🎬 Adaptive Video Encoder — English

> **The H.265 encoder that doesn't break your Dolby Vision.**

[![Discord](https://img.shields.io/badge/Discord-Join-5865F2?logo=discord&logoColor=white)](https://discord.gg/UHrEn2H6jD) [![Buy me a coffee](https://img.shields.io/badge/Buy%20me%20a%20coffee-PayPal-00457C?logo=paypal&logoColor=white)](https://paypal.me/thegrunge45)

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
- You're comfortable with the command line
- You're tired of tweaking x265 parameters and comparing 12 versions of the same film

## ⚠️ Not for you if...

- You're looking for maximum compression to save disk space
- You want a GUI
- You need fast encoding (the tool prioritizes quality, not speed)

---

## ⚡ Why a dedicated adaptive encoder?

| | Generic encoders | Manual ffmpeg | **Adaptive Video Encoder** |
|---|---|---|---|
| Dolby Vision Profile 7 | ❌ Broken | ⚠️ Possible with `dovi_tool` + scripting | ✅ Automatic (7→8.1 downgrade) |
| HDR10+ dynamic metadata | ❌ Stripped | ⚠️ If you extract the JSON manually | ✅ Auto-detected and reinjected |
| Settings adapted *per video* | ❌ Fixed presets | ⚠️ If you test yourself | ✅ Frame-by-frame analysis |
| HDR10 / HLG preserved | ⚠️ Sometimes | ⚠️ If you know what to flag | ✅ Always |
| Adaptive denoising | ❌ Fixed strength or absent | ⚠️ Manual, global strength | ✅ Strength calibrated from detected metrics |
| EBU R128 normalization | ❌ Absent or approximate | ⚠️ Measure then manual re-encode | ✅ Two-pass automatic |
| Black bar detection | ✅ | ⚠️ Manual | ✅ Automatic |
| Setup time | 5 min | 1-3 h per film | **0 min** |

---

## 🎞️ Particularly excellent on 1080p Blu-rays

Many users mistakenly think this tool is only for 4K. **It's not.** Adaptive Video Encoder shines particularly well on 1080p Blu-ray remuxes for 3 reasons:

**1. x265 parameters finely tuned for 1080p.** The tool automatically adjusts block sizes (`ctu=32`, `qg-size=8`) on sub-1440p content, which tracks psy-visual detail better than the x265 defaults that were designed for 4K. On 1440p and above, it switches to the larger blocks (`ctu=64`, `qg-size=16`) expected at that scale.

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
- 📺 **Dolby Vision Profile 5, 7, 8.x** — metadata extracted via `dovi_tool`, preserved, reinjected. Profile 7 converted to 8.1 by default (compatible with most DV players). `--preserve-dv-profile` outputs HDR10 instead of accepting the conversion.
- 🌟 **HDR10+ (SMPTE 2094-40)** — dynamic metadata auto-detected via `hdr10plus_tool`, extracted to JSON then reinjected into the HEVC bitstream via the x265 `dhdr10-info` parameter. DV takes priority when both are present.
- 🎨 **HDR10 and HLG** — color primaries, transfers, master display, MaxCLL/MaxFALL preserved
- 🌑 **Adaptive denoising** — strength auto-calibrated from measured noise/grain; if the combined score is below threshold (~0.08), no filter is applied. Three engines: `nlmeans`, `bm3d`, `hybrid` (hqdn3d+nlmeans), plus `auto`. `--denoise-preserve-grain` smooths only a fraction of the texture.
- 🔊 **EBU R128 audio normalization** — `single-pass` mode (dynamic loudnorm) or `two-pass` (measure then linear correction — recommended). Configurable LUFS target.
- ✂️ **Smart crop** — detects black bars without accidentally cutting content
- 🎞️ **All audio and subtitle tracks** copied by default, zero loss (unless normalization or downmix active)
- 🎞️ **Supported formats** — MKV, MP4, MOV, AVI, MXF, WebM, M4V, TS
- 📐 **Resolutions** — 480p to 8K
- 📦 **Single binary, zero dependencies** — `ffmpeg`, `ffprobe`, `dovi_tool`, `hdr10plus_tool` and `mkvmerge` bundled on all three platforms. Nothing to install separately.

---

## 💻 Platform support

| Platform | Status | Notes |
|---|---|---|
| 🐧 Linux (x64) | ✅ Supported | Ubuntu 22.04+, Debian 12+, Fedora 40+ |
| 🪟 Windows 10/11 (x64) | ✅ Supported | PowerShell or CMD |
| 🍎 macOS (Apple Silicon) | ✅ Supported | M1, M2, M3 — native arm64 binary |

---

## ☕ This tool is free — buy me a coffee if it helped!

Adaptive Video Encoder is completely free to use. If it saved you time or improved your library, a small coffee is always appreciated — but never required.

👉 **[Buy me a coffee](https://paypal.me/thegrunge45)** — totally optional, always appreciated ☕

💬 **Questions or feedback? Join the [Discord](https://discord.gg/UHrEn2H6jD)** — happy to help.

---

## ⚙️ Installation & requirements

All required tools (`ffmpeg`, `ffprobe`, `dovi_tool`, `hdr10plus_tool`, `mkvmerge`) are bundled inside the binary — **no external installation required** on Windows, Linux, or macOS.

### First launch — macOS only

macOS blocks unsigned binaries. Run this **once** after downloading:

```bash
xattr -d com.apple.quarantine ./adaptive-encoder
chmod +x ./adaptive-encoder
```

After that, macOS will never warn about this file again.

---

## 🚀 Quick start

```bash
# 🐧 Linux / 🍎 macOS
chmod +x ./adaptive-encoder
./adaptive-encoder "my_movie.mkv"

# 🪟 Windows (PowerShell or CMD)
.\adaptive-encoder.exe "my_movie.mkv"
```

> 💡 **Windows tip:** Shift + right-click in the folder → "Open PowerShell window here"

**Test mode — analyze without encoding:**
```bash
./adaptive-encoder "my_movie.mkv" --dry-run
```

**Preserve grain — disable denoising entirely:**
```bash
./adaptive-encoder "35mm_film.mkv" --no-denoise
```

**Cap the bitrate (useful for size targeting):**
```bash
./adaptive-encoder "film.mkv" --vbv
```

**Normalize loudness (recommended for heterogeneous mixes):**
```bash
./adaptive-encoder "film.mkv" --normalize-audio two-pass
```

**Broadcast EBU R128 loudness (-23 LUFS):**
```bash
./adaptive-encoder "film.mkv" --normalize-audio two-pass --normalize-audio-target -23.0
```

---

## 🗂️ Batch encode an entire library

```bash
# 🐧 Linux / 🍎 macOS
for file in *.mkv; do
    ./adaptive-encoder "$file"
done
```

```powershell
# 🪟 Windows
Get-ChildItem *.mkv | ForEach-Object {
    .\adaptive-encoder.exe $_.FullName
}
```

> 💡 **Tip:** run with `--dry-run` on a single file first to verify Dolby Vision and HDR are correctly detected.

---

## 📖 All options

```
-h, --help                        Display this help message and exit
-o, --output OUTPUT               Output video file (default: <input>_adaptive.mkv)

[ Video Settings ]
--force-fps FORCE_FPS             Force video frame rate conversion (e.g., 23.976).
                                  Ensures perfect A/V sync during Dolby Vision remux.
--max-samples MAX_SAMPLES         Max number of frames to sample for analysis
--target-hours TARGET_HOURS       Fallback duration (h) if ffprobe cannot determine it
--crop-samples CROP_SAMPLES       Number of time points for crop detection
--no-crop-detect                  Disable automatic black bar detection
--base-crf BASE_CRF               Shift the adaptive CRF baseline (default: 22.0).
                                  Raise to reduce file size further; lower for
                                  closer-to-remux quality.
--downscale-1080p-sdr             Downscale source to 1080p and convert to SDR via
                                  libplacebo (BT.2390) or zscale+tonemap=mobius fallback.
                                  Output: BT.709 colors, TV range, 10-bit.

[ Bitrate & Presets ]
--max-bitrate MAX_BITRATE         Force VBV max bitrate (kbps). Useful for targeting
                                  a specific file size.
--vbv-bufsize VBV_BUFSIZE         Optional VBV buffer size (kbits)
--vbv                             Enable automatic VBV bitrate cap (off by default).
                                  When enabled, max bitrate is calibrated on the
                                  effective resolution (post-crop) using a continuous
                                  curve 12000 × ratio^0.6, anchored at 1080p = 12 Mbps.
                                  ~7 Mbps at 720p, ~17 Mbps at 1440p, ~28 Mbps at 4K,
                                  capped at 35 Mbps. By default the encoder runs in
                                  pure CRF mode — complex/grainy scenes get all the
                                  bits they need.
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
--no-hdr10plus                    Ignore HDR10+ dynamic metadata even if present in the
                                  source (encoded as HDR10 only). HDR10+ is auto-detected
                                  and embedded by default via hdr10plus_tool when no
                                  Dolby Vision is active (DV takes priority when both are
                                  present).

[ Noise Reduction ]
--no-denoise                      Disable the adaptive noise reduction. By default
                                  denoising is enabled and auto-calibrated from
                                  detected noise/grain; if the source is very clean
                                  (combined score below ~0.08), no filter is applied
                                  anyway.
--denoise-strength STRENGTH       Override denoise strength (0.0=off, 1.0=max).
                                  Overrides the automatic calibration.
--denoise-preserve-grain          40% gentler denoise that preserves some film grain
                                  texture.
--denoise-engine {auto,nlmeans,bm3d,hybrid}
                                  Force a specific denoise engine instead of automatic
                                  selection. 'nlmeans' is fast and general-purpose.
                                  'bm3d' for max quality on stationary noise (3-5x
                                  slower). 'hybrid' chains hqdn3d + nlmeans for mixed
                                  sources. 'auto' picks based on the noise/grain profile.

[ Audio & Subtitles ]
--no-audio                        Remove audio tracks (copied by default)
--no-subs                         Remove subtitle tracks (copied by default)
--audio-lang AUDIO_LANG           Keep only specific audio languages (e.g., 'fre,eng').
                                  Removes unwanted dubs to save space. The first language
                                  listed becomes the player's default track.
--downmix-audio                   Downmix heavy 7.1/Atmos tracks to standard 5.1 or 2.0.
--normalize-audio {off,single-pass,two-pass}
                                  Apply EBU R128 loudness normalization to all kept audio
                                  tracks. 'single-pass' uses dynamic linear normalization
                                  (fast, slightly less accurate — single ffmpeg pass).
                                  'two-pass' first measures the integrated loudness across
                                  the whole file then applies a linear correction (slower
                                  but precise — recommended). When active, audio is
                                  re-encoded to AC3 at 640 kbps for 5.1 or 192 kbps for
                                  stereo. Off by default.
--normalize-audio-target LUFS     Integrated loudness target in LUFS (default: -16.0,
                                  suited for TV/streaming. Use -23.0 for EBU R128
                                  broadcast).

[ System ]
--verbose                         Display technical details of adaptive analysis
--dry-run                         Display analysis and command without encoding
```

---

## ❓ FAQ

**What platforms are supported?**
Windows 10/11 (x64), Linux (x64), and macOS Apple Silicon (M1/M2/M3). All required tools (`ffmpeg`, `ffprobe`, `dovi_tool`, `hdr10plus_tool`, `mkvmerge`) are bundled inside the binary — no external installation required.

**Is this only for 4K?**
No, the tool is excellent for 1080p too. x265 parameters (`ctu`, `qg-size`, preset) are automatically tuned to the effective resolution.

**Do I need to install ffmpeg or any other tools separately?**
No. `ffmpeg`, `ffprobe`, `dovi_tool`, `hdr10plus_tool` and `mkvmerge` are all bundled inside the binary on all three platforms. Download and run — that's it.

**Do Dolby Vision and HDR10+ work automatically?**
Yes. The binary auto-detects Dolby Vision (Profile 5/7/8.x) and HDR10+ (SMPTE 2094-40) sources and preserves the metadata with no configuration. If a source carries both (rare), Dolby Vision takes priority since both carry per-frame tone-mapping and only one can be active on the display at a time.

**Does Profile 7 → 8.1 conversion work?**
Yes, it's the default. Profile 7 (FEL/MEL) is extracted and reinjected as 8.1, compatible with most modern Dolby Vision players. If you'd rather output HDR10 than accept the conversion, use `--preserve-dv-profile`.

**Is denoising active by default? Will my grain be touched?**
**Adaptive** denoising is enabled by default, but it's not applied blindly. Strength is auto-calibrated from noise and grain metrics: if the combined score is below ~0.08, no filter is applied. On a clean source (recent Blu-ray without heavy grain), you'll get no processing. On a heavily-grained 35mm film, you'll get moderate denoising. To guarantee zero filtering regardless of the source, use `--no-denoise`. For a compromise (preserve some grain texture), use `--denoise-preserve-grain`.

**When should I use `--normalize-audio`?**
Mostly for heterogeneous libraries (films from different decades, mix of sources, dubs recorded at varying levels). The `two-pass` mode first measures integrated loudness across the whole file then applies a linear correction — the same approach Netflix/Apple/YouTube use on their platform side. Default target `-16 LUFS` is calibrated for TV/streaming; for strict EBU R128 broadcast, use `-23.0`. Important: enabling normalization forces audio re-encoding (AC3), so you lose the bit-perfect original audio. Without `--normalize-audio`, audio tracks are stream-copied.

**Why are my files larger than with other encoders?**
Intentional design choice — detail and HDR metadata preservation. To reduce file size, use `--vbv` (enables a resolution-aware cap), `--max-bitrate` (forces a manual cap), or raise `--base-crf`.

**Encoding speed?**
The tool uses x265 `slower` or `veryslow` presets depending on content complexity — not a fast encoder, a *good* one. For faster encoding use `--no-veryslow`. Note: `--normalize-audio two-pass` adds an audio measurement pass (proportional to film duration, no video encoding involved).

**What if it doesn't work for my files?**
Open an issue on GitHub or ask on Discord — happy to help.

---

## 📧 Support

- 💬 **Discord** (fast replies): [https://discord.gg/UHrEn2H6jD](https://discord.gg/UHrEn2H6jD)
- 📧 **Email**: [osx300@gmail.com](mailto:osx300@gmail.com)
- ☕ **Buy me a coffee** (optional): [paypal.me/thegrunge45](https://paypal.me/thegrunge45)
