# CO₂ EOR Economic Model

## Project Overview
React-based economic screening model for CO₂ Enhanced Oil Recovery (EOR) projects. Single-page app with interactive inputs, real-time NPV/IRR calculations, charts, sensitivity analysis, and Monte Carlo simulation.

## Tech Stack
- **Framework:** React 18 + Vite
- **Charts:** Recharts
- **Styling:** Tailwind CSS (CDN in index.html)
- **No backend** — all calculations run client-side

## Architecture
- `src/EOR_Model.jsx` — The entire model (single-file component, ~1650 lines)
  - State variables for all inputs (oil pricing, injection, CO₂ costs, 45Q credits, etc.)
  - `calculateProjectMetrics()` — core monthly DCF engine
  - CO₂/Oil utilization ratio model with ramp profiles (new vs existing floods)
  - CO₂ recycle S-curve model (fixed or ramping modes)
  - Literature-based CAPEX model (capture purity-cost, pipeline inch-mile)
  - Monte Carlo simulation engine
  - Six tabs: Inputs, Results, Charts, Sensitivity, Monte Carlo, Assumptions

## Key Concepts
- **CO₂/Oil Ratio:** Oil production = CO₂ injected ÷ effective ratio (t CO₂/bbl). Ratio ramps for new floods (reservoir filling → steady state over 5-7 years), near-constant for existing floods.
- **Recycle Model:** S-curve ramp from 0% to 80%+ over project life. Net CO₂ stored = injected − recycled.
- **Full Value Chain vs EOR Only:** Toggle that adds capture CAPEX/OPEX and transport CAPEX/OPEX for integrated CCUS operators.
- **Scenario Types:** "Existing" (no well costs, near-peak from start) vs "New" (well costs, production ramp lag).

## Commands
```bash
npm install    # Install dependencies
npm run dev    # Start dev server (localhost:5173)
npm run build  # Production build to dist/
```

## Data Sources
EERC, DOE, NETL, CATF/IEA, PMC, OGJ, Trimeric/OSTI, EPA Platform v6, Boundary Dam/Petra Nova/Quest benchmarks, Denbury field data, Enverus model framework.
