# MODULE-2-End-ASSIGNMENT-Bike-Station-Sharing-Power-BI-Project
Public bike-sharing systems generate continuous data from hundreds of stations across different cities. The task is to analyze this real-time bike station dataset to understand station performance, usage efficiency, and operational patterns across cities.

# 🚲 Bike Station Sharing Power BI Project

## 📌 Project Overview

The **Bike Station Sharing Power BI Project** focuses on analyzing bike-sharing station data to understand **station performance, bike availability, utilization, capacity, and operational status** across different cities or contract areas.

The project uses **Power Query, data modeling, DAX, and interactive Power BI visualizations** to transform raw bike station data into a meaningful and interactive dashboard.

---

## 🎯 Project Objectives

The main objectives of this project are:

* Analyze bike station performance across different cities.
* Understand bike availability and utilization.
* Calculate total bike capacity and used bike capacity.
* Identify high-performing and low-performing stations.
* Analyze bike usage trends over time.
* Monitor station operational status.
* Create an interactive dashboard using Power BI.
* Provide insights that can support bike redistribution and capacity planning.

---

## 📂 Dataset

The dataset contains information about bike-sharing stations and their current availability.

### Main Dataset Columns

* `Number` – Station number
* `Name` – Station name
* `Address` – Station address
* `Position` – Station geographical position
* `Banking` – Banking availability
* `Bonus` – Bonus station indicator
* `Status` – Station operational status
* `Contract name` – City/contract area
* `Bike stands` – Total station capacity
* `Available Bike stands` – Currently available stands
* `Available bikes` – Currently available bikes
* `last update` – Last update date and time
* `date` – Date of observation

---

## 🧹 Data Cleaning and Transformation

Data preparation was performed using **Power Query**.

The following steps were carried out:

* Reviewed the dataset structure.
* Checked and corrected data types.
* Removed unnecessary columns where required.
* Created the **Fact_BikeStation** fact table.
* Created the **Dim_Station** dimension table.
* Created the **Dim_Date** date dimension.
* Removed duplicate station records from the station dimension.
* Created date-related columns such as:

  * Year
  * Month
  * Month Name
  * Quarter
  * Day
  * Day Name

---

## 🏗️ Data Model

A **star-schema-style data model** was created.

### Fact Table

**Fact_BikeStation**

Contains operational bike station measurements such as:

* Station Number
* Bike Stands
* Available Bike Stands
* Available Bikes
* Last Update
* Date

### Dimension Tables

**Dim_Station**

Contains station-related information:

* Station Number
* Station Name
* Address
* Position
* Banking
* Bonus
* Status
* Contract Name

**Dim_Date**

Contains date information:

* Date
* Year
* Month
* Month Name
* Quarter
* Day
* Day Name

### Relationships

The following relationships were established:

```text
Dim_Station[Number]
        ↓
Fact_BikeStation[Number]

Dim_Date[Date]
        ↓
Fact_BikeStation[Date]
```

Both relationships use:

* **Cardinality:** One-to-Many (1:*)
* **Cross-filter direction:** Single
* **Relationship:** Active

---

## 📊 DAX Measures

Several DAX measures were created to calculate important performance indicators.

### Total Bike Capacity

```DAX
Total Bike Capacity =
SUM(Fact_BikeStation[Bike stands])
```

### Total Available Bikes

```DAX
Total Available Bikes =
SUM(Fact_BikeStation[Available bikes])
```

### Total Available Stands

```DAX
Total Available Stands =
SUM(Fact_BikeStation[Available Bike stands])
```

### Used Bikes

```DAX
Used Bikes =
[Total Bike Capacity] - [Total Available Bikes]
```

### Bike Usage Rate

```DAX
Bike Usage Rate =
DIVIDE(
    [Used Bikes],
    [Total Bike Capacity],
    0
)
```

### Bike Availability Rate

```DAX
Bike Availability Rate =
DIVIDE(
    [Total Available Bikes],
    [Total Bike Capacity],
    0
)
```

### Total Stations

```DAX
Total Stations =
DISTINCTCOUNT(Dim_Station[Number])
```

---

## 📈 Dashboard Visualizations

The Power BI dashboard contains several visuals to analyze bike station operations.

### 1. Bike Usage by City

A column chart compares **Used Bikes** across different contract areas/cities.

**Fields:**

* Axis → `Dim_Station[Contract name]`
* Values → `[Used Bikes]`

---

### 2. Station Performance

A bar chart is used to identify stations with higher and lower utilization.

**Fields:**

* Axis → `Dim_Station[Name]`
* Values → `[Used Bikes]`

A **Top 10** filter can be applied to identify the stations with the highest used-bike capacity.

---

### 3. Available vs Used Bikes

A chart compares:

* Total Available Bikes
* Used Bikes

This provides an overview of station capacity utilization.

---

### 4. Usage Trend Over Time

A line chart is used to analyze changes in bike usage over time.

**Fields:**

* Axis → `Dim_Date[Date]`
* Values → `[Used Bikes]` or `[Bike Usage Rate]`

---

### 5. Station Status

A donut or bar chart displays the distribution of stations according to their operational status.

**Fields:**

* Legend → `Dim_Station[Status]`
* Values → `[Total Stations]`

---

### 6. Interactive Slicers

Interactive slicers were added to allow users to filter the dashboard.

Examples include:

* City/Contract Name
* Station Name
* Date
* Station Status
* Year
* Month

The slicers interact with the dashboard visuals through the established data model.

---

## 🔍 Key Insights

The dashboard helps answer important business questions such as:

* Which cities or contract areas have the highest bike utilization?
* Which stations have the highest utilization?
* Which stations have comparatively lower utilization?
* How does available bike capacity compare with used capacity?
* How does bike usage change over time?
* What is the distribution of active and inactive stations?
* Which areas may require better bike redistribution or capacity management?

---

## 💡 Business Value

The analysis can help bike-sharing operators:

* Monitor station performance.
* Identify high-demand locations.
* Identify underutilized stations.
* Improve bike redistribution.
* Optimize station capacity.
* Monitor operational status.
* Improve availability for users.
* Support data-driven operational decisions.

---

## 🛠️ Tools and Technologies

| Tool                  | Purpose                          |
| --------------------- | -------------------------------- |
| **Power BI**          | Dashboard and data visualization |
| **Power Query**       | Data cleaning and transformation |
| **DAX**               | Measures and calculations        |
| **Data Modeling**     | Fact and dimension relationships |
| **Excel/CSV Dataset** | Source data                      |

---

## 📁 Project Structure

```text
Bike-Station-Sharing-PowerBI/
│
├── Dataset/
│   └── bike-stations-sharing-data.xlsx
│
├── PowerBI/
│   └── Bike_Station_Sharing.pbix
│
├── README.md
│
└── Project_Insights.md
```

---

## 📌 Conclusion

The Bike Station Sharing Power BI project successfully transformed raw bike station data into an interactive analytical dashboard.

Through **Power Query**, the data was cleaned and structured. A logical data model containing **Fact_BikeStation, Dim_Station, and Dim_Date** was created, and **DAX measures** were developed to calculate bike capacity, availability, utilization, and usage rates.

The final dashboard provides an easy way to monitor **city-wise usage, station performance, bike availability, usage trends, and station status**. Interactive slicers further improve the usability of the dashboard by allowing users to explore different cities, stations, dates, and operational conditions.

This project demonstrates the practical use of **Power BI for data cleaning, data modeling, DAX calculations, interactive visualization, and business insight generation**.

