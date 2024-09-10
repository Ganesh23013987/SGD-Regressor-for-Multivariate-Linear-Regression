# SGD-Regressor-for-Multivariate-Linear-Regression

## AIM:
To write a program to predict the price of the house and number of occupants in the house with SGD regressor.

## Equipments Required:
1. Hardware – PCs
2. Anaconda – Python 3.7 Installation / Jupyter notebook

## Algorithm
### Step 1: 
Load California housing data, select features and targets, and split into training and testing sets.
### Step 2:
Scale both X (features) and Y (targets) using StandardScaler.
### Step 3:
Use SGDRegressor wrapped in MultiOutputRegressor to train on the scaled training data.
### Step 4:
Predict on test data, inverse transform the results, and calculate the mean squared error.


## Program:

Program to implement the multivariate linear regression model for predicting the price of the house and number of occupants in the house with SGD regressor.
```
Developed by: GANESH D
RegisterNumber: 212223240035

import numpy as np
import pandas as pd
from sklearn.datasets import fetch_california_housing
from sklearn.linear_model import SGDRegressor
from sklearn.multioutput import MultiOutputRegressor
from sklearn.model_selection import train_test_split
from sklearn.metrics import mean_squared_error
from sklearn.preprocessing import StandardScaler

data=fetch_california_housing()
df=pd.DataFrame(data.data,columns=data.feature_names)
df['target']=data.target
print(df.head())
```
<img width="700" alt="image" src="https://github.com/user-attachments/assets/a0ec6323-828a-44a1-9509-cfa3ec43539d">

```
df.info()
```
<img width="600" alt="image" src="https://github.com/user-attachments/assets/1d36fa72-9bc3-4186-b7b7-01bfb78896ba">

```
X=df.drop(columns=['AveOccup','target'])
X.info()
```
<img width="700" alt="image" src="https://github.com/user-attachments/assets/79c58689-4d5b-4ef3-b812-8af90ce2635d">

```
Y=df[['AveOccup','target']]
Y.info()
```
<img width="700" alt="image" src="https://github.com/user-attachments/assets/2fd72354-1f3f-43d0-946a-bc2fe82ac5b1">

```
X_train, X_test, Y_train, Y_test = train_test_split(X, Y, test_size=0.2, random_state=1)
X.head()
```
<img width="700" alt="image" src="https://github.com/user-attachments/assets/9345586a-f14a-46fb-8353-665c7cd81418">


```
scaler_X = StandardScaler()
scaler_Y = StandardScaler()

X_train = scaler_X.fit_transform(X_train)
X_test = scaler_X.transform(X_test)
Y_train = scaler_Y.fit_transform(Y_train)
Y_test = scaler_Y.transform(Y_test)
print(X_train)
```

<img width="700" alt="image" src="https://github.com/user-attachments/assets/d1170ed7-b24d-44d5-af49-2c21a55c09b9">

```
# Initialize the SGDRegressor
sgd = SGDRegressor(max_iter=1000, tol=1e-3)

# Use MultiOutputRegressor to handle multiple output variables
multi_output_sgd = MultiOutputRegressor(sgd)

# Train the model
multi_output_sgd.fit(X_train, Y_train)

# Predict on the test data
Y_pred = multi_output_sgd.predict(X_test)

# Initialize the SGDRegressor
sgd = SGDRegressor(max_iter=1000, tol=1e-3)

# Use MultiOutputRegressor to handle multiple output variables
multi_output_sgd = MultiOutputRegressor(sgd)

# Train the model
multi_output_sgd.fit(X_train, Y_train)

# Predict on the test data
Y_pred = multi_output_sgd.predict(X_test)

# Inverse transform the predictions to get them back to the original scale
Y_pred = scaler_Y.inverse_transform(Y_pred)
Y_test = scaler_Y.inverse_transform(Y_test)

# Evaluate the model using Mean Squared Error
mse = mean_squared_error(Y_test, Y_pred)
print("Mean Squared Error:", mse)

# Optionally, print some predictions
print("\nPredictions:\n", Y_pred[:5])
```

<img width="700" alt="image" src="https://github.com/user-attachments/assets/ce694f32-0b32-411b-a934-883f5d712161">


## Result:
Thus the program to implement the multivariate linear regression model for predicting the price of the house and number of occupants in the house with SGD regressor is written and verified using python programming.
