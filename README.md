
# Solution for Kaggle Petfinder Adoption Prediction competition

![Petfinder Logo](petfinder-logo.png)

This repository contains Top 2% (31st place) solution for [Petfinder Adoption Prediction competition at Kaggle](https://www.kaggle.com/c/petfinder-adoption-prediction).

**Description from Kaggle**
In this competition you will be developing algorithms to predict the adoptability of pets - specifically, how quickly is a pet adopted? If successful, they will be adapted into AI tools that will guide shelters and rescuers around the world on improving their pet profiles' appeal, reducing animal suffering and euthanization.

**Solution** (*Final model - Best LB.ipynb*)

The following features were engineered:
* Image features: image vectors taken from Xception and NASNetLarge, height of the image
* Text features: TFIDF-transformed pet profile description
* Tabular features: original tabular data of pet profile, ratio features calculated at different aggregation levels, population and gdp of malaysia

Three layers of models, where out-of-fold features from previous layers are passed to next layers
1. "Feature-engineering" models: LinearRegression on PCA-transformed NASNet-features, ExtraTreesRegressor on SVD-transformed Xception-features
2. 3 models: LightGBM (LGBM) on image and text features, LGBM on non-image features, LGBM on all features. Mean out-of-fold probability at RescuerID-level is calculated at this level, and passed to the next.
3. 3 models: LGBM on all features, CatBoostRegressor on all features, and bagged BayesianRidge on only level 1 out-of-fold predictions
4. The final prediction is mode of the previous layer
    
Note that the notebooks here are just for inspiration - if you wan't to run them yourself with the data, it is recommended to sign up on Kaggle and fork the [original kernel](https://www.kaggle.com/jmyrberg/final-model-1-best-lb-31-lb?scriptVersionId=12101619).

---
Jesse Myrberg (jesse.myrberg@gmail.com)