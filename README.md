# Self-Supervised-Learning-in-Bee-Movement



This project uses machine learning to understand how bees move — without needing any labels.  
We built a model that learns patterns from bee movement data and groups similar behaviors together.


### What is self-supervised learning?
It’s a type of machine learning where the model learns patterns from the data itself — without any labels or human instructions. It teaches itself using the structure of the data.

---

##  Files Overview

| File | What it does |
|------|---------------|
| `practice1.ipynb` | Python notebook for preprocessing the raw data — it splits, cleans, and prepares the data |
| `practiceBuildModel.ipynb` | Python notebook for training the model, compressing, clustering, and plotting the results |
| `bee_samples.npy` | All clean movement segments of bees, shape `(162770, 30, 4)` |
| `bee_samples_active_only.npy` | Same as above but only for interesting movement, not when bees are still |
| `bee_compressed.npy` | Compressed data using a small (basic) autoencoder |
| `bee_compressed_deep.npy` | Compressed data using a better deep autoencoder (final version) |
| `bee_cluster_labels.npy` | Cluster labels from basic compression |
| `bee_cluster_labels_deep.npy` | Cluster labels from deep compression |
| `bee_cluster_labels_active_only.npy` | Cluster labels only for active bee segments |
| `cluster_sample_mapping.pkl` | Mapping each sample to its cluster and index (used for visualization) |
| `segments_with_angular_velocity.pkl` | Extra file used during preprocessing (velocity + angular velocity) |


---

##  What Was the Data?

- The data contains 3D movement of bees (`x`, `y`, `z`) over time.
- Each bee movement was divided into short clips (30 frames long).
- For each clip calculated:
  - `velocity_x`
  - `velocity_y`
  - `velocity_z`
  - `angular_velocity` (turning speed)

---

##  Steps Did in This project:

### 1. Preprocessing
- Split data into movement segments.
- Removed unrealistic speeds (over 1000 pixels/sec).
- Calculated velocities and angular velocities.
- Created clean, fixed-length samples (30 steps, 4 features each).
- Saved them as `bee_samples.npy`.

### 2. Self-Supervised Learning with Autoencoder
- Built an autoencoder to compress the data from 120 → 4 numbers.
- Trained the model with no labels.
- Saved compressed results as `bee_compressed_deep.npy`.

### 3. Clustering with K-Means
- Used KMeans to find 15 behavior groups from the compressed data.
- Visualized these groups in 2D using PCA.
- Mapped each behavior to human-understandable motion.

### 4. Naming Clusters
After plotting samples from each cluster, we gave them simple names:
- “Still or No Movement”
- “Sharp Horizontal Move”
- “Sudden Direction Flip”
- and many more…

### 5. Filtered Out Still Behaviors
- Most data (Cluster 0) was bees not moving.
- We filtered this out and focused only on the interesting behaviors.
- Result: 270 active movement clips from 14 interesting clusters.

---

##  What Was the Result?

- found 14 different types of bee movement like turning, flying up, dropping down, fast starts, and more.
- The model learned this automatically — without any labels.
- The cluster plots and sample plots show clear patterns of bee behaviors.
- Then turned raw movement data into interpretable behavior types.

---

##  Why Is This Useful?

- Shows how self-supervised learning can find real-world patterns with no labels.
- Can be used in biology, animal tracking, or robotics.
- Good example of combining deep learning + clustering + visualization.

## Note about the data
The original bee trajectory data (Excel files) is not included in this repository because of file size and privacy.



