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

# 4.Forensic Discovery: Cluster 0 (The Traffic Sink)
We identified Cluster 0 as the "Normal Baseline."
 - **Density**: Highest density in the dataset (lowest internal distance).

 - **Impact**: It acts as a "Mathematical Black Hole," pulling the global mean toward it and forcing any unique behavior to be measured against its massive density.

 # 5.Final Conclusion
 The analysis proves that a high Silhouette Score does not equal good Anomaly Detection.
  - **The Failure:** K-Means is "Greedy." It forced isolated "Orphan" points into the nearest satellite cluster to maintain mathematical cohesion.
  - **The Result:** We saw zero distinct anomaly separation in the plots because the model prioritized "grouping" over "isolating."

  

