# Historical Airplane Crash Insights

## Project Overview

This repository contains documents and resources that provide a **data-driven analysis of historical aviation accidents**, crash patterns, and fatalities over time.

The project was carried out using **Power Query** for data transformation and **Power BI** for visualizing insights.  
It also involved the use of **DAX** for calculations and logical measures.

Geographic coordinates (latitude and longitude) for cities were retrieved using **nominatim.openstreetmap.org** to enable accurate flight route mapping.

---

## Tools Used

- **Power Query** — data transformation and cleaning  
- **Power BI** — dashboard creation and visualization  
- **DAX** — calculated measures and analytics  

---

## Project Goal

The primary goal of this project is to **analyze historical airplane crash data** and visualize insights through an **interactive Power BI dashboard**.

### Analytical Visuals

1. Plot of all recorded flight routes  
2. Aircraft types involved in the most crashes  
3. Lives lost per year vs survivors per year  
4. Locations with the most crashes and lives lost  
5. Operators involved in the highest loss of lives  

### Summary Metrics

1. Total number of airplane crashes  
2. Total passengers onboard  
3. Total onboard fatalities  
4. Total ground fatalities  
5. Total survivors  
6. Number of operators involved  
7. Unique aircraft types  
8. Unique crash locations  

---

## Features

- Three-page **interactive Power BI dashboard**
- Slicers for:
  - Operator
  - Year
  - Location
  - Aircraft Type
- Toggle buttons for **Lives Lost / Survivors**
- Page navigation buttons
- Separate file containing all **DAX formulas**

---

## Data

### Raw Dataset

Airplane Crashes and Fatalities Dataset:  
https://github.com/ifioklee/Airplane-Crashes-and-Fatalities/tree/main/Airplane%20Crashes%20and%20Fatalities/Dataset

### Power BI Dashboard

Interactive Power BI file:  
https://github.com/ifioklee/Airplane-Crashes-and-Fatalities/blob/main/Airplane%20Crash%20and%20Fatalities.pbix

---

## Technical Details

### Data Preparation & Transformation (Power Query)

#### Airplane_Crashes_and_Fatalities Table

Transformations applied:

- Removed index and summary columns
- Removed empty Route rows
- Removed flights related to:
  - demonstration
  - bombing run
  - instructional flight
  - military exercise
  - sightseeing
  - test / testing
  - training flights
- Split Route column into:
  - Route.1, Route.2, Route.3, Route.4
- Created **Destination** column using last non-null route:

        List.Last(
            List.RemoveNulls({[Route.1],[Route.2],[Route.3],[Route.4]})
        )

- Renamed Route.1 to **Origin**
- Removed Route.2–Route.4
- Extracted city names from Origin and Destination
- Removed empty rows from:
  - Location
  - Operator
  - Type
  - Aboard, Fatalities, Ground
- Removed Registration, Time, Flight Number columns
- Created **Survivor** column
- Extracted **Month Name** and **Year** from Date

---

### Geocoding (Latitude & Longitude)

Latitude and longitude were retrieved using the **Nominatim OpenStreetMap API**.

**Origin Coordinates**

        Json.Document(
            Web.Contents(
                "https://nominatim.openstreetmap.org/search?format=json&q=" & [Origin]
            )
        )

**Destination Coordinates**

        Json.Document(
            Web.Contents(
                "https://nominatim.openstreetmap.org/search?format=json&q=" & [Destination]
            )
        )

Coordinates were extracted and used for route map visualization.

---

## Visualizations in Power BI

### Page 1
- KPI cards:
  - Total crashes
  - Passengers onboard
  - Lives lost onboard
  - Lives lost on ground
  - Survivors
- Clustered column chart:
  - Lives lost per year
  - Survivors per year (toggle buttons)
- Stacked bar chart:
  - Top 10 crashes vs lives lost
- Slicers:
  - Operator
  - Year
- Navigation buttons to Pages 2 & 3

---

### Page 2
- KPI cards:
  - Operators
  - Aircraft types
  - Unique crash locations
- Clustered bar charts:
  - Aircraft type vs lives lost
  - Operator vs lives lost
- Slicers:
  - Operator
  - Year
- Navigation buttons to Pages 1 & 3

---

### Page 3
- Route map visual showing flight movement
- Slicers:
  - Operator
  - Location
  - Year
- Navigation buttons to Pages 1 & 2

---

## Results & Insights

- **58,343** airplane crashes recorded
- **1,604,419** passengers onboard
- **1,087,163** passenger fatalities
- **517,256** survivors
- **131,432** ground fatalities
- **1972** recorded the highest fatalities (**45,434**)
- **Chita, Siberia (Russia)** had the highest lives lost by location
- **Aeroflot** recorded the highest fatalities by operator
- **Douglas DC-3** was the aircraft type with the highest fatalities

---


