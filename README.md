# Cool Solutions for Hot Cities
### Satellite-based thermal risk mapping to address transport poverty in the urban heat island

**SEEOB – Space Economy & Earth Observation Business | Politecnico di Milano**  
*Project partner: [Transform Transport](https://transformtransport.org)*  
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

---

## The problem

Low-income residents in European cities face a **double disadvantage**: limited access to public transport *and* higher exposure to extreme summer heat. Traditional tools fail to map where these two deprivations overlap at neighborhood resolution — ground weather stations are too sparse, and MODIS thermal imagery is too coarse (1 km pixel) to distinguish individual street blocks.

Applied to Milan (summer 2025), the analysis found:
- **27%** of the urban study area is simultaneously heat-stressed (LST > 32 °C) and underserved by public transit (> 400 m from any stop)
- **~268,000 residents** live in this *double-disadvantage zone*

---

## Pipeline overview

```
Study area (FAO GAUL L2)
    └─ Urban mask (ESA WorldCover, Class 50)
        └─ Sentinel-2 SR median composite (Jun–Aug)
            └─ Spectral indices: NDVI · NDWI · NDBI
                └─ MODIS MOD11A2 LST (1 km) ──── OLS regression ──▶ Predicted LST @ 10 m
                                                                         └─ Thermal stress layer (> 32 °C)
                                                                              └─ OSM PT stops (400 m buffer)
                                                                                   └─ Double-disadvantage map
                                                                                        └─ Population exposure (WorldPop)
```

The regression model (`LST = b₀ + b₁·NDVI + b₂·NDWI + b₃·NDBI`) achieves **R² = 0.78, RMSE = 1.87 °C** on 930 urban sample points — 100× finer resolution than any freely available thermal product.

---

## Repository structure

```
├── SEEOB.ipynb          # Full pipeline (Google Colab)
├── pics/                # Output figures (correlation plots, LST maps, bivariate choropleth, Folium dashboard)
├── requirements.txt     # Python dependencies
├── LICENSE              # MIT
└── README.md
```

---

## Data sources

| Dataset | Provider | Resolution | Role |
|---|---|---|---|
| Sentinel-2 SR Harmonised | Copernicus / GEE | 10 m | Spectral indices (NDVI, NDWI, NDBI) |
| MODIS MOD11A2 | NASA / GEE | 1 km | Land Surface Temperature (training target) |
| ESA WorldCover v200 | ESA / GEE | 10 m | Urban mask (Class 50 = Built-up) |
| JRC Global Surface Water | JRC / GEE | 30 m | Permanent water mask |
| WorldPop GP | WorldPop | 100 m | Population density |
| FAO GAUL Level 2 | FAO / GEE | Vector | City boundary |
| OpenStreetMap | OSM / Overpass API | Vector | Public transport stop locations |

All datasets are **freely available** — no proprietary licenses required.

---

## How to run

1. Open `SEEOB.ipynb` in [Google Colab](https://colab.research.google.com/)
2. In **Cell 1**, set your city and GEE project:
   ```python
   CITY = 'Milano'   # Roma | Torino | Napoli | Bologna | Firenze
   ee.Initialize(project='your-gee-project')
   ```
3. Mount Google Drive — outputs are saved to `MyDrive/SEEOB_TransportPoverty/`
4. **Runtime → Run all**

The pipeline caches EE samples locally (`.pkl`) so subsequent runs skip the slow sampling step.

---

## Key results (Milan, summer 2025)

| Metric | Value |
|---|---|
| Mean observed LST | 31.7 °C |
| LST range | 24.3 – 38.2 °C |
| Model R² | 0.78 |
| RMSE | 1.87 °C |
| MAE | 1.42 °C |
| Urban area above 32 °C | 42.6% |
| Urban area hot + no PT | 27% (~268,000 residents) |

---

## Business model (summary)

The platform targets three segments with EO-derived analytics:

- **B2G (Municipalities)** — Priority Intervention Maps + live monitoring dashboards for urban planners (Comune di Milano, Città Metropolitana)
- **B2B (Food delivery)** — Thermal risk dashboards + heat-aware routing API for Glovo / Deliveroo / Just Eat; riders double as IoT data-sensing partners
- **B2B (ESG / Impact finance)** — Before-after thermal impact assessment reports for funds like Oltre Impact and Fondazione Cariplo

---

## Course

Space Economy and Earth Observation Business | A.Y. 2025–2026 | Politecnico di Milano  
Professors: Prof. Paravano, Prof. Oxoli  
Group 5: M. Addazi, N. D. Fragnito, R. Naeijian, A. Pallotta, E. Pessina
