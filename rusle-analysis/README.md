# DEM Watershed Delineation & LS Factor Calculation

## Overview
This project uses a Digital Elevation Model (DEM) to model surface runoff and delineate watersheds using ArcGIS Pro. The workflow derives hydrologic flow paths from terrain data and calculates the LS (slope length and steepness) factor used in RUSLE erosion modeling.

## Data
### Digital Elevation Model (DEM)
- Raster DEM with a **3.125 ft cell size**
- Used as the base dataset for all hydrologic analysis

The DEM represents terrain elevation and allows derivation of slope, flow direction, and drainage patterns. :contentReference[oaicite:0]{index=0}

---

## Methods

### 1. Fill Depressions
The **Fill tool** was applied to the DEM to remove artificial sinks.  
Sinks can interrupt modeled water flow, so filling them ensures continuous drainage across the terrain. :contentReference[oaicite:1]{index=1}

### 2. Flow Direction
The **Flow Direction tool** was run on the filled DEM to determine the direction water flows from each raster cell based on the steepest downward slope. :contentReference[oaicite:2]{index=2}

### 3. Flow Accumulation
Using the flow direction raster, the **Flow Accumulation tool** was used to calculate how many upstream cells contribute flow to each location.  
High accumulation values represent drainage paths where water concentrates. :contentReference[oaicite:3]{index=3}

### 4. Pour Points
Pour points were manually created where runoff exits the forest boundary.  
These points represent the outlets used for watershed delineation. :contentReference[oaicite:4]{index=4}

### 5. Snap Pour Point
The **Snap Pour Point tool** was used to move each pour point to the nearest cell with the highest flow accumulation.  
This ensures the watershed boundaries align with the actual drainage network. :contentReference[oaicite:5]{index=5}

### 6. Watershed Delineation
The **Watershed tool** was run using the snapped pour points and the flow direction raster.  
This generated watershed boundaries representing the drainage areas contributing flow to each outlet. :contentReference[oaicite:6]{index=6}

---

## LS Factor Calculation

The LS factor represents the effect of **slope length and slope steepness on erosion potential**.

The LS raster was calculated using Raster Calculator:

