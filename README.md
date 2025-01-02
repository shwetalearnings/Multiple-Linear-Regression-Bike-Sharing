# Multiple-Linear-Regression-Bike-Sharing
Demand Prediction for Shared Bikes: A Multiple Linear Regression Approach

## Table of Contents
 
1. Overview
2. Problem Context
3. Objectives
4. Dataset
5. Data Preparation and Preprocessing
6. Methodology
7. Conclusions
8. Technologies Used
9. Acknowledgements
10. References
11. Contact

## Overview
This project involves building a multiple linear regression model to predict the demand for shared bikes. The model will help a US-based bike-sharing provider, BoomBikes, understand the key factors influencing bike demand and make informed business decisions to recover from the economic impacts of the COVID-19 pandemic.

## Problem Context
BoomBikes, like many other businesses, has faced significant revenue declines during the pandemic. To stay competitive and meet customer needs post-lockdown, the company seeks to identify factors affecting bike demand and leverage this information to optimize its operations and increase profitability.

## Objectives
The primary goal is to create a regression model that identifies the significant variables influencing bike demand and explains the relationship between these variables and demand. This analysis will empower BoomBikes to strategize effectively for market recovery, improve customer satisfaction, and expand into new markets with a deeper understanding of demand dynamics.



## Dataset
The dataset used in this project, named `day.csv`, contains information on daily bike rentals and associated factors. It has been sourced from the dataset accompanying the publication:

