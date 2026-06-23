# Supply Chain Risk & Predictive Inventory Intelligence Dashboard

## 📊 Project Overview
This repository contains an enterprise-ready Business Intelligence and Data Science portfolio project focused on identifying operational risk, capital exposure, and supplier logistics volatility. 

Instead of treating supply chain data as a flat log, this project implements a robust **Star Schema data model** in Power BI to monitor financial exposure and predict systemic delivery delays. Built utilizing a dark-mode UI customized for executive decision-making, it allows a Chief Procurement Officer (CPO) or VP of Supply Chain to isolate operational bottlenecks in seconds.

### 🔗 Key Features Demonstrated:
* **Data Modeling:** Implementation of a proper Star Schema with 1-to-Many relational integrity.
* **Advanced DAX:** Context modification (`CALCULATE`), data science variance measures (`STDEV.P`), and time-intelligence moving averages.
* **Root-Cause Exploration:** Dynamic Decomposition Tree architectures for drilling down into regional delivery failures.
* **UX/UI Optimization:** Context-aware, custom Report Page Tooltips and a responsive horizontal slicing banner.

---

## 🖥️ Executive Interface & Visual Interface

### Page 1: Executive Operations Summary
![Executive Operations Dashboard](Supply Chain Risk & Predictive Inventory Intelligence Dashboard/Summary-Supply-Chain-Risk-Analysis-Page1.png)

### Page 2: Root-Cause Supplier Risk Deep-Dive
![Supplier Risk Decomposition Tree](Supply Chain Risk & Predictive Inventory Intelligence Dashboard/Details-Supply-Chain-Risk-Analysis-Page2.png)

---

## 🛠️ Data Architecture & Star Schema
The architecture separates messy transaction data into optimized dimension tables and a centralized transaction log, reducing query processing times and eliminating data redundancy.

* **`Fact_Inventory_Movements`**: Tracks quantities ordered, items sold, transactional IDs, and actual delivery lead times.
* **`Dim_Products`**: Contains specific component metadata, catalog classification, and localized unit costs.
* **`Dim_Suppliers`**: Stores partner registries, procurement regions, and contractual lead time obligations.
* **`Dim_Calendar`**: A dedicated, marked calendar time-intelligence dimension mapping chronological time, weekend flags, and month numbers.

---

## 🔢 Key DAX Calculations & Advanced Logic

### 1. Capital Exposure (Total Inventory Value)
Iterates through transactional allocations to calculate real-time capital tied up in warehouse stock.
```dax
Total_Inventory_Value = 
SUMX(
    Fact_Inventory_Movements,
    Fact_Inventory_Movements[Quantity_Ordered] * RELATED(Dim_Products[Unit_Cost])
)
```

### 2. Supply Volatility Anomaly Detection (Lead Time Standard Deviation)
A predictive data science metric highlighting the unreliability and variance of delivery channels. Higher variance signals higher logistical risk.
```dax 
Lead_Time_Standard_Deviation = STDEV.P(Fact_Inventory_Movements[Actual_Lead_Time_Days]) 
```

### 3. Chronological Forecast Baseline (Rolling 3-Month Average Demand)
Smoothes monthly procurement spikes to generate an active baseline indicator for demand planning.
```dax 
Rolling_3M_Demand = 
AVERAGEX(
    KEEPFILTERS(VALUES(Dim_Calendar[Month_Name])),
    CALCULATE(SUM(Fact_Inventory_Movements[Quantity_Sold]))
)
```
---

## 💡 Core Business Insights Discovered

* **`The Outlier Bottleneck`**: The Financial Exposure Matrix isolated a severe anomaly where a single supplier, Zenith Micro Electronics, consistently averaged a 19-day delivery timeline against an industry-standard baseline.
* **`Financial Exposure Risk`**: The data revealed that this single high-risk supplier accounts for over $4.4M in tied-up capital, exposing the business to major cash-flow vulnerabilities and critical dependencies.

* **`Regional Vulnerability`**: Root-cause branching via the Decomposition Tree proved that logistics failures are highly concentrated in the East Region, specifically bottlenecking the procurement of high-priority component categories.


