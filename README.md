# Diamonds-datamad0121

![Diamond](https://images.squarespace-cdn.com/content/v1/56f155cb4d088e3037d11cb1/1491189624127-A4IRC2Q9IW4G9ZATPUEG/ke17ZwdGBToddI8pDm48kBIkQ6BpXxi_9dtfIasthhVZw-zPPgdn4jUwVcJE1ZvWQUxwkmyExglNqGp0IvTJZUJFbgE-7XRK3dMEBRBhUpwjSaaoaGppkKha9ZnvoYO43kj62dQGK0EtkcVsJV_yeCnmFJRGKYDWWwbF3ltV-m0/image-asset.png)


## Introduction:

This is one of the projects done during the [IronHack](https://www.ironhack.com/en) Data Analytics bootcamp. 
The current project is a [Kaggle competition](https://www.kaggle.com/c/diamonds-datamad0121). A dataset with diamond characteristics and their price was provided, and the objective was to predict diamond' prices regarding their features.


## Data:

Two datasets were provided, "train.csv" and "test.csv". The first one contained diamond features and the price, and had to be used to train the model. The second one only had diamond features and had to be used to predict the diamond prices regarding their characteristics.
The features included in the dataset were: carat, cut, color, clarity, depth, table, x, y, z and price.
A previous research was carried out to understand the importance of the diamond characteristics, in the [American Gem Society](https://www.americangemsociety.org) website are provided some interesting tables to understand the different color, cut and clarity parameters.

The following Python libraries were used:
- [sklearn](https://scikit-learn.org/stable/)
- [pandas](https://pandas.pydata.org/docs/user_guide/index.html)
- [seaborn](https://seaborn.pydata.org/index.html)
- [matplotlib.pyplot](https://matplotlib.org/stable/contents.html)


## Strategies:

![Figure](https://raw.githubusercontent.com/antoniogarciagiron/Diamonds-datamad0121/c8be7d1b7ae8a0d833ab481c678267aca69d47b2/figures/Diapositiva1.SVG)

### Linear Regression:

The first model was a Linear regression, and to make it, some cleaning steps were performed on the dataset. The data correlations were plotted and it was observed a strong correlation between x, y and z, so y and z were removed from the dataset. Furthermore, a relation between x and the carats was spotted, in such a way that the first iteration was to remove the rest of the columns and study the correlation with the price. 

A pipeline was prepared with StandardScaler and LinearRegression, and the model was trained with the 80% of the data provided and tested with the rest. A second iteration was launched to test the model with x, y, z and carats. However, the best mse (mean squared error) obtained was 0.087.


### Random Forest:

In order to improve the mse, a Random Forest model was planned.
The first step was to make a data encoding with the categorical columns, i.e. cut, color and clarity. In a first iteration, one hot encoding was performed (GetDummies), however, in this case there is an order in their values, in such a way that "IF" clarity is much better than "I1", and thus the diamond will be more expensive. Thus, an ordinal encoding was performed and the categorical data was substituted by integers from 0 to 10. 

With the categorical values turned into numerical values, a grid search (With GridSearchCV) was prepared to train the forest and get the best parameter combination (n_estimators, max_depth, min_samples_split...). The mse was used to measure the quality of the splits and to test the models. Several iterations were performed to adjust the optimal parameters. The best mse obtained was 0.0022, a magnitude order better than the Linear Regression.

Finally, the model was trained with the data and used to calculate the prices for the test.csv dataset.