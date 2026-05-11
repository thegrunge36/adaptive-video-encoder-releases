> 🇫🇷 **Français** ci-dessous — 🇬🇧 **English** follows below
>
> *La version française est en premier. / The French version comes first.*

---

# 🎬 Adaptive Video Encoder
> 🇫🇷 **Français** ci-dessous — 🇬🇧 **English** follows below
>
> *La version française est en premier. / The French version comes first.*

---

# 🎬 Adaptive Video Encoder

> **L'encodeur H.265 qui ne casse pas votre Dolby Vision.**

[![Discord](https://img.shields.io/badge/Discord-Rejoindre-5865F2?logo=discord&logoColor=white)](https://discord.gg/UHrEn2H6jD) [![Buy me a coffee](https://img.shields.io/badge/Un%20café-PayPal-00457C?logo=paypal&logoColor=white)](https://paypal.me/thegrunge45)

---

## Réencodez votre vidéothèque sans compromis de qualité

Vous avez une vidéothèque pleine de remux Blu-ray 1080p, de rips Dolby Vision 4K, de sources HDR10 ou HLG. Vous voulez réencoder en H.265 pour récupérer des téraoctets — sans détruire les métadonnées qui font s'afficher vos films correctement sur votre OLED.

**Le problème :** La plupart des outils H.265 suppriment les métadonnées Dolby Vision Profil 7 ou lissent le grain par défaut. ffmpeg en manuel nécessite des heures de tests pour trouver les bons paramètres — et ces paramètres changent pour chaque vidéo (grain, bruit, mouvement, complexité).

**La solution :** Adaptive Video Encoder analyse chaque vidéo image par image *avant* l'encodage, choisit automatiquement les meilleurs paramètres x265, et préserve intégralement votre Dolby Vision (Profil 5, 7, 8.x), ainsi que les métadonnées HDR10 et HLG.

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
- Vous êtes à l'aise avec la ligne de commande
- Vous en avez marre de régler les paramètres x265 et de comparer 12 versions du même film

## ⚠️ Pas pour vous si...

- Vous cherchez une compression maximale pour économiser l'espace disque
- Vous encodez surtout du contenu SDR simple sans grain (comédies récentes en intérieur, animation fluide, talking heads) — dans ces cas, des outils plus simples donnent souvent de meilleurs taux de compression
- Vous voulez une interface graphique
- Vous avez besoin d'un encodage rapide (l'outil privilégie la qualité, pas la vitesse)

---

## ⚡ Pourquoi un encodeur adaptatif dédié ?

| | Encodeurs génériques | ffmpeg manuel | **Adaptive Video Encoder** |
|---|---|---|---|
| Dolby Vision Profil 7 | ❌ Cassé | ⚠️ Possible avec `dovi_tool` + scripts | ✅ Automatique |
| Préservation du grain | ❌ Lissé par défaut | ⚠️ Si vous savez quoi activer | ✅ Préservé par défaut, jamais touché sans `--denoise` |
| Paramètres adaptés *par vidéo* | ❌ Préréglages fixes | ⚠️ Si vous testez vous-même | ✅ Analyse image par image |
| HDR10 / HLG préservé | ⚠️ Parfois | ⚠️ Si vous savez quoi activer | ✅ Toujours |
| Anti-banding adaptatif | ❌ Absent ou cassant le grain | ⚠️ Manuel et global | ✅ Activé sur scènes sombres uniquement |
| Détection des bandes noires | ✅ | ⚠️ Manuel | ✅ Automatique |
| Temps de configuration | 5 min | 1-3 h par film | **0 min** |

---

## 🎞️ Particulièrement excellent sur les Blu-rays 1080p

Beaucoup d'utilisateurs pensent à tort que cet outil est réservé à la 4K. **Ce n'est pas le cas.** Adaptive Video Encoder brille particulièrement sur les remux Blu-ray 1080p pour 3 raisons :

**1. Préservation du grain cinématique.** Les films classiques, les films d'horreur, les films d'auteur récents en 35mm ont un grain qui fait partie de leur identité visuelle. La plupart des encodeurs le lissent par défaut. Adaptive Encoder ne touche jamais au grain sans votre accord explicite via `--denoise`.

**2. Détection adaptative des scènes complexes.** Sur un film d'action 1080p, les scènes de combat ont une complexité radicalement différente des dialogues. L'analyse image par image ajuste les paramètres x265 en conséquence, là où les encodeurs génériques utilisent les mêmes réglages du début à la fin.

**3. Préservation des métadonnées HDR10 1080p.** Certains Blu-rays récents ont le HDR10 en 1080p. Adaptive Encoder préserve tout : master display, MaxCLL/MaxFALL, primaires de couleur.

**Moins pertinent pour :** le contenu numérique récent avec une image propre (comédies romantiques, sitcoms, documentaires en intérieur). Ces sources n'ont ni grain ni détail complexe à préserver.

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

- 🔍 **Analyse adaptative** — détecte le bruit, le grain, la complexité, la densité de contours pour régler x265
- 📺 **Dolby Vision Profil 5, 7, 8.x** — métadonnées extraites, préservées, réinjectées
- 🎨 **HDR10 et HLG** — primaires de couleur, transferts, master display, MaxCLL/MaxFALL préservés
- 🎞️ **Grain préservé par défaut** — aucun débruitage appliqué sans `--denoise` explicite
- 🧹 **Mode nettoyage gros grain** — chaîne `atadenoise+vaguedenoiser` opt-in via `--manual-grain-clean` pour les films au grain trop marqué
- 🌑 **Anti-banding adaptatif** — détecte les scènes sombres à faible grain (où le banding apparaît) et applique `gradfun` + `SAO` ciblé + bonus CRF pour lisser les dégradés sans toucher au reste du film. Désactivable via `--no-debanding`.
- ✂️ **Recadrage intelligent** — détecte les bandes noires sans couper accidentellement le contenu
- 🔊 **Toutes les pistes audio et sous-titres** copiées par défaut, zéro perte
- 🎞️ **Formats supportés** — MKV, MP4, MOV, AVI, MXF, WebM, M4V, TS
- 📐 **Résolutions** — 480p à 8K (excellent pour 1080p ET 4K)
- 📦 **Binaire unique, zéro dépendance** — ffmpeg, ffprobe, dovi_tool, hdr10plus_tool et mkvmerge intégrés sur les trois plateformes. Aucun outil externe à installer.

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

Tous les outils nécessaires (ffmpeg, ffprobe, dovi_tool, hdr10plus_tool, mkvmerge) sont intégrés dans le binaire — **aucune installation externe requise** sur Windows, Linux ou macOS.

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

**Film à gros grain — nettoyage propre :**
```bash
./adaptive-encoder "vieux_film_35mm.mkv" --manual-grain-clean
```

**Film à très gros grain — désactiver l'anti-banding pour préserver chaque grain :**
```bash
./adaptive-encoder "film_35mm.mkv" --no-debanding
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
--downscale-1080p-sdr             Réduit la source à 1080p et convertit en SDR.
                                  Applique un tone mapping pour les écrans non-HDR.
--no-debanding                    Désactive toute la chaîne anti-banding ajoutée par défaut :
                                  filtre gradfun final, deband libplacebo sur le chemin
                                  HDR→SDR, activation conditionnelle du SAO sur scènes
                                  sombres, et bonus CRF appliqué aux plans à forte fraction
                                  de bas-noirs. À utiliser sur les films à très gros grain
                                  où gradfun pourrait lisser la texture, ou pour reproduire
                                  le comportement de l'encodeur avant l'ajout de la chaîne
                                  anti-banding. Off par défaut (anti-banding actif).
--base-crf BASE_CRF               Décale la base du CRF adaptatif (défaut : 22.0).
                                  Calibré pour un bon équilibre qualité/taille (~50% de
                                  réduction sur les remux Blu-ray typiques).
                                  Augmenter réduit la taille du fichier au détriment
                                  de la qualité visuelle.

[ Débit & Préréglages ]
--max-bitrate MAX_BITRATE         Force le débit max VBV (kbps). Utile pour cibler
                                  une taille de fichier précise.
--vbv-bufsize VBV_BUFSIZE         Taille optionnelle du buffer VBV (kbits)
--vbv                             Active le plafonnement automatique du débit VBV
                                  (~12 Mbps pour 1080p, adapté à la résolution).
                                  Désactivé par défaut — le mode CRF pur donne plus
                                  de bits aux scènes complexes et granuleuses.
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
                                  et embarqué automatiquement.

[ Réduction du bruit ]
--denoise                         Active la réduction de bruit adaptative. Désactivée par
                                  défaut pour préserver le grain cinématique des Blu-rays.
                                  La force est calibrée automatiquement selon le niveau
                                  de bruit/grain détecté dans la source.
--denoise-strength STRENGTH       Force la force du débruitage (0.0=off, 1.0=max).
                                  Implique --denoise quand > 0.
--denoise-preserve-grain          Débruitage plus doux qui préserve une partie de la texture
                                  du grain. Implique --denoise.
--denoise-engine {auto,nlmeans,bm3d,hybrid,atadenoise,wavelet,fftdnoiz,grain-clean}
                                  Force un moteur de débruitage spécifique au lieu de la
                                  sélection automatique. 'grain-clean' chaîne
                                  atadenoise+vaguedenoiser — idéal pour gros grain
                                  cinématique. 'atadenoise' seul, rapide et excellent
                                  sur grain modéré (moyenne temporelle à seuil de
                                  mouvement). 'wavelet' (vaguedenoiser) doux, préserve
                                  les détails fins via ondelettes. 'fftdnoiz' débruiteur
                                  FFT 3D. 'bm3d' qualité maximale sur bruit stationnaire
                                  (3-5x plus lent). 'nlmeans' rapide. 'hybrid' mixe
                                  hqdn3d+nlmeans. Implique --denoise.
--manual-grain-clean              Mode manuel haute qualité pour films à gros grain.
                                  Active la chaîne atadenoise + vaguedenoiser avec force
                                  calibrée automatiquement à partir des niveaux de grain
                                  et bruit détectés. Équivalent à
                                  `--denoise --denoise-engine grain-clean` mais avec un
                                  plancher de force ≥ 0.55 pour garantir un nettoyage
                                  efficace. CPU uniquement, surcoût ~0.4× temps réel
                                  sur 1080p.

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
                                  normalisation linéaire dynamique (rapide, moins précise).
                                  'two-pass' mesure d'abord tout le fichier puis normalise
                                  (plus lent mais précis — recommandé). Ré-encode l'audio
                                  en AC3 à 640 kbps pour 5.1 / 192 kbps pour stéréo.
--normalize-audio-target LUFS     Cible de loudness intégrée en LUFS (défaut : -16.0, adapté
                                  à la TV/streaming. Utiliser -23.0 pour EBU R128 broadcast).

[ Encodage parallèle par chunks (expérimental) ]
--parallel-chunks N               Encode N chunks en parallèle (1 = encodage monolithique,
                                  défaut). Découpe la source aux coupures de scène en chunks
                                  d'environ 5 min et les encode simultanément. Énorme
                                  accélération sur les machines multi-cœurs. Incompatible
                                  avec Dolby Vision, HDR10+, --normalize-audio
                                  et --downmix-audio.
--chunk-seconds CHUNK_SECONDS     Durée cible d'un chunk en secondes pour --parallel-chunks
                                  (défaut : 300). Plus petit = plus de parallélisme,
                                  légèrement plus d'overhead conteneur. Plus grand = plus
                                  proche du monolithique.
--resume                          Reprend un encodage chunked interrompu via son manifest
                                  sidecar (<output>.chunks.json). Les chunks déjà terminés
                                  sont sautés. Implique --parallel-chunks (utiliser la même
                                  valeur qu'au run d'origine).

[ Système ]
--verbose                         Affiche les détails techniques de l'analyse adaptative
--dry-run                         Affiche l'analyse et la commande sans encoder
```

---

## ❓ FAQ

**Quelles plateformes sont supportées ?**
Windows 10/11 (x64), Linux (x64), et macOS Apple Silicon (M1/M2/M3). Tous les outils nécessaires (ffmpeg, ffprobe, dovi_tool, hdr10plus_tool, mkvmerge) sont intégrés dans le binaire — aucune installation externe requise.

**C'est seulement pour la 4K ?**
Non, l'outil est excellent en 1080p aussi. Particulièrement sur les remux Blu-ray avec grain cinématique (classiques, horreur, films d'auteur 35mm) ou les scènes complexes (action, sci-fi).

