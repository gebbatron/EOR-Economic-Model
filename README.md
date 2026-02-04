# CO₂ EOR Economic Model

A comprehensive React-based economic model for CO₂ Enhanced Oil Recovery (EOR) projects. Simulates pattern-based field development with support for continuous injection, Water-Alternating-Gas (WAG), and Huff & Puff (cyclic) methods.

![Screenshot](screenshot.png)

## Features

### EOR Methods
- **Continuous CO₂ Injection** - Traditional flood with dedicated injector wells
- **WAG (Water-Alternating-Gas)** - Alternating water and CO₂ slugs for improved sweep efficiency
  - Staggered operation for full facility utilization
  - 15% improved recovery (lower CO₂/oil ratio)
  - 15% slower decline rate
- **Huff & Puff (Cyclic)** - Single-well cyclic injection for unconventional reservoirs
  - Configurable injection/soak/production phases
  - Diminishing returns per cycle

### Pattern Types
- 5-Spot (injector center, 4 producers at corners)
- Inverted 5-Spot (4 injectors at corners, producer center)
- Single Well (H&P)

### Economics
- Full value chain modeling (capture → transport → injection)
- 45Q tax credit calculation with qualification tracking
- State-specific severance taxes
- IDC/TDC tax treatment
- Monte Carlo sensitivity analysis
- NPV, IRR, PIR, payback calculations

### Visualization
- Interactive field development animation
- Production and injection profiles
- CO₂ balance charts (injected/produced/stored)
- Water balance charts (WAG)
- Revenue vs costs breakdown
- Cumulative cash flow

## Quick Start

### Prerequisites
- Node.js 18+ 
- npm or yarn

### Installation

```bash
# Clone the repository
git clone https://github.com/yourusername/co2-eor-model.git
cd co2-eor-model

# Install dependencies
npm install

# Start development server
npm run dev
```

The app will be available at `http://localhost:5173`

### Build for Production

```bash
npm run build
```

The built files will be in the `dist/` directory.

## Deployment

### GitHub Pages

1. Build the project:
   ```bash
   npm run build
   ```

2. Deploy the `dist/` folder to GitHub Pages, or use a GitHub Action:

```yaml
# .github/workflows/deploy.yml
name: Deploy to GitHub Pages

on:
  push:
    branches: [main]

jobs:
  build-and-deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      
      - name: Setup Node
        uses: actions/setup-node@v3
        with:
          node-version: 18
          
      - name: Install and Build
        run: |
          npm install
          npm run build
          
      - name: Deploy
        uses: peaceiris/actions-gh-pages@v3
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./dist
```

### Vercel / Netlify

Simply connect your repository - both platforms auto-detect Vite projects.

## Project Structure

```
eor-model/
├── src/
│   ├── EOR_Model.jsx    # Main application component
│   ├── main.jsx         # React entry point
│   └── index.css        # Tailwind CSS
├── index.html           # HTML template
├── package.json         # Dependencies
├── vite.config.js       # Vite configuration
├── tailwind.config.js   # Tailwind configuration
└── postcss.config.js    # PostCSS configuration
```

## Model Documentation

### Key Assumptions

| Parameter | Default | Range | Source |
|-----------|---------|-------|--------|
| CO₂/Oil Ratio | 0.35 t/bbl | 0.2-0.6 | Kuuskraa, NETL |
| Pattern Decline | 12%/yr | 8-15% | Industry data |
| 45Q EOR Credit | $60/t | Fixed | IRS |
| Recycle Rate | 0-85% | Ramps over time | Field data |

### Pattern Lifecycle

1. **Fill Phase** (0.5-2 yr) - CO₂ bank development
2. **Ramp Phase** (1-3 yr) - Production response
3. **Peak Phase** (2-5 yr) - Maximum production
4. **Decline Phase** (8-15%/yr) - Exponential decline
5. **Blowdown** - No injection, continued production

### WAG Physics

- Improved sweep efficiency reduces effective CO₂/oil ratio by 15%
- Staggered groups alternate CO₂/water phases
- Number of stagger groups = 1 + WAG ratio

### H&P Physics

- Typical cycle: 2 weeks injection, 2 weeks soak, 4 months production
- Oil response: ~2 bbl per tonne CO₂ injected
- Efficiency decreases ~35% per cycle
- Best suited for tight/unconventional reservoirs

## Data Sources

- **CO₂ EOR Performance**: EERC, Kuuskraa et al., PMC, Denbury, Oxy
- **Capture & Transport**: NETL, Incorrys Pipeline Cost Model, IEA
- **Tax & Regulatory**: IRS (45Q, Section 43), State authorities
- **Project Benchmarks**: Boundary Dam, Petra Nova, Quest

## License

MIT License - see LICENSE file

## Contributing

Contributions welcome! Please open an issue or PR.

## Acknowledgments

Built with React, Recharts, and Tailwind CSS.
