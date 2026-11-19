# EMS Nearest ED — state-directory build

Vibecoded by ChatGPT. Do not use in place of protocols, on-line medical control, or your services SOPs.

Static GitHub Pages web app. No OpenAI API, no Overpass, no paid service required.

## What it does
- Captures one GPS fix per activation.
- Loads Missouri DHSS hospital records where `ED=1` and Illinois IDPH licensed-hospital directory records.
- Caches successfully loaded directory records in browser local storage for 7 days.
- Ranks nearby records by road time when public OSRM routing responds; otherwise displays straight-line distance and Google Maps directions.
- Stores up to 40 lookups in local browser storage.
- Supports Shortcut URL parameters: `?auto=1&lat=38.1&lon=-90.1`.

## Data sources and limits
- Missouri: [DHSS Hospital GIS layer](https://gis.mo.gov/arcgis/rest/services/DHSS/medicalFacility/MapServer/0). Its metadata says the hospital licensing data is provided monthly by the Bureau of Hospital Standards and TCD designations are maintained by the Time Critical Diagnosis Unit. App filters `ED=1`.
- Illinois: [IDPH Hospital Directory dataset](https://data.illinois.gov/resource/53nt-jwqq.json). This is a licensed-hospital directory, not a definitive live ED roster. Entries are labelled as candidates; the app does NOT claim that the directory confirms an operating ED or its trauma/specialty status.
- Illinois also publishes [EMS destination codes](https://illinois-doit-prod-idph.amsadobe.com/topics-services/emergency-preparedness-response/ems/prehospital-data-program/illinois-nemsis-specifications/destination-codes.html) and a [freestanding emergency center directory](https://dph.illinois.gov/topics-services/health-care-regulation/health-care-facilities/free-standing-emergency-centers.html); those are not yet merged into this build.
- Road routing: public OSRM demo server. It is optional and can be rate-limited/unavailable. If it fails, the app shows straight-line ranking, not driving time.

## Important operational warning
This is a prototype / situational-awareness aid, NOT an EMS dispatch or destination-control system. The directory is not yet reconciled facility-by-facility across both states. It does not know current diversion, staffing, acceptance, specialty coverage, or real-time capability. Confirm with medical control and current protocols. Do not delay care to use it.

## Publish on GitHub Pages
Upload the contents of this folder to the repository root. In Settings → Pages, choose Deploy from a branch, `main`, `/ (root)`.

## iPhone Shortcut
Use Get Current Location → Get Details of Locations (Latitude, Longitude) → URL:
`https://YOUR-USER.github.io/ems-nearest-ed/?auto=1&lat=LATITUDE&lon=LONGITUDE`
Then Open URLs. Allow location if opening the site directly instead. Add the published page to Home Screen for standalone use.

## Local data/history
Directory cache and history use localStorage on the device/browser profile. Clearing website data or using a different browser can remove/separate this data. This is not cloud-synced.
