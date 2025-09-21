1. Problem Statement

The project aims to automatically classify heartbeats from ECG signals into different categories (normal or arrhythmia types). Detecting arrhythmias early can help prevent heart diseases and save lives.

2. Dataset

I used a public dataset (MIT-BIH Arrhythmia / Kaggle version), which contains pre-segmented ECG beats. Each beat is labeled into one of 5 classes (normal and 4 types of arrhythmias).

3. Preprocessing

Each heartbeat vector was z-score normalized (so that amplitude differences don’t bias the model).

No additional filtering was needed, since the data was already segmented.

4. Baseline Model

As a first step, I trained a RandomForest classifier directly on the raw normalized ECG beats.

This gave me a baseline accuracy/F1 score to compare against.

5. Class Imbalance Handling

The dataset is imbalanced (normal beats are much more frequent than abnormal ones).

To solve this, I applied SMOTE (Synthetic Minority Oversampling Technique), which generates synthetic beats for minority classes.

This improved balance in the training set and helped the classifier learn better.

6. Feature Engineering

Instead of just using raw signals, I extracted meaningful features:

Statistical features: mean, std, RMS, skewness, kurtosis, peak-to-peak amplitude.

Spectral features: power spectral density, band powers, spectral entropy.

Wavelet features: energy of wavelet coefficients.

This transformed each heartbeat into a feature vector that captures its morphology and frequency content.

7. Models Evaluated

RandomForest Classifier: good at handling noisy features, interpretable.

Support Vector Machine (SVM): effective in high-dimensional feature spaces.

8. Results

With just raw beats, RandomForest worked decently but struggled with minority classes.

After applying SMOTE, recall for minority arrhythmia classes improved.

With feature engineering, performance further improved — the RandomForest could distinguish between all classes better.

Example: In the confusion matrix, most normal beats (class 0) are correctly classified, but some overlap occurs with arrhythmic classes (expected in ECGs).

9. Key Takeaways

Preprocessing (normalization) + imbalance handling (SMOTE) + feature engineering significantly improved performance.

RandomForest performed robustly and was faster to train than SVM.

The project shows how classical ML methods can still be powerful for biomedical signal classification.

10. Real-World Impact

If deployed in a hospital or wearable device, this pipeline could automatically alert doctors when irregular heartbeats are detected, helping in early diagnosis of arrhythmia.
