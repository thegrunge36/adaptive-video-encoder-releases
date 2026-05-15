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
- 🌟 **HDR10+ (SMPTE 2094-40)** — métadonnées dynamiques auto-détectées via `hdr10plus_tool`, extraites en JSON puis réinjectées dans le bitstream HEVC via le paramètre x265 `dhdr10-info`. DV et HDR10+ coexistent dans le même bitstream HEVC : les afficheurs Dolby Vision utilisent le RPU, les afficheurs HDR10+ (ex. Samsung) utilisent les SEI SMPTE 2094-40.
- 🎨 **HDR10 et HLG** — primaires de couleur, transferts, master display, MaxCLL/MaxFALL préservés
- 🌑 **Débruitage adaptatif** — force calibrée automatiquement à partir du bruit/grain mesurés ; si le score combiné est sous le seuil (~0.08), aucun filtre n'est appliqué. Trois moteurs : `nlmeans`, `bm3d`, `hybrid` (hqdn3d+nlmeans), plus `auto`. Option `--denoise-preserve-grain` pour ne lisser qu'une fraction de la texture.
- 🔊 **Normalisation audio EBU R128** — mode `single-pass` (loudnorm dynamique) ou `two-pass` (mesure puis correction linéaire — recommandé). Cible LUFS configurable.
- ✂️ **Recadrage intelligent** — détecte les bandes noires sans couper accidentellement le contenu
- 🎞️ **Toutes les pistes audio et sous-titres** copiées par défaut, zéro perte (sauf si normalisation ou downmix actif)
- 🎞️ **Formats supportés** — MKV, MP4, MOV, AVI, MXF, WebM, M4V, TS
- 📐 **Résolutions** — 480p à 8K
- 📦 **Binaire unique** — `ffmpeg` et `ffprobe` intégrés sur les trois plateformes. `dovi_tool`, `hdr10plus_tool` et `mkvmerge` sont intégrés sur Linux et macOS. **Sur Windows, téléchargez `dovi_tool.exe`, `hdr10plus_tool.exe` et `mkvmerge.exe` et placez-les dans le même dossier qu'`adaptive-encoder.exe`** pour activer le Dolby Vision, le HDR10+ et le remuxage MKV (voir ci-dessous).

---

## 💻 Plateformes supportées

| Plateforme | Statut | Notes |
|---|---|---|
| 🐧 Linux (x64) | ✅ Supporté | Ubuntu 22.04+, Debian 12+, Fedora 40+ |
| 🪟 Windows 10/11 (x64) | ✅ Supporté | PowerShell ou CMD. **`dovi_tool`, `hdr10plus_tool` et `mkvmerge` à déposer manuellement** |
| 🍎 macOS (Apple Silicon) | ✅ Supporté | M1, M2, M3 — binaire natif arm64 |

---

## ☕ Cet outil est gratuit — offrez-moi un café si ça vous a aidé !

Adaptive Video Encoder est entièrement gratuit. Si il vous a fait gagner du temps ou amélioré votre bibliothèque, un petit café est toujours apprécié — mais jamais obligatoire.

