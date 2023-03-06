## Classification algorithms

### [Logistic regression with Titanic data](https://github.com/tirthajyoti/Machine-Learning-with-Python/blob/master/Classification/Logistic_Regression_Classification.ipynb)
### [Naive bayes](https://github.com/tirthajyoti/Machine-Learning-with-Python/blob/master/Classification/Naive_Bayes_Classification.ipynb)
### [Support vector machine with breast cancer data](https://github.com/tirthajyoti/Machine-Learning-with-Python/blob/master/Classification/Support_Vector_Machine_Classification.ipynb)
### [Skewed logistic regression (imbalanced class divisions)](https://github.com/tirthajyoti/Machine-Learning-with-Python/blob/master/Classification/Skewed_Logistic_Regression.ipynb)
### [k-Nearest neighbor classification](https://github.com/tirthajyoti/Machine-Learning-with-Python/blob/master/Classification/KNN_Classification.ipynb)


## Logistic Regression Model Code sample
import numpy as np\
import pandas as pd\
from sklearn.model_selection import train_test_split\
from sklearn.preprocessing import StandardScaler\
from sklearn.linear_model import LogisticRegression

### Load the data
df = pd.read_csv('data.csv')\

### Preprocess the data
X = df.drop(columns='target')\
y = df['target']\
scaler = StandardScaler()\
X = scaler.fit_transform(X)

### Split the data into training and test sets
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2)\

### Train the model
model = LogisticRegression()\
model.fit(X_train, y_train)

### Evaluate the model
train_score = model.score(X_train, y_train)\
test_score = model.score(X_test, y_test)\
print(f'Train score: {train_score:.2f}')\
print(f'Test score: {test_score:.2f}')

### Make predictions on new data
new_data = np.array([[...], [...], ...], dtype=np.float64)  # Replace with appropriate values\
predictions = model.predict(new_data)


## Evaluation Matrics
import numpy as np\
from sklearn.metrics import accuracy_score, precision_score, recall_score, f1_score

### Make predictions on the test set
predictions = model.predict(X_test)

### Calculate evaluation metrics
accuracy = accuracy_score(y_test, predictions)\
precision = precision_score(y_test, predictions)\
recall = recall_score(y_test, predictions)\
f1 = f1_score(y_test, predictions)

### Print the results
print(f'Accuracy: {accuracy:.2f}')\
print(f'Precision: {precision:.2f}')\
print(f'Recall: {recall:.2f}')\
print(f'F1 score: {f1:.2f}')




## ROC curve

import matplotlib.pyplot as plt\
from sklearn.metrics import roc_curve, roc_auc_score

### Make predictions on the test set
predictions = model.predict_proba(X_test)[:, 1]  # Predict probability of the positive class

### Calculate the false positive rate and true positive rate
fpr, tpr, thresholds = roc_curve(y_test, predictions)

### Calculate the AUC
auc = roc_auc_score(y_test, predictions)

### Plot the ROC curve
plt.plot(fpr, tpr, label=f'AUC = {auc:.2f}')\
plt.xlabel('False Positive Rate')\
plt.ylabel('True Positive Rate')\
plt.legend()\
plt.show()

