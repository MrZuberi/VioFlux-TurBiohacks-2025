# VioFlux — Epigenetic Tuning Simulator (Violacein)

Interactive, self-contained web app that models epigenetic tuning on the **violacein** pathway (VioA–E). Built with React frontend and Python Flask backend, providing real-time simulation of gene expression modifications and their effects on biosynthetic yield.

## Demo & Project Links

## 🏆 Won 1st Place TurbioHacks Hackathon 2025
**[View on DevPost](https://devpost.com/software/vioflux)** -- 

### Demo Video

[![VioFlux Demo](https://img.youtube.com/vi/aeIjKiZMbDw/0.jpg)](https://www.youtube.com/watch?v=aeIjKiZMbDw)

*Click the thumbnail above to watch the full VioFlux demonstration*

## Features

**What you can do**
* **Toggle per-gene epigenetic modules** (buttons):
   * `CRISPRa` (activator)
   * `CRISPRi` (repressor)
   * `Methylation` (binary switch)
   * `Neutral` (no effect)
* **Set module "level"** (slider 0.00–1.00) for each gene.
* **See outputs update live:**
   * **Yield** (× relative units) and % change vs baseline
   * **Bottleneck** gene (if detected by rules)
   * **Gene sensitivity bars** (relative influence)
   * **Data view**: active genes, current supply cap, burden sensitivity, current yield
* **Run a sample grid search** (pre-computed examples) in the "Experiments" panel.
* **Reset** to the neutral starting state.

## Technologies

### Frontend
- **React** - Component-based UI framework with hooks
- **CSS3** - Advanced styling with animations and responsive design
- **Fetch API** - HTTP client for backend communication

### Backend
- **Python Flask** - Lightweight web framework
- **Flask-CORS** - Cross-origin resource sharing
- **NumPy** - Numerical computations for pathway simulation
- **Pandas** - Data manipulation and CSV handling

## Pathway & Modules

### Pathway (linear order)
`VioA → VioB → VioE → VioD → VioC`

Each step has a baseline activity and a burden weight:
* `baseline_k = 1.0` for all steps
* `burden_w = 1.0` except `VioC = 1.2`

### Module types (mathematical model)
* **CRISPRa** (`type: activator`) — increases gene expression using Hill function kinetics
* **CRISPRi** (`type: repressor`) — decreases gene expression with tunable minimum levels
* **Methylation** (`type: binary`) — ON (≥0.5) gives fixed expression; OFF gives minimal leak
* **Neutral** — baseline expression level (no modification)

## API Endpoints

```
GET    /api/health                    # Server health check
GET    /api/pathway                   # Get pathway gene data
GET    /api/modules                   # Get available epigenetic modules
POST   /api/simulate                  # Run pathway simulation
POST   /api/grid_search              # Run combinatorial optimization
```

## Data Sources

The simulation uses TSV/CSV configuration files:
- **Pathway Data**: `data/violacein_pathway.tsv` - Gene order, baseline activities, burden weights
- **Module Data**: `data/epigenetic_modules.csv` - Module parameters (EC50, Hill coefficients, etc.)

## Project Structure

```
├── backend/
│   ├── api_server.py            # Flask server and API endpoints
│   ├── sim_core.py             # Mathematical simulation engine
│   ├── data_io.py              # Data loading utilities
│   ├── start_vioflux.py        # Startup script
│   └── data/
│       ├── violacein_pathway.tsv    # Gene pathway configuration
│       └── epigenetic_modules.csv   # Module parameters
├── frontend/
│   ├── src/
│   │   ├── App.js              # Main React application
│   │   └── App.css             # Complete styling
│   └── public/
│       └── index.html          # HTML template
```

## Key Features

- **Real-time Simulation**: Updates yield calculations instantly as parameters change
- **Mathematical Modeling**: Uses Hill kinetics, soft-min bottleneck detection, and burden penalties
- **Interactive Visualization**: Gene sensitivity bars, yield comparisons, and bottleneck identification  
- **Grid Search**: Combinatorial optimization testing OFF/MED/ON levels for all genes
- **Responsive Design**: Works on desktop and mobile devices
- **Error Handling**: Graceful fallbacks when backend is unavailable

## Installation & Setup

### Backend (Python Flask)

1. Navigate to backend directory:
```bash
cd backend
```

2. Install dependencies:
```bash
pip install flask flask-cors pandas numpy
```

3. Run the Flask server:
```bash
python api_server.py
```

Backend will start on `http://localhost:5000`

### Frontend (React)

1. Navigate to frontend directory:
```bash
cd frontend
```

2. Install dependencies:
```bash
npm install
```

3. Start the development server:
```bash
npm start
```

Frontend will start on `http://localhost:3000`

## How to Use

1. **Start both servers** (backend on port 5000, frontend on port 3000)
2. **Select epigenetic modules** for each gene using the control buttons
3. **Adjust module levels** using the sliders (0.0 = OFF, 1.0 = maximum effect)
4. **Monitor real-time results** in the yield display and sensitivity bars
5. **Experiment with different combinations** to optimize violacein production
6. **Use grid search** to systematically test all OFF/MED/ON combinations
7. **View detailed data** in the Data tab for current settings and gene information

## Mathematical Model

The simulation implements:
- **Hill function kinetics** for module dose-response
- **Soft-minimum bottleneck detection** using smooth approximation
- **Metabolic burden penalties** based on total protein expression
- **Pathway-specific rules** (e.g., VioE gating, VioC shunting)
- **Finite difference sensitivity analysis** for gene importance ranking

## Credits

- **Backend/Mathematical modeling** - Alexei Manuel
- **Frontend/UI and Backend integration** - Taha Zuberi

---

### 🔗 Original Repository that we worked in
This project is a fork of [OriginalRepoName](https://github.com/aalxi/VioFlux)


## License

This project is available for educational and research purposes.
