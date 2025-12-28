# 🗺️ Sydney Urban Resource Intelligence: Spatial Data Analytics

[![Python](https://img.shields.io/badge/Python-3.8%2B-blue)](https://www.python.org/)
[![PostgreSQL](https://img.shields.io/badge/PostgreSQL-PostGIS-336791)](https://www.postgresql.org/)
[![Status](https://img.shields.io/badge/Status-Completed-success)]()

## 📖 Overview
**Project Focus:** Geospatial Analysis, ETL Pipeline, Scoring Algorithms, Urban Planning.

This project implements a **Spatial Data Analytics System** to evaluate the "Resource Adequacy" of different regions (SA2) across Greater Sydney. By integrating heterogeneous data—ranging from demographic census data to infrastructure points-of-interest (POIs)—the system quantifies how well-serviced a community is relative to its population and income levels.

> **Business Context:** The methodology developed here (Spatial Joins, Catchment Analysis, Z-Score Indexing) is directly transferable to **Retail Site Selection**, **Competitor Density Analysis**, and **Supply Chain Network Planning**.

---

## 🛠️ Tech Stack & Architecture

The project follows a rigorous Data Science lifecycle:

* **Data Collection (ETL):** Python (`requests`, `json`)
* **Data Manipulation:** Python (`pandas`, `geopandas`)
* **Spatial Database:** PostgreSQL with **PostGIS** extension
* **Visualization:** Matplotlib, Seaborn, QGIS (for final map rendering)

---

## 🚀 Key Technical Implementation

### 1. Automated Data Injection & Cleaning (ETL)
Developed a robust Python script to harvest data from the **NSW Government Open Data API**, handling **50,000+** Point-of-Interest (POI) records.

* **API Strategy:** Implemented a looping mechanism with `time.sleep()` strategies to ensure complete data extraction without triggering API rate limits.
* **Data Cleaning & CRS Alignment:** * Addressed **Coordinate Reference System (CRS)** inconsistencies by re-projecting raw API data (EPSG:4326) to match the SA2 administrative boundary shapefiles (GDA2020).
    * Filtered out "Ghost Data" (null geometries) and corrected coordinate offsets to ensure spatial accuracy for downstream analysis.

### 2. Spatial Database Engine (PostGIS Optimization)
Instead of relying solely on in-memory processing, I utilized **PostgreSQL** for scalable spatial queries.

* **Spatial Indexing (Core Competency):** Implemented **GIST (Generalized Search Tree) Indexing** on the geometry columns. This reduced the query time for spatial joins (`ST_Within`, `ST_Intersects`) on the 50k+ dataset from minutes to milliseconds, ensuring scalability.
* **Complex Spatial Joins:** Mapped specific facilities to their administrative boundaries (SA2) with high precision to calculate service density.

### 3. The "Resource Adequacy" Scoring Model
To fairly compare regions with vastly different population densities, I designed a weighted scoring algorithm:

$$Final Score = \sigma(\sum_{i=1}^{n} w_i \cdot Z(x_i))$$

* **Z-Score Normalization:** Standardized metrics (e.g., "Schools per 1,000 residents") to handle different data scales.
* **Sigmoid Transformation:** Applied a Sigmoid function to dampen the impact of extreme outliers (e.g., the CBD area), ensuring a balanced scoring distribution.

---

## 📊 Visual Insights & Strategic Observations

*(Note: Please refer to the `plots/` folder for high-resolution images)*


### 📍 Insight 1: Spatial Inequality across Multiple Regions
To understand the resource distribution, I analyzed three key strategic areas in Greater Sydney:

#### 1. Inner West (Saturated Resource Hub)
<p align="center">
  <img src="plots/Well-Resourced Score in (Inner West).png" width="80%" alt="Inner West Map">
</p>
*Highly concentrated resources correlating with established urban density.*

#### 2. Blacktown (High Growth, Infrastructure Lag)
<p align="center">
  <img src="plots/resource score heatmap(blacktown).png" width="80%" alt="Blacktown Map">
</p>
*Identified as a "Resource Desert" where infrastructure development hasn't kept pace with rapid population growth.*

#### 3. Regional Code 125 Area (Developing Corridors)
<p align="center">
  <img src="plots/well resourced score code start with 125.png" width="80%" alt="Code 125 Map">
</p>
* **Observation:** The analysis revealed a distinct "East-West Divide." The Inner West regions exhibit a high concentration of resources, correlating with established urban density.
* **Strategic Implication:** In contrast, rapid-growth corridors like **Blacktown** show a significant "Infrastructure Lag"—high population growth but disproportionately low resource scores. For a retail business, these "underserved" high-growth areas represent **prime greenfield expansion opportunities** compared to the saturated Inner West market.


### 📍 Insight 2: Multi-Regional Correlation Analysis
To validate the consistency of the scoring model, I conducted Pearson correlation analysis for each study area to explore the relationship between infrastructure indicators and the final resource score.

#### 1. Inner West Correlation Matrix
<p align="center">
  <img src="plots/Correlation Matrix of Score Components(Inner West).png" width="60%" alt="Inner West Matrix">
</p>

#### 2. Blacktown Correlation Matrix
<p align="center">
  <img src="plots/correlation between indicators and final score(blacktown).png" width="60%" alt="Blacktown Matrix">
</p>

#### 3. Regional Code 125 Correlation Matrix
<p align="center">
  <img src="plots/correlation matrix code start with 125.png" width="60%" alt="Code 125 Matrix">
</p>

> **Strategic Finding:** Across all regions, a consistent positive correlation was observed between transport accessibility and business density, though the strength varied, reflecting the diverse urban maturity levels of Greater Sydney.
* **Observation:** A moderate positive correlation ($r \approx 0.46$) exists between median income and resource scores.
* **Deep Dive:** While affluent areas generally enjoy better services, outliers exist. Several "High Income / Low Resource" pockets were identified. These specific SA2 regions suggest a market gap where high purchasing power is not met with adequate commercial or service coverage—an ideal target for **premium product positioning**.

---

## 💻 How to Run

1. **Clone the repository**
   ```bash
   git clone https://github.com/KyrieChen3372/Spatial-Data-Analytics-of-Sydney-Resource-Adequacy.git
   cd Spatial-Data-Analytics-of-Sydney-Resource-Adequacy
   ```
2.  **Install dependencies**
    ```bash
    pip install pandas geopandas sqlalchemy psycopg2 matplotlib
    ```
3.  **Database Setup**
    * Ensure PostgreSQL is running with PostGIS extension enabled.
    * Run the SQL setup script to create tables and **build GIST indexes**.
4.  **Run the ETL pipeline**
    ```bash
    python src/data_loader.py
    ```

---

## 💡 Competency Mapping

| Technical Skill Used | Business Application (e.g., for LEGO) |
| :--- | :--- |
| **GIST Spatial Indexing** | Handling massive logistics/store datasets efficiently |
| **CRS Transformation** | Accurate calculation of delivery radiuses & catchment areas |
| **SA2 Regional Analysis** | **Sales Territory Planning** & Market Segmentation |
| **Z-Score Scoring Model** | **Store Performance Grading** & Customer Potential Indexing |

---

## 📝 License
This project is for educational purposes as part of the DATA2001 course at the University of Sydney.
---

## 👥 Contributors
This project was developed as a collaborative effort for the **DATA2001** course at the **University of Sydney**.
* **Zelin Chen SID530333591** - Lead Developer**: Responsible for architecture,PostGIS optimization, Analysis for Parramatta/Code 125 and report writing.
* **SID540028959** - Inner West area Data Analysis & Visualization & analysis
* **SID540234273** - Blacktown Data Analysis & Visualization & analysis 
