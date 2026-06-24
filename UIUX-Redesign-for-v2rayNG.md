# UI/UX Redesign Guide for v2rayNG → GalaxyVPN Rebrand

> Complete guide for rebranding v2rayNG to GalaxyVPN including app name, icon, and new strings.

---

## 1. AndroidManifest.xml — App Name

**Path:** `V2rayNG/app/src/main/AndroidManifest.xml`

The `application` tag uses `android:label="@string/app_name"`. Update the referenced string in `strings.xml`.

---

## 2. strings.xml — App Name + New Strings

**Path:** `V2rayNG/app/src/main/res/values/strings.xml`

Update or add the following strings:

```xml
<!-- App Name -->
<string name="app_name">GalaxyVPN</string>

<!-- GalaxyVPN New Strings -->
<string name="download">Download</string>
<string name="upload">Upload</string>
<string name="current_server">Current Server</string>
<string name="server_icon">Server</string>
<string name="expand">Select Server</string>
<string name="connected">Connected</string>
<string name="connecting">Connecting…</string>
<string name="disconnected">Disconnected</string>
```

---

## 3. App Icons — mipmap Folders

**Path:** `V2rayNG/app/src/main/res/`

### Density Folders

| Folder | Size |
|--------|------|
| `mipmap-hdpi/` | 72x72 |
| `mipmap-mdpi/` | 48x48 |
| `mipmap-xhdpi/` | 96x96 |
| `mipmap-xxhdpi/` | 144x144 |
| `mipmap-xxxhdpi/` | 192x192 |
| `mipmap-anydpi-v26/` | Adaptive icon (API 26+) |

### Files Required

- `ic_launcher.png` (or `.webp`)
- `ic_launcher_round.png` (or `.webp`)
- `ic_launcher_foreground.png` (adaptive icon)
- `ic_launcher_background.png` (adaptive icon)

---

## Icon Options

### Option A: GalaxyVPN Logo (Vector) → PNG Convert

Convert `ic_galaxy_logo.xml` to PNG:

1. Right-click on `ic_galaxy_logo.xml` in Android Studio
2. Use **Asset Studio** → **Export to PNG**

Or use an online converter: [convertio.co/xml-png](https://convertio.co/xml-png)

### Option B: Simple Galaxy Icon (PNG Sizes)

| Density | File | Size |
|---------|------|------|
| xxxhdpi | `mipmap-xxxhdpi/ic_launcher.png` | 192x192 |
| xxhdpi | `mipmap-xxhdpi/ic_launcher.png` | 144x144 |
| xhdpi | `mipmap-xhdpi/ic_launcher.png` | 96x96 |
| hdpi | `mipmap-hdpi/ic_launcher.png` | 72x72 |
| mdpi | `mipmap-mdpi/ic_launcher.png` | 48x48 |

### Option C: Adaptive Icon (API 26+)

**`mipmap-anydpi-v26/ic_launcher.xml`**

```xml
<?xml version="1.0" encoding="utf-8"?>
<adaptive-icon xmlns:android="http://schemas.android.com/apk/res/android">
    <background android:drawable="@drawable/ic_launcher_background" />
    <foreground android:drawable="@drawable/ic_launcher_foreground" />
</adaptive-icon>
```

**`drawable/ic_launcher_background.xml`**

```xml
<?xml version="1.0" encoding="utf-8"?>
<shape xmlns:android="http://schemas.android.com/apk/res/android"
    android:shape="rectangle">
    <gradient
        android:type="linear"
        android:angle="135"
        android:startColor="#FF6B4EFF"
        android:endColor="#FF00D4AA" />
</shape>
```

**`drawable/ic_launcher_foreground.xml`**

```xml
<?xml version="1.0" encoding="utf-8"?>
<vector xmlns:android="http://schemas.android.com/apk/res/android"
    android:width="108dp"
    android:height="108dp"
    android:viewportWidth="108"
    android:viewportHeight="108">
    <path
        android:fillColor="#FFFFFF"
        android:pathData="M54,30 C68,30 78,40 78,54 C78,68 68,82 54,86 C40,82 30,68 30,54 C30,40 40,30 54,30 Z" />
    <path
        android:fillColor="#FF6B4EFF"
        android:pathData="M54,38 C62,38 70,44 70,54 C70,64 62,74 54,76 C46,74 38,64 38,54 C38,44 46,38 54,38 Z" />
</vector>
```

---

## Complete Checklist

| # | Task | File/Folder | Action |
|---|------|-------------|--------|
| 1 | App Name | `res/values/strings.xml` | `app_name` → "GalaxyVPN" |
| 2 | New Strings | `res/values/strings.xml` | Add download/upload/etc |
| 3 | Launcher Icon | `mipmap-xxxhdpi/ic_launcher.png` | Replace (192x192) |
| 4 | Launcher Icon | `mipmap-xxhdpi/ic_launcher.png` | Replace (144x144) |
| 5 | Launcher Icon | `mipmap-xhdpi/ic_launcher.png` | Replace (96x96) |
| 6 | Launcher Icon | `mipmap-hdpi/ic_launcher.png` | Replace (72x72) |
| 7 | Launcher Icon | `mipmap-mdpi/ic_launcher.png` | Replace (48x48) |
| 8 | Round Icon | `mipmap-*/ic_launcher_round.png` | Replace (same sizes) |
| 9 | Adaptive Icon | `mipmap-anydpi-v26/ic_launcher.xml` | New (optional) |
| 10 | Adaptive BG | `drawable/ic_launcher_background.xml` | New (optional) |
| 11 | Adaptive FG | `drawable/ic_launcher_foreground.xml` | New (optional) |

---

## Quick Setup

### App Name Only (icon not changed)

```bash
# Edit strings.xml → app_name = "GalaxyVPN"
git add .
git commit -m "GalaxyVPN rebrand - app name"
git push
```

### App Name + Icon (PNG icons ready)

```bash
# Copy icon files
cp ~/Downloads/galaxyvpn-icon-192.png app/src/main/res/mipmap-xxxhdpi/ic_launcher.png
cp ~/Downloads/galaxyvpn-icon-144.png app/src/main/res/mipmap-xxhdpi/ic_launcher.png
# ... etc for other densities

git add .
git commit -m "GalaxyVPN rebrand - app name and icon"
git push
```

---

## Icon Generator Tools

| Tool | URL | Use |
|------|-----|-----|
| Android Asset Studio | [romannurik.github.io/AndroidAssetStudio](https://romannurik.github.io/AndroidAssetStudio) | Auto generate all sizes |
| Icon Kitchen | [icon.kitchen](https://icon.kitchen) | Adaptive icons |
| Figma | [figma.com](https://figma.com) | Custom design |

**Android Asset Studio Usage:**
1. Upload GalaxyVPN logo
2. Set background color (gradient `#6B4EFF` → `#00D4AA`)
3. Download ZIP
4. Replace in `res/mipmap-*` folders

---

## Summary

| What | When | How |
|------|------|-----|
| App Name | **Now** | Edit `strings.xml` → `app_name` |
| Icon | **Now** | Replace PNGs in `mipmap-*` folders |
| Adaptive Icon | **Optional** | Add `mipmap-anydpi-v26/` + `drawable/` |

GitHub Actions build will use these changes to generate the APK!
