# Clustering - Manufacturing Control Data
Kaggle Tabular Playground Series Jul 2022 dataset
https://www.kaggle.com/competitions/tabular-playground-series-jul-2022/overview

#### Brief
In this challenge, you are given a dataset where each row belongs to a particular cluster. Your job is to predict the cluster each row belongs to. You are not given any training data, and you are not told how many clusters are found in the ground truth labels. 

#### Data Description
29 features, 22 float, 7 int.


## Notebook Table of Contents
#### EDA
- visualise distributions
- check features with Shapiro-Wilks tests for normality, Chi-squared tests for Poisson distributions
- review feature correlations
#### Processing
- Normalize using PowerTransformer
- clip outliers
- PCA analysis
  - PCA not useful, features can't really be compressed.
#### Finding optimal n_clusters
- k-Means
  - no obvious elbow, using k=8 gives an Adjusted Rand Index (ARI) score of about 0.256
- Gaussian Mixture Model
  - using BIC scores, elbow clearer at clusters=7
#### Finding informative features
- using above GMM, plotted feature means per cluster, selected only features with higher variance between clusters. Reduced from 29 to 14 features.
#### Model Selection
- GMM and Bayesian GMM trained, BGMM achieves ARI score 0.599
- BGMM ensemble of 5 models with soft voting, ARI score 0.606
- Semi-Supervised, HistGBM, max_depth=5
  - using above BGMM ensemble predict_probas, selectively choose datapoints where cluster prediction probabilities were higher than 0.7, and training HistGBM using ensemble's labels. ARI score 0.612
- DBSCAN: poor performance, ARI score 0.00, dataset density is rather homogeneous.
- MeanShift: poor performance, ARI score 0.06. Training took too long, so skipped trying to improve model.
- Agglomerative Modelling: took too long, skipped
- Birch: took too long, skipped
#### Visualise Feature KDEs according to clusters
#### Visualise Clusters with t-SNE



  

