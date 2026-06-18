# 3DNS: 3D Diabetes CGM Visualization (Nightscout)

A modern web application for visualizing and analyzing Continuous Glucose Monitoring (CGM) data from Nightscout. The project combines immediate 24h glucose insights with a roadmap to interactive 3D visualization for deeper trend analysis.

**GitHub Pages:** [https://iricigor.github.io/3dns/](https://iricigor.github.io/3dns/)

## Current Features

### 24h CGM Dashboard
- **Real-time glucose display** with trend direction and timestamp
- **24-hour sparkline chart** showing glucose trajectory
- **Summary metrics**: average, minimum, maximum, and data point count
- **Time-in-range analysis**: percentage breakdown for low, target, and high glucose zones
- **Reader-only token verification** with safe probe (no data modification attempted)
- **Light/Dark theme toggle** for comfortable viewing in any lighting
- **Unit conversion**: mg/dL ↔ mmol/L with live conversion
- **Responsive design** optimized for desktop and mobile

### Security
- Reader-scope validation ensures API token has read-only privileges
- Safe token capability probing (DELETE probe on non-existent records)
- No sensitive data stored locally
- Environment-based configuration

## Vision

The ultimate goal is a **3D interactive experience** that visualizes CGM patterns in space:
- **X axis**: time progression
- **Y axis**: glucose values  
- **Z axis**: daily layers or variability dimension
- Interactive rotation, zoom, and pan controls
- Hover tooltips for event details
- 3D treatment markers (meals, boluses, exercise)
- Animated transitions between date ranges

## Tech Stack

**Current Implementation:**
- Vanilla JavaScript (ES6+) for broad compatibility
- HTML5 + CSS3 (CSS Grid, Flexbox, CSS Variables)
- Nightscout REST API for data retrieval
- Fluent Design System principles for UI consistency

**Future 3D Stack (Planned):**
- TypeScript for type safety
- Vite as build/dev tool
- Three.js or Babylon.js for 3D rendering
- React Three Fiber for component-based 3D scenes (optional)
- D3.js for advanced data transformations

## Design Philosophy

This project follows **Microsoft Fluent Design System** guidelines:
- Clean, minimal interface with content-first approach
- Acrylic glass surfaces with subtle depth and layering
- Consistent spacing and typographic hierarchy
- Smooth animations and transitions
- Light and dark mode support
- Keyboard and screen-reader accessibility

## Data Source

Nightscout exposes CGM and treatment data through a REST API.

### Common Endpoints

- `GET /api/v1/entries.json` – glucose entries (CGM readings)
- `GET /api/v1/treatments.json` – insulin doses, carbs, exercise, notes
- `GET /api/v1/profile.json` – user profile and settings

### Example Request

```bash
# Fetch last 288 entries (approx. 24 hours at 5-min intervals)
curl "https://YOUR-NIGHTSCOUT-URL/api/v1/entries.json?count=288&token=YOUR_READER_TOKEN"
```

### Authentication

- **Public instances**: No token needed
- **Private instances**: Requires API secret or reader token in query string or header
- **Token scope**: Use a dedicated reader-only token for security

## Getting Started

### Quick Start (F5 Launch)

1. Install VS Code debugger for Edge or Chrome
2. Open this repo in VS Code
3. Press **F5** to launch `index.html` in your default browser
4. Paste your Nightscout URL with reader token:
   ```
   https://your-nightscout.com/?token=YOUR_READER_TOKEN
   ```
5. Click **Load 24h Data**
6. View your glucose dashboard, toggle themes, and convert units

### Manual Run

```bash
# Simple HTTP server (Python 3)
python -m http.server 8000

# Or Node.js
npx http-server
```

Then open `http://localhost:8000` (or your server port) in a browser.

### Project Structure

```
.
├─ index.html              # Main 24h dashboard (current)
├─ README.md               # This file
├─ .vscode/
│  ├─ launch.json          # F5 debug config
│  ├─ tasks.json           # Build tasks
│  └─ settings.json        # Editor preferences
└─ Future: src/            # TypeScript + 3D implementation
   ├─ api/                 # Nightscout API layer
   ├─ data/                # Data transformation pipeline
   ├─ scene/               # Three.js 3D scene setup
   ├─ ui/                  # Fluent Design UI components
   └─ main.ts              # App entry point
```

## Implementation Details

### Current Dashboard (24h View)

**HTML Structure:**
- Semantic HTML5 with accessibility landmarks
- ARIA labels for screen readers
- Form-based input with token extraction

**CSS Styling:**
- CSS Variables (custom properties) for theming
- CSS Grid for responsive layout
- Fluent Design System colors and spacing
- 2-tier theme system (light/dark)

**JavaScript:**
- Vanilla ES6+ (no build step required)
- Async/await for API calls
- Safe token probing (non-destructive DELETE on non-existent records)
- Real-time unit conversion (mg/dL ↔ mmol/L)
- Dynamic sparkline generation via SVG path

### Data Flow

1. User enters Nightscout URL + token
2. Parse URL and extract base + token
3. Fetch `/api/v1/entries.json?count=288&token=...`
4. Filter out invalid entries (missing sgv, date, etc.)
5. Sort chronologically
6. Probe token permissions (safe DELETE check)
7. Render 24h dashboard with metrics, sparkline, and ranges
8. Enable real-time unit/theme switching

## Future Roadmap

### Phase 2: Enhanced 2D Visualization
- [ ] Date range picker for custom time windows
- [ ] Treatment overlay (meals, insulin, exercise)
- [ ] Advanced statistics (standard deviation, TIR by time of day)
- [ ] Export data as CSV or PDF

### Phase 3: 3D Visualization (MVP)
- [ ] Three.js scene setup with camera and lights
- [ ] Render 24h glucose as 3D scatter or line
- [ ] Interactive orbit controls (mouse + touch)
- [ ] Acrylic UI panel over 3D scene
- [ ] Real-time data refresh

### Phase 4: Advanced 3D
- [ ] Multi-day 3D view (Z-axis = days)
- [ ] Treatment markers in 3D space
- [ ] Predictive glucose trajectory
- [ ] VR/immersive mode (WebXR)

## Privacy & Security

- **No backend storage**: All data fetches directly from your Nightscout instance
- **Token validation**: Reader-only scope is verified before dashboard loads
- **HTTPS recommended**: Use HTTPS URLs for Nightscout to prevent token interception
- **Local-only**: Page can run on `file://` (with CORS limitations) or via any HTTP server

## Contributing

Contributions welcome! Please:
1. Fork the repo
2. Create a feature branch (`git checkout -b feature/my-feature`)
3. Follow the existing code style (vanilla JS, semantic HTML, Fluent Design)
4. Test in both light and dark modes
5. Submit a pull request

## Resources

- [Nightscout Project](http://nightscout.info/)
- [Microsoft Fluent Design System](https://www.microsoft.com/design/fluent)
- [Three.js Documentation](https://threejs.org/docs/)
- [MDN Web Docs](https://developer.mozilla.org/)

## License

MIT – See LICENSE file for details