**Dois-je installer ffmpeg ou d'autres outils séparément ?**
Non. ffmpeg, ffprobe, dovi_tool, hdr10plus_tool et mkvmerge sont tous intégrés dans le binaire sur les trois plateformes. Téléchargez et lancez, c'est tout.

**Le Dolby Vision et le HDR10+ fonctionnent automatiquement ?**
Oui. Le binaire détecte automatiquement les sources Dolby Vision (Profil 5/7/8.x) et HDR10+ (SMPTE 2094-40) puis préserve les métadonnées sans configuration. Si la source contient les deux (rare), Dolby Vision prend la priorité.

**La conversion Profil 7 → 8.1 fonctionne ?**
Oui, c'est le comportement par défaut. Le Profil 7 (FEL/MEL) est extrait et réinjecté en 8.1, compatible avec la plupart des lecteurs Dolby Vision modernes.

**Pourquoi mes fichiers sont-ils plus lourds qu'avec d'autres encodeurs ?**
Choix de conception délibéré — préservation maximale du détail et des métadonnées HDR. Pour limiter la taille du fichier, utilisez `--max-bitrate` ou augmentez `--base-crf`.

**Le grain de mes Blu-rays est-il préservé ?**
Oui. Le débruitage est désactivé par défaut — aucun traitement n'est appliqué sur le grain sans votre accord explicite via `--denoise`. Le CRF adaptatif (base 22.0) traite le grain comme une feature à conserver, pas comme du bruit à éliminer.

