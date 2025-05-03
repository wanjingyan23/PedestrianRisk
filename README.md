# 🚦 San Diego Traffic Accident Analysis (2018–2024)

This project investigates how weather conditions, road infrastructure, and socioeconomic factors influence traffic accidents in San Diego. By integrating multiple datasets—including crash reports, weather history, traffic volumes, and road features—the analysis identifies high-risk conditions, explores spatial and temporal trends, and builds predictive models for accident severity.

---

#### 📁 Project Structure


```
├── data/
│   ├── crashes/                  # TIMS crash datasets (San Diego)
│   ├── weather-datasets/        # Historical weather (2018–2024)
│   ├── road_speed_volume.csv    # SANDAG road features (speed, lanes, volume)
│   ├── socioeconomic.csv        # Homeownership, income, equity metrics
│   ├── homeless_311.csv         # 311 reports on homelessness
├── notebooks/
│   ├── 01_eda_visuals.ipynb     # EDA and visualizations
│   ├── 02_weather_road_merge.ipynb  # Data cleaning and feature merging
│   ├── 03_modeling.ipynb        # Regression, feature importance
├── outputs/
│   ├── figures/                 # Exported charts (PNG)
│   ├── processed/               # Cleaned and filtered data
├── dashboard/                   # Tableau or Power BI files
├── README.md
```

---

#### 🔍 Data Sources

- **Traffic Crashes**: [TIMS SWITRS](https://tims.berkeley.edu/help/SWITRS.php)  
- **Weather**: [Visual Crossing](https://www.visualcrossing.com/weather-history/San%20Diego,%20CA,%20United%20States/us/last15days/)  
- **Road Infrastructure**: [SANDAG Speed/Volume](https://opendata.sandag.org/Transportation/SOC-Local-Roads-Speed-and-Volume/u8qv-h3d4/about_data)  
- **Socioeconomic**: [National Equity Atlas](https://nationalequityatlas.org/indicators/Homeownership)  
- **Homelessness**: [UCSD ArcGIS 311 Data](https://hhubsandiego-ucsdonline.hub.arcgis.com/pages/data-bank)

---

#### 🧹 Data Preprocessing

- Converted dates, removed nulls, and standardized text fields  
- Merged weather and crash data by date  
- Created derived features:
  - `weather_group` (e.g., clear, cloudy)
  - `hour` from `COLLISION_TIME`
  - `season` from month
- Removed temperature outliers using IQR  
- Mapped categorical fields and cleaned street names for merging  
- Filtered for 2019–2023 crash records

---

#### 📊 Exploratory Data Analysis (EDA)

Key charts (saved in `/outputs/figures`):

- `monthly_trend.png` – Accident trends by month  
- `yearly_trends.png` – Year-over-year variation  
- `accidents_weather_condition.png` – Accident count by weather  
- `light_condition.png` – Light condition breakdown  
- `vehicle_type.png` – Accidents by vehicle type  
- `causes.png` – Primary causes of crashes  
- `hour_weather.png`, `by_season_weather.png` – Time of day & seasonal breakdown  
- `corr_matrix.png` – Feature correlation heatmap

---

#### 📌 Key Insights

- Higher crash rates during **cloudy** and **commute hours**  
- Roads with **2 lanes** and **moderate speed limits** are high-risk  
- **Alcohol** and **road lighting** contribute significantly to crash severity  
- Certain road types and surfaces exhibit higher crash densities

---

#### 🤖 Regression & Machine Learning Models

##### OLS Regression  
- Inputs: weather (humidity, windspeed), road (speed, lanes), AADT, surface  
- VIF calculated to remove multicollinearity  
- Low R² for linear-only models due to non-linear behavior

##### Random Forest  
- Captures non-linear effects and interactions  
- Importance ranking highlights weather & road features  
- Performance evaluated via R² and RMSE

##### XGBoost  
- Used for severity classification with class-balancing strategies  
- Outperformed OLS in handling non-linear interactions

---

#### 📊 Dashboard

An interactive dashboard was built in **Tableau** to visualize:
- Crash counts by time, weather, lighting  
- High-risk streets and severity clusters  
- Filterable maps by road type, season, and speed

---

#### 🧠 Lessons Learned

- Weather, lighting, and infrastructure data require careful temporal alignment  
- Interaction terms (e.g., `speed × weather`) improve regression insights  
- Combining structured and geospatial data can yield more actionable results

---

#### 🚀 Future Directions

- Integrate live feeds for real-time crash prediction  
- Apply geospatial clustering (e.g., DBSCAN) for hotspot detection  
- Extend analysis to pedestrian injuries and bike crashes  
- Collaborate with city departments for pilot interventions