**[Fanaee-T, Hadi, and Gama, Joao, "Event labeling combining ensemble detectors and background knowledge"](http://dx.doi.org/10.1007/s13748-013-0040-3)**, Progress in Artificial Intelligence (2013).

### Key Features:
- **Time-related Variables**:
  - `instant`: Record index.
  - `dteday`: Date.
  - `season`: Season (1: Spring, 2: Summer, 3: Fall, 4: Winter).
  - `yr`: Year (0: 2018, 1: 2019).
  - `mnth`: Month (1 to 12).
  - `weekday`: Day of the week.
  - `holiday`: Whether the day is a holiday (1: Yes, 0: No).
  - `workingday`: Whether the day is a working day (1: Yes, 0: No).

- **Weather-related Variables**:
  - `weathersit`: Weather conditions:
    - 1: Clear or partly cloudy.
    - 2: Misty or cloudy.
    - 3: Light snow or rain.
    - 4: Heavy rain, thunderstorm, or snow.
  - `temp`: Actual temperature (°C).
  - `atemp`: Perceived temperature (°C).
  - `hum`: Humidity level.
  - `windspeed`: Wind speed.

- **Demand-related Variables**:
  - `casual`: Count of casual (unregistered) users.
  - `registered`: Count of registered users.
  - `cnt`: Total count of bike rentals (sum of `casual` and `registered`).

### Dataset Characteristics:
- The data spans two years (2018 and 2019), reflecting seasonal and yearly demand trends.
- Includes both numerical and categorical features, requiring preprocessing for model building.

### Usage License:
The dataset is licensed under the publication mentioned above. Please cite it appropriately in any publications or references.

For further details about the dataset, contact the original authors:
- **Hadi Fanaee-T** ([hadi.fanaee@fe.up.pt](mailto:hadi.fanaee@fe.up.pt)).

## Methodology
The project followed a structured approach to building a multiple linear regression model for predicting bike rental demand:

### 1. Data Understanding
- Examined the dataset (`day.csv`) to understand its structure and key attributes.
- Referenced the dataset dictionary for a detailed understanding of each feature and its significance.

### 2. Data Cleaning and Preprocessing
- Converted categorical features like `weekday, season`, `weathersit` etc to Dummy Variables to avoid incorrect ordinal assumptions
- Normalized numerical features like `temp`, `atemp`, `humidity`,  `windspeed` etc to improve model performance

### 3. Exploratory Data Analysis (EDA)
- Conducted a thorough analysis to understand correlations between features and the target variable (`cnt`).
- Visualized trends in bike rentals across seasons, weather conditions, and time (months, weekdays, etc.).
- Identified potential multicollinearity issues among predictor variables.

### 4. Feature Selection
- Applied a **manual approach** to evaluate the relevance of variables based on domain knowledge and exploratory analysis.
- Implemented **Recursive Feature Elimination (RFE)** to systematically select the most significant predictors based on model performance.

### 5. Model Building
- Used `cnt` (total rentals) as the target variable.
- Built a multiple linear regression model using the `statsmodels` and `sklearn` libraries.
- Incorporated key predictors identified through manual analysis and RFE, such as temperature, year etc 

### 6. Model Evaluation
- Evaluated the model using metrics such as:
  - **R-squared**: To measure how well the independent variables explain the variance in the dependent variable.
  - **Adjusted R-squared**: To account for the number of predictors in the model.
  - Residual analysis to check assumptions of linear regression.
  - Calculated the R-squared score on the test dataset using:
     ```python
     from sklearn.metrics import r2_score
     r2_score(y_test, y_pred)

### 7. Iterative Improvement
Refined the model by iteratively adding or removing predictors based on statistical significance, RFE outcomes, and domain relevance.

## Conclusions

### Key Observations from Data Analysis:
1. **Pair Plot Findings**:
   - A strong positive correlation exists between `temp` and `count`.

2. **Collinearity**:
   - High correlation between `temp` and `atemp` was identified, which could impact model performance due to multicollinearity.

3. **Heat Map Findings**:
   - Correlation coefficient of `0.63` observed between `temp/atemp` and `count`.

4. **Categorical Variables Analysis**:
   - **Season**: Season 1 performs poorly, while Seasons 2 and 3 show similar performance.
   - **Holiday**: Significant difference in mean `count` values for holidays versus non-holidays, with non-holidays showing higher counts.
   - **Weekday**: Rental counts are stable across weekdays, with only minor fluctuations.
   - **Working Day**: Slightly higher rental counts on working days compared to non-working days.
   - **Year**: The latter year shows a significant increase in counts, indicating growing popularity as the business matures.
   - **Month**: Counts steadily increase from January, peaking around July–September.
   - **Weather Conditions**: Variability in counts is prominent and consistent with changing weather patterns.

---

### Final Model Summary:
The multiple linear regression model provided the following results:

- **Model Performance Metrics**:
  - **R-squared**: 0.838
  - **Adjusted R-squared**: 0.834
  - **F-statistic**: 197.8
  - **Prob (F-statistic)**: 1.21e-186
  - **Durbin-Watson Statistic**: 2.048

- **Coefficients**:
The model is defined by this linear equation :

**count=0.2121+0.2346⋅year−0.0939⋅holiday+0.4741⋅temp−0.1570⋅windspeed−0.0383⋅January−0.0512⋅July+0.0760⋅September+0.0201⋅Saturday−0.0808⋅Cloudy Mist−0.2869⋅Rain Snow−0.0613⋅Spring+0.0425⋅Summer+0.0769⋅Winter**

- **Residual Analysis**:
  - Skewness: -0.715
  - Kurtosis: 5.174
  - Omnibus Test Prob: 0.000 (indicating non-normality in residuals)
  - Jarque-Bera Test Prob: 5.86e-32

- **Test Set Performance**:
  - R-squared score between `y_pred` and `y_test`: **0.803**



## Technologies Used
The following technologies and libraries were utilized in this project:

- **Python 3.12.4**: Programming language.
- **Jupyter Notebook**: For exploratory data analysis and model development.
- **Pandas 2.2.2**: Data manipulation and analysis.
- **NumPy 1.26.4**: Numerical computations.
- **Matplotlib 3.8.4** and **Seaborn 0.11.2**: Data visualization.
- **scikit-learn 1.4.2**: Machine learning model development and evaluation.
- **statsmodels 0.14.2**: Statistical analysis and modeling.
- **seaborn 0.13.2** : Plots and Charts.

---

## Acknowledgements
This project would not have been possible without the following contributions:

- The dataset used was sourced from the publication:
  **[Fanaee-T, Hadi, and Gama, Joao, "Event labeling combining ensemble detectors and background knowledge"](http://dx.doi.org/10.1007/s13748-013-0040-3)**, Progress in Artificial Intelligence (2013).
- Inspiration for the project approach and methodology came from related work in demand forecasting and statistical modeling.
- The Python libraries and community forums that provided invaluable resources and support.

---

## References
1. Fanaee-T, Hadi, and Gama, Joao, "Event labeling combining ensemble detectors and background knowledge", Progress in Artificial Intelligence (2013): pp. 1-15, Springer Berlin Heidelberg, doi:10.1007/s13748-013-0040-3.
2. Scikit-learn Documentation: [https://scikit-learn.org/](https://scikit-learn.org/)
3. Statsmodels Documentation: [https://www.statsmodels.org/](https://www.statsmodels.org/)
4. Python Visualization Libraries: Matplotlib and Seaborn.

---

## License 
Use of this dataset in publications must be cited to the following publication:

[1] Fanaee-T, Hadi, and Gama, Joao, "Event labeling combining ensemble detectors and background knowledge", Progress in Artificial Intelligence (2013): pp. 1-15, Springer Berlin Heidelberg, doi:10.1007/s13748-013-0040-3.

@article{
	year={2013},
	issn={2192-6352},
	journal={Progress in Artificial Intelligence},
	doi={10.1007/s13748-013-0040-3},
	title={Event labeling combining ensemble detectors and background knowledge},
	url={http://dx.doi.org/10.1007/s13748-013-0040-3},
	publisher={Springer Berlin Heidelberg},
	keywords={Event labeling; Event detection; Ensemble learning; Background knowledge},
	author={Fanaee-T, Hadi and Gama, Joao},
	pages={1-15}
}



## Contact
For further information or queries regarding this project, please reach out:

- **Author**: Shweta Soni
- **Email**: shweta.soni.1@outlook.com
- **GitHub**: [https://github.com/shwetalearnings](https://github.com/shwetalearnings)

Feel free to connect or share your feedback!


