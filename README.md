# Neuroimaging Analysis of Naturalistic Stimuli: Forrest Gump Project

> **A Multi-modal fMRI Analysis of the "Forrest Gump" Movie Watching Task**

**Author:** Ziyu Wang (Master's Project, 2025)  
**Institution:** Sino-Danish Center (SDC) / Institute of Biophysics, Chinese Academy of Sciences (CAS)

---

## 📖 Project Overview

This repository hosts the code and analysis pipeline for a neuroimaging master's project investigating brain dynamics under naturalistic conditions. Utilizing the **StudyForrest** dataset (3T fMRI extension), this project analyzes data from **15 participants** watching the movie *Forrest Gump*.

The core objective is to map high-dimensional brain activity into low-dimensional state trajectories and explore the synchronization between neural responses, movie content, and emotional experiences.

### Key Features
* **Multi-modal Alignment:** Precise synchronization of fMRI time-series, movie video stimuli, and continuous emotion ratings (TR = 2s).
* **Dimensionality Reduction:** Implementation of **UMAP** to project whole-brain signals into a 3D latent space.
* **Dynamic Synchronization:** Visualization of inter-subject synchronization (ISS) evolving over the 2-hour movie.
* **Emotion Decoding:** Analysis of 6 basic emotions and their PCA components (Polarity, Complexity, Intensity).

---

## ⚠️ Data Availability & Disclaimer

**Important:** This repository **does not** contain raw fMRI data or movie files due to copyright and storage limitations. All data used in this project is publicly available.

To reproduce the results, please acquire the data from the official sources:

1.  **fMRI Data (3T Extension)** * **Source:** [StudyForrest.org](http://studyforrest.org) or OpenNeuro.
    * **Description:** 15 subjects, 2-hour movie watching task, TR=2s.
    * *Reference:* [Hanke et al., Scientific Data (2016)](https://www.nature.com/articles/sdata201692)

2.  **Emotion Annotations** * **Source:** [OSF Repository (Lettieri et al.)](https://osf.io/tzpdf/)
    * **Description:** Continuous ratings for Happiness, Surprise, Fear, Sadness, Anger, and Disgust (10Hz).
    * *Reference:* [Lettieri et al., Nature Communications (2019)](https://www.nature.com/articles/ncomms10608)

---

## ⚙️ Methodology

### 1. Data Preprocessing
* **Pipeline:** Standard preprocessing using **fMRIPrep (v23.2.1)** (Motion correction, Slice timing, MNI normalization).
* **Overlap Removal:** Following the StudyForrest protocol, overlapping segments between the 8 movie runs were removed to create a concatenated time-series.
    * *Removed:* First 3 TRs (6s) and last 5 TRs (10s) of overlapping cuts.
    * *Final Duration:* 3543 TRs (approx. 2 hours).

### 2. Emotion Analysis (PCA)
Continuous ratings were downsampled to 0.5Hz to match fMRI TRs. **Principal Component Analysis (PCA)** revealed three latent dimensions explaining ~85% of the variance:
* **PC1 (45%):** Polarity (Positive vs. Negative valence).
* **PC2 (24%):** Complexity (Cognitive demand of the emotion).
* **PC3 (16%):** Intensity (Arousal level).

### 3. UMAP & Synchronization
* **Input:** Stacked time-series arrays from 15 subjects (Shape: `53145 x N_ROIs`).
* **Algorithm:** **UMAP** (Uniform Manifold Approximation and Projection) reduced data to 3 components.
* **Metric:** Inter-subject synchronization was quantified by calculating the Euclidean distance of each subject to the group centroid in the low-dimensional space.

---

## 📊 Visualization Highlights

### Brain State Trajectory
We generated dynamic 3D animations to visualize how participants' brain states evolve.
* **Points:** Represent individual subjects.
* **Color:** Represents the current emotional intensity or movie scene cluster.
* **Output:** `trajectory_animation.html` (Interactive 3D plot).

### Scene-Emotion Query System
The codebase includes a utility to query specific timepoints:
```python
# Example: Querying the 5th TR
movie_file, time_point = get_movie_info(tr=5)
# Output:
# > Movie: forrest_04.mp4 (Run 4) at 00:10
# > Emotion: Fear (High), Happiness (Low)
