# Abfahrtsanzeige Bern

A private, single-page replica of a "Tramli"-style departure display for stops in Bern, styled like the
Bernmobil stop signs (amber dot-matrix rows, bus pictogram when a vehicle is due, ticker for long destinations).
It runs as a normal web page and as an installable iPhone web app (PWA).

- No build step, no dependencies: `index.html` is the whole app.
- Data: [transport.opendata.ch](https://transport.opendata.ch) (`/v1/stationboard`, `/v1/locations`), no API key needed.
  Timetable data: opentransportdata.swiss.
- Settings (gear button): stop, lines, destinations, vehicle types, number of rows. Stored in the browser.

## Deploy with GitHub Pages

1. Create a new repository on GitHub and upload all files of this folder (all files sit in one folder, no subfolders needed).
2. Repository **Settings → Pages → Build and deployment**: Source **Deploy from a branch**, Branch **main**, folder **/ (root)**.
3. After a minute the app is available at `https://<your-user>.github.io/<repository>/`.

## Install on iPhone

Open the Pages address in **Safari** → Share button → **Add to Home Screen**.
Launch it from the home screen icon to get the full-screen app without browser bars.
Tip: Settings → Display & Brightness → Auto-Lock → Never, if the screen should stay on.

## URL parameters

`?station=Bern, Zytglogge&lines=6,7&dests=worb&modes=tram,bus&rows=4&demo=1`

## Destination names

`LINE_DESTS` in `index.html` maps each line to the destination texts shown on the real displays.
Names from the API are matched exactly, as a shorter form, or by distinctive words (towns and words like
"Bahnhof" or "Tram-Endstation" are ignored). Anything unknown falls back to simple formatting.
Too long a name is shortened ("Bahnhof" → "Bhf") and, if it still does not fit, runs as a ticker.

## Files

| File | Purpose |
|---|---|
| `index.html` | The app (HTML, CSS, JS) |
| `manifest.webmanifest` | Web app manifest (name, colors, icons) |
| `sw.js` | Service worker, caches the app shell for offline start |
| `*.png` | App icons (iOS home screen, Android, favicon) |
