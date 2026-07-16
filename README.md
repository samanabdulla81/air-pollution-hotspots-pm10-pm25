# air-pollution-hotspots-pm10-pm25
Geospatial analysis identifying PM10 and PM2.5 air pollution hotspots using QGIS and EXCEL based on spatial interpolation and hotspot detection techniques.
This project maps and analyzes PM10 and PM2.5 air pollution levels across [YOUR CITY/REGION NAME] to identify pollution hotspots. Raw monitoring station data was extracted, cleaned in Excel, and then processed and visualized in QGIS using spatial interpolation and hotspot analysis techniques. The final output highlights zones with the highest particulate matter concentration, supporting environmental awareness and public health planning.


 Objectives
Identify spatial patterns and hotspots of PM10 and PM2.5 concentrations.
Understand which areas within Jharkhan experience the worst air quality.
Provide a clear, visual, reproducible workflow from raw data to final map.



Repository Structure
air-pollution-hotspots-pm10-pm25/
├── data/
│   ├── raw/                  # Original, unedited data files (as downloaded)
│   ├── cleaned/               # Cleaned data ready for QGIS (Excel/CSV)
├── qgis_project/
│   └── air_quality_map.qgz    # Main QGIS project file
├── maps/
│   ├── pm10_hotspots.png
│   └── pm25_hotspots.png
├── scripts/                    # (Optional) Python scripts used for automation
├── README.md
└── .gitignore


 Data Source


Source: CPCB (Central Pollution Control Board), state pollution monitoring stations
Parameters used: PM10 (µg/m³), PM2.5 (µg/m³)
Spatial coverage: 1000 monitoring stations across Jharkhan
Format received: [CSV / Excel / API export]








 Data Cleaning Process (Excel)

The raw data required cleaning before it could be used for spatial analysis. Steps taken in Excel:


Consolidation

Combined multiple raw files  into a single master sheet using copy-paste / Power Query.
Standardized column headers (Station_Name, Latitude, Longitude, Date, PM10, PM2.5).



Handling Missing Values

Identified missing/blank readings using COUNTBLANK() and conditional formatting.
Removed rows with more than [X]% missing data, or interpolated small gaps using average of adjacent readings.



Removing Duplicates & Errors

Used Remove Duplicates to eliminate repeated station entries.
Flagged and removed unrealistic outlier values ( using conditional formatting and manual review.



Unit Standardization

Verified all PM10/PM2.5 values were in consistent units (µg/m³) across all sources.



Aggregation

Calculated average PM10 and average PM2.5 per station over the study period using AVERAGEIFS().
Created a final summary table: one row per monitoring station with average pollutant values and coordinates (Latitude/Longitude).



Export

Saved the cleaned summary table as data/cleaned/station_summary.csv — this is the file imported into QGIS.






.




 Map Building Process (QGIS)


Importing Data

Opened QGIS and added station_summary.csv as a Delimited Text Layer, using Longitude/Latitude fields to plot station points.
Set the correct CRS (Coordinate Reference System): [EPSG:4326 – WGS 84] for input, reprojected to [ EPSG:32643 – UTM Zone 43N] for accurate distance-based analysis.



Base Map

Added a base map (OpenStreetMap / Google Satellite via QuickMapServices plugin) for geographic context.
Added an administrative boundary shapefile of Jharkhan for reference.



Spatial Interpolation

Used [IDW (Inverse Distance Weighting) / Kriging] interpolation (Processing Toolbox → Interpolation) to estimate PM10 and PM2.5 values across the entire study area based on point station readings.
Generated continuous raster surfaces for PM10 and PM2.5.



Hotspot Analysis

Applied [Getis-Ord Gi / Kernel Density Estimation]* to identify statistically significant hotspots (high-concentration clusters) vs. cold spots.
Classified output into categories: Low, Moderate, High, Very High pollution zones.







Layout & Export

Built a print layout in QGIS with: title, legend, north arrow, scale bar, and data source note.
Exported final maps as PNG images to maps/pm10_hotspots.png and maps/pm25_hotspots.png.













 Tools & Technologies Used


QGIS  — spatial analysis & mapping
Plugins:  QuickMapServices, Heatmap, Semi-Automatic Classification Plugin
Microsoft Excel — data cleaning, aggregation

