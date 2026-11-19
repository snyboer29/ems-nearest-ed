# EMS Nearest ED (prototype)

A static iPhone-friendly web app intended for GitHub Pages. It captures one GPS fix per tap, searches OpenStreetMap within 80 km for hospitals and facilities explicitly tagged as emergency departments, asks the public OSRM demo service for driving estimates, links each result to Google Maps, and stores the last 50 lookups in this browser's local storage.

## Geographic coverage

The app can be opened anywhere in Illinois or eastern Missouri. Each lookup searches an 80 km radius around the current GPS fix; it does not download a complete statewide hospital directory. A hospital must have suitable OpenStreetMap emergency-department tagging to appear.

## Important limitations — do not use as sole destination-selection source

- This is a prototype, not a validated EMS navigation or dispatch product.
- OpenStreetMap tagging is incomplete and not authoritative. A real ED may be missing; a tag may be stale. This prototype deliberately requires an explicit emergency tag, so it may return no result even when an ED is nearby.
- Trauma designations, emergency specialties, capabilities, diversion status, and pediatric capabilities are **not populated or inferred**. They display as not verified. Do not use this app to make a clinical destination decision.
- OSRM's public demo server is best-effort, has no uptime or latency guarantee, and is not ambulance routing. Its published guidance asks users to keep requests reasonable (historical demo guidance: no more than 1 request/second). This app makes one routing-table request per lookup.
- Overpass public servers may be overloaded. The app tries a small list of public endpoints sequentially.
- No patient information is collected. Coordinates are sent to the public Overpass and OSRM services when a lookup is run. GitHub Pages logs visitor IP addresses. Lookup history is stored in local browser storage and can be cleared in the app.
- Google Maps opens ordinary consumer driving directions, not emergency-vehicle routing.

## Publish on GitHub Pages

1. For this project, use the GitHub account `snyboer29`. Create a **public** GitHub repository named `ems-nearest-ed` (GitHub Free requires a public repository for Pages).
2. Upload all files and folders in this project, preserving `.github/workflows/deploy.yml`.
3. In repository Settings → Pages, set Source to **GitHub Actions**.
4. The included workflow publishes the site on pushes to `main`. Wait for the Pages deployment to finish.
5. Open `https://YOUR-GITHUB-USERNAME.github.io/ems-nearest-ed/` in Safari on the iPhone.
6. In Safari, use Share → Add to Home Screen. Enable “Open as Web App” if offered.
7. When first prompted, allow location access. For reliable GPS, launch from the home-screen icon and allow location while using the app.

## iPhone Shortcut

Create a Shortcut named `Nearest ED` with these actions:

1. **Get Current Location**.
2. **Get Details of Locations** → Latitude (from Current Location).
3. **Get Details of Locations** → Longitude (from Current Location).
4. **Text** → `https://YOUR-GITHUB-USERNAME.github.io/ems-nearest-ed/?lat=[Latitude]&lon=[Longitude]&auto=1` (insert the Latitude and Longitude magic variables in the brackets).
5. **Open URLs** → the Text result.

The page recognizes `auto=1` and starts exactly one lookup using the coordinates supplied by Shortcuts. A bug fix ensures the Shortcut-provided location path does not try to read browser GPS accuracy. This avoids the ChatGPT Ask ChatGPT action and its conversation behavior. Add the Shortcut to the Home Screen or Lock Screen for fast activation. Test location permissions and behavior before operational use.

## Local development

Open `index.html` through a local static web server or deploy to HTTPS. Browser geolocation requires a secure context (HTTPS, or localhost).
