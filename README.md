# Project_Mudbrick

This project is part of research that uses a combination of techniques, including Geographic Information Systems (GIS) and spatial proximity analysis, to examine how modern human disturbances affect the preservation of Hellenistic (310-30 BCE)  and Roman (30 BCE – 4th century CE) tombs and graves across Cyprus.

## Research Aims

* Which sites are most exposed to modern disturbances, and how are they spatially distributed across the island?

* Which disturbance category (urban, infrastructure, or agriculture) contributes most to overall risk?

* Are Hellenistic sites more exposed to risk than Roman sites, or vice versa?


# GIS Workflow for the Tombs & Necropoleis Dataset

## Overview

This repository documents the GIS-based workflow developed to analyse modern disturbance around Hellenistic and Roman tombs and necropoleis in Cyprus.

The focus is methodological. It explains how spatial data was processed, transformed, and structured into a comparative dataset using QGIS and Excel. The workflow moves from raw spatial data to percentage-based exposure metrics and finally to a weighted scoring system.

The README does not focus on archaeological interpretation, but on how the digital analytical product was built.

## Coordinate Reference System (CRS)

To ensure consistency and correct spatial analysis, this project must be used with the following Coordinate Reference System (CRS):

**EPSG:32636 — WGS 84 / UTM zone 36N**

All spatial layers, buffers, and calculations were created using this CRS. Using a different CRS may result in:

- Incorrect distance and area calculations  
- Misalignment between layers  
- Inconsistent analysis results

## How to navigate the project

If the goal is to open the GIS project: go to  
GIS > Database > Workspace > Project_Mudbrick_Workspace.qgz  
and open this file in QGIS.

If the goal is to inspect the original raw data: go to  
GIS > Database > Shapefiles > Original_OSM  
or  
GIS > Database > Shapefiles > Original_TN.

If the goal is to inspect the final processed GIS layers: go to  
GIS > Database > Shapefiles > Shp_Reclass_OSM  
and  
GIS > Database > Shapefiles > Shp_T&N.

If the goal is to inspect the buffer-based outputs: go to  
GIS > Database > Shapefiles > Boundary_Radii.

If the goal is to use tabular results: go to  
GIS > Database > Export_Excel  
or  
GIS > Database > Export_CSV.

## Recommended workflow for a new user

Open the main QGIS project from the Workspace folder.  

Check the cleaned Tombs & Necropoleis layer in Shp_T&N.  

Review the reclassified disturbance layers in Shp_Reclass_OSM.  

Review the buffer outputs in Boundary_Radii.  

Use the Excel files in Export_Excel for the final analytical tables.  


## Table Folder Structure

| Folder | Function |
|--------|----------|
| Project_Mudbrick\GIS | Main working database folder containing spatial data, exports, and the QGIS workspace file |
| GIS/Database/Shapefiles/Original_OSM | Original OpenStreetMap shapefiles downloaded before reclassification; archive of raw OSM input data |
| GIS/Database/Shapefiles/Original_TN | Original Tombs & Necropoleis dataset before cleaning and restructuring; archive reference |
| GIS/Database/Shapefiles/Shp_Reclass_OSM | Reclassified OSM-based layers used in the final disturbance model, including agriculture, archaeology, infrastructure, land use, and urban |
| GIS/Database/Shapefiles/Shp_T&N | Cleaned and released Tombs & Necropoleis layer used in the GIS workflow |
| GIS/Database/Shapefiles/Boundary_Radii | Analytical boundary outputs and derived layers for 100 m, 250 m, and 500 m analyses, including designation-wide and GISNo-merged outputs |
| GIS/Database/Export_CSV | CSV exports of GIS attribute tables for checking, transfer, or lightweight spreadsheet use |
| GIS/Database/Export_Excel | Main Excel outputs derived from the GIS workflow, including combined TN risk and final analysis workbooks |
| GIS/Database/Workspace | Contains the QGIS project file; this is the main entry point for the spatial workspace |
| GIS/Metadata_Discriptions | Folder for metadata notes, dataset descriptions, workflow structure, and supporting documentation |
| GIS/Shortcuts | Alias/shortcut files pointing to the most important workspace and spreadsheet outputs for quick access |


## Data Processing, Cleaning, and Analysis

### 1. Source data collection
The workflow started with the collection of the Tombs & Necropoleis dataset and the OpenStreetMap-based modern disturbance layers for Cyprus. The archaeological dataset provided the site records, while the OpenStreetMap layers provided the modern land-use and infrastructure information used to model present-day disturbance.

### 2. Data standardisation in QGIS
All main layers were imported into QGIS and checked for geometry, attribute structure, and coordinate reference system. The archaeological layer was standardised so that the main identifiers, especially SerialNo and GISNo, could be used consistently in joins, exports, and later aggregation steps. All working layers were harmonised to EPSG:32636 (WGS 84 / UTM Zone 36N).

### 3. Reclassification of disturbance data
The OpenStreetMap-derived layers were reclassified into three main disturbance categories: Urban, Infrastructure, and Agriculture. Non-built land-cover classes such as forest, scrub, and water were excluded.

### 4. Preparation of thematic layers
Separate thematic layers were created for urban, agriculture, and infrastructure. Infrastructure data were converted from lines into polygons to allow area-based calculations.

### 5. Buffer generation
Three buffer distances were created around each site: 100 m, 250 m, and 500 m. These buffers represent different spatial scales of disturbance.

### 6. Overlay and intersection
Buffers were intersected with the disturbance layers using QGIS tools such as Intersection, Merge Vector Layers, and Join Attributes by Field/Value.

### 7. Area calculation
The area of intersected polygons and total buffer areas were calculated in square metres using the Field Calculator.

### 8. Percentage measurement workflow
Percentages were calculated using the formula:  
percentage = (class area within buffer / total buffer area) × 100  

This process was repeated for all buffers and sites. A residual category called not_classified was added to represent uncovered areas.

### 9. Tabular export and Excel preparation
Outputs were exported to CSV and Excel, preserving identifiers for further comparison.

### 10. Merging duplicate location records
Duplicate records were merged using GISNo to create a cleaner dataset for location-based analysis.

### 11. Data cleaning
Data cleaning was performed in Excel. Sites classified as "clearly urban" and "strongly developed/semi-urbanized" were removed to reduce bias and focus on sites not yet heavily impacted by urbanisation.

### 12. Final digital outputs
Final outputs include QGIS project files, shapefiles, GeoPackages, and Excel workbooks containing analytical results.


## Risk Classification (Website)

Risk classification was derived from the Multi-Criteria Analysis (MCA) points score calculated for each site.

Percentages of disturbance types within buffers (100 m, 250 m, 500 m) were used as input.

Weights applied:
- Agriculture = ×1  
- Infrastructure = ×2  
- Urban = ×3  

Formula:
(Agriculture % × 100 × 1) + (Infrastructure % × 100 × 2) + (Urban % × 100 × 3)

The scores were averaged across the three buffer distances to reduce variability.

Thresholds:
- < 74 → Below Median Risk  
- 74 – 99 → Above Median Risk  
- > 99 → Strongly Above Median Risk  

The median value (74) was used as the reference point.

This classification allows:
- Comparison between sites  
- Identification of higher-risk locations  
- Clear visualisation in maps and datasets  

Note: This classification reflects relative exposure to disturbance, not confirmed damage.

The workflow is reproducible and suitable for further analysis and web visualisation.

