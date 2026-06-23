# Supply Chain Risk & Predictive Inventory Intelligence Dashboard

## 📊 Project Overview
This repository contains an enterprise-ready Business Intelligence and Data Science portfolio project focused on identifying operational risk, capital exposure, and supplier logistics volatility. 

Instead of treating supply chain data as a flat log, this project implements a robust **Star Schema data model** in Power BI to monitor financial exposure and predict systemic delivery delays. Built utilizing a dark-mode UI customized for executive decision-making, it allows a Chief Procurement Officer (CPO) or VP of Supply Chain to isolate operational bottlenecks in seconds.

### 🔗 Key Features Demonstrated:
*   **Data Modeling:** Implementation of a proper Star Schema with 1-to-Many relational integrity.
*   **Advanced DAX:** Context modification (`CALCULATE`), data science variance measures (`STDEV.P`), and time-intelligence moving averages.
*   **Root-Cause Exploration:** Dynamic Decomposition Tree architectures for drilling down into regional delivery failures.
*   **UX/UI Optimization:** Context-aware, custom Report Page Tooltips and a responsive horizontal slicing banner.

---

## 🛠️ Data Architecture & Star Schema
The architecture separates messy transaction data into optimized dimension tables and a centralized transaction log, reducing query processing times and eliminating data redundancy.

*   **`Fact_Inventory_Movements`**: Tracks quantities ordered, items sold, transactional IDs, and actual delivery lead times.
*   **`Dim_Products`**: Contains specific component metadata, catalog classification, and localized unit costs.
*   **`Dim_Suppliers`**: Stores partner registries, procurement regions, and contractual lead time obligations.
*   **`Dim_Calendar`**: A dedicated, marked calendar time-intelligence dimension mapping chronological time, weekend flags, and month numbers.

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
