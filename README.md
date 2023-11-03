# Anomaly Detection Research Project

## Introduction

This research project aimed to find an improved anomaly detection algorithm compared to the Extended Isolation Forest (EIF). EIF demonstrated high accuracy in detecting intentionally introduced anomalies across four different datasets. However, it was noted that the optimal hyperparameter (threshold) varied depending on the dataset. The primary objective of this research was to develop a more generalized algorithm with a consistent hyperparameter that produces high accuracy across diverse datasets.

## Methods

In evaluating different anomaly detection algorithms, we considered silhouette scores and 3D plots. Silhouette scores were used to assess the performance of clustering methods, providing insights into how well data points are categorized. The silhouette coefficient measures an object's cohesion within its cluster relative to other clusters. It has a range of -1 to 1, with higher values indicating better cluster assignment.

Initially, K-Means Clustering, Local Outlier Factor (LOF), and DBSCAN were considered. However, both K-Means and LOF exhibited limited performance, with silhouette scores around 0.30, indicating low accuracy. They also failed to detect known anomalies. Consequently, the focus shifted to comparing DBSCAN and Extended Isolation Forest (EIF).

DBSCAN (Density-based spatial clustering of applications with noise) is an unsupervised clustering algorithm that groups nearby data points together while detecting outliers. It relies on two critical hyperparameters: "minPoints" and "eps," which define the minimum number of points required to form a cluster and the required distance between points for cluster membership, respectively.

Standardization using Standard Scaler was applied to account for varying feature ranges. "minPoints" was set to 16, and "eps" was determined using the elbow method. DBSCAN automatically labels anomalies as -1, and the first detected anomaly within one minute was retained for simplicity.

## Results

The average silhouette score for different datasets was 0.74, indicating successful clustering. The accuracy of correctly detected anomalies ranged between 70% and 100% across various datasets, as shown in Table 1 (DBSCAN).

| Data Set   | Accuracy | Silhouette Score |
|------------|----------|------------------|
| Anomaly 1  | 80%      | 0.76             |
| Anomaly 2  | 70%      | 0.68             |
| Anomaly 3  | 89%      | 0.75             |
| Anomaly 4  | 100%     | 0.75             |

In Table 2, the silhouette scores using EIF with a threshold of 0.67 are shown:

| Data Set   | Accuracy | Silhouette Score |
|------------|----------|------------------|
| Anomaly 1  | 63%      | 0.62             |
| Anomaly 2  | 61%      | 0.59             |
| Anomaly 3  | 51%      | 0.60             |
| Anomaly 4  | 52%      | 0.54             |

## Discussion & Conclusion

Tables 1 and 2 demonstrate that DBSCAN outperformed EIF in detecting known anomalies, but it also yielded a higher number of false positives. Adjusting the "eps" value can reduce the total number of anomalies but may compromise accuracy. For instance, in the Anomaly 1 dataset, an "eps" value of 0.5 identified 56 anomalies, while an "eps" value of 0.75 reduced the count to 20 but resulted in a drop in accuracy from 80% to 60%. Striking a balance between false positives and accuracy requires careful consideration.

In conclusion, this research suggests that DBSCAN is a more effective algorithm for anomaly detection than EIF, but fine-tuning the hyperparameters is necessary to optimize results for specific datasets. The choice between false positives and accuracy depends on the specific needs of the application.
