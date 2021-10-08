<img src="https://whatcar.vn/media/2018/09/car-lot-940x470.jpg" />

# Project: Predicting the price of a car based on its characteristics

#### Project done by Eugenia Voytik, October 2021

Let's imagine that there is a company that sells used cars in Moscow. The main task of the company and its managers is to find bargains as quickly as possible (to put it simply, to buy below the market and sell above the market price).

The company's management needs to create a model that will predict the value of the car based on its characteristics.

If this model works well, you will be able to quickly identify bargains (when the price desired by the seller is lower than the predicted market price). This will greatly speed up your managers' work and increase your company's profits.

Problem: Historically, the company has not collected data from the beginning. There is only a small dataset with a short period of sales history, which is clearly insufficient to train the model. We will use it for the test, the rest will have to be collected independently.

### Terms and Conditions:

- It is allowed to use external data, but its source must be public and accessible for all contestants (e.g. `auto.ru`);
- It is allowed to use any ML algorithms and libraries (except DL);
- Model quality metric: MAPE - Mean Absolute Percentage Error.

# Summary:
![](https://rgchannel.edu.sg/wp-content/uploads/2018/04/OGMT8M0-1024x694.jpg)

## Work on this project was carried out in several steps:

1. **Data enrichment** (parsing from `auto.ru`):
    - collection of additional relevant data for the training dataset containing **130201** observations;  
    > [all data](https://www.kaggle.com/eugeniavoytik/sf-dst-car-price-prediction-eda-ml/data?scriptVersionId=76635935) necessary for this notebook can be found on Kaggle.
2. **EDA**:
    - transforming the training and test datasets into a unified form and merging them;
    - cleaning and unification of the data;
    - handling of missing values;
    - handling of duplicates;
    - analysis of relationship between features (numerical, categorical, binary) and between the features and the target;
    - outlier analysis;
3. **Feature engineering**:
    - 4 numerical and 8 binary columns were added to the data and used for the final submission of the project to improve the MAPE metric. Additional columns (3 columns and polynomial features) were added during the development phase, but they did not improve the model, so they were removed for the final submission;
4. **ML**:
    - all binary and categorical data are encoded in the final model as labels as the hot-encoding method did not yield any improvements of the MAPE metric;
    - standartization was not used as it yielded no improvements;
    - 5 different ML models were tested: CatBoost, RandomForest, ExtraTrees, XGBoost and Stacking. For the RandomForest and ExtraTrees models the hyperparameters tuning was performed using hyperopt library but it didn't improve the result.

## Results:
The best MAPE metrics in the leaderboard were shown by the tree-based (ExtraTreeRegressor: 9.66%) and the booster (XGBoostRegressor: 10.75%) models. The stacking of these two models using a LinearRegression meta model showed also quite a high result on the submission - 10.80%. As a result, I decided to use the default ExtraTreeRegressor model as a final prediction model.

The proposed solution is ranked **9th** out of 202th on the leaderboard (**MAPE = 9.66%**) (08.10.2021).

## What could be improved:
- additional feature engineering, such as the feature extraction from text (NLP), parsing of new data, etc., could help to improve the MAPE metric;
- other methods to optimize the hyperparameters of the model;
- to run lazypredict library and try to use other high ranked ML models;
- analyse the results of the ML model work and try to understand why there is a difference between the MAPE metric results in the notebook and on the submission.
