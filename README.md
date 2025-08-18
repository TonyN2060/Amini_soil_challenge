# Soil Nutrient Prediction Using Remote Sensing and Machine Learning - Gold Medal Solution

This project was developed as part of the **Amini Soil Prediction Challenge**, hosted on [Zindi Africa](https://zindi.africa/competitions/amini-soil-prediction-challenge.-). The goal of the challenge was to use machine learning and satellite imagery to predict the availability of soil nutrients for agricultural productivity across Africa.

We would like to extend our sincere thanks to **Amini**, **Zindi Africa**, and all supporting partners for organizing this important competition. The opportunity to work on real-world agritech data and contribute to open-source environmental AI is greatly appreciated.

 The notebook used in this solution is: `amini_soil.ipynb`

---

##  Data Overview

| File | Description |
|------|-------------|
| `Train.csv` | Contains known nutrient levels and soil features |
| `Test.csv` | Similar structure but without target values |
| `LANDSAT8_data_updated.csv` | Remote sensing reflectance values for each plot over time |
| `Gap_train.csv`, `Gap_test.csv` | Binary matrix showing missing nutrients per plot |
| `SampleSubmission.csv` | Template for final predictions |

Each plot is uniquely identified using the `PID` column.

---

## 🛰️ Vegetation Indices Used

From the LANDSAT 8 bands, the following vegetation and water indices were computed:

- **NDVI** – Normalized Difference Vegetation Index  
- **EVI** – Enhanced Vegetation Index  
- **SAVI** – Soil Adjusted Vegetation Index  
- **NDWI** – Water Index (McFeeters & Gao)
- **NDRE** – Red Edge Vegetation Index  
- **NBR** – Normalized Burn Ratio  

Each index was aggregated per plot using mean, max, and min to summarize temporal variation.

---

##  Preprocessing Pipeline

- Dropped columns: `site`, `lat`, `lon`, `PID`
- Imputed missing values using column-wise mean
- Merged remote sensing features with tabular soil data
- Target variables: `N`, `P`, `K`, `Ca`, `Mg`, `S`, `Fe`, `Mn`, `Zn`, `Cu`, `B`

---

## Modeling

We used a `RandomForestRegressor` wrapped in a `MultiOutputRegressor` to handle multi-target regression. The model was trained on 80% of the data and evaluated on the remaining 20%.

**Evaluation metrics:**
- Root Mean Squared Error (RMSE)
- Mean Absolute Error (MAE)
- R² Score

---

## Optuna Hyperparameter Tuning

To improve model performance, we used **Optuna** to optimize Random Forest parameters.

---

##  Submission

Predictions were generated using the trained model and formatted using the `SampleSubmission.csv` template. Final predictions were exported to `submission.csv`.

---

## Dependencies

```bash
pip install pandas numpy scikit-learn matplotlib seaborn xgboost optuna
