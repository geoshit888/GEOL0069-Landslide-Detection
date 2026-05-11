# Landslide Detection Using Unsupervised Classification
**A Case Study in Hualien–Taroko, Taiwan (2021–2025)**

## Introduction

This project applies unsupervised machine learning and Sentinel-2 satellite imagery to identify potential landslide areas in the Hualien–Taroko region of eastern Taiwan between 2021 and 2025. The study aims to investigate how surface conditions changed before and after the 2024 Hualien earthquake, with particular focus on earthquake-triggered landslides and newly exposed bare ground.

Using Google Earth Engine and K-means clustering, the workflow analyses yearly satellite composites and spectral indices such as NDVI, NBR, NDMI and BSI to automatically classify landslide candidate areas without requiring manually labelled training data. The project demonstrates how freely available satellite imagery and cloud-based geospatial analysis can support rapid environmental assessment in mountainous hazard-prone regions.

## Background

**Why This Topic?**

Taiwan is one of the most landslide-prone regions in the world due to its steep mountainous terrain, active tectonic setting, intense rainfall and frequent typhoons (Lin et al., 2004). Earthquakes can destabilise hillslopes, trigger rockfalls and increase sediment transport, causing widespread geomorphic change across mountain catchments. The Taroko region of eastern Taiwan is characterised by steep relief, narrow valleys and highly fractured metamorphic rocks. Combined with intense rainfall from typhoons and frequent seismic activity, these conditions make the region highly susceptible to landslides and debris flows.

The 3 April 2024 Hualien earthquake (Mw 7.4) generated extensive slope failures across eastern Taiwan, particularly within and around Taroko National Park. Detecting these changes rapidly is important for hazard assessment, infrastructure monitoring and environmental management.

Remote sensing provides an effective way to monitor landslide activity over large areas where field surveys may be difficult or dangerous. This project therefore explores whether unsupervised classification of Sentinel-2 imagery can identify likely landslide areas and quantify landscape change through time.

**References**

- Lin, G. W., Chen, H., Hovius, N., Horng, M. J., Dadson, S., Meunier, P., & Lines, M. (2004). Effects of earthquake and cyclone sequencing on landsliding and fluvial sediment transfer in a mountain catchment. *Earth Surface Processes and Landforms*, 33(9), 1354–1373.
- Keefer, D. K. (1984). Landslides caused by earthquakes. *Geological Society of America Bulletin*, 95(4), 406–421.
- Dadson, S. J., Hovius, N., Chen, H., Dade, W. B., Hsieh, M. L., Willett, S. D., et al. (2004). Earthquake-triggered increase in sediment delivery from an active mountain belt. *Geology*, 32(8), 733–736.

---

**Why Use K-means and Unsupervised Classification**

Many landslide mapping studies rely on supervised machine learning, which requires manually labelled training datasets. However, accurate landslide inventories are often unavailable immediately after a disaster.

This project therefore uses **K-means clustering**, an unsupervised machine learning algorithm that groups pixels with similar spectral characteristics into clusters automatically. By combining spectral indices, topographic information and temporal change metrics, clusters with landslide-like properties can be identified without manually labelled data.

Advantages of the unsupervised approach include:

- No need for pre-labelled training data
- Rapid implementation after hazard events
- Ability to process large areas efficiently
- Suitable for exploratory or preliminary hazard mapping

However, unsupervised classification may also produce false positives, such as riverbeds, roads or bare agricultural land.

**References**

- Jain, A. K. (2010). Data clustering: 50 years beyond K-means. *Pattern Recognition Letters*, 31(8), 651–666.
- MacQueen, J. (1967). Some methods for classification and analysis of multivariate observations. *Proceedings of the Fifth Berkeley Symposium on Mathematical Statistics and Probability*, 281–297.

**Figure**
Example workflow showing how K-means clustering groups pixels with similar spectral and topographic characteristics into clusters.

---

**Sentinel-2 Satellite Data**

This project uses imagery from the Sentinel-2 mission operated by the European Space Agency (ESA). Sentinel-2 provides multispectral optical imagery with spatial resolutions of 10–20 m and revisit times of approximately 5 days.

The satellite includes spectral bands useful for vegetation, soil and moisture analysis, making it highly suitable for landslide detection and environmental monitoring.

Key spectral indices used in this project include:

| Index | Purpose |
|---|---|
| NDVI | Vegetation condition |
| NBR | Vegetation disturbance / bare ground |
| NDMI | Surface moisture |
| BSI | Bare soil exposure |

**References**
- Drusch, M., Del Bello, U., Carlier, S., Colin, O., Fernandez, V., Gascon, F., et al. (2012). Sentinel-2: ESA’s optical high-resolution mission for GMES operational services. *Remote Sensing of Environment*, 120, 25–36.

---

**Figure of Sentinel-2**

## Getting Started

**Requirements**

**Running the Notebook**

1. Download the .ipynb notebook from this repository.
2. Upload the notebook to Google Colab or run locally using Jupyter Notebook.
3. Authenticate Google Earth Engine
5. Run all cells

The workflow will:

- Download and preprocess Sentinel-2 imagery
- Generate annual composites
- Calculate spectral indices
- Perform K-means clustering
- Detect landslide candidate areas
- Export maps and CSV files

---

## How the Notebook Works

**1. Data Collection**

Sentinel-2 Level-2A surface reflectance imagery is retrieved from Google Earth Engine for each year between 2021 and 2025.

Clouds and cloud shadows are masked using the Sentinel-2 Scene Classification Layer (SCL).

**2. Annual Composite Generation**

For each year, median composites are generated to reduce cloud contamination and create representative annual images.

**3. Spectral Index Calculation**

Several spectral indices are calculated:

- NDVI
- NBR
- NDMI
- NDWI
- BSI

Temporal change metrics (`dNDVI`, `dNBR`, `dBSI`) are also computed by comparing each year with the previous year.

**4. Topographic Analysis**

Elevation and slope are derived from DEM data to help distinguish landslide-prone terrain.

**5. K-means Clustering**

Pixels are grouped into clusters using K-means clustering. Clusters with characteristics such as:

- low vegetation
- high bare soil exposure
- strong negative vegetation change
- steep slope

are interpreted as landslide-like clusters.

**6. Landslide Candidate Mask Generation**

Additional threshold filters are applied to reduce false positives and produce yearly landslide candidate masks.

**7. Area Calculation and Change Detection**

The notebook calculates:

- yearly candidate landslide area
- year-to-year new candidate landslide area

Results are exported as:

- CSV tables
- PNG 

## Results

The workflow successfully identified areas with strong spectral and topographic signatures consistent with landslide activity. Increased landslide candidate area was observed following the 2024 Hualien earthquake, particularly in steep mountainous terrain around Taroko Gorge.

The unsupervised approach provides a rapid and scalable method for preliminary landslide detection using freely available satellite imagery. However, further validation using official landslide inventories or high-resolution imagery would be required for operational hazard assessment.

[View the PDF](docs/result.pdf)