**J'ai un film au grain vraiment trop marqué, comment le nettoyer proprement ?**
Utilisez `--manual-grain-clean`. Ce mode active une chaîne dédiée `atadenoise + vaguedenoiser` qui attaque le grain temporel (frame-à-frame) puis le résidu spatial via ondelettes, sans effet plastique sur la peau ou les détails fins. La force est auto-calibrée selon le niveau de grain détecté, avec un plancher minimum pour garantir un résultat propre.

**Qu'est-ce que l'anti-banding adaptatif et quand le désactiver ?**
Le banding (paliers de couleur visibles dans les dégradés sombres ou les ciels) est un artefact classique de l'encodage H.265 sur les scènes à dynamique limitée. Adaptive Video Encoder détecte automatiquement les plans à risque (forte fraction de pixels sombres, faible niveau de grain) et active une chaîne ciblée : `gradfun` en post-filtrage, `SAO` selectif sur I-frames, et un léger bonus CRF pour mieux allouer les bits à ces zones. Le grain n'est pas affecté car la chaîne se déclenche uniquement quand le grain détecté est bas. **À désactiver via `--no-debanding`** dans deux cas : (1) film à très gros grain sur toute sa durée où gradfun risquerait de lisser la texture, (2) pour reproduire le comportement de l'encodeur avant l'ajout de cette chaîne (encodes legacy).

**Vitesse d'encodage ?**
L'outil utilise les préréglages x265 `slower` ou `veryslow` — pas un encodeur rapide, un *bon* encodeur. Pour un encodage plus rapide, utilisez `--no-veryslow`.

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

You have a video library full of 1080p Blu-rays, 4K Dolby Vision rips, HDR10 or HLG sources. You want to re-encode to H.265 to reclaim terabytes — without destroying the metadata that makes your movies display correctly on your OLED.

**The problem:** Most H.265 tools strip out Dolby Vision Profile 7 metadata or smooth grain by default. Manual ffmpeg requires hours of testing to find the right parameters — and those parameters change for every video (grain, noise, motion, complexity).

**The solution:** Adaptive Video Encoder analyzes each video frame by frame *before* encoding, automatically picks the best x265 parameters, and fully preserves your Dolby Vision (Profile 5, 7, 8.x), HDR10 and HLG metadata.

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
- You're comfortable with the command line
- You're tired of tweaking x265 parameters and comparing 12 versions of the same film

## ⚠️ Not for you if...

- You're looking for maximum compression to save disk space
- You mostly encode simple SDR content without grain (recent indoor comedies, smooth animation, talking heads) — for those cases, simpler tools often give better compression ratios
- You want a GUI
- You need fast encoding (the tool prioritizes quality, not speed)

---

## ⚡ Why a dedicated adaptive encoder?

| | Generic encoders | Manual ffmpeg | **Adaptive Video Encoder** |
|---|---|---|---|
| Dolby Vision Profile 7 | ❌ Broken | ⚠️ Possible with `dovi_tool` + scripting | ✅ Automatic |
| Grain preservation | ❌ Smoothed by default | ⚠️ If you know what to flag | ✅ Preserved by default, never touched without `--denoise` |
| Settings adapted *per video* | ❌ Fixed presets | ⚠️ If you test yourself | ✅ Frame-by-frame analysis |
| HDR10 / HLG preserved | ⚠️ Sometimes | ⚠️ If you know what to flag | ✅ Always |
| Adaptive anti-banding | ❌ Absent or kills grain | ⚠️ Manual and global | ✅ Triggered on dark scenes only |
| Black bar detection | ✅ | ⚠️ Manual | ✅ Automatic |
| Setup time | 5 min | 1-3 h per film | **0 min** |

---

## 🎞️ Particularly excellent on 1080p Blu-rays

Many users mistakenly think this tool is only for 4K. **It's not.** Adaptive Video Encoder shines particularly well on 1080p Blu-ray remuxes for 3 reasons:

**1. Film grain preservation.** Classic films, horror movies, recent 35mm auteur films have grain that's part of their visual identity. Most encoders smooth it by default. Adaptive Encoder never touches grain without your explicit `--denoise` flag.

**2. Adaptive complex scene detection.** On a 1080p action film, fight scenes have radically different complexity than dialogue. Frame-by-frame analysis adjusts x265 parameters accordingly, where generic encoders use the same settings start to finish.

**3. 1080p HDR10 metadata preservation.** Some recent Blu-rays have HDR10 in 1080p. Adaptive Encoder preserves everything: master display, MaxCLL/MaxFALL, color primaries.

**Less relevant for:** recently-shot digital content with clean image (romantic comedies, sitcoms, indoor documentaries). Those sources have neither grain nor complex detail to preserve.

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

- 🔍 **Adaptive analysis** — detects noise, grain, complexity, edge density to tune x265
- 📺 **Dolby Vision Profile 5, 7, 8.x** — metadata extracted, preserved, reinjected
- 🎨 **HDR10 and HLG** — color primaries, transfers, master display, MaxCLL/MaxFALL preserved
- 🎞️ **Grain preserved by default** — no denoising ever applied without explicit `--denoise`
- 🧹 **Heavy-grain cleanup mode** — opt-in `atadenoise+vaguedenoiser` chain via `--manual-grain-clean` for films where the grain is too heavy to keep
- 🌑 **Adaptive anti-banding** — detects dark scenes with low grain (where banding shows) and applies `gradfun` + targeted `SAO` + a small CRF bonus to smooth gradients without touching the rest of the film. Disable via `--no-debanding`.
- ✂️ **Smart crop** — detects black bars without accidentally cutting content
- 🔊 **All audio and subtitle tracks** copied by default, zero loss
- 🎞️ **Supported formats** — MKV, MP4, MOV, AVI, MXF, WebM, M4V, TS
- 📐 **Resolutions** — 480p to 8K (excellent for 1080p AND 4K)
- 📦 **Single binary, zero dependencies** — ffmpeg, ffprobe, dovi_tool, hdr10plus_tool and mkvmerge bundled on all three platforms. Nothing to install separately.

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

