Quick Guide: EMG Feature Extraction & Classification Workflow
Overall Process Flow
•	Main script (features_main.m) calls functions to process one subject at a time
•	Manual subject ID change needed ('s1' → 's2', etc.) - run separately for all 15 subjects
•	Two parallel pipelines: Time Domain (40 features) and Frequency Domain (6 features)

Step-by-Step Code Execution
1. Data Loading
•	Loads subject .mat file (e.g., s1_delsysEMG.mat)
•	Contains 3-channel EMG data from forearm muscles (2000 Hz sampling)
2. Preprocessing (in featuresextract_a.m)
•	Signal normalization
•	Bandpass filter: 45th-order FIR, 20-500 Hz (removes artifacts)
•	Notch filter: 50 Hz IIR (removes power line interference)
3. Segmentation
•	Window size: 300 ms (600 samples)
•	Overlap: 50% (150 ms)
•	Windowing options: Rectangular, Hamming, Hann, Blackman, Bartlett, Kaiser, Gaussian, Chebyshev
o	Manually uncomment desired window type before running
4. Feature Extraction (in getFeatures.m)
•	For each channel (3 muscles):
o	Time Domain: 40 features (WL, ZC, RMS, VAR, etc.)
o	Frequency Domain: 6 features (Mean/Median Frequency, Band Power, etc.)
•	Combines all channels → 120 features (40×3) for time domain or 18 features (6×3) for frequency domain
•	Adds class labels (1-15 for finger movements)
5. Output
•	Exports Excel file: features_extracted_subjectX.xlsx
•	Contains features + labels ready for classification

Classification Phase (separate step)
•	Load extracted Excel features into MATLAB Classification Learner App
•	Test models: Decision Trees, SVM, KNN, Neural Networks
•	Hyperparameters manually per model

Summary  
•	Total feature files will be 1680    (8 windowing x 7 classifiers x 2 sets x 15 subjects) 
•	112 unique (window + classifier) combinations per feature set
•	1,680 total model training runs across all subjects
•	Each combination needs manual hyperparameter tuning in Classification Learner App

