# 🏢 Prediksi Retensi Karyawan — Modul Human Capital ERP
> Mata Kuliah: Big Data dan Analitik (CSD60707) — Kelompok 3

## 👥 Anggota Tim
| Nama | NIM | Peran |
|------|-----|-------|
| Raya Abiathar | 235150400111001 | Data Engineer (Ingestion) |
| Annisa Kayla Jasmine | 235150407111004 | Data Analyst (Spark Processing) |
| Fadilah Puji Laily Maulidiyah | 245150401111008 | ML Engineer (Modeling & Analytics) |
| Dinda Azqa Nur Ramadhani | 235150407111041 | Project Manager & Documentation |

---

## 📌 Deskripsi Proyek
Proyek ini membangun pipeline analitik Big Data end-to-end untuk memprediksi retensi karyawan menggunakan dataset IBM HR Analytics Employee Attrition & Performance (1.470 records, 35 atribut). Pipeline dibangun di atas ekosistem Hadoop, Apache Spark, dan MinIO dengan pendekatan **Medallion Architecture (Bronze → Silver → Gold)**.

### Tujuan
- **Klasifikasi**: Memprediksi apakah seorang karyawan akan keluar dari perusahaan
- **Segmentasi**: Mengidentifikasi kelompok karyawan berisiko tinggi menggunakan K-Means
- **Rekomendasi**: Menghasilkan insight berbasis data untuk program retensi HR

---

---

## 🛠️ Tech Stack
| Komponen | Teknologi |
|----------|-----------|
| Data Storage | MinIO (S3-compatible) |
| Data Processing | Apache Spark (DataFrame API) |
| Machine Learning | Spark MLlib |
| Notebook & Visualisasi | Jupyter Notebook, Matplotlib, Seaborn |
| Bahasa | Python |

---

## 📊 Dataset
- **Sumber**: [Employee Attrition & Retention Analytics Dataset
](https://www.kaggle.com/datasets/ajinkyachintawar/employee-attrition-and-retention-analytics-dataset) (Kaggle)
- **Ukuran**: 1.470 baris × 35 kolom
- **Target**: `left_company` (0 = Bertahan, 1 = Keluar)
- **Class Imbalance**: 83.9% Bertahan vs 16.1% Keluar (rasio 5.2:1)

### Fitur yang Digunakan
| Fitur | Tipe | Keterangan |
|-------|------|------------|
| Age_scaled | Numerik | Usia karyawan (dinormalisasi) |
| MonthlyIncome_scaled | Numerik | Pendapatan bulanan (dinormalisasi) |
| JobSatisfaction_scaled | Numerik | Tingkat kepuasan kerja |
| PerformanceRating_scaled | Numerik | Rating performa |
| WorkLifeBalance_scaled | Numerik | Keseimbangan kerja-hidup |
| YearsAtCompany_scaled | Numerik | Lama bekerja di perusahaan |
| Department_index | Kategorikal | Departemen (0=R&D, 1=Sales, 2=HR) |
| JobRole_index | Kategorikal | Peran jabatan |
| Gender_index | Kategorikal | Jenis kelamin |
| OverTime_index | Kategorikal | Status lembur |

---

## 🤖 Model & Hasil

### Random Forest Classifier (Model Utama)
| Metrik | Nilai |
|--------|-------|
| AUC-ROC | **0.8146** ✅ |
| Accuracy | 0.8346 |
| Precision | 0.7963 |
| Recall | 0.8346 |
| F1-Score | 0.7816 |

### Logistic Regression (Baseline)
| Metrik | Nilai |
|--------|-------|
| AUC-ROC | 0.7640 |
| Accuracy | 0.8465 |
| Precision | 0.8704 |
| Recall | 0.8465 |
| F1-Score | 0.7892 |

> **Random Forest dipilih sebagai model utama** karena AUC-ROC lebih tinggi (0.8146 vs 0.7640), yang merupakan metrik paling relevan pada data imbalanced. Logistic Regression terbukti sangat bias ke kelas mayoritas (FP=0 pada confusion matrix).

### Feature Importance (Random Forest)
| Rank | Fitur | Score |
|------|-------|-------|
| 1 | Age_scaled | 0.210 |
| 2 | MonthlyIncome_scaled | 0.203 |
| 3 | OverTime_index | 0.194 |
| 4 | YearsAtCompany_scaled | 0.164 |
| 5 | JobRole_index | 0.083 |

---

## 🔵 Segmentasi K-Means (k=3)
| Cluster | Total | Attrition | Bertahan | Rate | Profil |
|---------|-------|-----------|----------|------|--------|
| Cluster 0 | 535 | 81 | 454 | 15.1% | Karyawan muda, income rendah, tenure pendek |
| Cluster 1 | 618 | 104 | 514 | 16.8% | Mid-level heterogen, prioritas utama retensi |
| Cluster 2 | 317 | 52 | 265 | 16.4% | Senior, income tinggi, tenure panjang |

---

## 💡 Rekomendasi HR
1. **Kurangi beban overtime** — OverTime adalah faktor risiko signifikan (importance 0.194)
2. **Program karier untuk karyawan muda** — Age & MonthlyIncome adalah prediktor terkuat
3. **Fokus pada Departemen Sales** — tingkat attrition tertinggi dibanding R&D dan HR
4. **Intervensi dini pada Cluster 1** — kelompok terbesar dengan attrition rate tertinggi
5. **Jadikan Cluster 0 benchmark** — attrition rate terendah, cocok jadi acuan rekrutmen
6. **Integrasikan RF ke ERP** sebagai early warning system yang dijalankan tiap kuartal