All required tools (ffmpeg, ffprobe, dovi_tool, hdr10plus_tool, mkvmerge) are bundled inside the binary — **no external installation required** on Windows, Linux, or macOS.

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

**Heavy-grain film — clean cleanup:**
```bash
./adaptive-encoder "old_35mm_film.mkv" --manual-grain-clean
```

**Very heavy grain — disable anti-banding to preserve every grain particle:**
```bash
./adaptive-encoder "35mm_film.mkv" --no-debanding
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
--downscale-1080p-sdr             Downscale source to 1080p and convert to SDR.
                                  Applies tone mapping for non-HDR display compatibility.
--no-debanding                    Disable the full anti-banding chain that runs by default:
                                  final gradfun post-filter, libplacebo deband on the
                                  HDR→SDR path, conditional SAO activation on dark scenes,
                                  and the CRF bonus applied to dark-fraction-heavy shots.
                                  Use this on films with very heavy grain throughout where
                                  gradfun could smooth texture, or to reproduce the
                                  encoder behavior from before the anti-banding chain was
                                  added (legacy encodes). Off by default (anti-banding on).
--base-crf BASE_CRF               Shifts the adaptive CRF baseline (default: 22.0).
                                  Tuned for a good quality/size balance (~50% reduction
                                  on typical Blu-ray remuxes). Raise to reduce file size
                                  further; lower for closer-to-remux quality.

[ Bitrate & Presets ]
--max-bitrate MAX_BITRATE         Force VBV max bitrate (kbps). Useful for targeting
                                  a specific file size.
--vbv-bufsize VBV_BUFSIZE         Optional VBV buffer size (kbits)
--vbv                             Enable automatic VBV bitrate cap (~12 Mbps for 1080p,
                                  scaled by resolution). Off by default — pure CRF mode
                                  gives complex/grainy scenes all the bits they need.
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
                                  and embedded by default.

[ Noise Reduction ]
--denoise                         Enable adaptive noise reduction. Off by default to
                                  preserve film grain on Blu-ray and cinema content.
                                  Strength is auto-calibrated from source noise/grain
                                  metrics.
--denoise-strength STRENGTH       Override denoise strength (0.0=off, 1.0=max).
                                  Implies --denoise when > 0.
--denoise-preserve-grain          Gentler denoise that preserves some film grain texture.
                                  Implies --denoise.
--denoise-engine {auto,nlmeans,bm3d,hybrid,atadenoise,wavelet,fftdnoiz,grain-clean}
                                  Force a specific denoise engine instead of automatic
                                  selection. 'grain-clean' chains atadenoise+vaguedenoiser
                                  — ideal for heavy film grain. 'atadenoise' alone is fast
                                  and excellent on moderate grain (motion-thresholded
                                  temporal averaging). 'wavelet' (vaguedenoiser) is gentle
                                  and preserves fine detail via wavelets. 'fftdnoiz' is a
                                  3D FFT denoiser. 'bm3d' for max quality on stationary
                                  noise (3-5x slower). 'nlmeans' for speed. 'hybrid' mixes
                                  hqdn3d+nlmeans. Implies --denoise.
--manual-grain-clean              Manual high-quality cleanup mode for films with heavy
                                  grain. Activates the atadenoise + vaguedenoiser chain
                                  with strength auto-calibrated from detected grain/noise
                                  levels. Equivalent to
                                  `--denoise --denoise-engine grain-clean` but with a
                                  strength floor of ≥ 0.55 to guarantee effective cleanup.
                                  CPU-only, ~0.4× realtime additional cost on 1080p.

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
                                  (fast, less accurate). 'two-pass' measures the whole
                                  file first then normalizes (slower but precise —
                                  recommended). Re-encodes audio to AC3 at 640 kbps for
                                  5.1 / 192 kbps for stereo.
--normalize-audio-target LUFS     Integrated loudness target in LUFS (default: -16.0,
                                  suited for TV/streaming. Use -23.0 for EBU R128 broadcast).

[ Parallel chunked encoding (experimental) ]
--parallel-chunks N               Encode N chunks in parallel (1 = monolithic encoding,
                                  default). Splits the source at scene cuts into ~5 min
                                  chunks and encodes them concurrently. Massive speedup
                                  on multi-core boxes. Incompatible with Dolby Vision,
                                  HDR10+, --normalize-audio, and --downmix-audio.
--chunk-seconds CHUNK_SECONDS     Target chunk length in seconds for --parallel-chunks
                                  (default: 300). Smaller = more parallelism, slightly
                                  more container overhead. Larger = closer to monolithic.
--resume                          Resume an interrupted chunked encode using its manifest
                                  sidecar (<output>.chunks.json). Already-completed chunks
                                  are skipped. Implies --parallel-chunks (use the same
                                  value as the original run).

[ System ]
--verbose                         Display technical details of adaptive analysis
--dry-run                         Display analysis and command without encoding
```

---

## ❓ FAQ

**What platforms are supported?**
Windows 10/11 (x64), Linux (x64), and macOS Apple Silicon (M1/M2/M3). All required tools (ffmpeg, ffprobe, dovi_tool, hdr10plus_tool, mkvmerge) are bundled inside the binary — no external installation required.

**Is this only for 4K?**
No, the tool is excellent for 1080p too. Particularly on Blu-ray remuxes with film grain (classics, horror, 35mm auteur films) or complex scenes (action, sci-fi).

**Do I need to install ffmpeg or any other tools separately?**
No. ffmpeg, ffprobe, dovi_tool, hdr10plus_tool and mkvmerge are all bundled inside the binary on all three platforms. Download and run — that's it.

**Do Dolby Vision and HDR10+ work automatically?**
Yes. The binary auto-detects Dolby Vision (Profile 5/7/8.x) and HDR10+ (SMPTE 2094-40) sources and preserves the metadata with no configuration. If a source carries both (rare), Dolby Vision takes priority.

**Does Profile 7 → 8.1 conversion work?**
Yes, it's the default. Profile 7 (FEL/MEL) is extracted and reinjected as 8.1, compatible with most modern Dolby Vision players.

