# Tesla Workforce Analytics Project

An end-to-end People Analytics case study built with SQL, Python, SQLite, pandas, NumPy, SciPy, statsmodels, and scikit-learn to simulate workforce decision-making at Tesla using the IBM HR Employee Attrition dataset.

This project transforms a general HR dataset into a Tesla-specific workforce analytics simulation across five major dimensions of the employee lifecycle:

* **Attrition analytics**
* **Compensation analytics**
* **Mobility analytics**
* **Performance analytics**
* **Recruitment analytics**

The goal was not just to describe patterns, but to test whether workforce signals were statistically meaningful and whether they could support real business decisions around retention, hiring, compensation, and workforce planning.

---

## Project Objective

Tesla operates in a high-intensity environment where workforce decisions can have major downstream effects on attrition, performance, hiring quality, internal mobility, and compensation efficiency.

This project asks a practical question:
> Which workforce patterns are just interesting correlations, and which ones hold up under statistical testing strongly enough to inform strategy?

To answer that, I structured the project into five focused analytics modules, each designed around a different business problem.

---

## Tools and Methods

### Tools
* **SQL / SQLite:** For querying and segmenting employee cohorts
* **Python:** For analysis and model building
* **pandas / NumPy:** For data transformation
* **SciPy:** For chi-square testing
* **statsmodels:** For logistic regression
* **matplotlib / seaborn:** For exploratory visualization where needed

### Statistical Methods
* Chi-square tests of independence
* Logistic regression
* Cohort segmentation
* Comparative percentage matrices
* Quartile-based compensation tiering
* Tesla-specific workforce role mapping and scenario framing

---

## Dataset

This project uses the IBM HR Employee Attrition dataset and reframes it into Tesla-style workforce scenarios.

> [!NOTE]
> Because the source data is simulated and not proprietary Tesla employee data, the analysis should be read as a decision-support simulation, not as a literal description of Tesla's internal workforce.

---

## Project Structure

```bash
.
├── attrition_analytics.py
├── compensation_analytics.py
├── mobility_analytics.py
├── performance_analytics.py
├── recruitment_analytics.py
├── IBM-HR-Employee-Attrition.csv


└── README.md

