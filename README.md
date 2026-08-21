# 🚕 Route Analysis with Databricks, Lakeflow Pipelines & Power BI

## Overview

Route Analysis is an end-to-end data engineering and analytics project built with Databricks, Spark Declarative Pipelines (Lakeflow), GitHub, and Power BI.

The project combines NYC Taxi trip data with external public datasets such as weather information, public holidays, and city events to generate business insights about transportation demand, route popularity, revenue generation, and environmental influences.

The goal is to demonstrate modern data engineering best practices including:

- Databricks Asset Bundles
- Spark Declarative Pipelines (Lakeflow)
- Delta Lake Medallion Architecture
- API Data Ingestion
- CI/CD with GitHub
- Power BI Reporting
- Data Modeling and Analytics

---

# Project Objectives

The project aims to answer questions such as:

- Which NYC areas generate the highest taxi demand?
- Which routes generate the most revenue?
- How does weather affect taxi demand?
- What are the busiest hours and days of the week?

---

# Possible Extensions
- Do public holidays influence trip volume?
- Do major events create transportation spikes?

---
# Repository Structure

```text
route-analysis/
│
├── databricks.yml
│
├── resources/
│   └── pipeline.yml
│
├── src/
│   ├── bronze/
│   │   ├── dwh_datum.ipynb
│   │   ├── dwh_nyc_taxi.ipynb
│   │   ├── dwh_nyc_taxi_payment.ipynb
│   │   ├── dwh_nyc_taxi_rate.ipynb
│   │   ├── dwh_nyc_taxi_zone.ipynb
│   │   └── dwh_nyc_weather.ipynb
│   │
│   ├── gold/
│   │   ├── datum.ipynb
│   │   ├── trips.ipynb
│   │   ├── weather.ipynb
│   │   └── zones.ipynb
│   │
│   ├── silver/
│   │   ├── calendar_stm_datum.ipynb
│   │   ├── geographics_stm_zone.ipynb
│   │   ├── payment_stm_payment.ipynb
│   │   ├── payment_stm_rate.ipynb
│   │   ├── trips_trn_trips.ipynb
│   │   └── weather_stm_weather.ipynb
│   │
│   └── testing/
│       ├── Testing Sample Data.ipynb
│       └── Testing with Spark SQL.ipynb
│
├── powerbi/
│   └── RouteAnalysis/
│       ├── RouteAnalysis.pbip
│       │
│       ├── RouteAnalysis.Report/
│       │   ├── definition.pbir
│       │   ├── .platform
│       │   ├── StaticResources/
│       │   └── definition/
│       │
│       └── RouteAnalysis.SemanticModel/
│           ├── .platform
│           ├── definition.pbism
│           ├── diagramLayout.json
│           ├── .pbi/
│           └── definition/
│
├── docs/
│   ├── NYC Taxi.jpg
│   ├── zones.geojson
│
├── .gitignore
└── README.md
```
---

# Architecture

```text
                  +-------------------+
                  |      GitHub       |
                  +---------+---------+
                            |
                            v
                  +-------------------+
                  | Databricks Bundle |
                  +---------+---------+
                            |
           +----------------+----------------+
           |                                 |
           v                                 v
+----------------------+      +----------------------+
| NYC Taxi Data        |      | External APIs        |
| TLC Trip Records     |      | Weather              |
+----------+-----------+      +----------+-----------+
           |                             |
           |                             |
           +-------------+---------------+
                         |
                         v
              +--------------------+
              | Lakeflow Pipeline  |
              | Bronze / Silver /  |
              | Gold Layers        |
              +---------+----------+
                        |
                        v
               +------------------+
               | Delta Tables     |
               +--------+---------+
                        |
                        v
               +------------------+
               | Power BI Report  |
               +------------------+
```

---

# Main Data Source

## NYC Taxi Data

Primary dataset used throughout the project.

### Relevant Attributes

| Column | Description |
|----------|----------|
| tpep_pickup_datetime | Pickup timestamp |
| tpep_dropoff_datetime | Dropoff timestamp |
| passenger_count | Number of passengers |
| trip_distance | Distance traveled |
| fare_amount | Base fare |
| total_amount | Total trip payment |
| PULocationID | Pickup location |
| DOLocationID | Dropoff location |

---
# Power BI Dashboard

## Page 1 - Executive Overview

### KPI Cards

- Total Trips
- Total Revenue
- Average Fare
- Average Trip Distance
- Average Trip Duration

### Trend Visuals

- Daily Trip Volume
- Daily Revenue
- Revenue by Day of Week

---

## Page 2 - Route Analysis

### Map Visual

Display:

- Pickup Locations
- Dropoff Locations

Pie Chart Size:

- Trip Volume

Pie Chart Color:

- Revenue

### Top Routes Table

| Metric |
|----------|
| Pickup Zone |
| Dropoff Zone |
| Amount Passangers |
| Revenue |

---

## Page 3 - Weather Impact

### KPIs

- Trips During Rain
- Trips During Clear Weather
- Average Revenue by Weather Type

### Visuals

- Rainfall vs Trip Count
- Temperature vs Revenue
- Weather Category Comparison

---



