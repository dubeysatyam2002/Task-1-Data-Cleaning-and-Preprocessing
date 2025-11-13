# 🧹 Data Cleaning and Preprocessing – Customer Personality Analysis

## 📌 Objective
Clean and prepare a raw dataset (containing nulls, duplicates and inconsistent formats) to make it ready for EDA or modeling.

**Tools:** Python, Pandas, NumPy, Jupyter Notebook  
**Deliverables:** Cleaned dataset + short summary of changes

---

## 🗂 Repository contents
- `marketing_campaign.csv` — original raw dataset (Customer Personality Analysis)
- `DataCleaningAndPreprocessing.ipynb` — step-by-step Jupyter Notebook (Steps 1–10)
- `marketing_campaign_cleaned.csv` — cleaned dataset output
- `README.md` — this file

---

## 🔎 Summary of the dataset (raw)
- Original file name: `marketing_campaign.csv`
- Original shape (rows × columns): **2240 × 29**
- Key issues observed:
  - Missing values in `Income` (24 rows)
  - Inconsistent categorical values in `Marital_Status` (e.g., `Alone`, `Absurd`, `YOLO`) and `Education` (e.g., `2n Cycle`)
  - `Dt_Customer` stored as strings (day-first format)
  - Some numeric columns were read as `object` (strings)

---

## 🧭 Step-by-step results (what the notebook runs and outputs)

**Step 1 — Import libraries**
- Libraries used: `pandas`, `numpy`
- Notebook executed successfully.

**Step 2 — Load dataset**
- File loaded using `pd.read_csv()` with `;` separator (Kaggle variant).
- Shape after load: **2240 rows × 29 columns**.

**Step 3 — Initial exploration**
- `df.info()` and `df.describe()` used.
- Duplicate rows: **0** exact duplicates detected.
- `Income` had **24 missing** values.

**Step 4 — Handle missing values**
- Action: Created `income_missing_flag` and imputed missing `Income` values with **median = 51,381.50**.
- Rows imputed: **24**

**Step 5 — Remove duplicates**
- Action: `df.drop_duplicates()` used.
- Duplicates removed: **0** (none found).

**Step 6 — Standardize text data**
- `Education` cleaned (`'2n Cycle'` → `'2nd Cycle'`, normalized other labels).
- `Marital_Status` mapping applied:
  - `'Together'` → `'Married/Partner'`
  - `'Alone'` → `'Single'`
  - `'Absurd'`, `'YOLO'` → `'Other'`
- Resulting `marital_status` unique values: `['Single','Married/Partner','Married','Divorced','Widow','Other']`.
- `education` unique values: `['Graduation','PhD','Master','Basic','2nd Cycle']`.

**Step 7 — Convert date column**
- `Dt_Customer` parsed to `datetime` (day-first). Any malformed entries coerced to `NaT`.

**Step 8 — Rename columns**
- All column headers converted to `snake_case` and lowercased (e.g., `Year_Birth` → `year_birth`, `Dt_Customer` → `dt_customer`).

**Step 9 — Fix data types**
- Numeric-like columns coerced to numeric (`pd.to_numeric(..., errors='coerce')`).
- Example: `income` float; `year_birth` numeric; date column is `datetime`.

**Step 10 — Outliers and final save**
- Income outliers detected using IQR method: **8 rows flagged** (column `income_outlier` added).
- Cleaned dataset saved as: `marketing_campaign_cleaned.csv`
- Final cleaned shape: **2240 rows × 31 columns** (two flag columns added: `income_missing_flag`, `income_outlier`).

---

## ✔ Final deliverables
- `marketing_campaign_cleaned.csv` — cleaned CSV (ready for EDA/modeling)
- `DataCleaningAndPreprocessing.ipynb` — reproducible notebook with all code + explanations
- `README.md` — this file

---

## 📌 Notes & next steps (recommendations)
- For modeling, consider log-transforming or capping `income`.
- Create aggregate features (e.g., `total_spent` from Mnt* columns, `customer_tenure_days` from `dt_customer`).
- Encode categorical variables (one-hot or label encoding) prior to ML models.
- Save a versioned dataset (e.g., `marketing_campaign_cleaned_v1.csv`) if you make more changes.

---

## 👤 Author
**Satyam Dubey**  
Aspiring Data Analyst — Python · Pandas · SQL · Visualization

---

## 🧾 License
This repository is provided for learning and demonstration purposes.
