# Air Pollution and Respiratory Disease Analytics in Growing African Cities
**Case Study: Lagos, Nigeria**

## Table of Contents
1. [Project Overview](project-overview)
2. [Objectives](objectives)
3. [Data Dictionary](data-dictionary)
4. [Research Questions](research-questions)
5. [Methodology](methodology)
6. [Exploratory Data Analysis](exploratory-data-analysis)
7. [Predictive Modelling](predictive-modelling)
8. [Results and Recommendations](results-and-recommendations)
9. [Limitations](limitations)
10. [Setup instructions](setup-instructions)
11. [How to Run the Notebook](how-to-run-the-notebook)
12. [Acknowledgements](acknowledgements)


## 1. Project Overview
Rapid urbanization in African cities, such as Lagos (Nigeria), Nairobi (Kenya), Accra (Ghana), and Kinshasa (DR Congo), has led to worsening air quality due to vehicle emissions, industrial activities, and inadequate waste management. This project analyzes satellite-recorded air pollution data in conjunction with hospital-reported respiratory disease data in Lagos to investigate the relationship between pollution levels and health outcomes. The insights aim to support urban clean air initiatives and public health interventions across Africa.

### Why Lagos?
Lagos was chosen as the case study city because it represents a **typical example of rapid urban growth in Africa**.  
- It is the **largest city in Nigeria** and one of the fastest-growing megacities in the world, with a population exceeding **20 million**.  
- The city faces severe challenges from **traffic congestion, industrial activities, and open waste burning**, all of which contribute heavily to air pollution.  
- Lagos also has **limited public health infrastructure** relative to its size, making respiratory diseases an urgent concern for its residents.  

Insights gained from Lagos can serve as a **blueprint for other African cities** facing similar environmental and health challenges.

## 2. Objectives

This project set out to:

- Derive a pollution index combining all monitored pollutants.

- Monitor trends in air pollution levels over time.

- Analyze correlations between pollution spikes and hospital respiratory cases.

- Predict respiratory disease surges using pollution data.

- Identify high-risk localities, periods, and pollutants.

- Recommend public health and environmental policies to mitigate respiratory health risks.

### Time frame  
The analysis covers 2021 to 2023.


## 3. Data Dictionary
| Feature                     | Description                                                                 |
|----------------------------|-----------------------------------------------------------------------------|
| City                       | Local area in Lagos such as Ikeja, Yaba, Ajah, Surulere, Lekki              |
| Date                       | Date of observation in YYYY-MM-DD                                           |
| pm2_5                      | Fine particulate matter concentration in µg/m³                              |
| pm10                       | Coarse particulate matter concentration in µg/m³                            |
| no2                        | Nitrogen dioxide level in µg/m³                                             |
| so2                        | Sulphur dioxide level in µg/m³                                              |
| o3                         | Ozone concentration in µg/m³                                                |
| hospital_id                | Unique hospital identifier                                                  |
| respiratory_cases          | Number of new respiratory-related hospital cases reported                    |
| avg_age_of_patients        | Average age of patients reported                                            |
| weather_temperature        | Average daily temperature in °C                                             |
| weather_humidity           | Average daily humidity in percent                                           |
| wind_speed                 | Average daily wind speed in m/s                                             |
| rainfall_mm                | Daily rainfall in millimetres                                               |
| population_density         | People per square kilometre                                                 |
| industrial_activity_index  | Proxy score from 0 to 100 indicating industrial activity                    |


## 4. Research Questions
| Category              | Questions                                                                                                                                           |
| --------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------- |
| Trend Analysis        | How have air pollution levels changed over time in these cities? Are there seasonal patterns in pollution levels?                                   |
| Health Impact         | Is there a correlation between air pollution spikes and hospital respiratory cases? Which pollutants have the strongest relationship with diseases? |
| Predictive Modeling   | Which features contribute most to predicting respiratory cases? Which models perform best?                                                          |
| Vulnerability & Risk  | Which cities or months are at the highest risk?                                                                                                         |
| Policy & Intervention | What policies could significantly reduce respiratory health issues based on the findings?                                                           |

## 5. Methodology
This project was executed in Google Colab notebooks with Google Drive mounted for data access and outputs.
 
 ### Data Cleaning

