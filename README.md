# Nova Rock Camp Website

Überarbeitete Single-Page-Website für GitHub Pages mit Camp-Infos, Biertracker, Firebase-Realtime-Stats, Gästebuch, Bingo, Minispielen und Zehntausend.

## Was verbessert wurde

- Keine Fake-Koordinaten mehr: Wenn `lat`/`lng` fehlen, zeigt die Seite sauber "wird ergänzt".
- Firebase ist optional und bricht die Seite nicht mehr, wenn die Config fehlt.
- Firebase nutzt Anonymous Auth und validierte Realtime-Database-Rules statt offenem Testmodus.
- Gästebuch-Einträge werden sicher per `textContent` gerendert und zusätzlich per Rules auf Länge/Struktur geprüft.
- Globale Bier- und Besucher-Zähler werden atomar mit Firebase-Increments geschrieben.
- Spotify-ID wird bereinigt, damit ein versehentliches `?` am Ende nicht mehr stört.
- Zitate bleiben lokal, können aber nur nach Eingabe des konfigurierten Camp-Passworts hinzugefügt werden (`quotePassword`, Standard: `NR26`).
- Kings Cup nutzt wieder eine echte Karten-Optik mit 52er-Deck, Regelanzeige, Verlauf und König-Zähler.
- Zehntausend wurde wieder als richtiges Würfelspiel umgesetzt: Würfeln, wertende Würfel auswählen, behalten, weiterwürfeln oder kassieren, inklusive 350-Punkte-Einstieg, Hot-Dice/Bestätigungswurf und Finalrunde.
- GitHub Actions prüft die HTML-/JavaScript-Syntax vor dem Deploy.

## Dateien

```text
/
├── index.html
├── firebase-rules.json
├── firebase.json
├── .nojekyll
├── scripts/
│   └── validate-html.mjs
├── .github/
│   └── workflows/
│       └── validate.yml
└── fotos/
    ├── camp.jpg
    ├── Standort.png
    ├── Andreas.jpg
    ├── Michael.jpg
    ├── Sophie.jpg
    └── Thomas.jpg
```

## Konfiguration

Öffne `index.html` und passe oben `window.NOVA_ROCK_CONFIG` an.

Wichtige Felder:

| Feld | Bedeutung |
|---|---|
| `campName` | Name des Camps |
| `festivalLabel` | Anzeige im Header |
| `festivalDays` | Tage im Format `YYYY-MM-DD` |
| `campImageUrl` | z. B. `fotos/camp.jpg` |
| `mapImageUrl` | z. B. `fotos/Standort.png` |
| `coordinates.lat/lng` | Exakte Camp-Koordinaten, optional |
| `spotifyPlaylistId` | Nur die Spotify-Playlist-ID, ohne `?` |
| `quotePassword` | Passwort zum Hinzufügen lokaler Camp-Zitate, Standard: `NR26` |
| `members` | Crew-Daten und Bildpfade |
| `firebase.config` | Firebase-Web-App-Config |

## Firebase richtig einrichten

1. In Firebase ein Projekt erstellen.
2. Realtime Database erstellen.
3. Nicht dauerhaft im Testmodus lassen.
4. Authentication → Sign-in method → Anonymous aktivieren.
5. In den Projekteinstellungen eine Web-App anlegen.
6. Die Firebase-Web-App-Config in `index.html` eintragen.
7. `firebase-rules.json` in Realtime Database → Rules einfügen und veröffentlichen.

Die Config ist kein klassisches Passwort. Die Sicherheit kommt aus Auth, Rules und optional App Check. Für ein öffentliches Festival-Projekt ist App Check zusätzlich empfehlenswert, wenn du Missbrauch weiter reduzieren willst.

## Lokal prüfen

```bash
node scripts/validate-html.mjs
```

## GitHub Pages

Die Seite ist statisch und läuft direkt auf GitHub Pages. Kopiere die Dateien ins Repo-Root, committe und pushe. Danach kann GitHub Pages aus dem Branch oder über einen Actions-Workflow veröffentlichen.

## Bekannte Grenzen

Eine komplett öffentliche Client-Seite kann Spam nie so gut verhindern wie ein Backend mit Rate-Limits. Die Rules verhindern falsche Datentypen, zu lange Texte, unautorisierte User-Pfade und direkte Manipulation vieler Felder. Für harte Anti-Spam-Regeln wären Firebase App Check oder Cloud Functions sinnvoll.

## Hinweise zu Zitate-Passwort und Zehntausend

Das Zitate-Passwort steht in `index.html` als `quotePassword: "NR26"`. Das ist bei einer statischen GitHub-Pages-Seite nur eine einfache Camp-Hürde, weil der Quellcode öffentlich lesbar ist. Für echte Admin-Rechte bräuchte man Firebase Auth plus serverseitige Rules.

Zehntausend nutzt diese Regeln:

- 1er = 100 Punkte, 5er = 50 Punkte
- Drilling = Zahl × 100, 1er-Drilling = 1000
- Vierling/Fünfling/Sechsling verdoppeln jeweils den Drillingwert
- Straße 1-6 = 3000 Punkte
- drei Paare = 1000 Punkte
- mindestens 350 Punkte zum Einsteigen
- wenn alle aktiven Würfel gewertet wurden, folgt ein Pflicht-Bestätigungswurf
- bei Niete gehen alle Punkte des laufenden Zugs verloren
- nach Erreichen von 10.000 bekommen alle anderen noch einen letzten Zug

