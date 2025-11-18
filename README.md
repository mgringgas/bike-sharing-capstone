# Capstone Project: Bike Sharing Demand Prediction

## Project Overview

Proyek ini bertujuan untuk memprediksi demand penyewaan sepeda pada sistem bike-sharing Capital Bikeshare menggunakan machine learning. Model prediksi ini membantu perusahaan mengoptimalkan inventory sepeda berdasarkan berbagai faktor seperti cuaca, waktu, dan musim.

## Business Problem

### Context
Sistem bike-sharing telah merevolusi cara orang menyewa sepeda di perkotaan dengan ekosistem yang sepenuhnya otomatis. Dengan lebih dari 500 program beroperasi global dan melayani lebih dari setengah juta unit sepeda, data yang dihasilkan menjadi sangat berharga untuk analisis mobilitas urban.

### Problem Statement
Tantangan utama adalah **memprediksi demand yang fluktuatif** berdasarkan waktu, cuaca, dan event kota. Prediksi yang meleset menyebabkan:
- **Stockout** → Pelanggan kecewa, revenue hilang, brand damage
- **Overstock** → Biaya operasional membengkak, profit rendah

### Goals
Membangun tool prediksi untuk menentukan jumlah unit sepeda yang perlu disediakan dengan tepat di setiap kondisi, sehingga dapat:
- Menjaga efisiensi operational cost
- Memenuhi kebutuhan pelanggan
- Maksimalkan revenue

## Dataset

**Sumber:** Capital Bikeshare (2011-2012)

**Ukuran:** 12,165 records (data per jam)

**Target Variable:** `cnt` (total rental bikes)

### Features

| Feature | Type | Description |
|---------|------|-------------|
| `dteday` | Object | Date |
| `season` | Integer | 1: Winter, 2: Spring, 3: Summer, 4: Fall |
| `hr` | Integer | Hour (0-23) |
| `holiday` | Integer | 0: Not holiday, 1: Holiday |
| `weekday` | Integer | Day of week (0: Sunday - 6: Saturday) |
| `workingday` | Integer | 0: Not working day, 1: Working day |
| `weathersit` | Integer | 1: Clear, 2: Mist, 3: Light Rain, 4: Heavy Rain |
| `temp` | Float | Normalized temperature in Celsius |
| `atemp` | Float | "Feels like" temperature in Celsius |
| `hum` | Float | Normalized humidity (0-1) |
| `windspeed` | Float | Normalized windspeed |
| `casual` | Integer | Count of casual users |
| `registered` | Integer | Count of registered users |
| `cnt` | Integer | **Target:** Count of total rental bikes |

## Methodology

### 1. Business Problem Understanding
- Analisis konteks bisnis bike-sharing
- Identifikasi problem statement dan goals
- Definisi stakeholder dan success metrics

### 2. Data Understanding
- Eksplorasi struktur dataset
- Pemahaman setiap feature dan target variable
- Validasi kualitas data (no missing values ✓)

### 3. Exploratory Data Analysis (EDA)
- **Distribusi Target:** Mean 189 bikes/jam, range 1-970 bikes/jam
- **Pola Temporal:** Peak hours di jam 8-9 pagi & 17-18 sore
- **Pola Musiman:** Demand tertinggi di Summer & Fall
- **Pengaruh Cuaca:** Clear weather = demand tertinggi
- **User Behavior:** 81% registered users, 19% casual users

### 4. Data Preprocessing
- Data cleaning (handling outliers)
- Feature engineering
- Encoding categorical variables
- Feature scaling
- Train-test split

### 5. Modeling
**Models Tested:**
- Linear Regression (baseline)
- Decision Tree
- Random Forest
- Gradient Boosting
- **XGBoost** (Final Model)

**Alasan Pemilihan XGBoost:**
- Performa terbaik pada cross-validation
- Mampu menangani non-linear relationships
- Robust terhadap outliers
- Feature importance yang jelas dan interpretable

### 6. Model Evaluation
**Metrics:**
- **MAE (Mean Absolute Error):** Rataan nilai absolut error
- **MAPE (Mean Absolute Percentage Error):** Rataan persentase error
- **R-squared:** Variance explained by model

