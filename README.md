# Abfahrt Bärn

A private, single-page replica of a "Tramli"-style departure display for stops in Bern, styled like the
Bernmobil stop signs (amber dot-matrix rows, bus pictogram when a vehicle is due, ticker for long destinations).
It runs as a normal web page and as an installable web app (PWA) on iPhone and Android.

- No build step, no dependencies: `index.html` is the whole app.
- Data: [transport.opendata.ch](https://transport.opendata.ch) (`/v1/stationboard`, `/v1/locations`), no API key needed.
  Timetable data: opentransportdata.swiss.
- Settings (gear button): stop, lines, destinations, vehicle types, number of rows (1-30). Stored in the browser.
- Quick selection (list button or tap on the stop title): the last used stops with their filters and their own number of rows (e.g. 4 for a small stop, 16 for Bern Bahnhof), removable one by one; the row count can be edited right in the list.
- Switching between the saved stops: swipe up/down on the sign (or arrow up/down, or tap a page dot on the right edge). The order of the list is fixed, new stops are added at the front. Swiping is only active while the whole sign fits on the screen. Stored in the browser (`localStorage`), nothing leaves the device.

## Deploy with GitHub Pages

1. Create a new repository on GitHub and upload all files of this folder (all files sit in one folder, no subfolders needed).
2. Repository **Settings → Pages → Build and deployment**: Source **Deploy from a branch**, Branch **main**, folder **/ (root)**.
3. After a minute the app is available at `https://<your-user>.github.io/<repository>/`.

## Install on your phone

Open the Pages address (`https://<your-user>.github.io/<repository>/`) and add it to the home screen.
Launch it from the new icon to get the full-screen app without browser bars.

### iPhone (Safari)

1. Open the address in **Safari** (other iOS browsers may not offer the option).
2. Tap the **Share** button (square with an arrow).
3. Choose **Add to Home Screen** and confirm with **Add**.
4. Optional: Settings → Display & Brightness → Auto-Lock → **Never**, if the screen should stay on.

### Android (Chrome)

1. Open the address in **Chrome**.
2. Tap the **menu** (⋮ at the top right).
3. Choose **Install app** (or **Add to Home screen** if the first entry is missing) and confirm.
4. Optional: Settings → Display → Screen timeout, if the screen should stay on longer. While the app is in
   the foreground it requests a wake lock, so the screen normally stays on anyway.

Other browsers (Firefox, Samsung Internet, ...) can open the page too, but the install entry is named
differently or may be missing; Chrome is the most reliable choice on Android.

### Notes

- Settings and the quick selection are stored per device and browser. A second device needs to be set up once.
- The first start needs internet (data and the dot-matrix font). Afterwards the app shell starts offline,
  but departures always need a connection.
- To update, close the app completely and open it again; the new version is picked up in the background.

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
