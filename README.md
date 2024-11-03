# Principal Component Analysis (PCA) in ECG Signal Processing
## Overview
This code processes ECG signals by segmenting and classifying QRS complexes and applies Principal Component Analysis (PCA) to reduce the dimensionality of the data. PCA is a valuable tool in this context because it captures essential signal characteristics while discarding redundant information, making it easier to analyze and visualize ECG patterns across different heartbeat types.
## Why PCA?
ECG signals are high-dimensional, especially when examining individual QRS complexes across hundreds of samples. PCA transforms these complex signals into a lower-dimensional space, retaining only the most significant features. This dimensionality reduction has several advantages:
- Data Compression: Reduces the amount of data without losing critical information.
- Noise Reduction: Removes less important, potentially noisy features.
- Visualization: Allows us to visualize clusters of different heartbeat types in 2D or 3D, facilitating comparison and classification.

In this code, PCA is applied to distinguish between types of beats (N, S, F, V, U) in a lower-dimensional space, making the differences more apparent.



## Requirements
### Libraries
Ensure that you have the following libraries installed:
- wfdb
- numpy
- scipy
- scikit-learn
- matplotlib

### Dataset
This code works with .dat files from the MIT-BIH Arrhythmia Database. These files contain ECG data along with annotations marking heartbeat events.


##  Workflow

### Step 1: Import and Define Parameters
#### 1. Sampling and Filter Settings:
- Sampling frequency fs is set to 360 Hz.
- High-pass (fl = 0.5 Hz) and low-pass (fh = 20 Hz) Butterworth filters are created to remove unwanted frequency components from the ECG signal.
#### 2. Classification Table: The table dictionary maps each heartbeat label (N, S, F, V, U) to its respective types.

### Step 2: Load and Preprocess Data
#### 1. File Processing:
- Loads all .dat files in the specified directory.
- Reads each ECG signal and its annotations to locate R-peak positions and associated beat types.
#### 2. Filtering:
- Applies high-pass and low-pass filters to remove low-frequency drift and high-frequency noise.


### Step 3: Segment and Classify QRS Complexes
#### 1. Segmentation:
- Each heartbeat is segmented around the R-peak to capture the QRS complex.
- Segmented QRS complexes are stored in separate lists (data0 to data4) based on the beat type (N, S, F, V, U).
#### 2. Limiting the Dataset:
- Limits each type to 800 samples for balance, preparing for downstream analysis.


### Step 4: Dimensionality Reduction with PCA
#### 1. PCA:
- Reduces the dimensionality of the dataset to 60 components, preserving the key features of the QRS complexes.
- This helps in efficiently visualizing and analyzing the signal patterns.

#### 2.Transform:
- Each QRS class is transformed using the fitted PCA model, which enables plotting and visualization of clusters based on the QRS morphology.

### Step 5: Visualization and Correlation Analysis
#### 1. Visualization of QRS Complexes:
- Plots the first 100 samples of each class to visually assess the variations in QRS complexes.

#### 2. 2D PCA Plot:
- Projects each class on the first two PCA components to visualize their separability in the feature space.


## Applications and Advantages of PCA in ECG Analysis
### 1. Classification and Clustering: The clusters formed in PCA space reveal the differences in morphology between normal and abnormal beats, aiding in classification.
### 2. Anomaly Detection: PCA enables anomaly detection by revealing beats that deviate significantly from normal clusters.
### 3.Feature Engineering: The reduced PCA components can serve as input features for machine learning models, enhancing performance while reducing computational cost.

## Conclusion
PCA is a powerful technique in ECG signal processing. By reducing the dimensionality of QRS complexes, PCA simplifies data, enhances interpretability, and reveals insights into heartbeat variability across different arrhythmias. This makes PCA an ideal preprocessing step for further analysis, such as classification or anomaly detection.


