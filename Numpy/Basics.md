## Numpy
NumPy (Numerical Python) is an open source Python library that’s used in almost every field of science and engineering. It’s the universal standard for working with numerical data in Python, and it’s at the core of the scientific Python and PyData ecosystems. NumPy users include everyone from beginning coders to experienced researchers doing state-of-the-art scientific and industrial research and development. The NumPy API is used extensively in Pandas, SciPy, Matplotlib, scikit-learn, scikit-image and most other data science and scientific Python packages.

## Matplotlib.pyplot
Matplotlib.pyplot is a collection of functions that make matplotlib work like MATLAB. Each pyplot function makes some change to a figure: e.g., creates a figure, creates a plotting area in a figure, plots some lines in a plotting area, decorates the plot with labels, etc.

In matplotlib.pyplot various states are preserved across function calls, so that it keeps track of things like the current figure and plotting area, and the plotting functions are directed to the current axes (please note that "axes" here and in most places in the documentation refers to the axes part of a figure and not the strict mathematical term for more than one axis).

## Pandas
Pandas is an open source, BSD-licensed library providing high-performance, easy-to-use data structures and data analysis tools for the Python programming language.

### Importing The Libraries

```python
import numpy as np
import matplotlib.pyplot as plt
import pandas as pd
```
### Importing The DataSet
```python
dataset = pd.read_csv('Data.csv')
X = dataset.iloc[:, :-1].values
y = dataset.iloc[:, -1].values
print(x)
```
>[['France' 44.0 72000.0]
 ['Spain' 27.0 48000.0]
 ['Germany' 30.0 54000.0]
 ['Spain' 38.0 61000.0]
 ['Germany' 40.0 nan]
 ['France' 35.0 58000.0]
 ['Spain' nan 52000.0]
 ['France' 48.0 79000.0]
 ['Germany' 50.0 83000.0]
 ['France' 37.0 67000.0]]

```python
print(y)
```

>['No' 'Yes' 'No' 'No' 'Yes' 'Yes' 'No' 'Yes' 'No' 'Yes']

## Taking care of missing data


```python
from sklearn.impute import SimpleImputer
imputer = SimpleImputer(missing_values=np.nan, strategy='mean')
imputer.fit(X[:, 1:3])
X[:, 1:3] = imputer.transform(X[:, 1:3])
```


```python
print(X)
```

    [['France' 44.0 72000.0]
     ['Spain' 27.0 48000.0]
     ['Germany' 30.0 54000.0]
     ['Spain' 38.0 61000.0]
     ['Germany' 40.0 63777.77777777778]
     ['France' 35.0 58000.0]
     ['Spain' 38.77777777777778 52000.0]
     ['France' 48.0 79000.0]
     ['Germany' 50.0 83000.0]
     ['France' 37.0 67000.0]]


## Encoding categorical data

### Encoding the Independent Variable


```python
from sklearn.compose import ColumnTransformer
from sklearn.preprocessing import OneHotEncoder
ct = ColumnTransformer(transformers=[('encoder', OneHotEncoder(), [0])], remainder='passthrough')
X = np.array(ct.fit_transform(X))
```


```python
print(X)
```

    [[1.0 0.0 0.0 44.0 72000.0]
     [0.0 0.0 1.0 27.0 48000.0]
     [0.0 1.0 0.0 30.0 54000.0]
     [0.0 0.0 1.0 38.0 61000.0]
     [0.0 1.0 0.0 40.0 63777.77777777778]
     [1.0 0.0 0.0 35.0 58000.0]
     [0.0 0.0 1.0 38.77777777777778 52000.0]
     [1.0 0.0 0.0 48.0 79000.0]
     [0.0 1.0 0.0 50.0 83000.0]
     [1.0 0.0 0.0 37.0 67000.0]]


### Encoding the Dependent Variable


```python
from sklearn.preprocessing import LabelEncoder
le = LabelEncoder()
y = le.fit_transform(y)
```


```python
print(y)
```

    [0 1 0 0 1 1 0 1 0 1]


## Splitting the dataset into the Training set and Test set


```python
from sklearn.model_selection import train_test_split
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size = 0.2, random_state = 1)
```


```python
print(X_train)
```

    [[0.0 0.0 1.0 38.77777777777778 52000.0]
     [0.0 1.0 0.0 40.0 63777.77777777778]
     [1.0 0.0 0.0 44.0 72000.0]
     [0.0 0.0 1.0 38.0 61000.0]
     [0.0 0.0 1.0 27.0 48000.0]
     [1.0 0.0 0.0 48.0 79000.0]
     [0.0 1.0 0.0 50.0 83000.0]
     [1.0 0.0 0.0 35.0 58000.0]]



```python
print(X_test)
```

    [[0.0 1.0 0.0 30.0 54000.0]
     [1.0 0.0 0.0 37.0 67000.0]]



```python
print(y_train)
```

    [0 1 0 0 1 1 0 1]



```python
print(y_test)
```

    [0 1]


## Feature Scaling


```python
from sklearn.preprocessing import StandardScaler
sc = StandardScaler()
X_train[:, 3:] = sc.fit_transform(X_train[:, 3:])
X_test[:, 3:] = sc.transform(X_test[:, 3:])
```


```python
print(X_train)
```

    [[0.0 0.0 1.0 -0.19159184384578545 -1.0781259408412425]
     [0.0 1.0 0.0 -0.014117293757057777 -0.07013167641635372]
     [1.0 0.0 0.0 0.566708506533324 0.633562432710455]
     [0.0 0.0 1.0 -0.30453019390224867 -0.30786617274297867]
     [0.0 0.0 1.0 -1.9018011447007988 -1.420463615551582]
     [1.0 0.0 0.0 1.1475343068237058 1.232653363453549]
     [0.0 1.0 0.0 1.4379472069688968 1.5749910381638885]
     [1.0 0.0 0.0 -0.7401495441200351 -0.5646194287757332]]



```python
print(X_test)
```

    [[0.0 1.0 0.0 -1.4661817944830124 -0.9069571034860727]
     [1.0 0.0 0.0 -0.44973664397484414 0.2056403393225306]]
