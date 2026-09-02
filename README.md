# GridBearing

A minimal, offline, single-file web app for converting between **MGRS**, **UTM**, and **Lat/Lon** coordinates, and calculating the **bearing (mils or degrees) and distance** from your current position to a saved target.

No install, no build step, no backend, no tracking. Everything runs client-side in the browser and works entirely offline once loaded (all math — including MGRS/UTM conversion on the WGS84 ellipsoid — is computed locally in JavaScript).

The interface automatically follows your device's language (German or English, detected from browser settings) and its light/dark mode setting.

## Why this exists

This tool bridges a gap between digital map planning and old-school compass navigation:

- **Take a bearing off your smartphone map.** Plan a route or mark a target on a standard map app (Apple Maps, Google Maps, OpenTopoMap, etc.), copy the coordinates, and get an exact bearing and distance to it.
- **Check your current position against the map.** Paste in a freshly copied location to see exactly where you stand relative to your target — no need to reformat it first.
- **No cellphone coverage required.** Once the page is loaded, it needs no network connection — useful in the field, backcountry, or anywhere signal is unreliable.
- **Training with minimal technological support.** Good for practicing dead-reckoning, pace counting, and compass navigation while still having a reliable way to double-check your azimuth.
- **Find a location with standard map software, then navigate home by compass.** Get your bearing and distance digitally, then switch off the screen and rely on a physical compass to get there — a fallback that doesn't depend on GPS or live map rendering.

## Supported coordinate formats

Both the target and current-location fields accept any of the following, pasted as-is — no manual reformatting needed:

| Format | Example |
|---|---|
| MGRS | `33UUB1234567890` |
| Decimal degrees (DD) | `49.21011, 12.68932` |
| DD with compass letters | `49,21011° N, 12,68932° E` |
| Degrees/decimal minutes (DDM) | `49°12.607'N 12°41.360'E` |
| Degrees/minutes/seconds (DMS) | `49°12'36.4"N 12°41'21.6"E` |
| UTM (MGRS band letter) | `33U 456789 5678901` |
| UTM (N/S hemisphere) | `33N 456789 5678901` |

Whatever you paste is parsed and internally converted to a common UTM/MGRS representation, so the bearing and distance calculation works the same regardless of which format the target and current location were entered in.

Not currently supported: Open Location Codes / Plus Codes (e.g. `8FVC9G8F+6X`) and Geohash strings — these use different encoding schemes and aren't parsed.

## How it works

1. **Set a target.** Paste in a coordinate in any supported format (see above) and tap **Setzen**. It's saved locally on your device.
2. **Enter your current position.** Paste in your current coordinate — any supported format, doesn't need to match the target's format (the 📋 button reads it straight from your clipboard).
3. **Read the result.** The app shows the bearing to your target (in mils or degrees — toggle between the two), the straight-line distance, and the easting/northing delta.

> **Note:** Bearing/distance calculations are only valid within the same MGRS 100 km grid square as the target. If your current position falls outside that square, the app will flag it instead of giving a (silently wrong) result.

## Usage

Just open `index.html` in any modern mobile or desktop browser. For the best experience (HTTPS, clipboard paste support, "Add to Home Screen"), host it via GitHub Pages or any static web host — see below.

No dependencies, no npm install, no server required.

## Hosting on GitHub Pages

1. Push this repo to GitHub.
2. In the repo settings, go to **Pages** and set the source to the `main` branch, root folder.
3. Your app will be live at `https://<your-username>.github.io/<repo-name>/`.

GitHub Pages serves over HTTPS by default, which is required for the clipboard-paste (📋) button to work. If you open `index.html` directly from disk (`file://`), clipboard access will be blocked by the browser — you can still paste manually into the input fields.

## Limitations

- Valid only within a single 100 km MGRS grid square (by design — this keeps the underlying math simple and avoids silent errors near zone boundaries).
- Open Location Codes (Plus Codes) and Geohash strings aren't recognized.
- Lat/Lon pastes with no compass letters (e.g. `49.21011, 12.68932`) are assumed to be in `lat, lon` order, since that can't be inferred from the string alone.
- No offline app install/caching (no service worker) — it behaves like a bookmarked page, not a fully installable PWA. Easy to add later if needed.
- No built-in map rendering — this tool is a calculator, meant to complement a map app and a physical compass, not replace either.

## License

MIT — see [LICENSE](LICENSE).
