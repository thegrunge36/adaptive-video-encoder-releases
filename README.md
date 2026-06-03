# 🎬 Adaptive Video Encoder

> **L'encodeur H.265 qui préserve votre Dolby Vision**

[![License: Commercial](https://img.shields.io/badge/License-Commercial-blue.svg)](LICENSE)
[![Python 3.8+](https://img.shields.io/badge/Python-3.8%2B-brightgreen.svg)](https://www.python.org/)
[![Platform Support](https://img.shields.io/badge/Platforms-Windows%20%7C%20Linux%20%7C%20macOS-lightgrey.svg)](#plateforme-support)

---

## 📋 Vue d'ensemble

**Adaptive Video Encoder** est un outil d'encodage vidéo professionnel conçu pour les créateurs de contenu, les passionnés d'audiovisuel et les studios de production. Il offre une compression H.265 intelligente tout en préservant **intégralement les métadonnées Dolby Vision**, HDR10+, HLG et les informations de film grain.

### ✨ Points forts

- **Dolby Vision Smart** : Analyse image par image | Profils 5, 7, 8.x supportés
- **Interface graphique native** : macOS (Tkinter/CustomTkinter), Windows et Linux
- **Préservation de la qualité HDR** : HDR10 | HLG | BT.2020 | Format grain
- **Débruitage intelligent** : Filtre hqdn3d avec fenêtres glissantes temporelles
- **Remuxage MKV** : Support mkvmerge + construction JSON rapide
- **Système de licence** : Essai gratuit 7 jours | Licence à vie $49.99
- **Cross-platform** : Code compilable avec PyInstaller/Nuitka
- **CLI puissante** : Intégration facile dans les scripts de production

---

## 🚀 Installation rapide

### Prérequis

- **Python 3.8+**
- **FFmpeg** (avec libplacebo pour HDR10 → SDR)
- **ffprobe** (inclus dans ffmpeg)
- **OpenCV** (`pip install opencv-python`)
- **Dovi Tool** (optionnel, pour extraction Dolby Vision)
- **mkvmerge** (optionnel, pour remuxage optimisé)
- **HDR10+ Tool** (optionnel, pour métadonnées HDR10+)

### Installation de dépendances Python

```bash
pip install opencv-python rich numpy
```

### Configuration FFmpeg

**macOS (Homebrew)**
```bash
brew install ffmpeg
brew install mkvtoolnix  # optionnel
```

**Ubuntu/Debian**
```bash
sudo apt-get install ffmpeg libplacebo-dev
sudo apt-get install mkvtoolnix  # optionnel
```

**Windows**
- Télécharger depuis [ffmpeg.org](https://ffmpeg.org/download.html)
- Ajouter au PATH système

---

## 💻 Utilisation

### Mode interface graphique (macOS recommandé)

```bash
python3 adaptive_encoder_gui_macos.py
```

**Fonctionnalités GUI**
- Sélection fichiers source/sortie
- Onglets configurable (Vidéo | Débit | HDR | Débruitage | Audio | Système)
- Barre de progression en temps réel
- Journal d'encodage détaillé
- Pause/Reprendre/Arrêter
- Gestion de la langue (FR/EN)

### Mode ligne de commande

#### Encodage basique H.265

```bash
python3 adaptive_encoder.py input.mkv -o output.mkv
```

#### Avec préservation Dolby Vision

```bash
python3 adaptive_encoder.py input.mkv \
  --profile hevc-10 \
  --preserve-dv \
  --hdr \
  -o output.mkv
```

#### HDR10 → SDR (avec tone mapping)

```bash
python3 adaptive_encoder.py input.mkv \
  --downscale-1080p-sdr \
  --tone-mapper libplacebo \
  -o output_sdr.mkv
```

#### Avec débruitage actif

```bash
python3 adaptive_encoder.py input.mkv \
  --denoise hqdn3d \
  --denoise-strength 3 \
  -o output_clean.mkv
```

#### Encodage audio personnalisé

```bash
python3 adaptive_encoder.py input.mkv \
  --audio-lang fra \
  --audio-preset high \
  --audio-channels 6 \
  -o output.mkv
```

### Options principales

| Option | Description |
|--------|-------------|
| `-i, --input` | Fichier source (obligatoire) |
| `-o, --output` | Fichier de sortie (défaut: `<source>_adaptive.mkv`) |
| `--profile` | Profil vidéo: `hevc-10`, `hevc-12`, etc. |
| `--preserve-dv` | Conserver Dolby Vision |
| `--hdr` | Activer traitement HDR avancé |
| `--downscale-1080p-sdr` | Convertir HDR → SDR 1080p |
| `--denoise` | Moteur: `hqdn3d` ou `nlmeans` |
| `--denoise-strength` | Intensité (1-5, défaut: 2) |
| `--tone-mapper` | `libplacebo` ou `tonemap` |
| `--audio-lang` | Langue audio (fra, eng, etc.) |
| `--audio-preset` | `low`, `medium`, `high` |
| `--auto-rename` | Renommer sortie si fichier existe |
| `--license-check` | Vérifier licence avant encodage |

Pour la liste complète :
```bash
python3 adaptive_encoder.py --help
```

---

## 📊 Cas d'usage

### Production cinématographique
Préserver Dolby Vision lors de la création de masters alternatifs H.265

### Archivage numérique
Compresser le stockage sans perte de qualité HDR

### Création contenu streaming
Générer variantes SDR/HDR depuis source unique

### Nettoyage grain de film
Débruitage adaptatif avec analyse grain intelligent

---

## 🔧 Architecture

```
adaptive_encoder.py          → Moteur d'encodage principal (CLI)
adaptive_encoder_gui_macos.py → Interface graphique (macOS/Tk)
licence.py                   → Système de gestion des licences
```

### Flux d'encodage Dolby Vision

```
1. Analyse source (ffprobe)
   ↓
2. Extraction métadonnées DV (dovi_tool)
   ↓
3. Encodage H.265 (ffmpeg + libx265)
   ↓
4. Remuxage + injection métadonnées (mkvmerge/json)
   ↓
5. Fichier final préservé DV
```

### Moteurs de traitement

- **Vidéo** : libx265 (HEVC 8/10/12-bit)
- **HDR** : libplacebo (tone mapping), zscale (gamut mapping)
- **Débruitage** : hqdn3d (spatial + temporal)
- **Audio** : libfdk-aac, libopus, FLAC
- **Conteneur** : Matroska (MKV)

---

## ✅ Gestion des licences

Le logiciel inclut un système de licence optionnel (`licence.py`) pour :

- Essai gratuit 7 jours
- Licence à vie $49.99
- Validation en ligne avec fallback hors-ligne

Pour développement/test sans licence :
```bash
# Le code s'exécute même sans licence.py
python3 adaptive_encoder.py input.mkv -o output.mkv
```

---

## 🐛 Dépannage

### FFmpeg non trouvé

```bash
# Vérifier l'installation
ffmpeg -version
ffprobe -version

# Sur macOS
which ffmpeg
```

### Libplacebo indisponible (HDR→SDR échoue)

```bash
# Réinstaller ffmpeg avec support Vulkan
brew reinstall ffmpeg --with-options --enable-libplacebo
```

### Dolby Vision non préservé

Vérifier que `dovi_tool` est dans le PATH :
```bash
which dovi_tool
```

### Encodage très lent

- Réduire `--preset` (rapide → moyen → lent)
- Désactiver débruitage (`--denoise none`)
- Activer GPU si disponible

---

## 📦 Distribution

### Créer un exécutable autonome (PyInstaller)

```bash
pip install pyinstaller
pyinstaller --onefile --add-data "ressources:." adaptive_encoder.py
```

### Build macOS application

```bash
# Créer .app bundle autonome
pyinstaller --windowed --onefile adaptive_encoder_gui_macos.py
```

---

## 📝 Licences des dépendances

| Dépendance | Licence |
|-----------|---------|
| FFmpeg | LGPL-2.1+ |
| libx265 | GPL-2.0 |
| OpenCV | Apache 2.0 |
| Rich | MIT |
| Dovi Tool | LGPL-2.1+ |
| mkvtoolnix | GPL-2.0 |

**Note** : Adaptive Encoder lui-même est sous **licence commerciale** avec essai gratuit.

---

## 🤝 Contribution

Les contributions sont bienvenues ! Avant de soumettre un PR :

1. Forker le projet
2. Créer une branche feature (`git checkout -b feature/amazing-feature`)
3. Committer les changements (`git commit -m 'Add amazing feature'`)
4. Pousser vers la branche (`git push origin feature/amazing-feature`)
5. Ouvrir une Pull Request

---

## 📧 Support & Contact

- **Site officiel** : https://adaptiveencoder.com
- **Email** : support@adaptiveencoder.com
- **Issues** : [GitHub Issues](../../issues)
- **Documentation** : [Voir index.html](./index.html)

---

## 📄 Licence

```
Copyright © 2024 Adaptive Encoder
Tous droits réservés.

Essai gratuit 7 jours
Licence à vie : $49.99

Voir LICENSE pour les termes complets.
```

---

## 🙏 Remerciements

- **FFmpeg** & **libx265** pour l'infrastructure d'encodage
- **Dolby Laboratories** pour les spécifications Dolby Vision
- **MkvToolNix** pour le remuxage Matroska
- La communauté vidéo open-source

---

<div align="center">

**[🌐 Site Web](https://adaptiveencoder.com)** • 
**[📖 Documentation](./index.html)** • 
**[🐛 Signaler un bug](../../issues)** • 
**[💬 Discussions](../../discussions)**

Encodez votre contenu vidéo avec intelligence. 🎬✨

</div>
