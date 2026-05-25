# 🫀 ECG Heartbeat Classification System

A comprehensive full-stack Machine Learning application for classifying heartbeats using Electrocardiogram (ECG) signals. This project integrates real-time hardware data acquisition (Arduino), a powerful Python backend with multiple Machine Learning models and Explainable AI (XAI), along with a modern React-based user interface.

## ✨ Key Features

* **Multi-Model Classification**: Classifies ECG signals into 5 heartbeat categories:

  * **Normal**
  * **Supraventricular Ectopic Beat**
  * **Ventricular Ectopic Beat**
  * **Fusion Beat**
  * **Unknown Beat**

  using various Machine Learning models:

  * Logistic Regression (implemented from scratch & Scikit-learn)
  * Support Vector Classifier (SVC - custom QP optimization & Scikit-learn)
  * Gradient Boosting Classifier
  * XGBoost

* **Advanced Data Processing**:

  * Handles class imbalance using:

    * **SMOTE** (Synthetic Minority Oversampling Technique)
    * **Class Weight Balancing**
  * Feature extraction using:

    * **FFT (Fast Fourier Transform)** for frequency-domain analysis.

* **Explainable AI (XAI)**:
  Understand and interpret model predictions through:

  * **SHAP** (SHapley Additive exPlanations)
  * **LIME** (Local Interpretable Model-agnostic Explanations)

* **Hardware Integration**:
  Real-time ECG signal acquisition using:

  * Arduino
  * AD8232 ECG sensor

* **Modern User Interface**:
  Responsive and interactive frontend built with:

  * React
  * Vite
  * Tailwind CSS

---

## 🛠️ Technologies Used

### Frontend

* React 19
* Vite
* Tailwind CSS
* Shadcn UI / Radix UI
* Chart.js

### Backend

* Python 3.10
* Flask
* Scikit-learn
* XGBoost
* CVXOPT

### Hardware

* Arduino
* AD8232 ECG Sensor

### Data Processing & XAI

* Pandas
* NumPy
* SHAP
* LIME

---

## 📂 Project Structure

* `/backend/`
  Contains:

  * Flask API server (`app.py`)
  * Trained Machine Learning models (`.pkl`)
  * Model explanation scripts (`shap_xgboost.py`, `lime_xgboost.py`)
  * Python dependencies

* `/src/` & `/public/`
  Source code for the React frontend application.

* `/ecg/`
  Contains:

  * Arduino source code (`.ino`)
  * Python scripts for serial communication, ECG signal reading, and real-time plotting.

* `mitbih_train.csv`
  Training dataset from the MIT-BIH Arrhythmia Database.

---

# 🚀 Installation & Setup Guide

## 1. Backend Setup

1. Open a terminal and navigate to the project directory:

   ```bash
   cd ECG-heartbeat-classifier
   ```

2. Create and activate a Python virtual environment (Python 3.10 recommended):

   ```bash
   python -m venv venv

   # Windows
   venv\Scripts\activate

   # macOS/Linux
   source venv/bin/activate
   ```

3. Navigate to the backend folder:

   ```bash
   cd backend
   ```

4. Install required dependencies:

   ```bash
   pip install numpy==1.26.4 scikit-learn==1.2.2 flask flask-cors joblib pandas xgboost cvxopt matplotlib
   ```

   *(Note: If you encounter NumPy compatibility issues, try using `numpy==1.24.4` instead.)*

5. Start the Flask server:

   ```bash
   python app.py
   ```

   The backend API will run at:

   ```bash
   http://localhost:5000
   ```

---

## 2. Frontend Setup

1. Open a **new terminal window** and navigate to the project root directory (`ECG-heartbeat-classifier`).

2. Install Node.js dependencies:

   ```bash
   npm install
   ```

3. Start the Vite development server:

   ```bash
   npm run dev
   ```

   The frontend application will be available at:

   ```bash
   http://localhost:5173
   ```

---

## 3. Hardware Setup (Optional for Real-Time Data)

If you are using the AD8232 sensor for real ECG acquisition:

1. Upload the `ecg/ad8232.ino` code to your Arduino board.

2. Run the Python scripts inside the `ecg/` folder, for example:

   ```bash
   python ecg_test_realtime_flaskplot.py
   ```

   These scripts will:

   * Read ECG data from the serial port
   * Process the signals
   * Display real-time ECG plots

---

# 📖 Usage Guide

1. Open the web application in your browser.

2. Select an ECG sample from the dropdown menu.

   * Samples are randomly extracted from `mitbih_train.csv`
   * Ensures representation of all 5 heartbeat classes.

3. Click the **"Classify"** button.

4. View prediction results from different Machine Learning models.

5. Explore **SHAP** and **LIME** visualizations to understand:

   * Which timesteps
   * Which signal features

   contributed most to the XGBoost model’s prediction.

---

# 📚 References

* [1] Alec Radford, Luke Metz, & Soumith Chintala (2016). *Unsupervised Representation Learning with Deep Convolutional Generative Adversarial Networks*. arXiv:1805.00794.
  [Paper Link](https://arxiv.org/abs/1805.00794?utm_source=chatgpt.com)
