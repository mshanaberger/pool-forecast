[README.md](https://github.com/user-attachments/files/28536054/README.md)
# Pool Forecast by ZIP Code

A simple, single-file weather web app that creates a pool usability forecast from public National Weather Service data.

The app lets a user enter a 5-digit U.S. ZIP Code, then pulls the official NWS forecast, active alerts, current observations, daytime hourly forecast details, and a custom Pool Score Forecast.

## What It Does

- Looks up weather by ZIP Code
- Converts ZIP Code to latitude/longitude using Zippopotam.us
- Pulls public forecast data from the National Weather Service API
- Displays:
  - Current Observation
  - Active Alerts
  - Pool Score Forecast
  - Calendar-style pool score view
  - Daily forecast table
  - Daytime Hourly Forecast
- Hides nighttime forecast periods
- Scores each day and daytime hour for pool usability
- Requires no API keys, no backend, and no login

## Data Sources

This app uses public endpoints:

- ZIP Code lookup:
  - `https://api.zippopotam.us/us/{zip}`

- National Weather Service:
  - `https://api.weather.gov/points/{lat},{lon}`
  - NWS daily forecast endpoint
  - NWS hourly forecast endpoint
  - NWS active alerts endpoint
  - NWS observation stations endpoint
  - NWS latest observation endpoint

The NWS forecast API is point-based, not ZIP-based. The ZIP Code is only used to find the approximate latitude and longitude.

## Pool Score

The Pool Score is a custom 0.0 to 10.0 score designed to estimate how usable a day or hour is for pool time.

### Labels and Colors

| Score Range | Label | Color |
|---|---|---|
| 10.0–8.5 | Excellent | Red |
| 8.4–7.0 | Good | Orange |
| 6.9–5.5 | Fine | Green |
| 5.4–3.5 | Poor | Blue |
| 3.4–0.0 | Awful | Purple |

The score, label, and color should always match.

## Scoring Philosophy

Temperature is the main driver.

Warm, dry, partly sunny, mostly sunny, or comfortable days score well. A sub-50% precipitation chance should not heavily reduce the score unless rain or storms are expected during the main pool window.

### Daily Pool Window

- Monday–Friday:
  - Emphasizes evening pool use, roughly 5 PM–9 PM

- Saturday–Sunday:
  - Uses a broader pool window, roughly 11 AM–9 PM

### Current Temperature Adjustment

If the current observed temperature is higher than today’s forecast high, the app updates today’s high to the current observed temperature and recalculates today’s pool score.

## Current Layout

1. Header
   - Pool Forecast
   - by ZIP Code

2. ZIP Code search card

3. Current Observation and Active Alerts

4. Pool Score Forecast
   - Calendar first
   - Daily forecast table below the calendar
   - At a Glance summary
   - Score Legend

5. Daytime Hourly Forecast
   - Time
   - Temperature
   - Conditions
   - Precipitation
   - Pool Score

## Running Locally

Because this app uses JavaScript and external API calls, the most reliable way to run it locally is with a simple local server.

From the folder that contains `index.html`, run:

```bash
python3 -m http.server 8000
```

Then open:

```text
http://localhost:8000
```

You can also try double-clicking `index.html`, but some browsers may block or limit parts of the app when it is opened directly from a local file.

## Hosting on GitHub Pages

This app is designed to work well on GitHub Pages.

### Steps

1. Create a new GitHub repository.
2. Upload `index.html` to the root of the repository.
3. Go to **Settings**.
4. Go to **Pages**.
5. Under **Build and deployment**, choose:
   - Source: `Deploy from a branch`
   - Branch: `main`
   - Folder: `/ root`
6. Save the settings.

After GitHub Pages publishes the site, the link will look something like:

```text
https://yourusername.github.io/repository-name/
```

## File Structure

For the single-file version:

```text
index.html
README.md
```

The CSS and JavaScript are embedded inside `index.html` so the styling and functionality are less likely to break when sharing or uploading.

## Browser Requirements

A modern browser is recommended:

- Chrome
- Edge
- Firefox
- Safari

The app requires internet access because it fetches live data from public APIs.

## Notes and Limitations

- Forecasts are only available for U.S. locations supported by the National Weather Service.
- ZIP Code lookup is approximate and may not perfectly represent every location inside a ZIP Code.
- NWS data availability can vary by location.
- Observation data may be unavailable if the nearest station is temporarily offline.
- Alerts only appear when active NWS alerts exist for the point.

## Safety

This is a static HTML/CSS/JavaScript site.

It does not:

- install software
- run executables
- collect login information
- use cookies
- require API keys
- store user data
- send data to a private backend

The only network requests are to public weather and ZIP Code lookup endpoints.