**Why are my files larger than with other encoders?**
Intentional design choice — maximum detail and HDR metadata preservation. To reduce file size, use `--max-bitrate` or raise `--base-crf`.

**Is film grain preserved?**
Yes. Noise reduction is off by default — no processing is ever applied to grain without your explicit `--denoise` flag. The adaptive CRF (base 22.0) treats grain as a feature to keep, not noise to eliminate.

**My film has really heavy grain — how do I clean it up properly?**
Use `--manual-grain-clean`. This mode activates a dedicated `atadenoise + vaguedenoiser` chain that attacks temporal grain frame-to-frame first, then cleans the spatial residue via wavelets — without the plastic look on skin or fine detail. Strength is auto-calibrated from the detected grain level, with a minimum floor to guarantee a clean result.

**What is adaptive anti-banding and when should I turn it off?**
Banding (visible color steps in dark gradients or skies) is a classic H.265 artifact on scenes with limited dynamic range. Adaptive Video Encoder automatically detects at-risk shots (high dark-pixel fraction, low grain level) and triggers a targeted chain: `gradfun` post-filter, `SAO` selectively enabled on I-frames, and a small CRF bonus to better allocate bits to those zones. Grain isn't affected because the chain only fires when detected grain is low. **Disable via `--no-debanding`** in two cases: (1) films with heavy grain throughout where gradfun might smooth texture, (2) to reproduce the encoder's behavior before this chain was added (legacy encodes).

**Encoding speed?**
The tool uses x265 `slower` or `veryslow` presets — not a fast encoder, a *good* one. For faster encoding use `--no-veryslow`.

**What if it doesn't work for my files?**
Open an issue on GitHub or ask on Discord — happy to help.

---

## 📧 Support

