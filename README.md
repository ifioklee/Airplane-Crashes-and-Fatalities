# Historical Airplan Crash Insights

## Project Overview
This repository contains documents and resources that gives data-driven overview of aviation accidents, crash patterns, and fatalities across time.

The project was carried out using **Power Query** for data transformation and **Power BI** for visualizing insights.  
It also involved the use of **DAX** for calculations and logical measures.
nominatim.openstreetmap.org was used to pull latitude and logitude data of cities that were used in plot the flight route map

### Tools Used
- Power Query — data transformation  
- Power BI — dashboard creation and visualization  
- DAX — calculated measures and analytics  

---

## Project Goal
The primary goal of this project is to analyse these historical airplane crash data and visulize insight derived on an interactive dashboard.

The final **Interactive dashboard** shows:

1. A plot of all flight routes
2. Analysis of what type of aircraft is involved in most crashes
3. Number of lives lost per year and number of airplan crashe survivors per year
4. Locations with most airplane crash and comparison of the number of lives lost in these location
5. Analysis of airplane of operators involved in most lost of lives.

The dashboard also shows information:

1. Total number of airplan crash
2. Total number of passengers onboard these airplane
3. Total number of lives of those onboard lost in these crashes
4. Total number of lives lost onground as a result of these crash
5. Total number of survivors
6. Number of operators who owned aircraft that crashed
7. Unique Number of aircraft types involved in these crash
8. Total number of unique location of these airplane crash

---

## Features
- A three page Interactive **Power BI dashboard** with slicers (Operator, Year, Location and Aircraft type)
- The first page of the the dashboard includes buttons( Lives lost and Survivors) which are used to switch between views of visuals of number of lives lost per year and number of survivors per year
- There are also navigation buttons on each page that helps navigate to different pages of the dashboard
- Includes a file containing all **DAX formulas** used in the report  

---

## Data

### Raw Dataset
The original dataset used for this analysis can be found in the folder below:

- **Bank and Customer Churn Dataset Folder:**  
  [Download Here](https://github.com/ifioklee/Airplane-Crashes-and-Fatalities/tree/main/Airplane%20Crashes%20and%20Fatalities/Dataset)

### DAX Scripts
This file contains all the DAX formulas used in this analysis:  
[View DAX Formula Script](#)

### Visualization
Interactive Power BI dashboard:  
[View Power BI Dashboard](https://github.com/ifioklee/Airplane-Crashes-and-Fatalities/blob/main/Airplane%20Crash%20and%20Fatalities.pbix)

### README Documentation
Full project documentation:  
[View README File](#)

---

## Technical Details

### Data Preparation & Transformation (Power Query)

### Airplane_Crashes_and_Fatalities Table
 - Remove the index column
 - Remove the summary column
 - Remove empty rows from the Route column
 - Remove all flight with "demostration, bombingrun, instructional flight, military exercise, sightseeing, test flight, test, testing,training, training exercise, training flight"
 - Split route column by delimitter to have columns Route.1, Route.2, Route.3, Route.4
 - Add new custom column called "destination" derived as the last non-null column using this: = List.Last(List.RemoveNulls({[Route.1],[Route.2],[Route.3],[Route.4]}))
 - Rename Route.1 column to Origin
 - Remove Route.2, Route.3, Route.4 columns
 - Split the Origin column by delimitter to have only the name of the city
 - Do the same for destination column
 - Remove empty rows in location column
 - Remove empty rows drom operator column
 - Remove empty rows from type column
 - Remove registration column
 - Remove empty rows from aboard, fatalities and ground columns
 - Get latitude and logitude value for cities in the origin and destination columns using an Api from nominatim.openstreetmap.org. this is done by creating a custom column with the code = Json.Document(
    Web.Contents(
        "https://nominatim.openstreetmap.org/search?format=json&q=" & [Origin]
    )
) for Origin colum and = Json.Document(
    Web.Contents(
        "https://nominatim.openstreetmap.org/search?format=json&q=" & [Destination]
    )
) column

- Select Latitude and Logitude
- Remove Time and Flight number columns
- Create Survivor column using custom column function
- Create a Month Name and Year Columns by extracting from date column



All transformations were then loaded into **Power BI**.

---

## Visualizations in Power BI

---

## Results & Insights

