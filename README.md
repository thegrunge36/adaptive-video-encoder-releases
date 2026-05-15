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
- 🌑 **Débruitage adaptatif** — force calibrée automatiquement à partir du bruit/grain mesurés ; si le score combiné est sous le seuil (~0.08), aucun filtre n'est appliqué. Quatre choix de moteur : `auto` (défaut — sélection intelligente selon le ratio bruit/grain et la force), `nlmeans`, `bm3d`, `hybrid` (hqdn3d+nlmeans). Option `--denoise-preserve-grain` pour ne lisser qu'une fraction de la texture.
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
--auto-rename                     Si le fichier de sortie est verrouillé par un autre processus
                                  (ouvert dans un player, scanné par l'antivirus, retenu par un
                                  ffmpeg orphelin, etc.), utilise automatiquement un nom alternatif
                                  (_v2, _v3, ...) au lieu d'abandonner. Défaut : abandonne avec un
                                  message diagnostic listant les causes courantes.

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
                                  Override le calibrage automatique. Toute valeur > 0
                                  est toujours honorée, peu importe la propreté de la
                                  source.
--denoise-preserve-grain          Débruitage 40% plus doux qui préserve une partie de la
                                  texture du grain.
--denoise-engine {auto,nlmeans,bm3d,hybrid}
                                  Choisit le moteur de débruitage. Défaut : 'auto' —
                                  sélection intelligente selon le ratio bruit/grain
                                  et la force calculée :
                                    • bm3d quand le bruit stationnaire domine (ratio
                                      bruit/grain > 1.3) — typique des sources numériques
                                    • hybrid (hqdn3d + nlmeans) quand le grain domine
                                      (ratio < 0.77) — typique du film 35mm
                                    • nlmeans dans les cas équilibrés ou à faible force
                                  Forcer une valeur explicite (nlmeans / bm3d / hybrid)
                                  désactive la sélection auto et la garantit appliquée.
                                  Si l'engine demandé est absent de ffmpeg, fallback vers
                                  un engine disponible avec avertissement visible (jamais
                                  d'échec silencieux).

[ Audio & Sous-titres ]
--no-audio                        Supprime les pistes audio (copiées par défaut)
--no-subs                         Supprime les sous-titres (copiés par défaut)
--audio-lang AUDIO_LANG           Garde uniquement certaines langues audio (ex. 'fre,eng').
                                  Supprime les doublages indésirables pour économiser de
                                  l'espace.
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

> ℹ️ **Comportement par défaut :** sans aucun flag de débit, l'encodeur fonctionne en **CRF pur** (pas de plafond de débit). La taille finale dépend uniquement de la complexité du contenu et de `--base-crf` (défaut : 22.0). Activer `--vbv` ou `--max-bitrate` impose un plafond.

#### Échelle CRF rapide

Le CRF est une échelle de qualité inversée (plus bas = mieux). Effet typique sur la taille finale d'un Blu-ray remux 1080p ré-encodé :

| `--base-crf` | Effet | Cas d'usage typique |
|---|---|---|
| 18 | Quasi-transparent, fichier très lourd | Archivage maximal, masters |
| 20 | Excellent, légèrement plus léger | Archivage qualité, **proche-remux** |
| 22 (défaut) | Bon compromis qualité/taille | Usage général |
| 24 | Visible sur scènes complexes | Réduction de taille, streaming perso |
| 26+ | Artefacts visibles | À éviter sauf contrainte espace |

Règle empirique : **chaque +1 sur le CRF réduit la taille d'environ 20-25 %**.

```bash
# Qualité plus haute (fichier plus lourd, plus proche du remux)
./adaptive-encoder "film.mkv" --base-crf 20.0

# Compromis (défaut implicite)
./adaptive-encoder "film.mkv" --base-crf 22.0

# Taille plus petite (qualité légèrement dégradée, utile pour la diffusion perso)
./adaptive-encoder "film.mkv" --base-crf 24.0
```

> ⚠️ Le CRF base est **ajusté image par image** par l'analyse adaptative. Les scènes simples reçoivent un CRF plus élevé (économies de bits), les scènes complexes un CRF plus bas (préservation du détail). `--base-crf` décale toute la courbe.

#### Plafonner le débit avec VBV

**`--vbv` — Plafond adaptatif automatique** : calibre le débit max selon la résolution effective post-crop (~7 Mbps en 720p, ~12 Mbps en 1080p, ~17 Mbps en 1440p, ~28 Mbps en 4K). Borné entre **2.5 Mbps et 35 Mbps** (plancher pour éviter de tuer la qualité sur SD/360p, plafond pour rester compatible avec les players grand public). Recommandé si vous voulez un plafond raisonnable sans réfléchir :

```bash
./adaptive-encoder "film.mkv" --vbv
```

**`--max-bitrate` — Plafond manuel en kbps** : impose une valeur précise, **override le calcul auto de `--vbv`**. Utile pour cibler une taille de fichier précise :

```bash
# Plafond manuel à 10 Mbps
./adaptive-encoder "film.mkv" --max-bitrate 10000

# Plafond à 20 Mbps pour du 4K
./adaptive-encoder "film_4k.mkv" --max-bitrate 20000
```

> ℹ️ **Interaction `--vbv` / `--max-bitrate` :** si vous passez `--max-bitrate`, sa valeur prime et le calcul automatique de `--vbv` est ignoré. Il n'est donc pas utile de combiner les deux flags.

**`--vbv-bufsize` — Taille du buffer VBV en kbits** : par défaut, le buffer = **1.5× max bitrate**. Élargir le buffer permet des pics plus longs (lisse les pompages sur contenu très variable) :

```bash
# Buffer 1.5× du plafond — comportement par défaut, donné pour référence
./adaptive-encoder "film.mkv" --max-bitrate 15000 --vbv-bufsize 22500

# Buffer 2× — pour scènes très variables (sports, action rapide, feux d'artifice)
./adaptive-encoder "film.mkv" --max-bitrate 15000 --vbv-bufsize 30000

# Buffer 3× — limite des spécifications de player typiques (au-delà : risques d'incompatibilité)
./adaptive-encoder "film.mkv" --max-bitrate 15000 --vbv-bufsize 45000
```

#### Préréglages d'encodage

**Encodage plus rapide** — bascule sur `slower` au lieu de `veryslow` (env. 2× plus rapide, qualité ~1-2 % en dessous, recommandé pour les gros lots) :
```bash
./adaptive-encoder "film.mkv" --no-veryslow
```

**Tune `grain` forcé** — préserve la structure du grain (psy-rd plus élevé, deblock désactivé). Pour pellicules 35mm/16mm scannées :
```bash
./adaptive-encoder "western_1970.mkv" --force-tune grain --no-denoise
```

**Tune `animation` forcé** — optimise pour les zones plates et les bords nets. Pour dessins animés, anime, motion design :
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

> ℹ️ **Comportement par défaut :** sans aucun flag denoise, l'engine est `auto` et la force est calibrée automatiquement à partir du bruit et du grain mesurés. Si la source est très propre (score combiné < 0.08), **aucun filtre n'est appliqué** — vous récupérez votre fichier sans traitement. Sur une source bruitée ou granuleuse, l'auto choisit l'engine et la force adaptés.

**Mode auto par défaut (aucun flag denoise)** — comportement implicite, l'outil décide tout. `auto` sélectionne intelligemment :

| Profil bruit/grain détecté | Engine choisi | Pourquoi |
|---|---|---|
| Bruit stationnaire dominant (ratio bruit/grain > 1.3) | **bm3d** | Idéal sur bruit capteur / numérique propre |
| Grain dominant (ratio < 0.77) | **hybrid** (hqdn3d + nlmeans) | Adapté au grain film 35mm/16mm |
| Équilibré ou faible force | **nlmeans** | Rapide et général |

```bash
# Tout en auto — l'outil mesure, choisit l'engine et la force
./adaptive-encoder "film.mkv"
```

**Désactiver totalement le débruitage** — pour les archives, sources film, ou tout contenu où la fidélité au master prime sur la propreté :
```bash
./adaptive-encoder "film_35mm.mkv" --no-denoise
```

**Forcer une force de débruitage spécifique** — override le calibrage automatique. **Toute valeur > 0 est toujours appliquée**, même sur une source que l'auto aurait classée comme « trop propre pour denoise » :
```bash
# Débruitage léger sur source numérique propre (l'auto aurait skip ce filtre)
./adaptive-encoder "source_numerique.mkv" --denoise-strength 0.2

# Débruitage fort sur capture VHS / SD bruitée
./adaptive-encoder "vhs_rip.mkv" --denoise-strength 0.8
```

**Mode préservation du grain** — débruite 40 % moins fort, conserve une partie de la texture (compromis archive ↔ propreté) :
```bash
./adaptive-encoder "film_70mm.mkv" --denoise-preserve-grain
```

**Forcer un moteur spécifique** — bypass la sélection auto. La valeur que vous donnez est **toujours appliquée** (avec fallback vers un engine disponible si ffmpeg ne contient pas celui demandé, avec avertissement visible) :
```bash
# bm3d — qualité max sur bruit stationnaire (capteur numérique, étalonnage moderne)
./adaptive-encoder "raw_camera.mkv" --denoise-engine bm3d

# nlmeans — rapide et général, force la sélection sans laisser l'auto décider
./adaptive-encoder "film.mkv" --denoise-engine nlmeans

# hybrid — chaîne hqdn3d + nlmeans, idéal pour sources mixtes (SD/HD upscalés)
./adaptive-encoder "remaster_dvd.mkv" --denoise-engine hybrid

# Repasser explicitement en auto (équivalent à ne rien passer)
./adaptive-encoder "film.mkv" --denoise-engine auto
```

> 💡 **Comment vérifier ce qui a été appliqué :** la ligne `denoise:` dans `▶ Selecting parameters…` affiche un préfixe `auto→` si la sélection vient de l'auto. Exemple :
> - `denoise: moderate (auto→hybrid, strength 35%)` → auto a choisi hybrid
> - `denoise: moderate (hybrid, strength 35%)` → vous avez forcé hybrid via `--denoise-engine hybrid`

### 🔊 Audio & sous-titres

> ℹ️ **Comportement par défaut :** sans aucun flag audio, **toutes les pistes audio sont copiées bit-perfect** (stream copy) — aucun ré-encodage, aucune perte. Toutes les pistes de sous-titres aussi. Activer `--normalize-audio` ou `--downmix-audio` force le ré-encodage en AC3 et fait perdre la copie bit-perfect.

**Supprimer toutes les pistes audio** — produit un master vidéo seul, utile avant un remux audio externe ou pour archiver une « image clean » :
```bash
./adaptive-encoder "film.mkv" --no-audio
```

**Supprimer tous les sous-titres** — retire toutes les pistes SRT / PGS / ASS / VobSub de la sortie :
```bash
./adaptive-encoder "film.mkv" --no-subs
```

#### Filtrer les pistes audio par langue

`--audio-lang` ne garde que les langues listées (codes ISO 639-2/B : `eng`, `fre`, `jpn`, `ger`, `spa`, `ita`, `por`, `rus`, etc.). **Le flag agit uniquement comme un filtre — il ne réordonne pas les pistes.** Les pistes audio conservées gardent l'ordre du fichier source ; la piste par défaut du player sera donc la première piste *du fichier source* qui correspond à une des langues listées. Les sous-titres ne sont **pas** filtrés par ce flag — utilisez `--no-subs` si vous voulez tout retirer.

```bash
# Garde anglais + français (l'ordre dans la sortie suit le fichier source,
# pas l'ordre listé ici)
./adaptive-encoder "film.mkv" --audio-lang "eng,fre"

# Uniquement la VO anglaise (toutes les autres pistes supprimées)
./adaptive-encoder "film.mkv" --audio-lang "eng"

# Anime : garde japonais + anglais + français, ordre source préservé
./adaptive-encoder "anime.mkv" --audio-lang "jpn,eng,fre"
```

> 💡 Pour réordonner les pistes ou changer la piste par défaut, c'est à faire en post-traitement avec `mkvmerge` (`--default-track-flag`) ou `mkvpropedit`.

#### Downmixer les pistes multicanal lourdes

`--downmix-audio` est **conditionnel** : il ne ré-encode que les pistes qui ont effectivement besoin d'être downmixées (8 canaux ou plus). Les pistes 5.1, stéréo et mono restent **stream-copiées bit-perfect** (codec d'origine préservé) tant que `--normalize-audio` n'est pas aussi actif.

