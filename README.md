# 🧪 Particles Trajectory Prediction

Predicting particle positions from signals detected by Resistive Silicon Detector (RSD) sensors using machine learning.

---

## 🔍 Project Summary

This project focuses on a regression task: predicting the 2D positions of particles based on signal data collected from RSD sensors. Each event consists of measurements from 18 pads (12 real, 6 noise) and 5 signal features.

---

## 📦 Dataset

* **Total Events**: 514,000
* **Training Set**: 385,500 labeled samples
* **Test Set**: 128,500 samples
* **Features per Event**:

  * 5 signal types: `pmax`, `negpmax`, `tmax`, `area`, `rms`
  * From 18 pads → 90 features per event

---

## ⚙️ Preprocessing

* **Noise Removal**: Excluded 6 noisy pads: 0, 7, 12, 15, 16, 17
* **Outlier Filtering**:

  * **Z-score**: Detected abnormal values per event
  * **Mahalanobis Distance**: Accounted for feature correlations
* **Feature Selection**:

  * Used Random Forest to assess feature importance
  * Kept: `pmax`, `negpmax`, `area`

---

## 🤖 Models

### Random Forest Regressor ✅

* Best performance
* Handles noise and high-dimensional data well

### k-Nearest Neighbors

* Local-based predictions
* Slower and less robust to noise

---

## 🔧 Hyperparameter Tuning

Used grid search to optimize:

**Random Forest**

* `n_estimators`: 300
* `max_depth`: 40
* `max_features`: sqrt
* `min_samples_leaf`: 2
* `min_samples_split`: 2
* `criterion`: squared\_error

**kNN**

* `n_neighbors`: 10
* `weights`: uniform
* `algorithm`: auto

---

## 📊 Results

| Model         | R² Score   | MAE  | MSE   | Public Score |
| ------------- | ---------- | ---- | ----- | ------------ |
| Random Forest | **0.9991** | 2.67 | 12.16 | **4.750**    |
| kNN           | 0.9985     | 2.81 | 20.12 | 5.683        |

> **Public Score**: Avg. Euclidean distance between predicted and true positions

---

## 📈 Key Takeaways

* Successfully filtered sensor noise and irrelevant features
* Random Forest yielded highly accurate particle position predictions
* Achieved R² score of **0.9991** on validation
* Scalable approach with potential for deep learning extensions

---

## 🧠 Future Work

* Experiment with **neural networks** for generalization
* **Refine hyperparameter tuning** with advanced search techniques
* Add **k-fold cross-validation** for robust evaluation
* Explore **additional denoising** and signal enhancement methods

---

## 👥 Authors

* **Tommaso Mazzarini** – Politecnico di Torino – [tommaso.mazzarini@studenti.polito.it](mailto:tommaso.mazzarini@studenti.polito.it)
* **Leonardo Merelli** – Politecnico di Torino – [leonardo.merelli@studenti.polito.it](mailto:leonardo.merelli@studenti.polito.it)
