# Forecasting Groundwater-Level Changes Across India Using PySpark and Machine Learning

## Project Overview

This project analyses groundwater-level observations reported across India using **Apache PySpark** and machine-learning techniques. It explores spatial patterns, temporal observation coverage, station-level data quality, and the prediction of subsequent groundwater-level observations.

The project uses data published by the **Central Ground Water Board (CGWB)** through the India Data Portal.

## Research Objectives

- Examine the spatial and temporal distribution of groundwater-level observations across India.
- Assess data quality, station coverage, and temporal consistency.
- Explore geographical and temporal patterns in recorded groundwater levels.
- Develop machine-learning models to predict the next available groundwater observation.
- Compare model performance using RMSE, MAE, and R².

## Dataset

**Source:** Central Ground Water Board (CGWB), India Data Portal  
**Dataset:** Changes in Depth to Water Level  
**Official dataset resource:**  
https://ckandev.indiadataportal.com/dataset/groundwater/resource/580a8f6e-3d86-4ca7-ac7d-cd5df12b443c

The CSV used in this analysis contains approximately **550,850 records and 14 columns**, covering observations from **January 2013 to March 2023**.

The dataset is not included in this repository because of its large file size. Please download the CSV from the official resource link above before running the notebook.

### How to load the dataset

1. Open the official dataset resource link.
2. Download the CSV file.
3. Open `Groundwater_Analytics_India_Final.ipynb` in Google Colab.
4. Run the environment setup and dataset-loading cells.
5. When prompted by Colab, upload the downloaded CSV file.

## Methodology

1. **Environment setup:** Configure Python and Apache PySpark.
2. **Dataset loading and inspection:** Load the CGWB CSV into a Spark DataFrame and inspect its schema and records.
3. **Data quality assessment:** Examine missing values, exact duplicates, numerical ranges, date coverage, and geographical coverage.
4. **Exploratory analysis:** Study annual and monthly observation distributions.
5. **Station-level preparation:** Construct station identifiers, assess observation-date gaps, and select stations with sufficient historical coverage.
6. **Feature engineering:** Generate lagged groundwater-level features and seasonal features using the current observation date.
7. **Model development:** Train and evaluate Linear Regression, Random Forest, and Gradient Boosted Trees.
8. **Baseline comparison:** Compare the models against a previous-observation persistence baseline.
9. **Validation and visualisation:** Evaluate prediction errors across observation-gap categories and examine spatial patterns.

## Technology Stack

- Python
- Apache PySpark / PySpark MLlib
- Pandas
- NumPy
- Matplotlib
- Seaborn
- Google Colab

## Final Model Results

The final chronological evaluation used observations with target dates before 2019 for training and observations from 2019 onward (within the selected evaluation period) for testing.

| Model | RMSE | MAE | R² |
|---|---:|---:|---:|
| Linear Regression | 3.4302 | 2.0836 | 0.8734 |
| Random Forest | 3.9468 | 2.0854 | 0.8324 |
| Gradient Boosted Trees | 3.9569 | 2.0884 | 0.8316 |
| Previous Observation Baseline | 4.0419 | 2.2667 | 0.8243 |

**Best-performing model:** Linear Regression.

The model predicts the **next available observation**, not a fixed three-month forecast. Observation intervals are irregular, and prediction errors increase for longer gaps.

> Note: The source documentation used for this project did not clearly establish the measurement unit or sign convention. Therefore, metric values are reported without assigning a physical unit.

## Repository Contents

- `Groundwater_Analytics_India_Final.ipynb` — Main notebook containing the analysis, modelling, visualisations, and results.
- `groundwater_analytics_india_final.py` — Python source export of the notebook (if included).
- `requirements.txt` — Python package requirements (if included).
- `images/` — Selected project charts used in the notebook and research poster (if included).

## Running the Project

The recommended environment is **Google Colab**.

1. Download or clone this repository.
2. Open `Groundwater_Analytics_India_Final.ipynb` in Google Colab.
3. Download the dataset from the official CGWB resource link.
4. Run the notebook cells in order.
5. Upload the downloaded CSV when prompted.

For local execution, install the packages listed in `requirements.txt`, configure a compatible Java runtime for Spark, and update the dataset-loading cell to point to the local CSV file.

## Important Limitations

- Monitoring coverage varies across years and geographical regions.
- Observation intervals are irregular; the task is next-observation prediction rather than a fixed-horizon forecast.
- Station identifiers are constructed from available station and location fields and may not represent unique physical wells.
- Evaluation focuses on stations represented in the training data; generalisation to entirely unseen stations has not been established.
- The selected station-history and data-quality filters may affect the representativeness of the modelling dataset.
- The measurement unit and sign convention should be confirmed from the original source documentation before interpreting values physically.

## Acknowledgement

I sincerely thank **Chanakya University** for conducting this research opportunity and providing the platform to undertake this study and present its findings.

I also acknowledge the **Central Ground Water Board (CGWB)** and the **India Data Portal** for making the groundwater dataset available for research and analysis.

## References

1. Central Ground Water Board (CGWB), *Changes in Depth to Water Level*, India Data Portal.  
   https://ckandev.indiadataportal.com/dataset/groundwater/resource/580a8f6e-3d86-4ca7-ac7d-cd5df12b443c
2. Apache Software Foundation, *Apache Spark 4.0.5 – Machine Learning Library (MLlib) Guide*.  
   https://spark.apache.org/docs/4.0.5/ml-guide.html
3. Apache Software Foundation, *PySpark Documentation*.  
   https://spark.apache.org/docs/4.0.5/api/python/
4. Central Ground Water Board (CGWB), *Ground Water Level Monitoring*.  
   https://cgwb.gov.in/hi/ground-water-level-monitoring
