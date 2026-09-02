# GridBearing

A minimal, offline, single-file web app for converting between **MGRS** grid coordinates and **Lat/Lon**, and calculating the **bearing (mils or degrees) and distance** from your current position to a saved target.

No install, no build step, no backend, no tracking. Everything runs client-side in the browser and works entirely offline once loaded (all math — including MGRS/UTM conversion on the WGS84 ellipsoid — is computed locally in JavaScript).

## Why this exists

This tool bridges a gap between digital map planning and old-school compass navigation:

- **Take a bearing off your smartphone map.** Plan a route or mark a target on a standard map app (Apple Maps, Google Maps, OpenTopoMap, etc.), copy the coordinates, and get an exact bearing and distance to it.
- **Check your current position against the map.** Paste in a freshly copied location (MGRS or lat/lon) to see exactly where you stand relative to your target.
- **No cellphone coverage required.** Once the page is loaded, it needs no network connection — useful in the field, backcountry, or anywhere signal is unreliable.
- **Training with minimal technological support.** Good for practicing dead-reckoning, pace counting, and compass navigation while still having a reliable way to double-check your azimuth.
- **Find a location with standard map software, then navigate home by compass.** Get your bearing and distance digitally, then switch off the screen and rely on a physical compass to get there — a fallback that doesn't depend on GPS or live map rendering.

## How it works

1. **Set a target.** Paste in an MGRS grid reference or a lat/lon pair (as copied from most map apps, e.g. `49,21011° N, 12,68932° E`) and tap **Setzen**. It's saved locally on your device.
2. **Enter your current position.** Paste in your current MGRS or lat/lon coordinate (the 📋 button reads it straight from your clipboard).
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
- No offline app install/caching (no service worker) — it behaves like a bookmarked page, not a fully installable PWA. Easy to add later if needed.
- No built-in map rendering — this tool is a calculator, meant to complement a map app and a physical compass, not replace either.

## License

MIT — see [LICENSE](LICENSE).
