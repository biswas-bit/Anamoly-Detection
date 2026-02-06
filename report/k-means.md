# Error Aalysis Report : k-means for Anomaly Detection

## 1.Executive Summary
The objective was to evaluate the effectiveness of K-Means Clustering as an unsupervised anomaly detection method. While the model achieved a mathematically superior Silhouette Score (0.47 - 0.55), forensic analysis revealed a "Centrality Bias" that makes it unreliable for detecting subtle network threats.

## 2.Quantitative Performance
We evaluated the model using the Silhouette Coefficient. This measures how well a point fits its own cluster versus the next nearest one.
| Analysis Stage              | Silhouette Score | Interpretation                                      |
|-----------------------------|------------------|----------------------------------------------------|
| Global Data                 | 0.4700           | Strong separation; appears successful              |
| Satellite-Only (No Giant)   | 0.5590           | Highest score; rare traffic is very distinct       |


## 3.Visual Analysis: The "Giant" vs. The "Satellites"
Our PCA projection (81% Variance) revealed why the score was high but the detection was poor.

### A.Global View (The Centrality Bias)
In the full plot, Cluster 0 occupies the dense center. K-Means creates "circular" boundaries. Anything outside the main circle is flagged as an anomaly, regardless of whether it belongs to a legitimate "Satellite" cluster or not.

### B.Satellite View (Hiding the Giant)
By removing Cluster 0, we "zoomed in" on the rare traffic. The score increased to 0.5590, proving these small groups are very well-defined. However, the "Orphan" points (true anomalies) were still being absorbed into these blue clusters.
