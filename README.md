# 📊 Employee Attrition Prediction using Big Data Ecosystem

Proyek ini merupakan implementasi analitik Big Data untuk memprediksi **retensi karyawan (employee attrition)** dalam modul **Human Capital Management (HCM)** pada sistem ERP.

Dikembangkan sebagai proyek akhir mata kuliah **Big Data dan Analitik (CSD60707)**, proyek ini memanfaatkan ekosistem Big Data seperti **Hadoop, Apache Spark, dan Spark MLlib** untuk membangun pipeline analitik end-to-end.

---

## 🎯 Objectives

* 🔍 **Employee Retention Prediction**
  Memprediksi apakah karyawan berpotensi keluar (Attrition)

* 👥 **Employee Segmentation**
  Mengelompokkan karyawan berdasarkan karakteristik menggunakan clustering

* 💡 **HR Insights & Recommendation**
  Memberikan insight berbasis data untuk strategi retensi karyawan

---

## 🏗️ Architecture

Menggunakan pendekatan **Medallion Architecture**:

* **Data Ingestion**: MinIO (S3-compatible) + Python (Jupyter)
* **Storage**: MinIO Object Storage
* **Processing**: Apache Spark (DataFrame API)
* **Analytics**: Spark MLlib
* **Visualization**: Jupyter Notebook (Matplotlib, Seaborn)

---

## ⚙️ Tech Stack

* Apache Spark
* Hadoop (S3A Connector)
* Spark MLlib
* MinIO
* Python (PySpark, Pandas, Boto3)
* Jupyter Notebook

---

## 📂 Dataset

* **Source**: IBM HR Analytics Employee Attrition Dataset (Kaggle)
* **Format**: CSV
* **Records**: 1,470 rows
* **Features**: 35 columns

### Selected Features for Modeling:

| Feature                 | Type            |
| ----------------------- | --------------- |
| MonthlyIncome           | Numeric         |
| YearsAtCompany          | Numeric         |
| JobSatisfaction         | Numeric         |
| EnvironmentSatisfaction | Numeric         |
| WorkLifeBalance         | Numeric         |
| JobRole                 | Categorical     |
| Department              | Categorical     |
| Attrition               | Target (Yes/No) |

---

## 🔄 Data Pipeline

1. **Data Acquisition**

   * Upload dataset ke MinIO (`/raw/`)

2. **Data Loading**

   * Load data dari MinIO ke Spark DataFrame

3. **Preprocessing**

   * Handle missing values
   * Encoding (StringIndexer + OneHotEncoder)
   * Normalization (MinMaxScaler)
   * Label transformation (Yes/No → 1/0)

4. **Modeling**

   * Train/Test Split (80:20)
   * Model:

     * Random Forest Classifier
     * Logistic Regression

5. **Evaluation**

   * AUC-ROC
   * Precision
   * Recall
   * F1-Score
   * Confusion Matrix

---

## 🤖 Machine Learning Models

### 1. Random Forest Classifier

* Cocok untuk data campuran (numerik + kategorikal)
* Menyediakan feature importance

### 2. Logistic Regression

* Model baseline
* Mudah diinterpretasikan

### 3. Clustering (K-Means)

* Digunakan untuk segmentasi karyawan
* Insight tambahan untuk HR

---

## 📊 Output & Insights

* Prediksi karyawan berisiko keluar
* Segmentasi kelompok karyawan
* Insight faktor utama attrition
* Rekomendasi strategi retensi HR


