# Predictioneer Hackathon

## Objective
To develop a predictive model for estimating the number of deaths, expected cases, and case fatality ratio (CFR) for multiple regions based on available data. The model is trained on development data and validated on a separate validation dataset.

---

## Column Descriptions
- **Lat**: Latitude of the location
- **Long_**: Longitude of the location
- **Deaths**: Number of deaths
- **Case_fatality_ratio**: Case fatality ratio of the location

---

## Data Analysis
Using various methods from the `pandas` library to extract useful insights from the dataset:

- **Statistical Insights**: Computed mean, standard deviation, and overall dataset size.
- **Missing Values**: 
  - The `Deaths` column had numerous missing values, which were dropped.
  - The `Case_fatality_ratio` column had invalid values (e.g., >100 or <0), which were excluded.
- **Visualization**:
  - A heatmap was used to check feature correlations.
  - A pair plot was created to explore relationships between features.

---

## Data Preprocessing

1. **Handling Missing Values**:
   - Dropped rows with missing values in the `Deaths` column.

2. **Logarithmic Transformation**:
   - Applied log transformation to `Deaths` and `Case_fatality_ratio` to reduce skewness and approximate a normal distribution.

3. **Feature Engineering**:
   - Created a new feature `Lat_Long_Interaction` to improve correlation with target variables.

4. **Feature Scaling**:
   - Used `StandardScaler` to normalize features, ensuring equal scaling and avoiding dominance by any single feature.

5. **Dataset Split**:
   - Split the dataset into training (80%) and validation (20%) sets.

---

## Model Selection: Random Forest Regressor

The **Random Forest Regressor** was chosen for its robustness and effectiveness with tabular data. 

### How it Works
- Builds multiple decision trees during training.
- Each tree is trained on a random subset of data and features.
- Predictions are made by averaging tree outputs (for regression).

### Advantages
1. **Handles Nonlinearity**: Captures complex relationships between features and target variables.
2. **Reduces Overfitting**: Ensemble nature reduces the risk of overfitting.
3. **Handles Skewed Data**: Performs well even with unbalanced data.
4. **Feature Importance**: Provides insights into feature relevance.

---

## Hyperparameter Tuning

Used **Grid Search** to optimize the model. Key parameters tuned:
- `n_estimators`: Number of decision trees in the forest.
- `max_depth`: Maximum depth of each tree to control overfitting.

---

## Model Evaluation

- **Evaluation Metric**: Root Mean Square Error (RMSE)
  - RMSE for Testing Data on Deaths: **0.819**
  - RMSE for Testing Data on CFR: **0.223**

---

## Validation and Prediction

1. **Validation Dataset Preprocessing**:
   - Created `Lat_Long_Interaction` feature.
   - Scaled features using the `StandardScaler` fitted on training data.

2. **Prediction**:
   - Predicted `Deaths` and `CFR` using the trained Random Forest Regressor.
   - Converted logarithmic predictions back to the original scale using the exponential function.

3. **Confirmed Cases Calculation**:
   - Used the formula: 
     
     ```
     Confirmed Cases = (Deaths / CFR) * 100
     ```

4. **Results**:
   - Saved results in a CSV file containing `Deaths`, `Case_Fatality_Ratio`, and `Confirmed_Cases`.

---

## Key Insights and Observations

- The dataset had a significant amount of missing data, reducing the training sample size.
- Weak correlations between features and target variables limited the model’s performance.
- Additional correlated features could significantly improve the RMSE score.

---

## Results
- **Deaths Prediction RMSE**: 0.819
- **CFR Prediction RMSE**: 0.223

---

## Files in Repository
- **`predictioneer.ipynb`**: Jupyter Notebook containing data analysis, preprocessing, modeling, and evaluation steps.
- **`predictions_validation_data.csv`**: Final predictions for deaths, CFR, and confirmed cases.
- **`README.md`**: This documentation.

---
Link to the training data:
- https://docs.google.com/spreadsheets/d/1lMcoJVzBb1yEBSZNxjMKjNELoc8o5FbP/edit?usp=sharing&ouid=103708407185636214847&rtpof=true&sd=true

Link to the test data:
- https://docs.google.com/spreadsheets/d/1D1ssBh24hHhvofJr1WBtnmjgkIKPqJ1t/edit?usp=sharing&ouid=103708407185636214847&rtpof=true&sd=tru



