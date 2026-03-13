# Jupiter Great Red Spot Visibility Predictor

A single-file HTML/JavaScript application that predicts when Jupiter's Great Red Spot (GRS) becomes visible, transits the central meridian, and disappears from view.

## Features

- **GRS transit predictions** based on Jupiter's System II rotation period (9h 55m 40.6s)
- **Appear / Transit / Disappear times** for each visibility window (~5 hours per rotation)
- **Live countdown timers** ticking down to the next appearance, transit, and disappearance
- **Jupiter altitude/azimuth** calculated for each event using a simplified planetary ephemeris (accurate to ~1°)
- **Sun altitude filtering** — default view shows only events during astronomical night (sun below -18°), with options for "night + Jupiter above horizon" or all events
- **IMCCE sync** — fetch the current GRS longitude from the [IMCCE JGRS](https://ssp.imcce.fr/webservices/vo-tools/jgrs/) web service (Paris Observatory) for accurate predictions
- **Persistent settings** — location, timezone, GRS longitude, and filter preferences saved to localStorage
- **Geolocation support** — one-click browser location detection

## Usage

Open `index.html` in a web browser. No build step or server required.

### Controls

| Control | Description |
|---------|-------------|
| GRS Longitude | System II longitude of the GRS (default 40.2°, adjustable) |
| Sync IMCCE | Fetches current GRS longitude from the IMCCE ephemeris service |
| Days to predict | How far ahead to compute events (3–30 days) |
| Show events | Filter: night only, night + above horizon, or all |
| Time zone | Display timezone for event times |
| Latitude / Longitude | Observer location for alt/az and twilight calculations |
| Locate me | Uses browser geolocation to set lat/lon |

## How It Works

The app calculates Jupiter's System II Central Meridian (CM) longitude for any given time using the standard formula relative to the J2000.0 epoch. The GRS transits the CM once per rotation. It becomes visible when it is within 90° of the CM (at the limb) and disappears when it passes 90° on the other side.

Jupiter's position (RA/Dec) is computed from simplified mean orbital elements for Earth and Jupiter (Standish 1992), solving Kepler's equation for each. This is converted to local altitude/azimuth for the observer's location. Sun altitude is computed similarly to determine astronomical twilight.

## Accuracy

With the correct GRS longitude (via IMCCE sync), transit time predictions match the professional IMCCE JGRS ephemeris to within ~1 minute over a week. The GRS drifts slowly in System II coordinates, so periodic re-syncing is recommended.

## Data Sources

- GRS transit ephemeris: [IMCCE JGRS service](https://ssp.imcce.fr/webservices/vo-tools/jgrs/) (Institut de Mécanique Céleste et de Calcul des Éphémérides)
- Jupiter image: [NASA/JPL — Voyager 1 (PIA01509)](https://www.jpl.nasa.gov/images/pia01509-jupiter-full-disk-with-great-red-spot/)
