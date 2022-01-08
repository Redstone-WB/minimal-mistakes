---
title: "Class imbalance"
date: 2020-05-04 23:59:00 -0400
categories: ML, DataAnalytics
published: true
---

### UnderSampling & OverSampling

- 데이터 비대칭 문제를 해결하기 위함.
- 출처 1 : https://datascienceschool.net/view-notebook/c1a8dad913f74811ae8eef5d3bedc0c3/
- 출처 2 : https://towardsdatascience.com/having-an-imbalanced-dataset-here-is-how-you-can-solve-it-1640568947eb
- 출처 3 : https://medium.com/james-blogs/handling-imbalanced-data-in-classification-problems-7de598c1059f
  

### 비대칭 데이터 문제라고 판단한 근거

- 단순히 우세한 클래스의 정확도 (accuracy)가 높아짐.
- 데이터 개수가 적은 클래스의 recall-rate가가 떨어짐.
- AS-IS : UnderSampling을 사용하고 있었음.


### trail #1. Oversampling Methods

- SMOTE (Synthetic Minority Over-sampling Technique)
- ADASYN (Adaptive Synthetic)


### trial #2. Using Ensemble of Samplers



###### code

```python

from imblearn.ensemble import BalancedBaggingClassifier
from sklearn.tree import DecisionTreeClassifier

#Create an object of the classifier.
bbc = BalancedBaggingClassifier(base_estimator=DecisionTreeClassifier(),
                                sampling_strategy='auto',
                                replacement=False,
                                random_state=0)

y_train = credit_df['Class']
X_train = credit_df.drop(['Class'], axis=1, inplace=False)

#Train the classifier.
bbc.fit(X_train, y_train)
preds = bbc.predict(X_train)

```

### trial #3. Using different weights 

- 출처3의 'class weights' 참고
- 숫자가 더 적은 class를 맞추는 것에 더 큰 가중치를 부여하는 방법.

###### code



```python
# Scaling by total/2 helps keep the loss to a similar magnitude.
# The sum of the weights of all examples stays the same.

weight_for_0 = (1 / neg)*(total)/2.0 
weight_for_1 = (1 / pos)*(total)/2.0

class_weight = {0: weight_for_0, 1: weight_for_1}

print('Weight for class 0: {:.2f}'.format(weight_for_0))
print('Weight for class 1: {:.2f}'.format(weight_for_1))

weighted_model = make_model()
weighted_model.load_weights(initial_weights)

weighted_history = weighted_model.fit(
    train_features,
    train_labels,
    batch_size=BATCH_SIZE,
    epochs=EPOCHS,
    callbacks = [early_stopping],
    validation_data=(val_features, val_labels),
    # The class weights go here
    class_weight=class_weight) 

```