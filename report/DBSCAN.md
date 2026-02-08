# Density-Based Analysis (DBSCAN)
After identifying the "Centrality Bias" in K-Means, we attempted to use DBSCAN (Density-Based Spatial Clustering of Applications with Noise) to isolate true anomalies.
---
## 1. The Cracked Mirror Problem
nitially, using a small eps value resulted in 261 clusters.

- **Discovery:** The model was "over-segmenting" the data. It treated tiny gaps in the network traffic as distinct boundaries, failing to see the larger "Satellite" structures.
- **Interpretation:** This confirms that our network traffic has Variable Density—the "Normal" core is extremely tight, while the rare behaviors are very spread out.

## 2.The Computational "Wall"
Attempts to increase eps to 1.90 to merge these clusters resulted in a system freeze.

- **Technical Root Cause:** At higher distance thresholds, the "density" became too high for the memory to process. The algorithm attempted to calculate a massive neighborhood matrix, leading to an $O(n^2)$ complexity explosion.

- **Conclusion:** DBSCAN is not "computationally feasible" for this specific high-dimensional dataset without significant downsampling.
---

## 3. Final Comparision: k-Means vs DBSCAN 

| Feature      | K-Means                                      | DBSCAN                                   |
|--------------|----------------------------------------------|------------------------------------------|
| Logic        | Force every point into a group               | Group only what is "crowded"              |
| Anomaly Result | False negatives: anomalies "hidden" inside groups | Over-segmentation: too many groups to analyze |
| Performance  | Fast but biased                               | Slow / memory-heavy on this data          |
| Verdict      | Fails to isolate anomalies                   | Fails to scale                            |
