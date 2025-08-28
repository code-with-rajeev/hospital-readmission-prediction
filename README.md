# 🏥 Diabetes Patient Readmission Prediction

This project aims to predict **whether a diabetic patient will be readmitted to the hospital within 30 days** based on their medical history, treatments, and demographic details.  
Reducing hospital readmissions is a critical challenge for healthcare providers, as it improves **patient outcomes** and reduces **financial penalties** for hospitals.

---

## 📂 Dataset

- Source: Diabetes 130-US hospitals dataset  
- Shape: **101,766 rows × 50 columns**  
- Key Features:
  - `age`, `gender`, `race`  
  - `admission_type_id`, `discharge_disposition_id`, `admission_source_id`  
  - `num_lab_procedures`, `num_medications`, `number_inpatient`, `time_in_hospital`  
  - Various diabetes-related medications and lab results  
  - **Target:** `readmitted` → converted into binary (`readmitted_binary`)

---

## ⚙️ Data Preprocessing

1. **Handled Missing Values**  
   - Columns with >90% missing (`weight`, `max_glu_serum`, `A1Cresult`) dropped.  
   - Other missing values replaced with `"Unknown"` or mode.

2. **Mapped ID Columns**  
   - Replaced numeric codes in `admission_type_id`, `discharge_disposition_id`, `admission_source_id` with human-readable categories.

3. **Encoding**  
   - Applied **Label Encoding** to categorical variables.  
   - Converted `readmitted` into binary:  
     - `0` → Not readmitted  
     - `1` → Readmitted within 30 days  

4. **Class Imbalance Handling**  
   - Original distribution: ~89% No, 11% Yes (highly imbalanced).  
   - Used **SMOTE (Synthetic Minority Oversampling Technique)** to balance classes.

---

## 🤖 Models Trained

- Random Forest  
- XGBoost (final chosen model)

### Why XGBoost?
- Handles **imbalanced data** better with class weighting.  
- Provides **feature importance**.  
- Achieved **AUC ~ 0.66**, better than baseline models.  

---

## 📊 Results

- Accuracy: ~70%  
- AUC: **0.66**  
- Precision/Recall trade-off handled using SMOTE.  
- Feature Importance (Top predictors):
  - `num_lab_procedures`  
  - `number_inpatient`  
  - `num_medications`  
  - `time_in_hospital`  


Confusion Matrix (XGBoost after SMOTE):  