| Source détectée | Cible avec `--downmix-audio` seul | Avec `--downmix-audio` + `--normalize-audio` |
|---|---|---|
| Atmos / TrueHD Atmos / DTS:X (8+ canaux) | **5.1 AC3 640 kbps** (ré-encodé) | 5.1 AC3 640 kbps |
| 7.1 (8 canaux) | **5.1 AC3 640 kbps** (ré-encodé) | 5.1 AC3 640 kbps |
| 5.1 (6 canaux) | **stream-copiée** (codec d'origine) | 5.1 AC3 640 kbps |
| Stéréo (2 canaux) | **stream-copiée** (codec d'origine) | Stéréo AC3 192 kbps |
| Mono (1 canal) | **stream-copiée** (codec d'origine) | Mono AC3 96 kbps |

> ℹ️ Atmos en EAC3 JOC est typiquement délivré sur une base 5.1 (6 canaux) — l'outil le détecte comme 5.1 et le **stream-copie** (préservant les métadonnées Atmos). Seul Atmos en TrueHD (base 7.1.x → 8 canaux reportés) déclenche le downmix vers 5.1 AC3.

```bash
# Downmix Atmos / 7.1 → 5.1 AC3 640 kbps (les pistes 5.1 ou stéréo restent intactes)
./adaptive-encoder "film_atmos.mkv" --downmix-audio
```

> ⚠️ **Pour répondre à la question « comment obtenir spécifiquement 5.1 AC3 à 640 kbps ? » :** c'est exactement ce que produit `--downmix-audio` sur une source 7.1 ou TrueHD Atmos. Le 640 kbps n'est pas configurable en CLI — c'est la valeur fixe utilisée par l'outil pour le 5.1 (192 kbps pour la stéréo, 96 kbps pour le mono). Si vous voulez **forcer le ré-encodage AC3 même sur une source déjà en 5.1** (par exemple pour normaliser la loudness et avoir un débit identique sur toute la bibliothèque), combinez avec `--normalize-audio two-pass`.
>
> Si vous avez besoin d'un autre débit (ex. 448 kbps), d'un autre codec (EAC3, AAC, Opus), ou de forcer la sortie en stéréo (le flag `--downmix-audio` cible toujours le 5.1 sur source 7.1+), c'est à faire en post-traitement avec ffmpeg.

#### Normalisation EBU R128 (loudness)

`--normalize-audio` applique une normalisation de loudness aux pistes audio conservées. **Active obligatoirement le ré-encodage** en AC3 → vous perdez l'audio bit-perfect d'origine. Débits AC3 : 640 kbps pour 5.1, 192 kbps pour stéréo, **96 kbps pour mono**.

Deux modes :

```bash
# Single-pass — rapide (1 passe ffmpeg), normalisation dynamique
# Légèrement moins précise sur les variations de loudness scène par scène
./adaptive-encoder "film.mkv" --normalize-audio single-pass

# Two-pass — recommandé : passe de mesure puis correction linéaire
# Plus lent (mesure ~= durée du film en plus), mais précis
./adaptive-encoder "film.mkv" --normalize-audio two-pass
```

**Cible LUFS personnalisée** — défaut `-16 LUFS` (TV / streaming). Quelques cibles courantes :

```bash
# Broadcast EBU R128 strict (TV européenne : BBC, ARTE, France 2, etc.)
./adaptive-encoder "film.mkv" --normalize-audio two-pass --normalize-audio-target -23.0

# ATSC A/85 (broadcast US)
./adaptive-encoder "film.mkv" --normalize-audio two-pass --normalize-audio-target -24.0

# Streaming type Spotify / YouTube
./adaptive-encoder "film.mkv" --normalize-audio two-pass --normalize-audio-target -14.0

# Apple Music / Apple TV (équivalent au défaut)
./adaptive-encoder "film.mkv" --normalize-audio two-pass --normalize-audio-target -16.0
```

#### Combinaisons audio courantes

**Downmix + normalisation (home cinéma 5.1 cohérent)** — sortie 5.1 AC3 640 kbps avec loudness alignée. La combinaison la plus utilisée pour une bibliothèque destinée à un AV receiver 5.1 :

```bash
./adaptive-encoder "film_atmos.mkv" --downmix-audio --normalize-audio two-pass
```

**Bibliothèque 5.1 broadcast EBU R128 complète** — filtre langues + downmix + normalisation -23 LUFS :

```bash
./adaptive-encoder "film_atmos.mkv" \
  --audio-lang "fre,eng" \
  --downmix-audio \
  --normalize-audio two-pass \
  --normalize-audio-target -23.0
```

**Préservation maximale audio** — toutes les pistes copiées bit-perfect, aucune transformation (comportement par défaut, donné ici pour référence) :

```bash
./adaptive-encoder "film.mkv"
```

**Filtrer langues mais préserver le bit-perfect** — supprime les doublages indésirables tout en gardant les pistes conservées en copie pure :

```bash
./adaptive-encoder "film.mkv" --audio-lang "eng,fre"
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

**J'ai forcé `--denoise-strength` ou `--denoise-engine` et l'outil semble ignorer mon choix.**
Vérifiez la ligne `denoise:` affichée dans `▶ Selecting parameters…` :
- Préfixe `auto→` = le mode auto a choisi pour vous (vous n'avez pas forcé)
- Pas de préfixe = votre choix est appliqué tel quel
- `disabled` = vous avez passé `--no-denoise` ou la source est trop propre (auto sans force)

Si vous avez forcé `--denoise-strength 0.5` et que l'engine n'est pas disponible dans ffmpeg, l'outil affiche un avertissement jaune et fallback vers un engine disponible. La force que vous avez demandée est conservée.

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
Le débruitage **adaptatif** est activé par défaut, avec l'engine en mode `auto`. La force est auto-calibrée à partir des métriques de bruit et de grain : si le score combiné est sous ~0.08, aucun filtre n'est appliqué. Sur une source propre (Blu-ray récent sans grain marqué), vous n'aurez aucun traitement. Sur un film 35mm très grenu, vous aurez un débruitage modéré avec l'engine `hybrid` (sélectionné automatiquement parce que le grain domine). Pour garantir zéro filtre quelle que soit la source, utilisez `--no-denoise`. Pour un compromis (préserver une partie de la texture du grain), utilisez `--denoise-preserve-grain`.

**Comment fonctionne le mode `auto` de `--denoise-engine` ?**
En mode auto (le défaut), l'outil regarde le ratio bruit/grain mesuré sur la source et la force calculée, puis choisit l'engine optimal : **bm3d** quand le bruit stationnaire domine (sources numériques modernes, ratio bruit/grain > 1.3), **hybrid** (hqdn3d + nlmeans) quand le grain domine (film 35mm/16mm, ratio < 0.77), **nlmeans** dans les cas équilibrés ou à faible force. Si vous forcez `--denoise-engine` avec une valeur explicite, l'auto est complètement bypassé et votre choix est appliqué. Si l'engine demandé n'est pas disponible dans le ffmpeg embarqué, l'outil fallback automatiquement vers un engine compatible avec un avertissement visible (jamais d'échec silencieux).

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
- 🌑 **Adaptive denoising** — strength auto-calibrated from measured noise/grain; if the combined score is below threshold (~0.08), no filter is applied. Four engine choices: `auto` (default — smart selection by noise/grain ratio and strength), `nlmeans`, `bm3d`, `hybrid` (hqdn3d+nlmeans). `--denoise-preserve-grain` smooths only a fraction of the texture.
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
--auto-rename                     If the output file is locked by another process (open in a
                                  player, scanned by antivirus, held by a stale ffmpeg, etc.),
                                  automatically pick an alternative name (_v2, _v3, ...) instead
                                  of aborting. Default: abort with a diagnostic message listing
                                  common causes.

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
                                  Overrides the automatic calibration. Any value > 0
                                  is always honored, regardless of how clean the
                                  source is.
--denoise-preserve-grain          40% gentler denoise that preserves some film grain
                                  texture.
--denoise-engine {auto,nlmeans,bm3d,hybrid}
                                  Pick the denoising engine. Default: 'auto' — smart
                                  selection from the noise/grain ratio and computed
                                  strength:
                                    • bm3d when stationary noise dominates (noise/grain
                                      ratio > 1.3) — typical of digital sources
                                    • hybrid (hqdn3d + nlmeans) when grain dominates
                                      (ratio < 0.77) — typical of 35mm film
                                    • nlmeans for balanced cases or low strength
                                  Forcing an explicit value (nlmeans / bm3d / hybrid)
                                  disables the auto selection and guarantees it's
                                  applied. If the requested engine is missing from
                                  ffmpeg, the tool falls back to an available engine
                                  with a visible warning (never silent failure).

[ Audio & Subtitles ]
--no-audio                        Remove audio tracks (copied by default)
--no-subs                         Remove subtitle tracks (copied by default)
--audio-lang AUDIO_LANG           Keep only specific audio languages (e.g., 'fre,eng').
                                  Removes unwanted dubs to save space.
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

> ℹ️ **Default behavior:** without any bitrate flag, the encoder runs in **pure CRF mode** (no bitrate cap). Final size depends only on content complexity and `--base-crf` (default: 22.0). Enabling `--vbv` or `--max-bitrate` imposes a cap.

#### Quick CRF scale

CRF is an inverted quality scale (lower = better). Typical effect on the final size of a re-encoded 1080p Blu-ray remux:

| `--base-crf` | Effect | Typical use case |
|---|---|---|
| 18 | Near-transparent, very large file | Maximum archival, masters |
| 20 | Excellent, slightly lighter | Quality archival, **near-remux** |
| 22 (default) | Good quality/size tradeoff | General use |
| 24 | Visible on complex scenes | Size reduction, personal streaming |
| 26+ | Visible artifacts | Avoid unless space-constrained |

Rule of thumb: **each +1 on CRF reduces size by about 20-25%**.

```bash
# Higher quality (larger file, closer to remux)
./adaptive-encoder "film.mkv" --base-crf 20.0

# Tradeoff (implicit default)
./adaptive-encoder "film.mkv" --base-crf 22.0

# Smaller size (slightly degraded quality, useful for personal streaming)
./adaptive-encoder "film.mkv" --base-crf 24.0
```

> ⚠️ The base CRF is **adjusted frame-by-frame** by the adaptive analysis. Simple scenes get a higher CRF (bit savings), complex scenes a lower CRF (detail preservation). `--base-crf` shifts the whole curve.

#### Cap the bitrate with VBV

**`--vbv` — Automatic adaptive cap**: calibrates max bitrate to the effective post-crop resolution (~7 Mbps at 720p, ~12 Mbps at 1080p, ~17 Mbps at 1440p, ~28 Mbps at 4K). Bounded between **2.5 Mbps and 35 Mbps** (floor to keep SD/360p watchable, cap to stay compatible with consumer players). Recommended if you want a reasonable cap without thinking:

```bash
./adaptive-encoder "film.mkv" --vbv
```

**`--max-bitrate` — Manual cap in kbps**: forces a precise value, **overrides the auto-calc of `--vbv`**. Useful for targeting a specific file size:

```bash
# Manual cap at 10 Mbps
./adaptive-encoder "film.mkv" --max-bitrate 10000

# 20 Mbps cap for 4K
./adaptive-encoder "film_4k.mkv" --max-bitrate 20000
```

> ℹ️ **`--vbv` / `--max-bitrate` interaction:** if you pass `--max-bitrate`, its value wins and `--vbv`'s automatic calc is ignored. Combining both flags isn't useful.

**`--vbv-bufsize` — VBV buffer size in kbits**: by default, buffer = **1.5× max bitrate**. A larger buffer allows longer peaks (smooths bitrate pumping on highly variable content):

```bash
# Buffer 1.5× cap — default behavior, shown for reference
./adaptive-encoder "film.mkv" --max-bitrate 15000 --vbv-bufsize 22500

# Buffer 2× — for highly variable scenes (sports, fast action, fireworks)
./adaptive-encoder "film.mkv" --max-bitrate 15000 --vbv-bufsize 30000

# Buffer 3× — typical player spec ceiling (beyond that: compatibility risks)
./adaptive-encoder "film.mkv" --max-bitrate 15000 --vbv-bufsize 45000
```

#### Encoding presets

**Faster encoding** — switches to `slower` instead of `veryslow` (about 2× faster, quality ~1-2% below, recommended for large batches):
```bash
./adaptive-encoder "film.mkv" --no-veryslow
```

**Force `grain` tune** — preserves grain structure (higher psy-rd, deblock disabled). For scanned 35mm/16mm film:
```bash
./adaptive-encoder "western_1970.mkv" --force-tune grain --no-denoise
```

**Force `animation` tune** — optimizes for flat areas and sharp edges. For cartoons, anime, motion design:
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

> ℹ️ **Default behavior:** without any denoise flag, the engine is `auto` and the strength is auto-calibrated from measured noise and grain. If the source is very clean (combined score < 0.08), **no filter is applied** — you get your file back without any processing. On a noisy or grainy source, auto picks the engine and the strength.

**Default auto mode (no denoise flag)** — implicit behavior, the tool decides everything. `auto` selects intelligently:

| Detected noise/grain profile | Engine picked | Why |
|---|---|---|
| Stationary noise dominates (noise/grain ratio > 1.3) | **bm3d** | Ideal on sensor / clean digital noise |
| Grain dominates (ratio < 0.77) | **hybrid** (hqdn3d + nlmeans) | Suited for 35mm/16mm film grain |
| Balanced or low strength | **nlmeans** | Fast and general-purpose |

```bash
# Full auto — the tool measures, picks the engine and the strength
./adaptive-encoder "film.mkv"
```

**Fully disable denoising** — for archival, film sources, or any content where master fidelity matters more than cleanliness:
```bash
./adaptive-encoder "film_35mm.mkv" --no-denoise
```

**Force a specific denoise strength** — overrides the automatic calibration. **Any value > 0 is always applied**, even on a source that auto would have classified as "too clean to denoise":
```bash
# Light denoise on clean digital source (auto would have skipped this filter)
./adaptive-encoder "digital_source.mkv" --denoise-strength 0.2

# Strong denoise on VHS / noisy SD capture
./adaptive-encoder "vhs_rip.mkv" --denoise-strength 0.8
```

**Grain preservation mode** — denoises 40% less aggressively, keeps some texture (compromise between archival and cleanliness):
```bash
./adaptive-encoder "film_70mm.mkv" --denoise-preserve-grain
```

**Force a specific engine** — bypasses the auto selection. The value you provide is **always applied** (with fallback to an available engine if ffmpeg lacks the one requested, with a visible warning):
```bash
# bm3d — max quality on stationary noise (digital sensor, modern grading)
./adaptive-encoder "raw_camera.mkv" --denoise-engine bm3d

# nlmeans — fast and general-purpose, forces selection without letting auto decide
./adaptive-encoder "film.mkv" --denoise-engine nlmeans

# hybrid — chains hqdn3d + nlmeans, ideal for mixed sources (upscaled SD/HD)
./adaptive-encoder "remaster_dvd.mkv" --denoise-engine hybrid

# Explicitly back to auto (same as passing nothing)
./adaptive-encoder "film.mkv" --denoise-engine auto
```

> 💡 **How to verify what was applied:** the `denoise:` line in `▶ Selecting parameters…` shows an `auto→` prefix if auto picked the engine. Example:
> - `denoise: moderate (auto→hybrid, strength 35%)` → auto picked hybrid
> - `denoise: moderate (hybrid, strength 35%)` → you forced hybrid with `--denoise-engine hybrid`

### 🔊 Audio & subtitles

> ℹ️ **Default behavior:** without any audio flag, **all audio tracks are stream-copied bit-perfect** — no re-encoding, no loss. All subtitle tracks too. Enabling `--normalize-audio` or `--downmix-audio` forces re-encoding to AC3 and loses bit-perfect copy.

**Strip all audio tracks** — produces a video-only master, useful before an external audio remux or to archive a "clean image":
```bash
./adaptive-encoder "film.mkv" --no-audio
```

**Strip all subtitle tracks** — removes all SRT / PGS / ASS / VobSub tracks from the output:
```bash
./adaptive-encoder "film.mkv" --no-subs
```

#### Filter audio tracks by language

`--audio-lang` keeps only the listed languages (ISO 639-2/B codes: `eng`, `fre`, `jpn`, `ger`, `spa`, `ita`, `por`, `rus`, etc.). **The flag acts only as a filter — it does not reorder tracks.** Kept audio tracks preserve the source file's order; the player's default track will therefore be the first track *from the source file* that matches one of the listed languages. Subtitles are **not** filtered by this flag — use `--no-subs` if you want all of them removed.

```bash
# Keep English + French (output order follows the source file, not the order
# listed here)
./adaptive-encoder "film.mkv" --audio-lang "eng,fre"

# Original English VO only (all other tracks stripped)
./adaptive-encoder "film.mkv" --audio-lang "eng"

# Anime: keep Japanese + English + French, source order preserved
./adaptive-encoder "anime.mkv" --audio-lang "jpn,eng,fre"
```

> 💡 To reorder tracks or change the default track, do it as a post-processing step with `mkvmerge` (`--default-track-flag`) or `mkvpropedit`.

#### Downmix heavy multichannel tracks

`--downmix-audio` is **conditional**: it only re-encodes tracks that actually need to be downmixed (8 channels or more). Tracks already in 5.1, stereo or mono remain **stream-copied bit-perfect** (original codec preserved) as long as `--normalize-audio` is not also active.

| Source detected | With `--downmix-audio` alone | With `--downmix-audio` + `--normalize-audio` |
|---|---|---|
| Atmos / TrueHD Atmos / DTS:X (8+ channels) | **5.1 AC3 640 kbps** (re-encoded) | 5.1 AC3 640 kbps |
| 7.1 (8 channels) | **5.1 AC3 640 kbps** (re-encoded) | 5.1 AC3 640 kbps |
| 5.1 (6 channels) | **stream-copied** (original codec) | 5.1 AC3 640 kbps |
| Stereo (2 channels) | **stream-copied** (original codec) | Stereo AC3 192 kbps |
| Mono (1 channel) | **stream-copied** (original codec) | Mono AC3 96 kbps |

> ℹ️ Atmos in EAC3 JOC is typically delivered on a 5.1 base (6 channels) — the tool detects it as 5.1 and **stream-copies** it (preserving the Atmos metadata). Only Atmos in TrueHD (7.1.x base → 8 reported channels) triggers the downmix to 5.1 AC3.

```bash
# Downmix Atmos / 7.1 → 5.1 AC3 640 kbps (already-5.1 or stereo tracks stay intact)
./adaptive-encoder "film_atmos.mkv" --downmix-audio
```

> ⚠️ **To answer "how do I get specifically 5.1 AC3 at 640 kbps?":** that's exactly what `--downmix-audio` produces on a 7.1 or TrueHD Atmos source. 640 kbps isn't configurable on the CLI — it's the fixed value the tool uses for 5.1 (192 kbps for stereo, 96 kbps for mono). If you want to **force AC3 re-encoding even on an already-5.1 source** (e.g. to normalize loudness and have a uniform bitrate across the library), combine with `--normalize-audio two-pass`.
>
> If you need a different bitrate (e.g. 448 kbps), a different codec (EAC3, AAC, Opus), or want to force stereo output (the `--downmix-audio` flag always targets 5.1 from 7.1+ sources), do it as a post-processing step with ffmpeg.

#### EBU R128 normalization (loudness)

`--normalize-audio` applies loudness normalization to all kept audio tracks. **It mandatorily enables re-encoding** to AC3 → you lose bit-perfect original audio. AC3 bitrates: 640 kbps for 5.1, 192 kbps for stereo, **96 kbps for mono**.

Two modes:

```bash
# Single-pass — fast (1 ffmpeg pass), dynamic normalization
# Slightly less accurate on scene-by-scene loudness variations
./adaptive-encoder "film.mkv" --normalize-audio single-pass

# Two-pass — recommended: measure pass then linear correction
# Slower (measurement ~= film duration extra), but precise
./adaptive-encoder "film.mkv" --normalize-audio two-pass
```

**Custom LUFS target** — default `-16 LUFS` (TV / streaming). Common targets:

```bash
# Strict EBU R128 broadcast (European TV: BBC, ARTE, France 2, etc.)
./adaptive-encoder "film.mkv" --normalize-audio two-pass --normalize-audio-target -23.0

# ATSC A/85 (US broadcast)
./adaptive-encoder "film.mkv" --normalize-audio two-pass --normalize-audio-target -24.0

# Spotify / YouTube-style streaming
./adaptive-encoder "film.mkv" --normalize-audio two-pass --normalize-audio-target -14.0

# Apple Music / Apple TV (equivalent to the default)
./adaptive-encoder "film.mkv" --normalize-audio two-pass --normalize-audio-target -16.0
```

#### Common audio combinations

**Downmix + normalization (consistent 5.1 home theater)** — 5.1 AC3 640 kbps output with aligned loudness. The most common combination for a library targeting a 5.1 AV receiver:

```bash
./adaptive-encoder "film_atmos.mkv" --downmix-audio --normalize-audio two-pass
```

**Full 5.1 EBU R128 broadcast library** — language filter + downmix + -23 LUFS normalization:

```bash
./adaptive-encoder "film_atmos.mkv" \
  --audio-lang "eng,fre" \
  --downmix-audio \
  --normalize-audio two-pass \
  --normalize-audio-target -23.0
```

**Maximum audio preservation** — all tracks stream-copied bit-perfect, no transformation (default behavior, shown here for reference):

```bash
./adaptive-encoder "film.mkv"
```

**Filter languages but preserve bit-perfect** — strip unwanted dubs while keeping kept tracks in pure copy:

```bash
./adaptive-encoder "film.mkv" --audio-lang "eng,fre"
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

**I forced `--denoise-strength` or `--denoise-engine` and the tool seems to ignore my choice.**
Check the `denoise:` line shown in `▶ Selecting parameters…`:
- `auto→` prefix = auto mode picked for you (you didn't force)
- No prefix = your choice is applied as-is
- `disabled` = you passed `--no-denoise` or the source is too clean (auto without force)

If you forced `--denoise-strength 0.5` and the engine isn't available in ffmpeg, the tool shows a yellow warning and falls back to an available engine. The strength you requested is preserved.

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
**Adaptive** denoising is enabled by default, with the engine in `auto` mode. Strength is auto-calibrated from noise and grain metrics: if the combined score is below ~0.08, no filter is applied. On a clean source (recent Blu-ray without heavy grain), you'll get no processing. On a heavily-grained 35mm film, you'll get moderate denoising with the `hybrid` engine (selected automatically because grain dominates). To guarantee zero filtering regardless of the source, use `--no-denoise`. For a compromise (preserve some grain texture), use `--denoise-preserve-grain`.

**How does the `--denoise-engine` `auto` mode work?**
In auto mode (the default), the tool looks at the measured noise/grain ratio on the source and the computed strength, then picks the optimal engine: **bm3d** when stationary noise dominates (modern digital sources, noise/grain ratio > 1.3), **hybrid** (hqdn3d + nlmeans) when grain dominates (35mm/16mm film, ratio < 0.77), **nlmeans** in balanced cases or at low strength. If you force `--denoise-engine` with an explicit value, auto is completely bypassed and your choice is applied. If the requested engine isn't available in the bundled ffmpeg, the tool automatically falls back to a compatible engine with a visible warning (never silent failure).

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
