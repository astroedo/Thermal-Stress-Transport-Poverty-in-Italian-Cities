# Thermal Stress & Transport Poverty in Italian Cities
**SEEOB – Space Economy & Earth Observation Business | Politecnico di Milano**  
*Project partner: Transform Transport*

## Overview
This project explores transport poverty through Earth Observation data, integrating satellite-derived thermal and spectral indicators with public transport infrastructure to identify urban heat vulnerability hotspots across Italian cities.

EO question addressed: *How can integrating Earth Observation data with socio-economic and open data reveal new spatial patterns of transport poverty and vulnerability beyond the urban scale?*

## Repository Structure
```
├── notebook/SEEOB.ipynb       # Main analysis notebook (Google Colab)
├── pics/                      # Ouput images of the notebook
└── requirements.txt           # Python dependencies
```

## Data Sources
| Dataset | Source | Resolution |
|---|---|---|
| Land Surface Temperature | MODIS MOD11A2 | 1 km, 8-day |
| Spectral indices (NDVI, NDWI, NDBI) | Copernicus Sentinel-2 SR | 10 m |
| Urban extent | ESA WorldCover v200 | 10 m |
| Population | WorldPop GP 100m | 100 m |
| Surface water mask | JRC Global Surface Water | 30 m |
| Transit stops | OpenStreetMap (via Overpass API) | — |

## How to Run
1. Open `SEEOB.ipynb` in [Google Colab](https://colab.research.google.com/)
2. Set `CITY` in Cell 1 (options: `Milano`, `Roma`, `Torino`, `Napoli`, `Bologna`, `Firenze`)
3. Authenticate with Google Earth Engine (`ee-edoardo-polimi` project) and Google Drive
4. Run all cells — outputs are saved to `Google Drive/SEEOB_TransportPoverty/`

## Requirements
See `requirements.txt`. Key dependencies: `earthengine-api`, `folium`, `scipy`, `scikit-learn`, `pandas`, `matplotlib`.

## Course
SEEOB – Module 2 | A.Y. 2025/2026 | Politecnico di Milano  
Professors: D. Oxoli, A. Paravano, V. Zancan, M. Zgela