- 💬 **Discord** (fast replies): [https://discord.gg/UHrEn2H6jD](https://discord.gg/UHrEn2H6jD)
- 📧 **Email**: [osx300@gmail.com](mailto:osx300@gmail.com)
- ☕ **Buy me a coffee** (optional): [paypal.me/thegrunge45](https://paypal.me/thegrunge45)
> **L'encodeur H.265 qui ne casse pas votre Dolby Vision.**

[![Discord](https://img.shields.io/badge/Discord-Rejoindre-5865F2?logo=discord&logoColor=white)](https://discord.gg/UHrEn2H6jD) [![Buy me a coffee](https://img.shields.io/badge/Un%20café-PayPal-00457C?logo=paypal&logoColor=white)](https://paypal.me/thegrunge45)

---

## Réencodez votre vidéothèque sans compromis de qualité

Vous avez une vidéothèque pleine de remux Blu-ray 1080p, de rips Dolby Vision 4K, de sources HDR10 ou HLG. Vous voulez réencoder en H.265 pour récupérer des téraoctets — sans détruire les métadonnées qui font s'afficher vos films correctement sur votre OLED.

**Le problème :** La plupart des outils H.265 suppriment les métadonnées Dolby Vision Profil 7 ou lissent le grain par défaut. ffmpeg en manuel nécessite des heures de tests pour trouver les bons paramètres — et ces paramètres changent pour chaque vidéo (grain, bruit, mouvement, complexité).

**La solution :** Adaptive Video Encoder analyse chaque vidéo image par image *avant* l'encodage, choisit automatiquement les meilleurs paramètres x265, et préserve intégralement votre Dolby Vision (Profil 5, 7, 8.x), ainsi que les métadonnées HDR10 et HLG.

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
- Vous êtes à l'aise avec la ligne de commande
- Vous en avez marre de régler les paramètres x265 et de comparer 12 versions du même film

## ⚠️ Pas pour vous si...

- Vous cherchez une compression maximale pour économiser l'espace disque
- Vous encodez surtout du contenu SDR simple sans grain (comédies récentes en intérieur, animation fluide, talking heads) — dans ces cas, des outils plus simples donnent souvent de meilleurs taux de compression
- Vous voulez une interface graphique
- Vous avez besoin d'un encodage rapide (l'outil privilégie la qualité, pas la vitesse)

---

## ⚡ Pourquoi un encodeur adaptatif dédié ?

| | Encodeurs génériques | ffmpeg manuel | **Adaptive Video Encoder** |
|---|---|---|---|
| Dolby Vision Profil 7 | ❌ Cassé | ⚠️ Possible avec `dovi_tool` + scripts | ✅ Automatique |
| Préservation du grain | ❌ Lissé par défaut | ⚠️ Si vous savez quoi activer | ✅ Préservé par défaut, jamais touché sans `--denoise` |
| Paramètres adaptés *par vidéo* | ❌ Préréglages fixes | ⚠️ Si vous testez vous-même | ✅ Analyse image par image |
| HDR10 / HLG préservé | ⚠️ Parfois | ⚠️ Si vous savez quoi activer | ✅ Toujours |
| Détection des bandes noires | ✅ | ⚠️ Manuel | ✅ Automatique |
| Temps de configuration | 5 min | 1-3 h par film | **0 min** |

---

## 🎞️ Particulièrement excellent sur les Blu-rays 1080p

Beaucoup d'utilisateurs pensent à tort que cet outil est réservé à la 4K. **Ce n'est pas le cas.** Adaptive Video Encoder brille particulièrement sur les remux Blu-ray 1080p pour 3 raisons :

**1. Préservation du grain cinématique.** Les films classiques, les films d'horreur, les films d'auteur récents en 35mm ont un grain qui fait partie de leur identité visuelle. La plupart des encodeurs le lissent par défaut. Adaptive Encoder ne touche jamais au grain sans votre accord explicite via `--denoise`.

**2. Détection adaptative des scènes complexes.** Sur un film d'action 1080p, les scènes de combat ont une complexité radicalement différente des dialogues. L'analyse image par image ajuste les paramètres x265 en conséquence, là où les encodeurs génériques utilisent les mêmes réglages du début à la fin.

**3. Préservation des métadonnées HDR10 1080p.** Certains Blu-rays récents ont le HDR10 en 1080p. Adaptive Encoder préserve tout : master display, MaxCLL/MaxFALL, primaires de couleur.

**Moins pertinent pour :** le contenu numérique récent avec une image propre (comédies romantiques, sitcoms, documentaires en intérieur). Ces sources n'ont ni grain ni détail complexe à préserver.

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

- 🔍 **Analyse adaptative** — détecte le bruit, le grain, la complexité, la densité de contours pour régler x265
- 📺 **Dolby Vision Profil 5, 7, 8.x** — métadonnées extraites, préservées, réinjectées
- 🎨 **HDR10 et HLG** — primaires de couleur, transferts, master display, MaxCLL/MaxFALL préservés
- 🎞️ **Grain préservé par défaut** — aucun débruitage appliqué sans `--denoise` explicite
- 🧹 **Mode nettoyage gros grain** — chaîne `atadenoise+vaguedenoiser` opt-in via `--manual-grain-clean` pour les films au grain trop marqué
- ✂️ **Recadrage intelligent** — détecte les bandes noires sans couper accidentellement le contenu
- 🔊 **Toutes les pistes audio et sous-titres** copiées par défaut, zéro perte
- 🎞️ **Formats supportés** — MKV, MP4, MOV, AVI, MXF, WebM, M4V, TS
- 📐 **Résolutions** — 480p à 8K (excellent pour 1080p ET 4K)
- 📦 **Binaire unique, zéro dépendance** — ffmpeg, ffprobe, dovi_tool, hdr10plus_tool et mkvmerge intégrés sur les trois plateformes. Aucun outil externe à installer.

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

Tous les outils nécessaires (ffmpeg, ffprobe, dovi_tool, hdr10plus_tool, mkvmerge) sont intégrés dans le binaire — **aucune installation externe requise** sur Windows, Linux ou macOS.

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

**Film à gros grain — nettoyage propre :**
```bash
./adaptive-encoder "vieux_film_35mm.mkv" --manual-grain-clean
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
--downscale-1080p-sdr             Réduit la source à 1080p et convertit en SDR.
                                  Applique un tone mapping pour les écrans non-HDR.
--base-crf BASE_CRF               Décale la base du CRF adaptatif (défaut : 22.0).
                                  Calibré pour un bon équilibre qualité/taille (~50% de
                                  réduction sur les remux Blu-ray typiques).
                                  Augmenter réduit la taille du fichier au détriment
                                  de la qualité visuelle.

[ Débit & Préréglages ]
--max-bitrate MAX_BITRATE         Force le débit max VBV (kbps). Utile pour cibler
                                  une taille de fichier précise.
--vbv-bufsize VBV_BUFSIZE         Taille optionnelle du buffer VBV (kbits)
--vbv                             Active le plafonnement automatique du débit VBV
                                  (~12 Mbps pour 1080p, adapté à la résolution).
                                  Désactivé par défaut — le mode CRF pur donne plus
                                  de bits aux scènes complexes et granuleuses.
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
                                  et embarqué automatiquement.

[ Réduction du bruit ]
--denoise                         Active la réduction de bruit adaptative. Désactivée par
                                  défaut pour préserver le grain cinématique des Blu-rays.
                                  La force est calibrée automatiquement selon le niveau
                                  de bruit/grain détecté dans la source.
--denoise-strength STRENGTH       Force la force du débruitage (0.0=off, 1.0=max).
                                  Implique --denoise quand > 0.
--denoise-preserve-grain          Débruitage plus doux qui préserve une partie de la texture
                                  du grain. Implique --denoise.
--denoise-engine {auto,nlmeans,bm3d,hybrid,atadenoise,wavelet,fftdnoiz,grain-clean}
                                  Force un moteur de débruitage spécifique au lieu de la
                                  sélection automatique. 'grain-clean' chaîne
                                  atadenoise+vaguedenoiser — idéal pour gros grain
                                  cinématique. 'atadenoise' seul, rapide et excellent
                                  sur grain modéré (moyenne temporelle à seuil de
                                  mouvement). 'wavelet' (vaguedenoiser) doux, préserve
                                  les détails fins via ondelettes. 'fftdnoiz' débruiteur
                                  FFT 3D. 'bm3d' qualité maximale sur bruit stationnaire
                                  (3-5x plus lent). 'nlmeans' rapide. 'hybrid' mixe
                                  hqdn3d+nlmeans. Implique --denoise.
--manual-grain-clean              Mode manuel haute qualité pour films à gros grain.
                                  Active la chaîne atadenoise + vaguedenoiser avec force
                                  calibrée automatiquement à partir des niveaux de grain
                                  et bruit détectés. Équivalent à
                                  `--denoise --denoise-engine grain-clean` mais avec un
                                  plancher de force ≥ 0.55 pour garantir un nettoyage
                                  efficace. CPU uniquement, surcoût ~0.4× temps réel
                                  sur 1080p.

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
                                  normalisation linéaire dynamique (rapide, moins précise).
                                  'two-pass' mesure d'abord tout le fichier puis normalise
                                  (plus lent mais précis — recommandé). Ré-encode l'audio
                                  en AC3 à 640 kbps pour 5.1 / 192 kbps pour stéréo.
--normalize-audio-target LUFS     Cible de loudness intégrée en LUFS (défaut : -16.0, adapté
                                  à la TV/streaming. Utiliser -23.0 pour EBU R128 broadcast).

[ Encodage parallèle par chunks (expérimental) ]
--parallel-chunks N               Encode N chunks en parallèle (1 = encodage monolithique,
                                  défaut). Découpe la source aux coupures de scène en chunks
                                  d'environ 5 min et les encode simultanément. Énorme
                                  accélération sur les machines multi-cœurs. Incompatible
                                  avec Dolby Vision, HDR10+, --normalize-audio
                                  et --downmix-audio.
--chunk-seconds CHUNK_SECONDS     Durée cible d'un chunk en secondes pour --parallel-chunks
                                  (défaut : 300). Plus petit = plus de parallélisme,
                                  légèrement plus d'overhead conteneur. Plus grand = plus
                                  proche du monolithique.
--resume                          Reprend un encodage chunked interrompu via son manifest
                                  sidecar (<output>.chunks.json). Les chunks déjà terminés
                                  sont sautés. Implique --parallel-chunks (utiliser la même
                                  valeur qu'au run d'origine).

[ Système ]
--verbose                         Affiche les détails techniques de l'analyse adaptative
--dry-run                         Affiche l'analyse et la commande sans encoder
```

---

## ❓ FAQ

**Quelles plateformes sont supportées ?**
Windows 10/11 (x64), Linux (x64), et macOS Apple Silicon (M1/M2/M3). Tous les outils nécessaires (ffmpeg, ffprobe, dovi_tool, hdr10plus_tool, mkvmerge) sont intégrés dans le binaire — aucune installation externe requise.

**C'est seulement pour la 4K ?**
Non, l'outil est excellent en 1080p aussi. Particulièrement sur les remux Blu-ray avec grain cinématique (classiques, horreur, films d'auteur 35mm) ou les scènes complexes (action, sci-fi).

**Dois-je installer ffmpeg ou d'autres outils séparément ?**
Non. ffmpeg, ffprobe, dovi_tool, hdr10plus_tool et mkvmerge sont tous intégrés dans le binaire sur les trois plateformes. Téléchargez et lancez, c'est tout.

**Le Dolby Vision et le HDR10+ fonctionnent automatiquement ?**
Oui. Le binaire détecte automatiquement les sources Dolby Vision (Profil 5/7/8.x) et HDR10+ (SMPTE 2094-40) puis préserve les métadonnées sans configuration. Si la source contient les deux (rare), Dolby Vision prend la priorité.

**La conversion Profil 7 → 8.1 fonctionne ?**
Oui, c'est le comportement par défaut. Le Profil 7 (FEL/MEL) est extrait et réinjecté en 8.1, compatible avec la plupart des lecteurs Dolby Vision modernes.

**Pourquoi mes fichiers sont-ils plus lourds qu'avec d'autres encodeurs ?**
Choix de conception délibéré — préservation maximale du détail et des métadonnées HDR. Pour limiter la taille du fichier, utilisez `--max-bitrate` ou augmentez `--base-crf`.

**Le grain de mes Blu-rays est-il préservé ?**
Oui. Le débruitage est désactivé par défaut — aucun traitement n'est appliqué sur le grain sans votre accord explicite via `--denoise`. Le CRF adaptatif (base 22.0) traite le grain comme une feature à conserver, pas comme du bruit à éliminer.

**J'ai un film au grain vraiment trop marqué, comment le nettoyer proprement ?**
Utilisez `--manual-grain-clean`. Ce mode active une chaîne dédiée `atadenoise + vaguedenoiser` qui attaque le grain temporel (frame-à-frame) puis le résidu spatial via ondelettes, sans effet plastique sur la peau ou les détails fins. La force est auto-calibrée selon le niveau de grain détecté, avec un plancher minimum pour garantir un résultat propre.

**Vitesse d'encodage ?**
L'outil utilise les préréglages x265 `slower` ou `veryslow` — pas un encodeur rapide, un *bon* encodeur. Pour un encodage plus rapide, utilisez `--no-veryslow`.

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

You have a video library full of 1080p Blu-rays, 4K Dolby Vision rips, HDR10 or HLG sources. You want to re-encode to H.265 to reclaim terabytes — without destroying the metadata that makes your movies display correctly on your OLED.

**The problem:** Most H.265 tools strip out Dolby Vision Profile 7 metadata or smooth grain by default. Manual ffmpeg requires hours of testing to find the right parameters — and those parameters change for every video (grain, noise, motion, complexity).

**The solution:** Adaptive Video Encoder analyzes each video frame by frame *before* encoding, automatically picks the best x265 parameters, and fully preserves your Dolby Vision (Profile 5, 7, 8.x), HDR10 and HLG metadata.

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
- You're comfortable with the command line
- You're tired of tweaking x265 parameters and comparing 12 versions of the same film

## ⚠️ Not for you if...

- You're looking for maximum compression to save disk space
- You mostly encode simple SDR content without grain (recent indoor comedies, smooth animation, talking heads) — for those cases, simpler tools often give better compression ratios
- You want a GUI
- You need fast encoding (the tool prioritizes quality, not speed)

---

## ⚡ Why a dedicated adaptive encoder?

| | Generic encoders | Manual ffmpeg | **Adaptive Video Encoder** |
|---|---|---|---|
| Dolby Vision Profile 7 | ❌ Broken | ⚠️ Possible with `dovi_tool` + scripting | ✅ Automatic |
| Grain preservation | ❌ Smoothed by default | ⚠️ If you know what to flag | ✅ Preserved by default, never touched without `--denoise` |
| Settings adapted *per video* | ❌ Fixed presets | ⚠️ If you test yourself | ✅ Frame-by-frame analysis |
| HDR10 / HLG preserved | ⚠️ Sometimes | ⚠️ If you know what to flag | ✅ Always |
| Black bar detection | ✅ | ⚠️ Manual | ✅ Automatic |
| Setup time | 5 min | 1-3 h per film | **0 min** |

---

## 🎞️ Particularly excellent on 1080p Blu-rays

Many users mistakenly think this tool is only for 4K. **It's not.** Adaptive Video Encoder shines particularly well on 1080p Blu-ray remuxes for 3 reasons:

**1. Film grain preservation.** Classic films, horror movies, recent 35mm auteur films have grain that's part of their visual identity. Most encoders smooth it by default. Adaptive Encoder never touches grain without your explicit `--denoise` flag.

**2. Adaptive complex scene detection.** On a 1080p action film, fight scenes have radically different complexity than dialogue. Frame-by-frame analysis adjusts x265 parameters accordingly, where generic encoders use the same settings start to finish.

**3. 1080p HDR10 metadata preservation.** Some recent Blu-rays have HDR10 in 1080p. Adaptive Encoder preserves everything: master display, MaxCLL/MaxFALL, color primaries.

**Less relevant for:** recently-shot digital content with clean image (romantic comedies, sitcoms, indoor documentaries). Those sources have neither grain nor complex detail to preserve.

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

- 🔍 **Adaptive analysis** — detects noise, grain, complexity, edge density to tune x265
- 📺 **Dolby Vision Profile 5, 7, 8.x** — metadata extracted, preserved, reinjected
- 🎨 **HDR10 and HLG** — color primaries, transfers, master display, MaxCLL/MaxFALL preserved
- 🎞️ **Grain preserved by default** — no denoising ever applied without explicit `--denoise`
- 🧹 **Heavy-grain cleanup mode** — opt-in `atadenoise+vaguedenoiser` chain via `--manual-grain-clean` for films where the grain is too heavy to keep
- ✂️ **Smart crop** — detects black bars without accidentally cutting content
- 🔊 **All audio and subtitle tracks** copied by default, zero loss
- 🎞️ **Supported formats** — MKV, MP4, MOV, AVI, MXF, WebM, M4V, TS
- 📐 **Resolutions** — 480p to 8K (excellent for 1080p AND 4K)
- 📦 **Single binary, zero dependencies** — ffmpeg, ffprobe, dovi_tool, hdr10plus_tool and mkvmerge bundled on all three platforms. Nothing to install separately.

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

All required tools (ffmpeg, ffprobe, dovi_tool, hdr10plus_tool, mkvmerge) are bundled inside the binary — **no external installation required** on Windows, Linux, or macOS.

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

**Heavy-grain film — clean cleanup:**
```bash
./adaptive-encoder "old_35mm_film.mkv" --manual-grain-clean
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
--downscale-1080p-sdr             Downscale source to 1080p and convert to SDR.
                                  Applies tone mapping for non-HDR display compatibility.
--base-crf BASE_CRF               Shifts the adaptive CRF baseline (default: 22.0).
                                  Tuned for a good quality/size balance (~50% reduction
                                  on typical Blu-ray remuxes). Raise to reduce file size
                                  further; lower for closer-to-remux quality.

[ Bitrate & Presets ]
--max-bitrate MAX_BITRATE         Force VBV max bitrate (kbps). Useful for targeting
                                  a specific file size.
--vbv-bufsize VBV_BUFSIZE         Optional VBV buffer size (kbits)
--vbv                             Enable automatic VBV bitrate cap (~12 Mbps for 1080p,
                                  scaled by resolution). Off by default — pure CRF mode
                                  gives complex/grainy scenes all the bits they need.
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
                                  and embedded by default.

[ Noise Reduction ]
--denoise                         Enable adaptive noise reduction. Off by default to
                                  preserve film grain on Blu-ray and cinema content.
                                  Strength is auto-calibrated from source noise/grain
                                  metrics.
--denoise-strength STRENGTH       Override denoise strength (0.0=off, 1.0=max).
                                  Implies --denoise when > 0.
--denoise-preserve-grain          Gentler denoise that preserves some film grain texture.
                                  Implies --denoise.
--denoise-engine {auto,nlmeans,bm3d,hybrid,atadenoise,wavelet,fftdnoiz,grain-clean}
                                  Force a specific denoise engine instead of automatic
                                  selection. 'grain-clean' chains atadenoise+vaguedenoiser
                                  — ideal for heavy film grain. 'atadenoise' alone is fast
                                  and excellent on moderate grain (motion-thresholded
                                  temporal averaging). 'wavelet' (vaguedenoiser) is gentle
                                  and preserves fine detail via wavelets. 'fftdnoiz' is a
                                  3D FFT denoiser. 'bm3d' for max quality on stationary
                                  noise (3-5x slower). 'nlmeans' for speed. 'hybrid' mixes
                                  hqdn3d+nlmeans. Implies --denoise.
--manual-grain-clean              Manual high-quality cleanup mode for films with heavy
                                  grain. Activates the atadenoise + vaguedenoiser chain
                                  with strength auto-calibrated from detected grain/noise
                                  levels. Equivalent to
                                  `--denoise --denoise-engine grain-clean` but with a
                                  strength floor of ≥ 0.55 to guarantee effective cleanup.
                                  CPU-only, ~0.4× realtime additional cost on 1080p.

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
                                  (fast, less accurate). 'two-pass' measures the whole
                                  file first then normalizes (slower but precise —
                                  recommended). Re-encodes audio to AC3 at 640 kbps for
                                  5.1 / 192 kbps for stereo.
--normalize-audio-target LUFS     Integrated loudness target in LUFS (default: -16.0,
                                  suited for TV/streaming. Use -23.0 for EBU R128 broadcast).

[ Parallel chunked encoding (experimental) ]
--parallel-chunks N               Encode N chunks in parallel (1 = monolithic encoding,
                                  default). Splits the source at scene cuts into ~5 min
                                  chunks and encodes them concurrently. Massive speedup
                                  on multi-core boxes. Incompatible with Dolby Vision,
                                  HDR10+, --normalize-audio, and --downmix-audio.
--chunk-seconds CHUNK_SECONDS     Target chunk length in seconds for --parallel-chunks
                                  (default: 300). Smaller = more parallelism, slightly
                                  more container overhead. Larger = closer to monolithic.
--resume                          Resume an interrupted chunked encode using its manifest
                                  sidecar (<output>.chunks.json). Already-completed chunks
                                  are skipped. Implies --parallel-chunks (use the same
                                  value as the original run).

[ System ]
--verbose                         Display technical details of adaptive analysis
--dry-run                         Display analysis and command without encoding
```

---

## ❓ FAQ

**What platforms are supported?**
Windows 10/11 (x64), Linux (x64), and macOS Apple Silicon (M1/M2/M3). All required tools (ffmpeg, ffprobe, dovi_tool, hdr10plus_tool, mkvmerge) are bundled inside the binary — no external installation required.

**Is this only for 4K?**
No, the tool is excellent for 1080p too. Particularly on Blu-ray remuxes with film grain (classics, horror, 35mm auteur films) or complex scenes (action, sci-fi).

**Do I need to install ffmpeg or any other tools separately?**
No. ffmpeg, ffprobe, dovi_tool, hdr10plus_tool and mkvmerge are all bundled inside the binary on all three platforms. Download and run — that's it.

**Do Dolby Vision and HDR10+ work automatically?**
Yes. The binary auto-detects Dolby Vision (Profile 5/7/8.x) and HDR10+ (SMPTE 2094-40) sources and preserves the metadata with no configuration. If a source carries both (rare), Dolby Vision takes priority.

**Does Profile 7 → 8.1 conversion work?**
Yes, it's the default. Profile 7 (FEL/MEL) is extracted and reinjected as 8.1, compatible with most modern Dolby Vision players.

**Why are my files larger than with other encoders?**
Intentional design choice — maximum detail and HDR metadata preservation. To reduce file size, use `--max-bitrate` or raise `--base-crf`.

**Is film grain preserved?**
Yes. Noise reduction is off by default — no processing is ever applied to grain without your explicit `--denoise` flag. The adaptive CRF (base 22.0) treats grain as a feature to keep, not noise to eliminate.

**My film has really heavy grain — how do I clean it up properly?**
Use `--manual-grain-clean`. This mode activates a dedicated `atadenoise + vaguedenoiser` chain that attacks temporal grain frame-to-frame first, then cleans the spatial residue via wavelets — without the plastic look on skin or fine detail. Strength is auto-calibrated from the detected grain level, with a minimum floor to guarantee a clean result.

**Encoding speed?**
The tool uses x265 `slower` or `veryslow` presets — not a fast encoder, a *good* one. For faster encoding use `--no-veryslow`.

**What if it doesn't work for my files?**
Open an issue on GitHub or ask on Discord — happy to help.

---

## 📧 Support

- 💬 **Discord** (fast replies): [https://discord.gg/UHrEn2H6jD](https://discord.gg/UHrEn2H6jD)
- 📧 **Email**: [osx300@gmail.com](mailto:osx300@gmail.com)
- ☕ **Buy me a coffee** (optional): [paypal.me/thegrunge45](https://paypal.me/thegrunge45)
