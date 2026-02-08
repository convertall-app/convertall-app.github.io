# ConvertAll — Convertisseur de Fichiers Gratuit

**ConvertAll** est une application web tout-en-un de conversion de fichiers, 100% gratuite et respectueuse de la vie privée. Tous les fichiers sont traités **directement dans le navigateur** — rien n'est envoyé sur un serveur.

---

## Démo rapide

Ouvrez simplement `index.html` dans votre navigateur (Chrome recommandé).

---

## Fonctionnalités

### Images (onglet 🖼️ Images)

| Outil | Description |
|-------|-------------|
| **Convertir** | Convertir entre PNG, JPG, WebP avec contrôle de qualité |
| **Redimensionner** | Changer la taille avec presets (Instagram, YouTube, Twitter, Facebook, HD, 4K, iPhone, Favicon, Avatar) |
| **Compresser** | Réduire le poids d'une image en ajustant la qualité |
| **Recadrer** | Sélectionner visuellement une zone à recadrer (souris + tactile) |
| **Pivoter** | Rotation 90°/180°/270° + miroir horizontal/vertical |
| **Favicon** | Générer un pack ZIP avec toutes les tailles de favicon (16x16 → 512x512) + fichier `usage.html` avec le code à coller |

### Documents (onglet 📄 Documents)

| Outil | Description |
|-------|-------------|
| **Images → PDF** | Combiner plusieurs images en un seul PDF |
| **Fusionner PDFs** | Fusionner plusieurs fichiers PDF en un seul |
| **Extraire pages** | Extraire des pages spécifiques d'un PDF (ex: `1-3, 5, 8`) |
| **Compresser PDF** | Réduire le poids d'un PDF en supprimant les métadonnées |

### Vidéo / Audio (onglet 🎬 Vidéo/Audio)

| Format d'entrée | Formats de sortie |
|-----------------|-------------------|
| MP4, WebM, AVI, MKV, MOV | MP4, WebM, GIF animé |
| MP3, WAV, OGG, AAC, FLAC | MP3, WAV, OGG |

