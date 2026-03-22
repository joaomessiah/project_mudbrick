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

## Methodological Approach

The workflow is based on an exposure model. It measures the proportion of modern land use surrounding archaeological locations rather than attempting to quantify direct physical destruction.

A buffer-based approach was used due to variable spatial precision in the archaeological dataset. Multiple radii (100 m, 250 m, 500 m) provide a more robust representation of site surroundings.

Three main disturbance domains were defined:

* Urban
* Infrastructure
* Agriculture

## Data Sources

* Tombs & Necropoleis dataset
* OpenStreetMap (OSM) vector data

## Project Structure

The GIS project was organised to support iterative work and reproducibility:

* QGIS workspace versions (V1–V6)
* GeoPackage as main storage format
* Structured folders for spatial data, Excel outputs, and documentation

Core layers include TN points, land-use layers, infrastructure, buffers, and outputs.

## OpenStreetMap Reclassification

OSM data was simplified into:

* Urban
* Infrastructure
* Agriculture

Other classes (forest, water, scrub) were excluded from analysis.

## Spatial Preprocessing

* CRS harmonisation
* Geometry and attribute consistency
* Infrastructure converted from line to polygon
* Visual validation in QGIS

## GIS Processing Workflow

1. Prepare TN points with unique IDs
2. Create buffers (100 m, 250 m, 500 m)
3. Prepare land-use layers
4. Intersect buffers with land-use
5. Calculate class areas
6. Convert to percentages
7. Export to Excel

## Buffer Design

* 100 m: immediate surroundings
* 250 m: intermediate context
* 500 m: broader landscape

## Percentage Calculation

% class = (class area / total buffer area) × 100

## Additional Category

* not_classified: represents unclassified buffer area

## Excel Data Structure

* Wide-format tables (one row per site)
* Separate outputs per buffer
* Merged site-level dataset

Dataset reduced from 940 records to 312 cleaned sites.

## Multi-Criteria Analysis

Weights:

* Agriculture × 1
* Infrastructure × 2
* Urban × 3
* Others × 0

Points formula:

Points = (Agri × 100 × 1) + (Infra × 100 × 2) + (Urban × 100 × 3)

Max = 300 points

## Data Cleaning

* Highly urban sites removed at 100 m
* 127 sites excluded
* Final dataset: 312 sites

## Urbanisation Categories

* > 60%: clearly urbanized
* 40–60%: strongly developed
* 20–40%: moderately developed
* 10–20%: limited
* < 10%: not urbanized

## Risk Categories

* < 74: below median
* 74–99: above median
* > 99: strongly above median

## Key Findings

* Most sites exposed to risk factors within 250 m and 500 m
* Agriculture is the dominant factor by surface area
* Sites mainly located in peri-urban zones
* Limited chronological differences

## Limitations

* Spatial uncertainty (±100 m)
* OSM data from 2016
* No direct measurement of destruction
* No preservation measures considered

## Output

* GIS layers (buffers, intersections)
* Excel datasets (percentages, scores)

The workflow is reproducible and suitable for further analysis and web visualisation.