**Top 5 Important Features:**
1. Hour (hr) - Pola commuter sangat kuat
2. Temperature (temp/atemp) - Cuaca nyaman tingkatkan demand
3. Season - Variasi musiman signifikan
4. Weather situation - Clear vs rainy berbeda drastis
5. Humidity - Faktor kenyamanan

## Results & Business Impact

### Model Performance
- Error rate rendah dengan prediksi akurat
- Feature importance sesuai dengan business understanding
- Model siap untuk production deployment

### Business Impact

**Sebelum ML:**
- ✗ Estimasi manual sering meleset
- ✗ Stockout di peak hours
- ✗ Overstock di low demand
- ✗ Biaya operasional tinggi

**Setelah ML:**
- ✓ Prediksi akurat per jam
- ✓ Optimasi inventory
- ✓ Efisiensi biaya operasional
- ✓ Kepuasan pelanggan meningkat

**Expected Impact:**
- Pengurangan operational cost 15-20%
- Peningkatan customer satisfaction
- Peningkatan bike utilization rate

## Recommendations

### Operasional
1. **Peak Hour Management**
   - Tambah stock di jam 8-9 pagi & 17-18 sore
   - Pre-positioning sepeda di stasiun high-demand
   - Strategi redistribusi sebelum peak hours

2. **Weather-Based Strategy**
   - Kurangi stock saat prediksi hujan
   - Maksimalkan availability saat cuaca cerah
   - Dynamic pricing saat high demand

3. **Seasonal Planning**
   - Maintenance di musim dingin (low demand)
   - Full capacity di musim panas & gugur
   - Kampanye marketing di low season

### Technical
- Deploy model sebagai API untuk real-time prediction
- Retrain model berkala (quarterly) dengan data baru
- Tambah fitur: event calendar, traffic data
- Dashboard monitoring actual vs predicted
- Alert system untuk anomaly detection

### Business Development
- Implementasi dynamic pricing
- Partnership dengan event organizer
- Targeted marketing saat low demand
- Ekspansi ke lokasi baru menggunakan model insights

## Tech Stack

- **Python 3.x**
- **Libraries:**
  - `pandas` - Data manipulation
  - `numpy` - Numerical computing
  - `matplotlib` & `seaborn` - Data visualization
  - `scikit-learn` - Machine learning
  - `xgboost` - Gradient boosting

## How to Run

### Prerequisites
- Python 3.x
- Jupyter Notebook atau Jupyter Lab

### Installation & Setup

1. **Clone repository atau download files**

2. **Install dependencies:**
   ```bash
   pip install pandas numpy matplotlib seaborn scikit-learn xgboost jupyter
   ```

3. **Install optional dependencies (untuk generate presentation):**
   ```bash
   pip install python-pptx PyPDF2
   ```

### Running the Project

1. **Run Jupyter Notebook:**
   ```bash
   jupyter notebook capstone_bike_sharing.ipynb
   ```
   
2. **Jalankan semua cells** untuk melihat analisis lengkap dari:
   - Business Problem Understanding
   - Data Understanding & EDA
   - Data Preprocessing
   - Modeling & Evaluation
   - Conclusion & Recommendations

3. **Generate PowerPoint Presentation (optional):**
   ```bash
   python create_presentation.py
   ```
   File `Presentasi_Bike_Sharing_Capstone.pptx` akan dibuat secara otomatis

## Key Insights

1. **Hour adalah prediktor terkuat** - Pola commuter sangat jelas dengan peak di pagi dan sore
2. **Temperature berpengaruh signifikan** - Cuaca nyaman meningkatkan demand
3. **Registered users dominan** - 81% dari total users, terutama di hari kerja
4. **Seasonal variation jelas** - Summer & Fall memiliki demand tertinggi
5. **Weather condition critical** - Clear weather vs rainy berbeda drastis

## Limitations

- Model trained pada data 2011-2012, perlu update berkala
- Special events (festival, konser) belum tercapture
- Bergantung pada akurasi weather forecast
- Perlu monitoring performa di production

## Author

**Capstone Project - Machine Learning Module 3**  
Michael Gary Ringgas

---

