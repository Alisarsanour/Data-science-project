# Data-science-project
An end-to-end data science study analyzing architectural factors affecting building energy performance, featuring machine learning imputation, exploratory data analysis (EDA), and Simpson's Paradox resolution.
# 🏢 Building Energy Efficiency & Thermal Load Analysis

An end-to-end data science and statistical modeling study analyzing architectural parameters affecting building energy performance (Heating and Cooling Loads) across residential structures[cite: 7]. This project features robust data wrangling, machine learning-driven missing data imputation, advanced exploratory data analysis (EDA), and empirical resolution of **Simpson's Paradox**[cite: 7].

📄 **[View Full Technical Report (PDF)](./DSP-Technical%20Report.pdf)**

---

## 📌 Project Overview
Evaluating building thermal performance is critical for sustainable architectural design[cite: 7]. This project models how 8 physical and structural factors influence annual Heating Load (winter) and Cooling Load (summer)[cite: 7]:
* **Features:** Surface Area, Relative Compactness, Roof Area, Wall Area, Building Orientation, Overall Height, Glazing Area, and Glazing Area Distribution[cite: 7].
* **Targets:** `Heating_Load` (kWh/m²) and `Cooling_Load` (kWh/m²)[cite: 7].

---

## 🛠️ Tech Stack & Libraries
* **Language:** Python 3.x
* **Data Processing & Manipulation:** Pandas, NumPy[cite: 7]
* **Statistical Modeling & Machine Learning:** Scikit-learn (Linear Regression, Label Encoding)[cite: 7]
* **Data Visualization:** Seaborn, Matplotlib[cite: 7]

---

## 🔬 Pipeline & Methodology

### 1. Data Wrangling & Standardization
* **Schema Refinement:** Renamed abstract column indices ($X_1 \dots X_8, Y_1, Y_2$) to descriptive physical domain variables using deterministic dictionary mapping[cite: 7].
* **Deduplication:** Identified and purged 30 duplicate records to eliminate sampling bias[cite: 7].
* **Text Normalization:** Standardized whitespace and capitalization anomalies in categorical features (`Orientation`) using `.str.strip().str.capitalize()` to enforce strict nominal categories[cite: 7].
* **Outlier Capping:** Handled leverage anomalies in `Relative Compactness` by enforcing domain-valid bounds ($0.0 \le \text{Compactness} \le 1.0$), capping anomalous entries ($\ge 100$) at $1.0$ without dropping observations[cite: 7].

### 2. Machine Learning Imputation (Target Variables)
Rather than discarding records with missing values (41 records in `Heating_Load` and 41 in `Cooling_Load`) or applying naive mean imputation (which distorts distribution variance and creates synthetic mid-range values)[cite: 7]:
* Extracted correlation matrices to isolate high-impact structural features (`Overall_Height` and `Roof_Area`)[cite: 7].
* Trained a **Linear Regression Imputer** using Scikit-learn to estimate missing target entries based on structural mass, preserving the natural variance and distribution shape[cite: 7].

### 3. Exploratory Data Analysis & Statistical Discoveries
* **Bimodal Thermal Distribution (KDE Plot):** Density estimations revealed non-normal, dual-peaked distributions with a $>100\%$ consumption gap between low-rise ($3.5\,\text{m}$) and multi-story ($7.0\,\text{m}$) structures[cite: 7].
* **Simpson's Paradox Resolution:** The raw Pearson correlation between `Surface_Area` and `Heating_Load` appeared negative ($r = -0.67$)[cite: 7]. However, stratifying by building height revealed a strong positive relationship ($r = +0.45$)[cite: 7]. Increased surface area directly amplifies conductive heat dissipation when building volume is held constant[cite: 7].
* **Orientation Fallacy Disproved:** One-way categorical analysis via bar plots confirmed that building orientation has no statistically significant impact on annual cumulative thermal demand[cite: 7].
* **Glazing Impact:** Multivariate scatter analysis showed that higher window-to-wall ratios (glazing area $= 0.40$) add up to $13\,\text{kWh/m²}$ to heating demand in multi-story configurations[cite: 7].

---

## 📊 Key Findings & Engineering Recommendations
1. **Vertical Mass Dominance:** Doubling building height from $3.5\,\text{m}$ to $7.0\,\text{m}$ increases median winter heating load by over $130\%$[cite: 7]. Stricter thermal envelope insulation must be mandated for multi-story buildings[cite: 7].
2. **Glazing Caps:** Multi-story buildings require strict caps on window-to-wall ratios and mandates for Double/Triple Low-E insulated glazing to counteract facade heat leakage[cite: 7].
3. **Volumetric Compactness:** Architectural policies should prioritize compact structural envelopes to minimize exposed wall-to-ambient surface areas[cite: 7].

