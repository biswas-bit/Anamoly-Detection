# Error Aalysis Report : k-means for Anomaly Detection

## 1.Executive Summary
The objective was to evaluate the effectiveness of K-Means Clustering as an unsupervised anomaly detection method. While the model achieved a mathematically superior Silhouette Score (0.47 - 0.55), forensic analysis revealed a "Centrality Bias" that makes it unreliable for detecting subtle network threats.

## 2.Quantitative Performance
We evaluated the model using the Silhouette Coefficient. This measures how well a point fits its own cluster versus the next nearest one.
| Analysis Stage              | Silhouette Score | Interpretation                                      |
|-----------------------------|------------------|----------------------------------------------------|
| Global Data                 | 0.4700           | Strong separation; appears successful              |
| Satellite-Only (No Giant)   | 0.5590           | Highest score; rare traffic is very distinct       |