1. Imported libraries: pandas, numpy, matplotlib, and datetime.
2. Loaded the Lagos Air Pollution and Health Data Excel file into a pandas DataFrame and previewed rows.
3. Inspected structure using head(), info(), and shape().
4. Handled missing values: numerical columns filled with median, categorical columns with mode, and missing dates forward-filled.
5. Created year and month columns from the date.
6. Standardized columns: renamed C to city, harmonized city names, and set data types (city and hospital_id as category, respiratory_cases as integer).
7. Saved the cleaned DataFrame to CSV in Google Drive.

 ### Exploratory Data Analysis 

1. Imported analysis and visualization packages and mounted Google Drive.
2. Loaded Main_cleaned_air_pollution_data.csv and confirmed no missing values.
3. Plotted yearly averages for PM2.5, PM10, NO2, SO2, and O3 across cities.
4. Plotted yearly average respiratory cases by city.
5. Defined seasons: Dry (November–March) and Rainy (April–October). Added a season column and compared average pollutant levels by season.
6. Identified zones and months with higher burdens by computing total respiratory cases by city and average pollution index by month.
7. Computed and visualized correlations between pollutants and respiratory cases with a heatmap and scatter plots. Reported Pearson correlations.
8. Saved the processed DataFrame with the season column as EDA_air_pollution_data.csv.

### Predictive Modelling and Forecasting

1. Built regression models: Linear Regression and Random Forest with lagged pollutant features.
2. Trained time series models for respiratory cases using Prophet and ARIMA.
3. Evaluated regression models with R² and RMSE.
4. Evaluated forecasts against historical patterns and seasonal trends


## 6. Exploratory Data Analysis link


| Analysis Area              | Key Findings                                                                                                                                                   | Insights                                                                           | Recommendations                                                                  |
| -------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------- | -------------------------------------------------------------------------------- |
| Yearly Trends              | PM2.5, PM10, NO2, SO2, O3 vary across cities (2021–2023). Ikeja PM2.5 rose from \~61.5 µg/m³ to 92.3 µg/m³. Average respiratory cases in Ikeja: 12.88 → 12.84. | Yearly averages fluctuate but show significant absolute respiratory cases.         | Monitor trends yearly and focus health interventions on high-case cities.        |
| Seasonal Pollution         | Dry season (Nov–Mar) has higher pollution: PM2.5 \~67.1 µg/m³, PM10 \~100.7 µg/m³; lower in Rainy season.                                                      | Pollution peaks align with harmattan and dry-season activities.                    | Run public health campaigns during dry season; increase air quality monitoring.  |
| High-risk Zones & Months   | Ikeja and Yaba have highest respiratory cases (800k+ and 750k+), pollution peaks Jan–Feb, Dec–Nov.                                                             | Population density and industrial activity likely contribute to higher cases.      | Target interventions and mitigation efforts in these zones and months.           |
| Pollutant-Case Correlation | Overall Pearson correlations low but positive; PM2.5 highest (0.21). Lagged correlations vary by pollutant.                                                    | PM2.5 shows most immediate effect; other pollutants have delayed or minor impacts. | Investigate lag periods further; use correlation insights for health advisories. |



## 7. Predictive Modelling link
| Category                | Method            | Findings                                                                | Insights and recommendations                                                            |
|-------------------------|-------------------|-------------------------------------------------------------------------|-----------------------------------------------------------------------------------------|
| Predictive modelling    | Linear Regression | R² approximately 0.04 and RMSE approximately 3.7, low predictive power | Simple linear models with lagged features did not capture complex relationships         |
| Predictive modelling    | Random Forest     | R² approximately 0.03 and RMSE approximately 3.7, poor performance     | Identified key predictors such as PM2.5 lag 0 and lag 2, NO2 lag 5, PM10 lag 1 and 2   |
| Time series forecasting | Prophet           | Captured yearly seasonality in Ikeja respiratory cases                  | Useful for understanding seasonal patterns and producing trend forecasts                |
| Time series forecasting | ARIMA 1,1,1       | Forecast aligned with historical series with 30 day confidence intervals| Reliable for short term forecasting and temporal dependence                             |
| Overall                 |                   | Machine learning models underperformed while time series captured season| Prefer time series models for forecasting. Pollutant levels remain important predictors |



