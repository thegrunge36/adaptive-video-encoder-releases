# 🎬 Adaptive Video Encoder

### L'encodeur H.265 qui ne casse pas votre *Dolby Vision*.

[![Windows](https://img.shields.io/badge/Windows-10%2F11%20x64-0078D6?logo=windows&logoColor=white)](https://github.com/thegrunge36/adaptive-video-encoder-releases/releases)
[![Linux](https://img.shields.io/badge/Linux-x64-FCC624?logo=linux&logoColor=black)](https://github.com/thegrunge36/adaptive-video-encoder-releases/releases)
[![macOS](https://img.shields.io/badge/macOS-Apple%20Silicon-000?logo=apple&logoColor=white)](https://github.com/thegrunge36/adaptive-video-encoder-releases/releases)
[![Trial](https://img.shields.io/badge/Essai-7%20jours%20gratuit-22c55e)](https://adaptive-video-encoder.lemonsqueezy.com)
[![License](https://img.shields.io/badge/Licence%20à%20vie-%2449.99-3b82f6)](https://adaptive-video-encoder.lemonsqueezy.com)
[![Discord](https://img.shields.io/badge/Discord-rejoindre-5865F2?logo=discord&logoColor=white)](https://discord.gg/UHrEn2H6jD)

Analyse adaptative **image par image**. Dolby Vision Profil **5, 7, 8.x** — HDR10 — HLG — grain cinématique. Tout préservé, sans compromis. Conçu pour les **remux Blu-ray 1080p** et les **rips UHD 4K**. Binaires natifs pour Windows, Linux et macOS (Apple Silicon).

> **🌐 Site officiel : [adaptive-encoder.com](https://adaptive-encoder.com/)**

<div align="center">

**[⬇ Essai gratuit 7 jours](https://adaptive-video-encoder.lemonsqueezy.com)** ·
**[Acheter — $49.99](https://adaptive-video-encoder.lemonsqueezy.com)** ·
**[💬 Discord](https://discord.gg/UHrEn2H6jD)**

</div>

---

## Le problème

Réencoder une vidéothèque en H.265 sans détruire les métadonnées, le grain et la dynamique : c'est exactement là où les outils grand public échouent.

- **Les encodeurs génériques cassent le Dolby Vision** — La plupart suppriment ou convertissent mal le Profil 7 (FEL/MEL). Ce qui était superbe sur votre OLED devient du SDR plat — ou du HDR cassé.
- **ffmpeg manuel : des heures de tests** — Trouver les bons paramètres x265 prend 1 à 3 heures par film, et ils changent à chaque source.
- **Presets fixes vs contenu variable** — Un preset universel donne des résultats médiocres partout. Un film granuleux et une animation lisse n'ont pas les mêmes besoins.

---

## Pour qui c'est fait (et pour qui ça ne l'est pas)

Soyons honnêtes d'entrée : Adaptive Encoder privilégie une **qualité proche du remux** plutôt qu'une compression maximale — c'est un choix de conception assumé.

**✓ Excellent pour :**
- Les **remux Blu-ray 1080p** avec grain — classiques, films d'horreur, films d'auteur 35 mm
- Les **rips UHD 4K** avec Dolby Vision, HDR10, HLG
- Les **bibliothèques mixtes** que vous ne voulez pas calibrer film par film
- **L'archivage long terme** — encodez une fois, regardez 100 fois

**⚖ Qualité avant taille brute.** Sur du contenu déjà propre et sans grain, les gains d'espace sont plus modestes — un compromis délibéré pour ne jamais sacrifier la fidélité d'image. Pour l'archivage, 8 Go proches du remux valent mieux que 5 Go « acceptables » : le stockage devient moins cher chaque année, la qualité d'image, elle, est définitive.

---

## ✨ Fonctionnalités

| # | Fonctionnalité | Description |
|---|----------------|-------------|
| 01 | **Analyse adaptative** | Détecte le bruit, le grain, la complexité et la densité des contours pour régler automatiquement les paramètres x265 par source |
| 02 | **Dolby Vision 5, 7, 8.x** | Métadonnées extraites avec `dovi_tool`, préservées et réinjectées sans perte |
| 03 | **HDR10 et HLG** | Primaires de couleur, transferts, master display, MaxCLL et MaxFALL intégralement conservés |
| 04 | **Recadrage intelligent** | Détection automatique des barres noires sans risquer de couper le contenu réel |
| 05 | **Audio et sous-titres** | Toutes les pistes copiées par défaut. TrueHD Atmos, DTS-HD MA, sous-titres PGS — zéro perte |
| 06 | **Tous formats, 480p à 8K** | MKV, MP4, MOV, AVI, MXF, WebM, M4V, TS. Binaire unique, aucune dépendance Python |

### En détail

**🎞️ HDR & Dolby Vision**
- Préservation complète du Dolby Vision Profil 5, 7, 8.x
- Conversion automatique Profil 7 → 8.1
- HDR10 et HLG intégralement préservés
- Primaires, transferts, master display, MaxCLL & MaxFALL transmis

**🔬 Analyse & qualité**
- Analyse image par image — paramètres x265 optimaux par vidéo
- Préservation du grain de film (35 mm, films d'horreur, classiques)
- Détection automatique des barres noires — sans couper le contenu
- Encodage 10-bit, preset adaptatif de *fast* à *veryslow*

**🎬 Compatibilité**
- Toutes les pistes audio et sous-titres copiées (TrueHD Atmos, DTS-HD MA, PGS)
- Formats : MKV, MP4, MOV, AVI, MXF, WebM, M4V, TS
- Résolutions de 480p à 8K
- Application autonome — ffmpeg, ffprobe & dovi_tool intégrés. Aucune dépendance, aucune installation

---

## 📊 Comparaison

| | Encodeurs génériques | ffmpeg manuel | **Adaptive Video Encoder** |
|---|:---:|:---:|:---:|
| **Dolby Vision Profil 7** | ✗ Cassé | ~ Avec scripts | **✓ Automatique** |
| **Préservation du grain** | ✗ Lissé | ~ Si vous savez quoi activer | **✓ Automatique** |
| **Réglages adaptés par vidéo** | ✗ Presets fixes | ~ Si vous testez vous-même | **✓ Image par image** |
| **HDR10 / HLG préservés** | ~ Parfois | ~ Si bien marqués | **✓ Toujours** |
| **Détection des barres noires** | ✓ | ~ Manuel | **✓ Automatique** |
| **Temps de configuration** | 5 min | 1–3 h par film | **0 min** |

---

## Pourquoi pas NVENC ?

NVENC, QuickSync et AMF sont conçus pour la **vitesse**, pas la qualité. Parfaits pour streamer sur Twitch — médiocres pour archiver une bibliothèque que vous regarderez sur OLED pendant 10 ans.

- **À débit égal**, x265 (preset *slower* ou *veryslow*) produit des fichiers visuellement meilleurs que NVENC HEVC — surtout sur le grain, les scènes sombres et les mouvements complexes.
- **À qualité égale**, x265 produit des fichiers nettement **plus petits**. Chaque gigaoctet économisé l'est pour toujours.
- NVENC est **figé dans le silicium** ; x265 reçoit des optimisations psychovisuelles depuis plus de 10 ans.

Pour archiver, la vitesse n'a pas d'importance : on encode une fois, on regarde 100 fois.

---

## 💻 Plateformes supportées

Toutes les versions sont des **applications graphiques autonomes** — ffmpeg, ffprobe et dovi_tool sont intégrés dans l'exécutable. **Aucune dépendance, aucune installation.**

| Plateforme | Détails |
|------------|---------|
| 🪟 **Windows 10 / 11 (x64)** | Exécutable `.exe` natif. Double-cliquez pour lancer. Fonctionne aussi sous Windows Server |
| 🐧 **Linux (x64)** | Binaire natif. Testé sur Ubuntu 22.04+, Debian 12+, Fedora 40+. Lancement depuis le gestionnaire de fichiers ou le menu |
| 🍎 **macOS (Apple Silicon)** | Application native arm64 (M1/M2/M3). Lancement depuis le Finder ou le Launchpad |

> Les Mac Intel et les variantes Linux ARM ne sont pas pris en charge pour le moment.

---

## ⬇ Téléchargement & installation

1. Rendez-vous sur les **[releases GitHub](https://github.com/thegrunge36/adaptive-video-encoder-releases/releases)** — aucun paiement ni licence requis pour télécharger
2. Choisissez votre binaire : **Windows (.exe)**, **Linux** ou **macOS**
3. **Double-cliquez pour lancer** — tout est autonome, rien à installer

---

## 🔑 Licence

**Essai gratuit. Puis décidez.**

- **Essai gratuit de 7 jours** — testez sur vos propres fichiers, *aucune carte de crédit requise*
- **Licence à vie : $49.99** — pour un seul ordinateur
- **Transfert gratuit** si vous changez de machine

> Vous changez d'ordinateur ? Écrivez à **osx300@gmail.com** ou contactez-nous sur Discord — le transfert est gratuit et rapide.

**[🕐 Commencer l'essai gratuit](https://adaptive-video-encoder.lemonsqueezy.com)**

---

## ❓ FAQ

**Est-ce uniquement pour la 4K ?**
Non, l'outil est aussi excellent en 1080p — surtout sur les remux Blu-ray avec grain (classiques, horreur, films d'auteur 35 mm) ou les scènes complexes. La plupart des encodeurs lissent le grain par défaut ; Adaptive Encoder le détecte et le préserve automatiquement, quelle que soit la résolution.

**Pourquoi mes fichiers sont-ils plus gros qu'avec d'autres encodeurs ?**
C'est un choix délibéré. L'outil est calibré pour préserver au maximum le détail, le grain et les métadonnées HDR — même quand l'algorithme pourrait compresser davantage. Pour archiver, 8 Go proches du remux valent mieux que 5 Go « acceptables ». Vous pouvez toujours fixer un débit maximum dans les options d'encodage.

**La conversion Profil 7 → 8.1 fonctionne-t-elle vraiment ?**
Oui, c'est la conversion par défaut. Le Profil 7 (FEL/MEL) est extrait avec `dovi_tool` et réinjecté en 8.1 dans le fichier de sortie. Compatible avec la plupart des lecteurs Dolby Vision modernes (téléviseurs, box, lecteurs récents).

**L'encodage est-il lent ?**
Oui — volontairement. L'outil utilise par défaut les presets x265 *slower* ou *veryslow* pour maximiser la qualité. Ce n'est pas un encodeur *rapide*, c'est un *bon* encodeur. Si vous voulez de la vitesse, NVENC est gratuit — mais ce n'est pas le même produit.

**Une licence par machine, c'est restrictif ?**
Si vous changez d'ordinateur, écrivez à osx300@gmail.com ou contactez-nous sur Discord : le transfert est gratuit et rapide.

**Et si ça ne marche pas sur mes fichiers ?**
C'est exactement à ça que sert l'essai gratuit. Demandez votre clé d'essai sur Discord ou par e-mail avant d'acheter, testez sur vos propres fichiers, et décidez ensuite.

---

## 🔗 Liens

- **🌐 Site web** — [adaptive-encoder.com](https://adaptive-encoder.com/)
- **⬇ Téléchargements** — [Releases GitHub](https://github.com/thegrunge36/adaptive-video-encoder-releases/releases)
- **💬 Discord** — [rejoindre la communauté](https://discord.gg/UHrEn2H6jD)
- **🛒 Acheter / essai** — [LemonSqueezy](https://adaptive-video-encoder.lemonsqueezy.com)
- **✉ Email** — osx300@gmail.com

---

<div align="center">

**Réencodez votre bibliothèque. Sans compromis.**

7 jours d'essai gratuit · Licence à vie $49.99 · Windows · Linux · macOS

© 2026 Adaptive Video Encoder

</div>
