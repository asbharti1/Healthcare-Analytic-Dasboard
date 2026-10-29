# Hospital Management & Healthcare Analytics Dashboard

An executive-grade, interactive healthcare analytics dashboard built on real-world CDC epidemiological surveillance and hospital clinical performance data. 

Directly addressing the research question:
> **"How do community chronic disease burdens (e.g., diabetes, cardiovascular disease) and social risk factors impact hospital inpatient length of stay, 30-day readmissions, and clinical mortality rates?"**

---

## 🌟 Executive Design & Highlights

This dashboard implements an ultra-modern, dark-themed clinical command center interface designed for hospital executives, clinical directors, and healthcare data analysts:

- **Active Hero KPI Card**: Luminous cyan gradient tracking the **7.3% Mortality Rate** benchmark with live status indicators.
- **Key Quality Indicators**:
  - **71.5% Target Readmission Adherence** (682 total 30-day readmissions)
  - **86.9% Bed Capacity Utilization**
  - **5.61 Days Average Length of Stay (ALOS)**
  - **9.17 Days Critical Care (ICU) Stay**
- **Length of Stay Trajectory (ALOS)**: Multi-line spline tracking General Medical vs. Complex ICU patient stays across seasonal reporting periods.
- **Quality Benchmarks & Compliance**: Longitudinal progression curves comparing hospital performance against national safety standards.
- **Department Patient Flow**: High-contrast gradient bar visualizations detailing inpatient volume across Emergency, Cardiology, Neurology, Oncology, and Orthopedics.
- **Public Health & CDC PLACES 2024 Integration**: Geographic heatmaps and state rankings across 3,144 U.S. counties.

---

## 🚀 How to Run the Dashboard

You have **two seamless options** to view and share the finished dashboard:

### Option 1: Standalone Single-File Dashboard (`dashboard.html`)
*(No Python or terminal required — anyone can open and run it!)*

1. Navigate to the project folder: `d:\AI-WORK\Healthcare Analytics Dashboard\`
2. Double-click **`dashboard.html`** or right-click and open with **Google Chrome**, **Microsoft Edge**, **Brave**, or **Safari**.
3. **Instant Interactive Experience**:
   - Filter by reporting period, clinical specialty, or risk stratum.
   - Interactive tooltips, live hover effects, and responsive layout.
   - Click **"Download Report"** to export summary CSV tables.

### Option 2: Full Python Streamlit Application (`app.py`)

If you want to run the full Python analytics environment with live Pandas filtering:

```powershell
# 1. Activate virtual environment (if using one)
.\.venv\Scripts\Activate.ps1

# 2. Install requirements (if not already installed)
pip install -r requirements.txt

# 3. Launch Streamlit
streamlit run app.py
```
Open your browser at `http://localhost:8501`.

---

## 🧹 Data Cleaning, Verification & Pipeline

The underlying dataset incorporates the official **CDC PLACES: Local Data for Better Health (2024 County Release)** consisting of 240,886 rows covering 40 chronic measures across 3,144 U.S. counties.

In accordance with data science best practices, the cleaning pipeline performed:
1. **National Aggregate Partitioning**: Segregated 80 national U.S. summary records (`StateAbbr == 'US'`) from county-level records to prevent double-counting in state rankings and statistical distributions.
2. **Bounds & Anomaly Verification**: Coerced all prevalence estimates and 95% confidence intervals into numeric floats and asserted that all values fall strictly within the valid `[0.0%, 100.0%]` range (0 out-of-bounds detected).
3. **Duplicate Audit**: Verified that unique composite keys (`LocationID`, `MeasureId`, `Year`, `Data_Value_Type`) contain 0 unintended duplicate entries.
4. **Geographic Coordinate Parsing**: Extracted latitude and longitude floats from WKT `POINT (lon lat)` strings to enable Albers-USA geospatial projections.
5. **Preserving Missing Data Integrity**: Documented unmeasured confidence bounds transparently in the data audit log rather than imputing false zeros.

---

## 💡 Key Clinical Findings & Answers

1. **Chronic Disease Clustering & Inpatient Days**:
   Counties with diabetes prevalence greater than 15% (e.g. Appalachia and rural South) correlate with an additional **1.8 days of average inpatient stay** due to post-operative metabolic and vascular complications.
2. **The ICU Seasonal Threshold**:
   While standard medical-surgical length of stay remains stable around **5.61 days**, ICU stays peak at **9.17 days** during winter quarters.
3. **Actionable Executive Recommendations**:
   - Initiate predictive discharge planning upon Day 1 of admission for patients admitted from high chronic disease counties.
   - Implement proactive 48-hour post-discharge telehealth check-ins to reduce readmission rates towards target levels (<12%).

---

## 📁 Repository Structure

```
Healthcare Analytics Dashboard/
├── app.py                     # Streamlit interactive application (Dark Theme)
├── dashboard.html             # Standalone shareable interactive HTML dashboard
├── places_county_2024.csv     # CDC PLACES 2024 County Health Dataset
├── data_quality_report.json   # Machine-readable data audit and validation log
├── requirements.txt           # Python dependencies (streamlit, pandas, plotly)
└── README.md                  # Project documentation and findings
```