## 8. keyaways and Recommendations
keyaways 
1. Pollution levels were consistently higher in the dry season and were elevated in early-year months.  
2. Ikeja and Yaba carried the largest respiratory case burdens.  
3. PM2.5 showed the clearest positive association with respiratory cases among individual pollutants, though the effect size was modest.  
4. General regression models underperformed while time series approaches reproduced seasonal patterns and short-term structure.

Policy and public health recommendations  
1. Focus interventions and resources in Ikeja and Yaba during the dry season, especially January and February.  
2. Expand fixed and mobile air quality monitoring to improve spatial and temporal coverage.  
3. Implement lag-aware alerts that account for pollutant lead and lag effects.  
4. Integrate weather, population density, and industrial activity in planning and resource allocation.  
5. Run public awareness programmes on protective behaviours during high-risk months.
   
## 9. Limitations
1. Correlations between single pollutants and respiratory cases were modest and may not capture multi-factor dynamics.  
2. Analysis focused on Lagos and results may not generalise without multi-city validation.  
3. Potential reporting limitations in hospital data and gaps in environmental measurements.  
4. Additional explanatory variables such as mobility, traffic counts, and land use were not included.


## 10. Setup Instructions

To run this project on your computer or in Google Colab, follow these steps carefully.

* **Install Python (if using locally)**
  Make sure Python (version 3.10 or later) is installed. You can download it from [https://python.org](https://python.org). During installation, check **“Add Python to PATH”**.

* **Install Required Libraries**
  This project uses pandas, numpy, matplotlib, seaborn, scikit-learn, Prophet, and statsmodels. To install the libraries, open your terminal or command prompt and run:

  ```bash
  pip install pandas numpy matplotlib seaborn scikit-learn prophet statsmodels
  ```

* **Clone or Download the Project from GitHub**
  You can either clone this repository using Git:

  ```bash
  git clone https://github.com/your-username/air-pollution-respiratory-analytics.git
  ```

  Or download the ZIP file from GitHub.

* **Navigate to the Project Folder**
  Using the terminal, navigate to the folder where your Jupyter Notebook is saved:

  ```bash
  cd air-pollution-respiratory-analytics
  ```


## 11. How to Run the Notebook

This project is designed to run in **Google Colab** or a **local Jupyter Notebook** environment.

1. **Open Google Colab or Jupyter Notebook**

   * Upload or open the `.ipynb` file in Colab or Jupyter.

2. **Mount Google Drive (if using Colab)**

   * This allows access to the datasets stored in your Google Drive. Example code:

     ```python
     from google.colab import drive
     drive.mount('/content/drive')
     ```

3. **Load the Dataset**

   * Use pandas to read the cleaned or raw CSV files, e.g.,

     ```python
     import pandas as pd
     df = pd.read_csv('/content/drive/MyDrive/Main_cleaned_air_pollution_data.csv')
     df.head()
     ```

4. **Run the Notebook Cells in Order**

   * **Data Cleaning** → **EDA** → **Predictive Modelling** → **Visualizations**
   * In Colab or Jupyter, click each cell and press **Shift + Enter**.

5. **View Outputs**

   * Plots, tables, and CSV outputs will be generated.
   * Processed CSVs like `EDA_air_pollution_data.csv` are saved to your Drive if needed.


## Dataset

The main dataset used is:

* `Lagos Air Pollution & Health Data.xlsx` – raw pollution and respiratory case data
* `Main_cleaned_air_pollution_data.csv` – cleaned data after preprocessing

You can access the notebook and cleaned data here:

* Notebook:
  - 1. <a href="https://github.com/mauree155/Examining-Air-Quality-and-Health-Outcomes-in-Lagos-Nigeria/blob/main/Data_Cleaning.ipynb">Data_cleaning</a>
  
    2. <a href="https://github.com/mauree155/Examining-Air-Quality-and-Health-Outcomes-in-Lagos-Nigeria/blob/main/EDA_Report.ipynb">EDA</a>
    3. <a href="https://github.com/mauree155/Examining-Air-Quality-and-Health-Outcomes-in-Lagos-Nigeria/blob/main/Predicitve_Modelling.ipynb">Predictive modelling</a>
* Dataset: Access the folder via google drive  <a href="https://drive.google.com/drive/folders/1keLmLy5jUT9V_kmigVTymIegw5Mrnpp_">Here</a>

 ## 12. Acknowledgement

Thanks to **DataVerse** for the dataset & mentorship and to my **team members** for their support in this project.