👉 **[M'offrir un café](https://paypal.me/thegrunge45)** — totalement optionnel, toujours apprécié ☕

💬 **Questions ou retours ? Rejoignez le [Discord](https://discord.gg/UHrEn2H6jD)** — avec plaisir.

---

## ⚙️ Installation et prérequis

`ffmpeg` et `ffprobe` sont intégrés dans le binaire sur toutes les plateformes.

> ⚠️ **Windows — `dovi_tool`, `hdr10plus_tool` et `mkvmerge` à déposer manuellement**
>
> Sur Windows, ces trois outils ne sont pas fonctionnels dans le binaire. Téléchargez les exécutables et placez-les dans le même dossier qu'`adaptive-encoder.exe` — aucune installation, juste déposer les fichiers :
>
> - **`dovi_tool.exe`** → [https://github.com/quietvoid/dovi_tool/releases](https://github.com/quietvoid/dovi_tool/releases)
> - **`hdr10plus_tool.exe`** → [https://github.com/quietvoid/hdr10plus_tool/releases](https://github.com/quietvoid/hdr10plus_tool/releases)
> - **`mkvmerge.exe`** → [https://mkvtoolnix.download](https://mkvtoolnix.download) (inclus dans MKVToolNix — prenez l'installeur ou l'archive portable)
>
> Sans ces fichiers, le Dolby Vision, le HDR10+ et le remuxage MKV sont silencieusement ignorés ou échouent.

### Premier lancement — macOS uniquement

macOS bloque les binaires non signés. Exécutez ceci **une seule fois** après le téléchargement :

```bash
xattr -d com.apple.quarantine ./adaptive-encoder
chmod +x ./adaptive-encoder
```

Après ça, macOS ne vous avertira plus jamais pour ce fichier.

---

## 🚀 Démarrage rapide — un seul fichier

### 🪟 Windows — étape par étape

**1. Placez `adaptive-encoder.exe` dans le dossier qui contient votre vidéo.**

**2. Ouvrez PowerShell *dans ce dossier*.** Maintenez `Shift` puis clic droit dans une zone vide du dossier → **"Ouvrir la fenêtre PowerShell ici"**.

> ✅ Vérifiez que le prompt commence par `PS C:\...>`. Si vous voyez juste `C:\...>`, vous êtes dans CMD. Les deux fonctionnent, mais la syntaxe diffère (voir plus bas).

**3. Lancez la commande :**

```powershell
.\adaptive-encoder.exe "mon_film.mkv"
```

Le fichier de sortie sera créé à côté, nommé `mon_film_adaptive.mkv`.

### 🐧 Linux / 🍎 macOS

```bash
chmod +x ./adaptive-encoder
./adaptive-encoder "mon_film.mkv"
```

### Variantes utiles

**Mode test — analyser sans encoder (toujours faire ça en premier sur un nouveau type de source) :**
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

## 🗂️ Encoder un dossier complet (batch)

> ⚠️ **Le piège à connaître :** la sortie par défaut s'appelle `<entrée>_adaptive.mkv`. Sans précaution, si vous relancez le script, il va re-traiter en boucle les fichiers déjà encodés (`film_adaptive.mkv` → `film_adaptive_adaptive.mkv`, etc.). **Toutes les commandes ci-dessous excluent les fichiers `*_adaptive.mkv`** pour éviter ce problème.

### 🪟 Windows — PowerShell (recommandé)

**1. Placez `adaptive-encoder.exe` dans le dossier qui contient vos vidéos.**

**2. Ouvrez PowerShell dans ce dossier** (`Shift` + clic droit → "Ouvrir la fenêtre PowerShell ici"). Vérifiez le prompt `PS C:\...>`.

**3. Choisissez la commande selon votre besoin :**

**Dossier courant uniquement :**
```powershell
Get-ChildItem *.mkv -Exclude *_adaptive.mkv | ForEach-Object {
    .\adaptive-encoder.exe $_.FullName
}
```

**Récursif — inclure tous les sous-dossiers :**
```powershell
Get-ChildItem -Recurse -Include *.mkv -Exclude *_adaptive.mkv | ForEach-Object {
    .\adaptive-encoder.exe $_.FullName
}
```

**Plusieurs formats à la fois (récursif) :**
```powershell
Get-ChildItem -Recurse -Include *.mkv,*.mp4,*.mov -Exclude *_adaptive.* | ForEach-Object {
    .\adaptive-encoder.exe $_.FullName
}
```

> 💡 **Si PowerShell refuse de lancer le `.exe`** (politique d'exécution), tapez d'abord :
> ```powershell
> Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass
> ```
> Ça ne dure que le temps de la session.

### 🪟 Windows — CMD ou fichier .bat

```cmd
for %F in (*.mkv) do adaptive-encoder.exe "%F"
```

Dans un fichier `.bat`, doublez les `%` :
```bat
@echo off
for %%F in (*.mkv) do adaptive-encoder.exe "%%F"
pause
```

### 🐧 Linux / 🍎 macOS

**Dossier courant uniquement :**
```bash
for f in *.mkv; do
    [[ "$f" == *_adaptive.mkv ]] && continue
    ./adaptive-encoder "$f"
done
```

**Récursif (tous sous-dossiers) :**
```bash
find . -type f -name "*.mkv" ! -name "*_adaptive.mkv" -exec ./adaptive-encoder {} \;
```

---

> 💡 **Avant de lancer sur toute la bibliothèque,** testez d'abord avec `--dry-run` sur un seul fichier pour vérifier que Dolby Vision, HDR10+ et HDR sont correctement détectés.

> 💡 **Charge/durée :** un encodage en `veryslow` peut prendre plusieurs heures par film. Pour une grosse bibliothèque, lancez ça en soirée ou utilisez `--no-veryslow` pour limiter à `slower`.

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
                                  et embarqué automatiquement via hdr10plus_tool, y compris
                                  en présence de Dolby Vision — les deux couches coexistent
                                  dans le bitstream HEVC.

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

## 🧰 Exemples d'utilisation des flags

Cette section regroupe des exemples concrets, organisés par catégorie de flag. Les exemples utilisent la syntaxe Linux/macOS (`./adaptive-encoder`) — sur Windows, remplacez par `.\adaptive-encoder.exe`.

### 📐 Paramètres vidéo

**Forcer le framerate à 23.976 (typique cinéma) — utile si la source affiche un framerate variable ou un wrap A/V suspect :**
```bash
./adaptive-encoder "film.mkv" --force-fps 23.976
```

**Désactiver la détection des bandes noires** — à utiliser si la source n'a aucune bande noire (Academy 1.37, 1.85 plein cadre) ou si l'auto-crop coupe à tort des éléments graphiques :
```bash
./adaptive-encoder "film_137.mkv" --no-crop-detect
```

**Ajuster manuellement la baseline CRF** — un CRF de base plus élevé réduit la taille au prix de la qualité visuelle :
```bash
# Qualité plus haute (fichier plus lourd, plus proche du remux)
./adaptive-encoder "film.mkv" --base-crf 20.0

# Taille plus petite (qualité légèrement dégradée, utile pour la diffusion)
./adaptive-encoder "film.mkv" --base-crf 24.0
```

**Convertir une source 4K HDR en 1080p SDR** — pour les TV anciennes ou les écrans non-HDR. La conversion utilise libplacebo (BT.2390) avec fallback zscale+tonemap=mobius :
```bash
./adaptive-encoder "4k_dolbyvision.mkv" --downscale-1080p-sdr
```

**Plus d'échantillons pour l'analyse adaptative** — utile sur les films avec contenu très varié (anthologie, documentaire long) où le défaut peut sous-représenter certaines scènes :
```bash
./adaptive-encoder "anthologie_3h.mkv" --max-samples 600
```

### 🎚️ Débit & préréglages

**Activer le plafonnement adaptatif VBV** — `--vbv` calibre automatiquement le débit max selon la résolution (7 Mbps en 720p, 12 Mbps en 1080p, 17 Mbps en 1440p, 28 Mbps en 4K) :
```bash
./adaptive-encoder "film.mkv" --vbv
```

**Imposer un plafond manuel** — pour cibler une taille de fichier précise, par exemple 10 Mbps :
```bash
./adaptive-encoder "film.mkv" --max-bitrate 10000
```

**Plafond manuel + buffer VBV ajusté** — sur du contenu très variable, élargir le buffer évite les pompages de débit :
```bash
./adaptive-encoder "film.mkv" --max-bitrate 15000 --vbv-bufsize 30000
```

**Encodage plus rapide** — bascule sur `slower` au lieu de `veryslow` (env. 2× plus rapide, qualité ~1-2 % en dessous) :
```bash
./adaptive-encoder "film.mkv" --no-veryslow
```

**Tune `grain` forcé** — pour les pellicules 35mm/16mm scannées où vous voulez garder la structure du grain :
```bash
./adaptive-encoder "western_1970.mkv" --force-tune grain --no-denoise
```

**Tune `animation` forcé** — pour les dessins animés, anime, motion design (zones plates, bords nets) :
```bash
./adaptive-encoder "anime.mkv" --force-tune animation
```

### 📺 Dolby Vision & HDR

**Forcer la sortie en HDR10 même si la source est Dolby Vision** — utile pour la compatibilité avec les lecteurs qui buguent sur le DV :
```bash
./adaptive-encoder "uhd_dolbyvision.mkv" --no-dolby-vision
```

**Refuser la conversion Profil 7 → 8.1** — préserve le DV uniquement si le profil source est reproductible nativement, sinon sort en HDR10 :
```bash
./adaptive-encoder "blu-ray_dv_profil7.mkv" --preserve-dv-profile
```

**Rediriger les fichiers temporaires DV** — crucial sur Linux avec `/tmp` en tmpfs (limité à la RAM) ou si la partition système est petite :
```bash
# Linux
./adaptive-encoder "film_dv.mkv" --temp-dir /mnt/ssd/temp

# macOS
./adaptive-encoder "film_dv.mkv" --temp-dir ~/temp

# Windows (depuis PowerShell)
.\adaptive-encoder.exe "film_dv.mkv" --temp-dir D:\temp
```

**Ignorer HDR10+ même si présent** — utile si votre TV ne gère que HDR10 et que vous voulez éviter les SEI inutiles :
```bash
./adaptive-encoder "film_hdr10plus.mkv" --no-hdr10plus
```

### 🌑 Réduction du bruit

**Désactiver totalement le débruitage** — pour les archives, sources film, ou tout contenu où la fidélité au master prime sur la propreté :
```bash
./adaptive-encoder "film_35mm.mkv" --no-denoise
```

**Forcer une force de débruitage spécifique** — override le calibrage automatique (0.0 = aucun filtre, 1.0 = max) :
```bash
# Débruitage léger sur source numérique propre
./adaptive-encoder "source_numerique.mkv" --denoise-strength 0.2

# Débruitage fort sur capture VHS / SD bruitée
./adaptive-encoder "vhs_rip.mkv" --denoise-strength 0.8
```

**Mode préservation du grain** — débruite 40 % moins fort, conserve une partie de la texture (compromis archive ↔ propreté) :
```bash
./adaptive-encoder "film_70mm.mkv" --denoise-preserve-grain
```

**Forcer un moteur spécifique** :
```bash
# bm3d — qualité max sur bruit stationnaire (capteur numérique, étalonnage moderne)
./adaptive-encoder "raw_camera.mkv" --denoise-engine bm3d

# nlmeans — rapide et général
./adaptive-encoder "film.mkv" --denoise-engine nlmeans

# hybrid — chaîne hqdn3d + nlmeans, idéal pour sources mixtes (SD/HD upscalés)
./adaptive-encoder "remaster_dvd.mkv" --denoise-engine hybrid
```

### 🔊 Audio & sous-titres

**Supprimer toutes les pistes audio** — pour produire un master vidéo seul :
```bash
./adaptive-encoder "film.mkv" --no-audio
```

**Supprimer tous les sous-titres** :
```bash
./adaptive-encoder "film.mkv" --no-subs
```

**Garder uniquement le français et l'anglais** — supprime les autres doublages, première langue listée = défaut du player :
```bash
./adaptive-encoder "film.mkv" --audio-lang "fre,eng"
```

**Garder uniquement la VO anglaise (suppression des doublages)** :
```bash
./adaptive-encoder "film.mkv" --audio-lang "eng"
```

**Downmix 7.1/Atmos → 5.1 ou 2.0** — pour les setups home cinéma plus simples ou pour économiser de l'espace :
```bash
./adaptive-encoder "film_atmos.mkv" --downmix-audio
```

**Normalisation audio rapide (single-pass)** :
```bash
./adaptive-encoder "film.mkv" --normalize-audio single-pass
```

**Normalisation audio précise (two-pass) — recommandé** :
```bash
./adaptive-encoder "film.mkv" --normalize-audio two-pass
```

**Cible LUFS personnalisée** :
```bash
# Broadcast EBU R128 strict
./adaptive-encoder "film.mkv" --normalize-audio two-pass --normalize-audio-target -23.0

# Streaming type Spotify/YouTube (-14 LUFS)
./adaptive-encoder "film.mkv" --normalize-audio two-pass --normalize-audio-target -14.0
```

### 🖥️ Système

**Mode verbose — voir le détail de l'analyse adaptative** :
```bash
./adaptive-encoder "film.mkv" --verbose
```

**Dry-run — analyser et afficher la commande sans encoder** :
```bash
./adaptive-encoder "film.mkv" --dry-run
```

**Spécifier un fichier de sortie personnalisé** :
```bash
./adaptive-encoder "input.mkv" -o "/mnt/library/Movies/Inception (2010).mkv"
```

---

### 🎯 Combinaisons utiles (scénarios complets)

**📼 Archive 35mm grenu, fidélité au master maximale**
Préserve la structure du grain, aucun débruitage, tune adapté :
```bash
./adaptive-encoder "western_1970.mkv" \
  --no-denoise \
  --force-tune grain \
  --base-crf 20.0
```

**🎌 Anime / dessin animé optimisé**
Tune animation, débruitage actif (l'anime moderne a peu de grain) :
```bash
./adaptive-encoder "anime_serie_s01e01.mkv" \
  --force-tune animation \
  --audio-lang "jpn,fre"
```

**💾 Réduction de taille agressive pour serveur de streaming personnel**
CRF plus haut + plafond bitrate + downmix + langues filtrées :
```bash
./adaptive-encoder "film.mkv" \
  --base-crf 24.0 \
  --max-bitrate 8000 \
  --downmix-audio \
  --audio-lang "fre,eng" \
  --no-veryslow
```

**📡 Bibliothèque hétérogène avec audio normalisé**
Two-pass loudness à -16 LUFS, filtres langue, plafond VBV adaptatif :
```bash
./adaptive-encoder "film.mkv" \
  --vbv \
  --audio-lang "fre,eng" \
  --normalize-audio two-pass
```

**📺 Blu-ray UHD Dolby Vision Profil 7 — qualité maximale, A/V parfait**
Force 23.976 pour resync DV, temp dir externe, base-crf bas :
```bash
./adaptive-encoder "uhd_dv_profil7.mkv" \
  --force-fps 23.976 \
  --temp-dir /mnt/ssd/temp \
  --base-crf 20.0
```

**📺 Conversion 4K HDR → 1080p SDR pour TV ancienne avec loudness contrôlé**
Downscale + tonemap + downmix + normalisation broadcast :
```bash
./adaptive-encoder "4k_hdr10plus.mkv" \
  --downscale-1080p-sdr \
  --downmix-audio \
  --normalize-audio two-pass \
  --normalize-audio-target -23.0
```

**🧪 Test avant gros batch — vérifier la détection sans encoder**
Dry-run + verbose pour voir l'analyse complète :
```bash
./adaptive-encoder "echantillon.mkv" --dry-run --verbose
```

**⚡ Encodage rapide d'un gros lot, qualité raisonnable**
Slower au lieu de veryslow, CRF légèrement plus haut :
```bash
./adaptive-encoder "film.mkv" \
  --no-veryslow \
  --base-crf 23.0 \
  --vbv
```

**🎞️ Capture VHS/DVD restaurée — débruitage agressif**
bm3d + force manuelle + tune grain pour ce qui reste de texture :
```bash
./adaptive-encoder "vhs_concert.mkv" \
  --denoise-engine bm3d \
  --denoise-strength 0.7 \
  --base-crf 22.0
```

---

## 🛠️ Dépannage

**La commande ne fait rien / "n'est pas reconnu".**
Vous êtes probablement dans le mauvais dossier, ou `adaptive-encoder.exe` n'est pas dans le dossier courant. Vérifiez avec `pwd` (PowerShell) ou `cd` (CMD) que vous êtes au bon endroit, et avec `ls` / `dir` que le `.exe` est bien là.

**Le Dolby Vision ou le HDR10+ ne fonctionne pas sur Windows.**
Sur Windows, `dovi_tool`, `hdr10plus_tool` et `mkvmerge` ne sont pas fonctionnels dans le binaire. Téléchargez les trois exécutables et placez-les dans le même dossier qu'`adaptive-encoder.exe` — aucune installation, juste déposer les fichiers. Sans eux, le DV et le HDR10+ sont silencieusement ignorés et la sortie tombe en HDR10 uniquement.

**Mes fichiers `_adaptive.mkv` sont re-traités à chaque lancement du batch.**
Utilisez la version des commandes batch avec `-Exclude *_adaptive.mkv` (PowerShell) ou la boucle bash qui filtre `*_adaptive.mkv` (Linux/macOS). Voir la section "Encoder un dossier complet" ci-dessus.

**PowerShell refuse de lancer le `.exe`.**
Lancez d'abord `Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass` dans la fenêtre PowerShell. Ça ne dure que le temps de la session.

**`Get-ChildItem` ne fonctionne pas.**
Vous êtes dans CMD, pas PowerShell. Le prompt doit commencer par `PS`. Tapez `powershell` puis Entrée pour basculer.

**L'encodage prend des heures par film — c'est normal ?**
Oui. `veryslow` est intentionnellement lent pour maximiser la qualité. Utilisez `--no-veryslow` pour basculer sur `slower` (env. 2× plus rapide) ou `--no-veryslow --base-crf 24` pour réduire encore.

**Espace disque saturé pendant l'encodage Dolby Vision.**
Les fichiers temporaires DV peuvent être lourds. Utilisez `--temp-dir D:\temp` (Windows) ou `--temp-dir /chemin/disque-libre` (Linux/macOS) pour les rediriger vers un disque avec plus d'espace.

---

## ❓ FAQ

**Quelles plateformes sont supportées ?**
Windows 10/11 (x64), Linux (x64), et macOS Apple Silicon (M1/M2/M3). `ffmpeg` et `ffprobe` sont intégrés dans le binaire sur les trois plateformes. `dovi_tool`, `hdr10plus_tool` et `mkvmerge` sont intégrés sur Linux et macOS. **Sur Windows, téléchargez `dovi_tool.exe`, `hdr10plus_tool.exe` et `mkvmerge.exe` et placez-les dans le même dossier qu'`adaptive-encoder.exe`** — aucune installation, juste déposer les fichiers.

**C'est seulement pour la 4K ?**
Non, l'outil est excellent en 1080p aussi. Les paramètres x265 (`ctu`, `qg-size`, preset) sont adaptés automatiquement à la résolution effective.

**Dois-je télécharger des outils séparément ?**
Sur Linux et macOS : non, tout est intégré. Sur Windows : `ffmpeg` et `ffprobe` sont intégrés, mais **`dovi_tool.exe`, `hdr10plus_tool.exe` et `mkvmerge.exe` doivent être téléchargés et placés dans le même dossier qu'`adaptive-encoder.exe`** — pas d'installation, juste déposer les fichiers.

**Le Dolby Vision et le HDR10+ fonctionnent automatiquement ?**
Oui, sous réserve que `dovi_tool`, `hdr10plus_tool` et `mkvmerge` soient disponibles. Sur Linux et macOS, tout est intégré et fonctionne sans configuration. **Sur Windows, téléchargez `dovi_tool.exe`, `hdr10plus_tool.exe` et `mkvmerge.exe`** et placez-les dans le même dossier qu'`adaptive-encoder.exe` — aucune installation, juste déposer les fichiers. Le binaire détecte automatiquement les sources Dolby Vision (Profil 5/7/8.x) et HDR10+ (SMPTE 2094-40) puis préserve les métadonnées. Si la source contient les deux, les deux métadonnées sont préservées et coexistent dans le bitstream HEVC : les afficheurs Dolby Vision utilisent le RPU, les afficheurs HDR10+ (ex. Samsung) utilisent les SEI SMPTE 2094-40. Le choix se fait côté lecteur/afficheur selon ce qu'il supporte.

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
- 🌟 **HDR10+ (SMPTE 2094-40)** — dynamic metadata auto-detected via `hdr10plus_tool`, extracted to JSON then reinjected into the HEVC bitstream via the x265 `dhdr10-info` parameter. DV and HDR10+ coexist in the same HEVC bitstream: Dolby Vision displays use the RPU, HDR10+-only displays (e.g. Samsung) use the SMPTE 2094-40 SEI.
- 🎨 **HDR10 and HLG** — color primaries, transfers, master display, MaxCLL/MaxFALL preserved
- 🌑 **Adaptive denoising** — strength auto-calibrated from measured noise/grain; if the combined score is below threshold (~0.08), no filter is applied. Three engines: `nlmeans`, `bm3d`, `hybrid` (hqdn3d+nlmeans), plus `auto`. `--denoise-preserve-grain` smooths only a fraction of the texture.
- 🔊 **EBU R128 audio normalization** — `single-pass` mode (dynamic loudnorm) or `two-pass` (measure then linear correction — recommended). Configurable LUFS target.
- ✂️ **Smart crop** — detects black bars without accidentally cutting content
- 🎞️ **All audio and subtitle tracks** copied by default, zero loss (unless normalization or downmix active)
- 🎞️ **Supported formats** — MKV, MP4, MOV, AVI, MXF, WebM, M4V, TS
- 📐 **Resolutions** — 480p to 8K
- 📦 **Single binary** — `ffmpeg` and `ffprobe` bundled on all three platforms. `dovi_tool`, `hdr10plus_tool` and `mkvmerge` are bundled on Linux and macOS. **On Windows, download `dovi_tool.exe`, `hdr10plus_tool.exe` and `mkvmerge.exe` and place them in the same folder as `adaptive-encoder.exe`** to enable Dolby Vision, HDR10+ and MKV remuxing (see below).

---

## 💻 Platform support

| Platform | Status | Notes |
|---|---|---|
| 🐧 Linux (x64) | ✅ Supported | Ubuntu 22.04+, Fedora 40+ |
| 🪟 Windows 10/11 (x64) | ✅ Supported | PowerShell or CMD. **`dovi_tool`, `hdr10plus_tool` and `mkvmerge` must be dropped manually** |
| 🍎 macOS (Apple Silicon) | ✅ Supported | M1, M2, M3 — native arm64 binary |

---

## ☕ This tool is free — buy me a coffee if it helped!

Adaptive Video Encoder is completely free to use. If it saved you time or improved your library, a small coffee is always appreciated — but never required.

👉 **[Buy me a coffee](https://paypal.me/thegrunge45)** — totally optional, always appreciated ☕

💬 **Questions or feedback? Join the [Discord](https://discord.gg/UHrEn2H6jD)** — happy to help.

---

## ⚙️ Installation & requirements

`ffmpeg` and `ffprobe` are bundled inside the binary on all platforms.

> ⚠️ **Windows — `dovi_tool`, `hdr10plus_tool` and `mkvmerge` must be dropped manually**
>
> On Windows, these three tools are not functional inside the binary. Download the executables and place them in the same folder as `adaptive-encoder.exe` — no installation, just drop the files:
>
> - **`dovi_tool.exe`** → [https://github.com/quietvoid/dovi_tool/releases](https://github.com/quietvoid/dovi_tool/releases)
> - **`hdr10plus_tool.exe`** → [https://github.com/quietvoid/hdr10plus_tool/releases](https://github.com/quietvoid/hdr10plus_tool/releases)
> - **`mkvmerge.exe`** → [https://mkvtoolnix.download](https://mkvtoolnix.download) (included in MKVToolNix — use the installer or portable archive)
>
> Without these files, Dolby Vision, HDR10+ and MKV remuxing will silently fail or be skipped.

### First launch — macOS only

macOS blocks unsigned binaries. Run this **once** after downloading:

```bash
xattr -d com.apple.quarantine ./adaptive-encoder
chmod +x ./adaptive-encoder
```

After that, macOS will never warn about this file again.

---

## 🚀 Quick start — single file

### 🪟 Windows — step by step

**1. Place `adaptive-encoder.exe` in the folder that contains your video.**

**2. Open PowerShell *in that folder*.** Hold `Shift` and right-click in an empty area of the folder → **"Open PowerShell window here"**.

> ✅ Make sure the prompt starts with `PS C:\...>`. If you only see `C:\...>`, you're in CMD. Both work, but the syntax differs (see below).

**3. Run the command:**

```powershell
.\adaptive-encoder.exe "my_movie.mkv"
```

The output file will be created next to it, named `my_movie_adaptive.mkv`.

### 🐧 Linux / 🍎 macOS

```bash
chmod +x ./adaptive-encoder
./adaptive-encoder "my_movie.mkv"
```

### Useful variants

**Test mode — analyze without encoding (always do this first on a new source type):**
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

## 🗂️ Batch encode an entire folder

> ⚠️ **Gotcha to know:** the default output is named `<input>_adaptive.mkv`. Without precautions, re-running the script will reprocess already-encoded files in a loop (`film_adaptive.mkv` → `film_adaptive_adaptive.mkv`, etc.). **All commands below exclude `*_adaptive.mkv` files** to avoid this issue.

### 🪟 Windows — PowerShell (recommended)

**1. Place `adaptive-encoder.exe` in the folder containing your videos.**

**2. Open PowerShell in that folder** (`Shift` + right-click → "Open PowerShell window here"). Confirm the `PS C:\...>` prompt.

**3. Pick the command that matches your need:**

**Current folder only:**
```powershell
Get-ChildItem *.mkv -Exclude *_adaptive.mkv | ForEach-Object {
    .\adaptive-encoder.exe $_.FullName
}
```

**Recursive — include all subfolders:**
```powershell
Get-ChildItem -Recurse -Include *.mkv -Exclude *_adaptive.mkv | ForEach-Object {
    .\adaptive-encoder.exe $_.FullName
}
```

**Multiple formats at once (recursive):**
```powershell
Get-ChildItem -Recurse -Include *.mkv,*.mp4,*.mov -Exclude *_adaptive.* | ForEach-Object {
    .\adaptive-encoder.exe $_.FullName
}
```

> 💡 **If PowerShell refuses to launch the `.exe`** (execution policy), first run:
> ```powershell
> Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass
> ```
> This only lasts for the current session.

### 🪟 Windows — CMD or .bat file

```cmd
for %F in (*.mkv) do adaptive-encoder.exe "%F"
```

In a `.bat` file, double the `%`:
```bat
@echo off
for %%F in (*.mkv) do adaptive-encoder.exe "%%F"
pause
```

### 🐧 Linux / 🍎 macOS

**Current folder only:**
```bash
for f in *.mkv; do
    [[ "$f" == *_adaptive.mkv ]] && continue
    ./adaptive-encoder "$f"
done
```

**Recursive (all subfolders):**
```bash
find . -type f -name "*.mkv" ! -name "*_adaptive.mkv" -exec ./adaptive-encoder {} \;
```

---

> 💡 **Before running on the whole library,** test with `--dry-run` on a single file first to verify Dolby Vision, HDR10+ and HDR are correctly detected.

> 💡 **Load/duration:** a `veryslow` encode can take several hours per film. For a large library, run it overnight or use `--no-veryslow` to cap at `slower`.

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
                                  and embedded by default via hdr10plus_tool, including
                                  alongside Dolby Vision — both metadata layers coexist
                                  in the HEVC bitstream.

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

## 🧰 Flag usage examples

This section gathers concrete examples, organized by flag category. Examples use Linux/macOS syntax (`./adaptive-encoder`) — on Windows, replace with `.\adaptive-encoder.exe`.

### 📐 Video settings

**Force framerate to 23.976 (typical cinema)** — useful if the source reports variable framerate or has a suspicious A/V wrap:
```bash
./adaptive-encoder "film.mkv" --force-fps 23.976
```

**Disable black bar detection** — use this when the source has no black bars (Academy 1.37, full-frame 1.85) or when auto-crop is incorrectly trimming graphic elements:
```bash
./adaptive-encoder "film_137.mkv" --no-crop-detect
```

**Manually adjust the CRF baseline** — a higher base CRF reduces size at the cost of visual quality:
```bash
# Higher quality (larger file, closer to remux)
./adaptive-encoder "film.mkv" --base-crf 20.0

# Smaller size (slightly degraded quality, useful for streaming)
./adaptive-encoder "film.mkv" --base-crf 24.0
```

**Convert a 4K HDR source to 1080p SDR** — for older TVs or non-HDR displays. The conversion uses libplacebo (BT.2390) with zscale+tonemap=mobius fallback:
```bash
./adaptive-encoder "4k_dolbyvision.mkv" --downscale-1080p-sdr
```

**More samples for adaptive analysis** — useful for films with highly varied content (anthology, long documentaries) where the default may under-represent some scenes:
```bash
./adaptive-encoder "anthology_3h.mkv" --max-samples 600
```

### 🎚️ Bitrate & presets

**Enable adaptive VBV cap** — `--vbv` automatically calibrates max bitrate to resolution (7 Mbps at 720p, 12 Mbps at 1080p, 17 Mbps at 1440p, 28 Mbps at 4K):
```bash
./adaptive-encoder "film.mkv" --vbv
```

**Force a manual cap** — to target a specific file size, e.g. 10 Mbps:
```bash
./adaptive-encoder "film.mkv" --max-bitrate 10000
```

**Manual cap + custom VBV buffer** — on highly variable content, a larger buffer prevents bitrate pumping:
```bash
./adaptive-encoder "film.mkv" --max-bitrate 15000 --vbv-bufsize 30000
```

**Faster encoding** — switches to `slower` instead of `veryslow` (about 2× faster, quality ~1-2% below):
```bash
./adaptive-encoder "film.mkv" --no-veryslow
```

**Force `grain` tune** — for scanned 35mm/16mm film where you want to keep the grain structure:
```bash
./adaptive-encoder "western_1970.mkv" --force-tune grain --no-denoise
```

**Force `animation` tune** — for cartoons, anime, motion design (flat areas, sharp edges):
```bash
./adaptive-encoder "anime.mkv" --force-tune animation
```

### 📺 Dolby Vision & HDR

**Force HDR10 output even if the source is Dolby Vision** — useful for compatibility with players that bug on DV:
```bash
./adaptive-encoder "uhd_dolbyvision.mkv" --no-dolby-vision
```

**Refuse the Profile 7 → 8.1 conversion** — preserves DV only if the source profile can be reproduced natively, otherwise outputs HDR10:
```bash
./adaptive-encoder "blu-ray_dv_profile7.mkv" --preserve-dv-profile
```

**Redirect DV temp files** — crucial on Linux with `/tmp` on tmpfs (limited to RAM) or if the system partition is small:
```bash
# Linux
./adaptive-encoder "film_dv.mkv" --temp-dir /mnt/ssd/temp

# macOS
./adaptive-encoder "film_dv.mkv" --temp-dir ~/temp

# Windows (from PowerShell)
.\adaptive-encoder.exe "film_dv.mkv" --temp-dir D:\temp
```

**Ignore HDR10+ even if present** — useful if your TV only handles HDR10 and you want to avoid unnecessary SEI:
```bash
./adaptive-encoder "film_hdr10plus.mkv" --no-hdr10plus
```

### 🌑 Noise reduction

**Fully disable denoising** — for archival, film sources, or any content where master fidelity matters more than cleanliness:
```bash
./adaptive-encoder "film_35mm.mkv" --no-denoise
```

**Force a specific denoise strength** — overrides the automatic calibration (0.0 = no filter, 1.0 = max):
```bash
# Light denoise on clean digital source
./adaptive-encoder "digital_source.mkv" --denoise-strength 0.2

# Strong denoise on VHS / noisy SD capture
./adaptive-encoder "vhs_rip.mkv" --denoise-strength 0.8
```

**Grain preservation mode** — denoises 40% less aggressively, keeps some texture (compromise between archival and cleanliness):
```bash
./adaptive-encoder "film_70mm.mkv" --denoise-preserve-grain
```

**Force a specific engine:**
```bash
# bm3d — max quality on stationary noise (digital sensor, modern grading)
./adaptive-encoder "raw_camera.mkv" --denoise-engine bm3d

# nlmeans — fast and general-purpose
./adaptive-encoder "film.mkv" --denoise-engine nlmeans

# hybrid — chains hqdn3d + nlmeans, ideal for mixed sources (upscaled SD/HD)
./adaptive-encoder "remaster_dvd.mkv" --denoise-engine hybrid
```

### 🔊 Audio & subtitles

**Strip all audio tracks** — to produce a video-only master:
```bash
./adaptive-encoder "film.mkv" --no-audio
```

**Strip all subtitle tracks:**
```bash
./adaptive-encoder "film.mkv" --no-subs
```

**Keep only English and French** — removes other dubs, first language listed = player default:
```bash
./adaptive-encoder "film.mkv" --audio-lang "eng,fre"
```

**Keep only the original English VO (drop dubs):**
```bash
./adaptive-encoder "film.mkv" --audio-lang "eng"
```

**Downmix 7.1/Atmos → 5.1 or 2.0** — for simpler home theater setups or space savings:
```bash
./adaptive-encoder "film_atmos.mkv" --downmix-audio
```

**Fast audio normalization (single-pass):**
```bash
./adaptive-encoder "film.mkv" --normalize-audio single-pass
```

**Precise audio normalization (two-pass) — recommended:**
```bash
./adaptive-encoder "film.mkv" --normalize-audio two-pass
```

**Custom LUFS target:**
```bash
# Strict EBU R128 broadcast
./adaptive-encoder "film.mkv" --normalize-audio two-pass --normalize-audio-target -23.0

# Spotify/YouTube-style streaming (-14 LUFS)
./adaptive-encoder "film.mkv" --normalize-audio two-pass --normalize-audio-target -14.0
```

### 🖥️ System

**Verbose mode — see adaptive analysis details:**
```bash
./adaptive-encoder "film.mkv" --verbose
```

**Dry-run — analyze and display the command without encoding:**
```bash
./adaptive-encoder "film.mkv" --dry-run
```

**Specify a custom output file:**
```bash
./adaptive-encoder "input.mkv" -o "/mnt/library/Movies/Inception (2010).mkv"
```

---

### 🎯 Useful combinations (full scenarios)

**📼 Grainy 35mm archive, maximum master fidelity**
Preserves grain structure, no denoising, tuned encoder:
```bash
./adaptive-encoder "western_1970.mkv" \
  --no-denoise \
  --force-tune grain \
  --base-crf 20.0
```

**🎌 Anime / cartoon optimized**
Animation tune, denoising active (modern anime has little grain):
```bash
./adaptive-encoder "anime_series_s01e01.mkv" \
  --force-tune animation \
  --audio-lang "jpn,eng"
```

**💾 Aggressive size reduction for personal streaming server**
Higher CRF + bitrate cap + downmix + filtered languages:
```bash
./adaptive-encoder "film.mkv" \
  --base-crf 24.0 \
  --max-bitrate 8000 \
  --downmix-audio \
  --audio-lang "eng,fre" \
  --no-veryslow
```

**📡 Heterogeneous library with normalized audio**
Two-pass loudness at -16 LUFS, language filter, adaptive VBV cap:
```bash
./adaptive-encoder "film.mkv" \
  --vbv \
  --audio-lang "eng,fre" \
  --normalize-audio two-pass
```

**📺 UHD Blu-ray Dolby Vision Profile 7 — max quality, perfect A/V**
Force 23.976 for DV resync, external temp dir, low base-crf:
```bash
./adaptive-encoder "uhd_dv_profile7.mkv" \
  --force-fps 23.976 \
  --temp-dir /mnt/ssd/temp \
  --base-crf 20.0
```

**📺 4K HDR → 1080p SDR for an older TV with controlled loudness**
Downscale + tonemap + downmix + broadcast normalization:
```bash
./adaptive-encoder "4k_hdr10plus.mkv" \
  --downscale-1080p-sdr \
  --downmix-audio \
  --normalize-audio two-pass \
  --normalize-audio-target -23.0
```

**🧪 Test before a large batch — verify detection without encoding**
Dry-run + verbose to see the full analysis:
```bash
./adaptive-encoder "sample.mkv" --dry-run --verbose
```

**⚡ Fast batch encoding, reasonable quality**
Slower instead of veryslow, slightly higher CRF:
```bash
./adaptive-encoder "film.mkv" \
  --no-veryslow \
  --base-crf 23.0 \
  --vbv
```

**🎞️ Restored VHS/DVD capture — aggressive denoising**
bm3d + manual strength + grain tune for what texture remains:
```bash
./adaptive-encoder "vhs_concert.mkv" \
  --denoise-engine bm3d \
  --denoise-strength 0.7 \
  --base-crf 22.0
```

---

## 🛠️ Troubleshooting

**The command does nothing / "not recognized".**
You're probably in the wrong folder, or `adaptive-encoder.exe` isn't in the current folder. Check with `pwd` (PowerShell) or `cd` (CMD) that you're in the right place, and with `ls` / `dir` that the `.exe` is actually there.

**Dolby Vision or HDR10+ doesn't work on Windows.**
On Windows, `dovi_tool`, `hdr10plus_tool` and `mkvmerge` are not functional inside the binary. Download all three executables and place them in the same folder as `adaptive-encoder.exe` — no installation, just drop the files. Without them, DV and HDR10+ are silently ignored and the output falls back to HDR10 only.

**My `_adaptive.mkv` files get reprocessed every time I run the batch.**
Use the batch commands that include `-Exclude *_adaptive.mkv` (PowerShell) or the bash loop that filters `*_adaptive.mkv` (Linux/macOS). See the "Batch encode" section above.

**PowerShell refuses to run the `.exe`.**
First run `Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass` in the PowerShell window. It only lasts for the current session.

**`Get-ChildItem` doesn't work.**
You're in CMD, not PowerShell. The prompt should start with `PS`. Type `powershell` then Enter to switch.

**Encoding takes hours per film — is that normal?**
Yes. `veryslow` is intentionally slow to maximize quality. Use `--no-veryslow` to switch to `slower` (about 2× faster), or `--no-veryslow --base-crf 24` to reduce further.

**Disk space saturated during Dolby Vision encoding.**
DV temp files can be large. Use `--temp-dir D:\temp` (Windows) or `--temp-dir /path/free-disk` (Linux/macOS) to redirect them to a disk with more space.

---

## ❓ FAQ

**What platforms are supported?**
Windows 10/11 (x64), Linux (x64), and macOS Apple Silicon (M1/M2/M3). `ffmpeg` and `ffprobe` are bundled on all three platforms. `dovi_tool`, `hdr10plus_tool` and `mkvmerge` are bundled on Linux and macOS. **On Windows, download `dovi_tool.exe`, `hdr10plus_tool.exe` and `mkvmerge.exe` and place them in the same folder as `adaptive-encoder.exe`** — no installation, just drop the files.

**Is this only for 4K?**
No, the tool is excellent for 1080p too. x265 parameters (`ctu`, `qg-size`, preset) are automatically tuned to the effective resolution.

**Do I need to download any tools separately?**
On Linux and macOS: no, everything is bundled. On Windows: `ffmpeg` and `ffprobe` are bundled, but **`dovi_tool.exe`, `hdr10plus_tool.exe` and `mkvmerge.exe` must be downloaded and placed in the same folder as `adaptive-encoder.exe`** — no installation, just drop the files.

**Do Dolby Vision and HDR10+ work automatically?**
Yes, provided `dovi_tool`, `hdr10plus_tool` and `mkvmerge` are available. On Linux and macOS, everything is bundled and works with no setup. **On Windows, download `dovi_tool.exe`, `hdr10plus_tool.exe` and `mkvmerge.exe`** and place them in the same folder as `adaptive-encoder.exe` — no installation, just drop the files. The binary auto-detects Dolby Vision (Profile 5/7/8.x) and HDR10+ (SMPTE 2094-40) sources and preserves both metadata tracks with no configuration. If a source carries both, they coexist in the HEVC bitstream: Dolby Vision displays use the RPU, HDR10+-only displays (e.g. Samsung) use the SMPTE 2094-40 SEI. Selection happens on the player/display side based on what it supports.

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