> **Note :** La conversion vidéo/audio utilise FFmpeg.wasm. Elle nécessite un hébergement sur un serveur web avec les headers `Cross-Origin-Opener-Policy` et `Cross-Origin-Embedder-Policy` pour fonctionner (SharedArrayBuffer). En local (file://), un message d'erreur s'affichera.

### Outils (onglet 🔧 Outils)

| Outil | Description |
|-------|-------------|
| **QR Code** | Générateur de QR Codes personnalisés (taille, couleur, fond) |
| **Pipette** | Extraire les couleurs d'une image (HEX, RGB, HSL) + palette automatique |
| **Base64** | Convertir image → Base64 ou Base64 → image |
| **Suppr. fond** | Supprimer le fond d'une image (blanc, noir, vert, auto) avec tolérance réglable |
| **Suppr. EXIF** | Supprimer les métadonnées EXIF d'une image |
| **Texte → Image** | Convertir du texte en image PNG avec police, couleur et fond personnalisables |
| **ASCII Art** | Convertir une image en art ASCII (copie + téléchargement .txt) |

---

## Fonctionnalités générales

### Interface
- **Thème sombre / clair** — Toggle avec le bouton ☀️/🌙 (sauvegardé)
- **Bilingue FR / EN** — Bouton `FR`/`EN` dans le header (sauvegardé)
- **Responsive** — Adapté mobile et desktop
- **Design glassmorphism** — Effets de flou, transparences, animations

### Gestion des fichiers
- **Drag & drop** — Glisser-déposer des fichiers sur la zone
- **Ctrl+V** — Coller une image depuis le presse-papier
- **Drag-to-reorder** — Réorganiser l'ordre des fichiers avec la poignée ⠿
- **Conversion en lot** — Plusieurs fichiers à la fois → téléchargement individuel ou ZIP
- **Renommage en lot** — Modèle personnalisable avec `{name}`, `{index}`, `{ext}`

### Après conversion
- **Aperçu avant/après** — Comparaison visuelle côte à côte
- **Statistiques** — Taille d'entrée, de sortie, et pourcentage de réduction
- **Animation confettis** — Célébration visuelle après chaque conversion réussie
- **Historique** — Liste des conversions passées (bouton 📋, sauvegardé en localStorage)

### Monétisation
- **2 espaces publicitaires** — En haut et en bas de la zone principale (remplacer par votre code AdSense)
- **Interstitial publicitaire** — Pop-up avec compte à rebours de 5 secondes, affiché toutes les 2 conversions
- **Cookie banner RGPD** — Bannière de consentement aux cookies (obligatoire pour AdSense en Europe)

---

## Technologies utilisées

| Technologie | Usage |
|-------------|-------|
| **HTML / CSS / JS** | Application mono-fichier, aucun build nécessaire |
| **Canvas API** | Conversion, redimensionnement, compression, rotation, recadrage d'images |
| **[pdf-lib](https://pdf-lib.js.org/)** | Création, fusion, extraction et compression de PDF côté client |
| **[FFmpeg.wasm](https://ffmpegwasm.netlify.app/)** | Conversion vidéo et audio côté client |
| **[QRCode.js](https://github.com/soldair/node-qrcode)** | Génération de QR Codes |
| **[JSZip](https://stuk.github.io/jszip/)** | Téléchargement en lot au format ZIP |

Toutes les librairies sont chargées via CDN (unpkg).

---

## Installation

### En local (basique)
```
Ouvrir index.html dans Chrome / Edge / Firefox
```
> Les conversions d'images, PDF, QR codes, et tous les outils fonctionnent en local. Seule la conversion vidéo/audio nécessite un serveur.

### Sur un serveur web (complet)
```bash
# Avec Python
python -m http.server 8080

# Avec Node.js
npx serve .

# Avec PHP
php -S localhost:8080
```

Pour que FFmpeg.wasm fonctionne, ajoutez ces headers HTTP :
```
Cross-Origin-Opener-Policy: same-origin
Cross-Origin-Embedder-Policy: require-corp
```

---

## Intégrer AdSense

1. Remplacez le contenu des `<div class="ad-space">` (id `adTop` et `adBottom`) par votre code AdSense
2. Remplacez le contenu de `<div class="interstitial-ad-box">` par votre code publicitaire
3. L'interstitial s'affiche automatiquement toutes les 2 conversions

---

## Structure du fichier

```
index.html (fichier unique ~2050 lignes)
├── <head>
│   ├── Métadonnées SEO
│   ├── CDN : pdf-lib, JSZip, QRCode.js
│   └── <style> CSS complet (~330 lignes)
│       ├── Variables CSS (thème clair/sombre)
│       ├── Layout (header, tabs, main, footer)
│       ├── Composants (drop zone, fichiers, options, résultats)
│       ├── Outils (QR, couleur, crop, base64, txt2img, ascii)
│       ├── Overlays (cookie banner, interstitial, confetti, toast)
│       └── Responsive (mobile)
├── <body>
│   ├── Header (logo, langue, historique, thème)
│   ├── Tabs (Images, Documents, Vidéo/Audio, Outils, À propos)
│   ├── Main
│   │   ├── Espace pub haut
│   │   ├── Sous-outils (sub-tools)
│   │   ├── Zone de drop
│   │   ├── Liste des fichiers (drag-to-reorder)
│   │   ├── Panneau d'options (format, qualité, resize, rotation, presets)
│   │   ├── Sections spéciales (QR, Base64, Txt2Img, ASCII, Pipette, Crop)
│   │   ├── Aperçu, stats, progression, résultats
│   │   ├── Espace pub bas
│   │   ├── Historique
│   │   └── À propos
│   ├── Cookie banner RGPD
│   ├── Interstitial pub
│   └── <script> JavaScript complet (~1100 lignes)
│       ├── Traductions FR/EN
│       ├── État global
│       ├── Thème
│       ├── Tabs & sous-outils
│       ├── Drag & drop fichiers
│       ├── Gestion des fichiers (ajout, suppression, reorder)
│       ├── Conversion (images, documents, media, outils)
│       ├── Outils individuels (crop, QR, couleur, base64, favicon, txt2img, ascii)
│       ├── Aperçu, stats, résultats, historique
│       ├── Cookie banner, Ctrl+V, confetti, interstitial
│       └── Initialisation
└── </html>
```

---

## Raccourcis

| Raccourci | Action |
|-----------|--------|
| **Ctrl+V** | Coller une image depuis le presse-papier |
| **Glisser-déposer** | Ajouter des fichiers |
| **Clic sur code couleur** | Copier la valeur (HEX/RGB/HSL) |

---

## Navigateurs supportés

| Navigateur | Support |
|------------|---------|
| Chrome 90+ | Complet |
| Edge 90+ | Complet |
| Firefox 90+ | Complet (sauf FFmpeg.wasm) |
| Safari 15+ | Partiel (pas de FFmpeg.wasm) |

---

## Licence

Projet libre — utilisez, modifiez et distribuez comme vous le souhaitez.
