# GTFS Transit Stop & Morning Peak Service Frequency Analysis (QGIS & SQL)

![QGIS](https://img.shields.io/badge/QGIS-3.34_LTR-588240?logo=qgis&logoColor=white)
![Data Standard](https://img.shields.io/badge/Data_Format-GTFS_Schedule-blue)
![CRS](https://img.shields.io/badge/Projection-EPSG%3A3035%20(ETRS89)-003399)

## Project Overview
This repository presents a public transit service frequency analysis for Brussels using General Transit Feed Specification (GTFS) schedule data. 

By executing relational SQL joins across non-spatial GTFS text feeds (`stops.txt`, `stop_times.txt`, `trips.txt`, `calendar.txt`), the pipeline spatializes bus/tram/metro stops, isolates the **Morning Peak Period (07:00 – 09:00 AM)**, calculates hourly departure frequencies, and visualizes service intensity using graduated proportional symbology.

## Objectives
1. **GTFS Relational Ingestion:** Import non-spatial GTFS text files into QGIS and construct spatial point geometries from `stop_lat` / `stop_lon` (`EPSG:4326` reprojected to `EPSG:3035`).
2. **Relational Table Joining:** Link `stops` $\rightarrow$ `stop_times` $\rightarrow$ `trips` $\rightarrow$ `calendar` using unique key identifiers (`stop_id`, `trip_id`, `service_id`).
3. **Temporal Peak Filtering:** Extract transit departures occurring strictly between `07:00:00` and `09:00:00` on a representative weekday.
4. **Frequency & Headway Metrics:** Calculate total morning departures (`departures_count`) and derive average headway spacing (`headway_min = 120 / departures_count`).
5. **Graduated Cartography:** Produce an A3 publication-ready map displaying stop-level transit service density across urban corridors.

---

## GTFS Relational Schema Architecture
