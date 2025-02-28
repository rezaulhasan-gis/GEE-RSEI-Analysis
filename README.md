# Remote Sensing Ecological Index (RSEI) using Landsat 8 and Google Earth Engine

## 🛠️ Project Overview
Cox's Bazar, home to the world's largest refugee settlement, has experienced an unprecedented ecological strain since the 2017 Rohingya refugee crisis. The rapid deforestation for shelter, firewood, and infrastructure, coupled with increased waste generation and soil erosion, has significantly disrupted the region's fragile ecosystem. Later, from 2018, there had been some small-scale reforestation programs carried out to improve the ecological conditions of the camp area.

The Remote Sensing Ecological Index (RSEI) is an essential tool for assessing these environmental impacts. By analyzing key ecological indicators such as vegetation cover, surface temperature, wetness, and soil conditions, RSEI aids policymakers in:

✅ Monitoring ecological changes over time  
✅ Implementing sustainable land management practices  
✅ Evaluating the effectiveness of restoration efforts  

## Overview
This project calculates the **Remote Sensing Ecological Index (RSEI)** using **Landsat 8** imagery in **Google Earth Engine (GEE)**. The RSEI is a composite index derived from multiple ecological parameters to assess environmental quality. The workflow includes **data preprocessing, ecological index calculations, standardization, Principal Component Analysis (PCA), and classification into five ecological stress levels**.

## Methodology
### Data Collection
- Landsat 8 Collection 2 Level 2 imagery from Google Earth Engine (GEE)
- Best growth season imagery (August – November)
- Masking cloud shadows and water bodies using **QA_PIXEL** and **NDWI**

# Calculation of Ecological Indices

### 1. Normalized Difference Vegetation Index (NDVI)
NDVI is calculated using the formula:

NDVI = (NIR - RED) / (NIR + RED)

- **NIR (Near-Infrared)** = `SR_B5`
- **RED** = `SR_B4`

NDVI values range from **-1 to 1**:
- Negative values indicate **water or bare soil**.
- Values near zero suggest **barren areas**.
- Higher values indicate **vegetation**.

---

### 2. Land Surface Temperature (LST)
LST is derived from **thermal band ST_B10** and emissivity (**EM**) using the Planck function:

LST = (TB / (1 + (0.00115 * (TB / 1.438)) * log(em))) - 273.15

where:
- **TB** = Top of Atmosphere Brightness Temperature from **ST_B10** (Kelvin).
- **Emissivity (EM)** is estimated from the **Fractional Vegetation Cover (FV)**:
  
  EM = (FV * 0.004) + 0.986
  
  with **FV** calculated as:
  
  FV = ((NDVI - NDVI_min) / (NDVI_max - NDVI_min))^2

LST is expressed in **Celsius** by subtracting **273.15**.

---

### 3. Normalized Difference Built-up Index (NDBSI)
NDBSI is calculated as:

NDBSI = ((RED + SWIR1) - (NIR + BLUE)) / ((RED + SWIR1) + (NIR + BLUE))

- **RED** = `SR_B4`
- **SWIR1 (Shortwave Infrared 1)** = `SR_B6`
- **NIR** = `SR_B5`
- **BLUE** = `SR_B2`

**Higher NDBSI values** indicate **urban and built-up areas**.
**Lower values** indicate **vegetated or water areas**.

---

### 4. Wetness Index (Tasseled Cap Transformation - Wetness Component)
Wetness is calculated using:

Wetness = 0.1511 * B2 + 0.1973 * B3 + 0.3283 * B4 + 0.3407 * B5 - 0.7117 * B6 - 0.4559 * B7

- **B2 (Blue)** = `SR_B2`
- **B3 (Green)** = `SR_B3`
- **B4 (Red)** = `SR_B4`
- **B5 (NIR)** = `SR_B5`
- **B6 (SWIR1)** = `SR_B6`
- **B7 (SWIR2)** = `SR_B7`

**Higher values** indicate **moisture-rich surfaces** (e.g., water bodies).
**Lower values** indicate **drier surfaces**.

---

### Summary of Index Calculations
| Index  | Formula  | Interpretation  |
|---------|------------------------------------|--------------------------------|
| **NDVI**  | (NIR - RED) / (NIR + RED) | Measures vegetation health (higher = greener) |
| **LST**  | Derived from ST_B10 using Planck’s function | Surface temperature in °C |
| **NDBSI**  | ((RED + SWIR1) - (NIR + BLUE)) / ((RED + SWIR1) + (NIR + BLUE)) | Measures built-up area intensity |
| **Wetness**  | Tasseled Cap Wetness Component | Indicates surface moisture content |


## Classification of RSEI
RSEI values are categorized into five ecological stress levels:

| RSEI Range  | Stress Level |
|-------------|-------------|
| 0.0 - 0.2   | Very Low    |
| 0.2 - 0.4   | Low         |
| 0.4 - 0.6   | Moderate    |
| 0.6 - 0.8   | High        |
| 0.8 - 1.0   | Very High   |

This classification helps assess **urbanization effects, land degradation, and reforestation success**.

## Features
- **Google Earth Engine (GEE) for cloud-based analysis**
- **Landsat 8 Collection 2 Level 2 data processing**
- **Automated masking of clouds, shadows, and water bodies**
- **Computation of ecological indices (NDVI, LST, Wetness, NDBSI)**
- **Principal Component Analysis (PCA) to derive RSEI**
- **Classification of RSEI into five environmental stress levels**
- **Visualization and histogram plotting in GEE**

## Results
- **RSEI Map**: Visual representation of environmental quality.
- **Classified RSEI**: Five stress levels for easy interpretation.
- **Histogram Analysis**: Distribution of RSEI values across the AOI.

## Prerequisites
- **Google Earth Engine (GEE) account**
- Basic knowledge of **JavaScript** for GEE scripting
- Familiarity with **remote sensing indices and PCA**

## How to Use

### 📜 Code Repository
You can find the complete script for this project in the GitHub repository:

➡️ **[GitHub Repository Link](https://github.com/rezaulhasan-gis/GEE-RSEI-Analysis/blob/main/GEE_code.js)**

### Steps to Run
1. **Open Google Earth Engine** and create a new script.
2. **Copy and paste the code** into the GEE script editor.
3. **Modify AOI and date range** as needed.
4. **Run the script** to generate the RSEI map and classification.

---

This version improves readability, correctly formats the equations in LaTeX, and ensures proper Markdown syntax for GitHub. Let me know if you need further refinements! 🚀


## Output
![Sample output](RSEI_result.png)

## References
- Xu, H. (2013). Remote sensing evaluation index for ecological quality assessment.
- Landsat 8 Science Team (2013). Surface Reflectance and Radiometric Correction.
- Haque, M.R. et al. (2024). "Land Use Transition and Ecological Consequences: A Spatiotemporal Analysis in South-Eastern Bangladesh."

## License
This project is open-source and licensed under the **MIT License**.

---

### Author

*Your Name Here*

📌 **Contributions are welcome!** Feel free to fork, modify, and improve this repository.

