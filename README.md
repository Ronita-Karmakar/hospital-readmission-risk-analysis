# hospital-readmission-risk-analysis
Analyzing 70,000+ patient records from 130 US hospitals to identify high risk patients and reduce 30-day readmissions and CMS financial penalties.

# 📌 Business Problem

Hospitals in the US are financially penalized by the government (CMS) when patients are readmitted within 30 days of discharge under the **Hospital Readmissions Reduction Program (HRRP)**. A single hospital can lose millions of dollars annually in penalties while also indicating poor quality of care.

**The hospital needs to understand:**
- Which patients are at high risk of returning within 30 days?
- What factors — age, diagnosis, medications, length of stay — are driving readmissions?
- Where should clinical teams intervene before a patient is discharged?

**Goal:** Analyze patient records to identify readmission patterns, segment high risk patient groups, and deliver actionable insights that help hospital leadership reduce the 30-day readmission rate and avoid CMS penalties.


# 🛠️ Tools & Technologies

| Tool | Purpose |
|---|---|
| Python (Pandas, NumPy) | Data cleaning & feature engineering |
| Matplotlib, Seaborn | Exploratory data analysis & visualization |
| MySQL | Business SQL queries & aggregations |
| Power BI | Interactive 3-page dashboard |

# 📁 Dataset

- **Source:** [UCI Machine Learning Repository — Diabetes 130-US Hospitals](https://archive.ics.uci.edu/dataset/296/diabetes+130-us+hospitals+for+years+1999-2008)

# 🔧 Data Cleaning & Feature Engineering

- Replaced `?` with NaN and handled missing values across all columns
- Removed deceased and hospice patients as they cannot be readmitted
- Deduplicated patient records — kept one record per patient
- Dropped irrelevant columns with high null rates or no analytical value
- Mapped ICD-9 diagnosis codes to 9 readable disease categories
- Mapped admission type, admission source and discharge disposition IDs to readable labels
- Grouped detailed categories into meaningful business buckets for analysis
- Engineered new features including severity score, high risk flag, prior visit groups and stay categories

# 🔍 EDA Highlights

**Demographics:**
- Readmission rate increases with age — patients 80-90 have highest rate at 10.8%
- Gender is a weak predictor — difference between male and female is only 0.12%
- Elderly males 70+ show highest readmission rates across all age-gender combinations

**Clinical & Hospital Stay:**
- High risk patients have **2x** higher readmission rate than low risk patients
- High severity patients readmit at 12.1% vs 6.9% for low severity
- Longer stays indicate sicker patients — Long Stay (6-9 days) has 11.4% readmission rate

**Admission & Discharge:**
- Discharge destination is the strongest predictor found in the analysis
- Psychiatric Care transfers: **44%** readmission rate
- Patients discharged Home: **7%** readmission rate — 6x difference

**Prior Utilization:**
- Prior inpatient visits is the strongest single numeric predictor
- Patients with 5+ prior inpatient admissions: **36.8%** readmission rate
- Patients with 8+ total prior visits: **16.1%** readmission rate

**Diagnosis:**
- Circulatory disease: highest volume — 1,719 readmissions (33% of total)
- Injury: highest readmission rate at 10.9%

# 🗄️ SQL Analysis
Wrote 15+ queries across 5 business question groups using MySQL:

- **Overall Readmission Summary** — overall readmission rate, patient breakdown, average stay length
- **Patient Demographics** — readmission rate by age, gender, race and high risk elderly segments
- **Clinical & Hospital Stay** — readmission by stay category, severity, diagnoses and high risk flag
- **Admission & Discharge** — readmission by admission type, source, discharge group and AMA patients
- **Medication & Prior Utilization** — readmission by prior visits, inpatient history and medication change

# 📈 Power BI Dashboard
**Page 1 — Executive Summary**
<img width="1083" height="725" alt="image" src="https://github.com/user-attachments/assets/6359b1e6-20bb-4493-b77e-b3ab5c76840e" />




- Out of 59K patients, 5,219 were readmitted within 30 days — an 8.88% readmission rate
- Elderly patients aged 80-90 have the highest readmission rate at 10.8%
- Injury and Circulatory diseases drive the most readmissions
- 1,760 patients are flagged as High Risk — these need immediate attention

**Page 2 — Patient Risk Analysis**
<img width="1000" height="600" alt="image" src="https://github.com/user-attachments/assets/02d02ec4-5c0b-4c8b-bc21-deb342de4099" />


- High Risk patients have 16.9% readmission rate — double the 8.6% of Low Risk patients
- Circulatory disease has the highest patient volume — largest block in treemap
- High Severity patients readmit at 12.1% vs 6.9% for Low Severity
- Elderly males aged 70-80 and 80-90 consistently show highest readmission rates across both genders
- Long stays (6-9 days) have highest readmission rate at 11.4%

**Page 3 — Operational Insights**
<img width="946" height="723" alt="image" src="https://github.com/user-attachments/assets/10ecaf6e-fe01-4640-966e-6ab6841cdaa0" />


- Patients transferred to Psychiatric Care have 44% readmission rate — highest of all groups
- Patients discharged Home have lowest rate at 7% — stable patients are correctly sent home
- Patients with 5+ prior inpatient visits have 36.8% readmission rate
- Circulatory disease accounts for 1,719 readmissions — more than double any other diagnosis
- Patients with 8+ prior visits have 16.1% readmission rate — chronic patients need special care
- Medication change during visit slightly increases readmission risk (9.4% vs 8.5%)

# 💡 Business Recommendations

1. **Create a High Risk Patient Program** — 1,760 flagged patients need a dedicated care coordinator to call within 48 hours of discharge

2. **Focus on Circulatory Disease** — responsible for 33% of all readmissions. Cardiology team needs mandatory 7-day post discharge follow up

3. **Psychiatric Transfers Need Urgent Attention** — 44% readmission rate requires direct coordination with psychiatric facilities for diabetes management continuity

4. **Target Elderly Patients 70+** — consistently show 10%+ readmission rates. Mandatory home health assessment before discharge

5. **Manage Chronic Repeat Patients** — patients with 5+ prior admissions need a personalized chronic disease management plan

6. **Pharmacist Review for Medication Changes** — patients with medication changes during visit have higher readmission risk
