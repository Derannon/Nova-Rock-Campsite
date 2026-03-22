# 🏕️ Festival Camp Website

Eine vollständige Festival-Website für GitHub Pages – mit Bier-Tracker, Statistiken, Slideshow und Minispielen.

## 🚀 Schnellstart

### 1. Konfiguration (`index.html`)

Öffne die `index.html` und passe den oberen **KONFIGURATION**-Abschnitt an:

| Variable | Beschreibung |
|---|---|
| `CAMP_NAME` | Name deines Camps |
| `FESTIVAL_LABEL` | Beschriftung (z.B. "Rocken am Brocken 2025") |
| `LAT` / `LNG` | GPS-Koordinaten des Camps |
| `CAMP_IMAGE_URL` | Pfad/URL zum Camp-Foto (z.B. `"fotos/camp.jpg"`) |
| `MAP_IMAGE_URL` | Optional: Geländekarte |
| `SPOTIFY_PLAYLIST_ID` | ID aus der Playlist-URL |
| `FESTIVAL_DAYS` | Tage im Format `YYYY-MM-DD` |
| `MEMBERS` | Campmitglieder (Name, Rolle, Bio, Emoji, Foto) |
| `TASKS` | Aufgaben für den Task-Roller |
| `COOLDOWN_SEC` | Wartezeit zwischen zwei Bier-Klicks (Standard: 30s) |

### 2. Fotos hinzufügen

Erstelle einen Ordner `fotos/` und lege die Bilder dort ab:
```
fotos/
  camp.jpg
  max.jpg
  lisa.jpg
  ...
```

### 3. Firebase einrichten (für globale Zähler)

Ohne Firebase funktioniert der Tracker nur lokal auf jedem Gerät.
Für **gemeinsame Zähler** (alle zählen zusammen):

1. Gehe zu [console.firebase.google.com](https://console.firebase.google.com)
2. Neues Projekt erstellen
3. **Build → Realtime Database** → Testmodus starten
4. **Projekteinstellungen ⚙️** → Deine Apps → Web-App hinzufügen
5. Kopiere das `firebaseConfig`-Objekt in die `index.html`

> **Tipp:** Die Datenbank-Regeln auf Testmodus lassen (öffentlich lesen/schreiben).
> Nach dem Festival einfach das Projekt löschen oder die Regeln sperren.

### 4. Auf GitHub Pages deployen

```bash
# Repository erstellen und pushen
git init
git add .
git commit -m "Festival Website 🏕️"
git remote add origin https://github.com/DEIN_USER/REPO_NAME.git
git push -u origin main
```

Dann im GitHub Repo: **Settings → Pages → Source: main branch / root**

Die Seite ist dann erreichbar unter:
`https://DEIN_USER.github.io/REPO_NAME/`

### 5. QR-Code erstellen

Gehe zu [qr-code-generator.com](https://www.qr-code-generator.com) oder [goqr.me](https://goqr.me), füge die GitHub Pages URL ein und generiere den QR-Code.

---

## 📁 Dateistruktur

```
/
├── index.html          ← Die gesamte Website
├── fotos/              ← Bilder (Camp, Mitglieder)
│   ├── camp.jpg
│   └── ...
└── README.md
```

## ✨ Features

- 🏕️ **Camp-Seite** – Bild, Koordinaten, Google Maps Link, Slideshow
- 🎵 **Spotify** – Eingebetteter Playlist-Player
- 🍺 **Bier-Tracker** – +1 Bier Button mit 30s Cooldown, persönlicher & globaler Counter
- 📊 **Statistiken** – Balkendiagramm pro Tag, Stundendiagramm, Tabellen
- 👥 **Besucher-Counter** – Zählt einmalige Besucher (mit Firebase)
- 🪙 **Münzwurf** – Animierter 3D-Münzwurf
- 🎲 **Zufalls-Aufgabe** – Zufälliger Task-Roller mit History
- ⭐ **Sternenhimmel** – Animierter Hintergrund

## 🔧 Anpassungen

### Mehr Mitglieder
Ergänze weitere Objekte im `MEMBERS`-Array.

### Mehr Aufgaben
Ergänze weitere Strings im `TASKS`-Array.

### Andere Farben
Passe die CSS-Variablen in `:root` an (am Anfang des `<style>`-Blocks).

---

Viel Spaß auf dem Festival! 🎉🍺
