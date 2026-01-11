Neuroimaging Analysis of Naturalistic Stimuli: Forrest Gump Project
A Multi-modal fMRI Analysis of the "Forrest Gump" Movie Watching Task

Author: Ziyu Wang (2025)

Institution: Sino-Danish Center (SDC) / Institute of Biophysics, CAS

📖 Overview
This repository contains the code and analysis pipeline for a neuroimaging project investigating brain dynamics during naturalistic stimuli. Utilizing the StudyForrest dataset (3T fMRI extension), this project analyzes data from 15 participants watching the movie Forrest Gump.

Key features of this project include:

Multi-modal Alignment: Synchronization of fMRI time-series, movie stimuli, and continuous emotion ratings (TR = 2s).

Dimensionality Reduction: Using UMAP to project high-dimensional whole-brain signals into a low-dimensional state space.

Inter-Subject Synchronization: visualizing the similarity of brain states across participants dynamically over time.

Emotion Decoding: correlating basic emotion ratings (and their PCA components) with neural trajectories.

⚠️ Data Availability & Disclaimer
Note: This repository does not contain the raw fMRI data or the movie files due to copyright and size constraints.

All data used in this project is publicly available from the following sources:

fMRI Data (3T Extension): The dataset (15 subjects) can be downloaded from OpenNeuro or the StudyForrest website.

Reference: A studyforrest extension, simultaneous fMRI and eye gaze recordings during prolonged natural stimulation (Scientific Data, 2016)

Emotion Annotations: Continuous ratings for 6 basic emotions provided by 12 observers.

Source: OSF Repository

Reference: Emotionotopy in the human right temporo-parietal cortex (Nature Communications)

To run the code in this repository, you must download the datasets and update the file paths in the configuration scripts.

⚙️ Methodology
1. Data Preprocessing
fMRIPrep (v23.2.1): Standard preprocessing pipeline including slice timing correction, motion correction, and spatial normalization (MNI152NLin6Asym).

Time-series Extraction:

Data was segmented into 8 runs corresponding to movie cuts.

Overlap Removal: Following the StudyForrest protocols, overlapping TRs at the beginning and end of each run were removed to create a continuous time-series (Total TRs = 3543).

Denoising: Nuisance regression (motion parameters) and temporal filtering.

2. Emotion Annotation Processing
Raw ratings for Happiness, Surprise, Fear, Sadness, Anger, and Disgust (10Hz) were downsampled to match the fMRI TR (0.5Hz / 2s).

PCA Analysis: Performed on emotion ratings, revealing 3 main components explaining ~85% of variance:

Polarity (Positive/Negative)

Complexity

Intensity

3. Dimensionality Reduction (UMAP)
Whole-brain functional connectivity (or ROI-based signals) from 15 subjects were stacked.

UMAP (Uniform Manifold Approximation and Projection) was applied to reduce the dimensions to 3 components.

This allows for the visualization of "Brain State Trajectories" in a 3D space.

4. Synchronization Metrics
Calculated the Euclidean distance of each subject to the group centroid in the UMAP space.

Closer distance indicates higher inter-subject synchronization during specific movie scenes.

📊 Visualization Highlights
Brain State Trajectory Animation
One of the core outputs of this project is a dynamic HTML animation showing how the 15 subjects' brain states evolve over the 2-hour movie.

Visual: Points represent subjects in the UMAP space.

Dynamics: Points cluster together during highly engaging emotional scenes (high synchronization) and disperse during resting or transitional scenes.

(You can find the trajectory_animation.html in the results folder)

Movie-fMRI-Emotion Alignment
The code enables querying specific Time Repetition (TR) points to retrieve:

The exact frame/timestamp of the movie.

The corresponding fMRI signal state.

The intensity of the 6 basic emotions at that moment.


Plaintext

> Movie: forrest_04.mp4 (Run 4)
> Emotion Ratings: 
  Happiness: 0.00 | Surprise: 8.78 | Fear: 31.94 | Sadness: 22.83

💻 Requirements
To run the analysis notebooks, you will need the following Python packages:

numpy, pandas, scipy

nibabel, nilearn (for neuroimaging data)

umap-learn (for dimensionality reduction)

scikit-learn (for PCA and clustering)

matplotlib, plotly (for visualization)

h5py

📚 References
Dataset: Hanke et al. (2016). A studyforrest extension, simultaneous fMRI and eye gaze recordings during prolonged natural stimulation. Scientific Data.

Original 7T Data: Hanke et al. (2014). A high-resolution 7-Tesla fMRI dataset from complex natural stimulation with an audio movie. Scientific Data.

Emotion Processing: Lettieri et al. (2019). Emotionotopy in the human right temporo-parietal cortex. Nature Communications.
