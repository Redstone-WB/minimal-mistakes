---
title: "Simple Procedure of Data analytics"
date: 2020-12-12 23:59:00 -0400
categories: ML, DataAnalytics
published: false
---

### Author : Taewan Kim

#### 1. Set up a problem -> what is Y?
#### 2. Data collection -> collect X and Y
- (Traditionally) design a study, perform experiments, and collect data
- (Now) dig up a database and collect any related data 

#### 3. Data Preprocessing
- Transform data into usable form 

#### 4. Exploratory data analysis (EDA)
- See how data looks like 

#### 5. Data analysis (prediction)
- Initial data size: n = 100M, p = 10k
- Separate training and test set (often by data collection time)
- Select features via univariate statistical test (t-test, cor-test)
- (optionally) Dimension reduction (PCA)
- Select learning methods (often based on intuition)
- Model selection via cross-validation (methods & parameters)
- Test performance over the test set

#### 6. Validation with a totally new data set (often not existing data when the model is built)