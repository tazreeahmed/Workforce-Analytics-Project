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


```
## 1) Attrition Analytics

This module focuses on burnout, equity incentives, workplace conditions, and pay-position stressors.

### Business Questions
* Does overtime meaningfully increase attrition risk?
* Does a longer commute intensify burnout?
* Can stock options reduce attrition among overtime workers?
* Do environment satisfaction and job satisfaction buffer attrition among lower-paid employees?
* Does being below the pay median within a job tier increase attrition, especially for high performers?

### Key Findings

#### Gigafactory Burnout Risk
A combined overtime + commute-risk model showed that attrition rises sharply when heavy overtime overlaps with longer travel distances.
* **Employees not working overtime:** 10.4% attrition rate
* **Employees working overtime:** 30.5% attrition rate
* **Employees with 20-25 mile commutes:** Highest attrition band at 27.4%
* **Workers flagged as High Risk (overtime + distance > 10 miles):** 40.1% attrition
* **Standard-risk employees:** 13.7% attrition

#### Statistical Validation
A chi-square test found the burnout risk flag to be highly significant:
* **Chi-square:** 62.5328
* **p-value:** `2.6204e-15`

A logistic regression also showed both overtime and commute distance as significant predictors of attrition:
* **OverTime coefficient:** 1.3254 (p < 0.001)
* **DistanceFromHome coefficient:** 0.0246 (p = 0.005)

> **Conclusion:** The burnout effect is not just descriptive—it is statistically supported.

#### "Think Like Owners" Equity Analysis
This phase tested whether stock options help offset burnout among overtime employees.

* **Among overtime workers:**
  * Stock Option Level 0: **45.1%** attrition
  * Level 1: **17.4%** attrition
  * Level 2: **15.8%** attrition
  * Level 3: **34.5%** attrition
* **Among regular-hours workers:**
  * Level 0: **16.0%** attrition
  * Level 1: **6.3%** attrition
  * Level 2: **5.0%** attrition
  * Level 3: **8.9%** attrition

**Interpretation:** Equity appears to reduce attrition meaningfully at lower stock-option levels, especially among overtime workers, but the effect weakens or reverses at the highest level in this simulation.

#### Statistical Validation
* **Overtime group chi-square p-value:** `8.0250e-08`
* **Regular group chi-square p-value:** `6.2781e-06`

A logistic regression including an overtime $\times$ stock-option interaction produced a strong overall model fit:
* **Pseudo R²:** 0.1117
* **LLR p-value:** `4.418e-28`

#### Low-Pay Workplace Conditions
This phase tested whether workplace conditions and job satisfaction help retain below-median earners.

For employees earning below the median:
* **Environment satisfaction vs. Attrition:**
  * Satisfaction 1: **33.6%** attrition
  * Satisfaction 2: **17.0%** attrition
  * Satisfaction 3: **19.7%** attrition
  * Satisfaction 4: **19.5%** attrition
* **Job satisfaction vs. Attrition:**
  * Satisfaction 1: **31.5%** attrition
  * Satisfaction 2: **21.8%** attrition
  * Satisfaction 3: **22.4%** attrition
  * Satisfaction 4: **14.7%** attrition

#### Statistical Validation
* **Environment satisfaction chi-square p-value:** `2.2209e-03`
* **Job satisfaction chi-square p-value:** `2.4175e-03`

A logistic regression further showed that frequent travel and low pay increased attrition risk, while better environment/job satisfaction reduced it. Notably:
* **Low_Pay coefficient:** 0.9007 (p < 0.001)
* Higher environment satisfaction levels were consistently negative and significant.
* Job satisfaction level 4 had a strong protective effect.

#### Below-Tier-Median Pay vs. Performance
This final attrition phase tested whether being underpaid relative to peers at the same job level increases attrition, especially among strong performers.
* **At/Above Tier Median, Performance 3:** 14.4% attrition
* **At/Above Tier Median, Performance 4:** 10.9% attrition
* **Below Tier Median, Performance 3:** 17.8% attrition
* **Below Tier Median, Performance 4:** 21.6% attrition

#### Statistical Validation
* **p-value:** `5.7130e-02`

**Interpretation:** This pattern is directionally interesting, especially for higher performers, but did not cross conventional statistical significance thresholds in this sample. That makes it a useful exploratory signal, but not a strong decision rule by itself.

---

## 2) Compensation Analytics

This module focuses on how compensation interacts with commute burden, overtime, and role-specific retention.

### Business Questions
* Does higher pay offset attrition among long-commute employees?
* Does equity matter differently across role groups?
* Are there compensation tiers where retention improves sharply?

### Key Findings

#### Long-Commute Pay Tier Analysis
Among employees living more than 10 miles from work:
* **Low Pay:** 34.2% attrition
* **Mid-Low:** 16.2% attrition
* **Mid-High:** 18.9% attrition
* **High Pay:** 14.4% attrition

#### Statistical Validation
* **Chi-square:** 16.4716
* **Degrees of Freedom:** 3
* **p-value:** `0.000907`

**Interpretation:** Compensation tier is statistically associated with attrition in the long-commute cohort. The highest-risk group is clearly the low-pay, long-commute segment, suggesting that compensation can partially offset commute-related strain.

#### Role-Specific Equity Analysis for Overtime Workers
This phase mapped IBM job roles into Tesla-style workforce roles and tested whether stock option level relates to attrition within each overtime-heavy role group.

* **Tesla Advisor / Account Manager**
  * Level 0: **54.8%** attrition | Level 1: **14.3%** attrition | Level 2: **20.0%** attrition | Level 3: **14.3%** attrition
* **Test Technician (Battery/Drive Unit)**
  * Level 0: **73.9%** attrition | Level 1: **35.5%** attrition | Level 2: **50.0%** attrition | Level 3: **25.0%** attrition
* **Battery R&D / AI Engineer**
  * Level 0: **45.7%** attrition | Level 1: **22.9%** attrition | Level 2: **0.0%** attrition | Level 3: **50.0%** attrition

#### Role-level statistical verdicts
The script found statistically meaningful stock-option/attrition relationships in some overtime role groups, including:
* Tesla Advisor / Account Manager
* Test Technician (Battery/Drive Unit)
* Battery R&D / AI Engineer

Other role groups did not show strong enough evidence in this sample, often due to smaller subgroup sizes or limited variation.

**Interpretation:** Equity incentives may not work uniformly across the workforce. Their retention impact appears role-sensitive, which suggests compensation design should be segmented rather than applied as a universal policy.

---

## 3) Mobility Analytics

This module focuses on whether internal movement, promotion timing, and managerial stability relate to performance outcomes and attrition risk.

### Business Questions
* Does longer time with a manager improve performance?
* Does longer time in role improve performance?
* Does delayed promotion increase attrition?

### Key Findings

#### Years With Current Manager vs. Performance
The distribution of performance ratings did not differ significantly by years with the current manager.
* **Chi-square:** 13.8433
* **Degrees of Freedom:** 17
* **p-value:** `0.678165`

**Interpretation:** In this dataset, simply staying longer with the same manager does not appear to be a strong driver of performance outcomes.

#### Years In Current Role vs. Performance
Performance distributions were also not significantly different across years in the current role.
* **Chi-square:** 14.8397
* **Degrees of Freedom:** 18
* **p-value:** `0.672946`

**Interpretation:** This suggests role tenure alone is not enough to explain performance differences. More context—such as role complexity, team quality, or advancement path—may matter more than tenure itself.

#### Years Since Last Promotion vs. Attrition
Promotion stagnation showed some descriptive variation, but did not reach statistical significance.
* **0 years since promotion:** 18.9% attrition
* **7 years since promotion:** 21.1% attrition
* **9 years since promotion:** 23.5% attrition
* **15 years since promotion:** 23.1% attrition

#### Statistical Validation
* **Chi-square:** 21.8450
* **Degrees of Freedom:** 15
* **p-value:** `0.111934`

**Interpretation:** This is a plausible workforce story, but the dataset does not provide strong enough evidence to conclude that promotion timing alone drives attrition risk.

---

## 4) Performance Analytics

This module tests whether workload, training, leadership stability, role tenure, and salary growth are meaningfully associated with performance ratings.

### Business Questions
* Does overtime improve performance outcomes?
* Does more training produce higher performance?
* Does longer time with a manager improve ratings?
* Does longer time in role improve ratings?
* Are salary hikes aligned with performance?

### Key Findings

#### Overtime vs. Performance
Performance ratings were nearly identical across overtime groups:
* **No overtime:** 84.7% rating 3, 15.3% rating 4
* **Overtime:** 84.4% rating 3, 15.6% rating 4

#### Statistical Validation
* **Chi-square:** 0.0076
* **p-value:** `0.930471`

**Interpretation:** More overtime does not appear to improve performance outcomes in this dataset. It increases strain, but not output quality.

#### Training Frequency vs. Performance
Performance distributions were also nearly flat across training frequencies.
* **Chi-square:** 1.8580
* **Degrees of Freedom:** 6
* **p-value:** `0.932280`

**Interpretation:** The dataset does not support the idea that more training sessions alone translate into higher performance ratings.

#### Years With Current Manager & Current Role vs. Performance
No statistically significant relationships were found:
* **Manager Tenure p-value:** `0.678165`
* **Role Tenure p-value:** `0.672946`

**Interpretation:** Performance does not appear to be explained well by simple tenure measures in this workforce simulation.

#### Percent Salary Hike vs. Performance
This was the strongest signal in the performance module. The distribution was perfectly separated in this dataset:
* Salary hikes **11–19%** aligned completely with Performance Rating 3
* Salary hikes **20–25%** aligned completely with Performance Rating 4

#### Statistical Validation
* **Chi-square:** 1470.0000
* **Degrees of Freedom:** 14
* **p-value:** `0.000000`

**Interpretation:** This indicates a very strong association between salary hike and performance rating in the source data. That said, this pattern likely reflects how the underlying dataset was constructed, so it should be interpreted carefully. It is statistically strong, but may also be partly baked into the HR system logic rather than discovered behaviorally.

---

## 5) Recruitment Analytics

This module focuses on hiring-risk signals, especially for early attrition.

### Business Questions
* Which candidate profiles are most prone to first-year attrition?
* Does number of prior companies predict culture-shock risk?
* Does academic pedigree outperform experience in workforce outcomes?

### Key Findings

#### Quality of Hire: Prior Companies Worked
This module isolated new hires with 1 year or less at the company.
* **Total new hires in sample:** 215

**Attrition by number of prior companies worked:**
* **0-1 prior companies:** 49.0% attrition
* **2-5 prior companies:** 18.8% attrition
* **6+ prior companies:** 33.3% attrition

**Interpretation:** This suggests a U-shaped hiring risk pattern. Very low prior-company count may indicate first-job adjustment risk, while a very high prior-company count may indicate instability risk. Moderate prior-company exposure appears to be the lowest-risk profile. This became the basis for the Quality of Hire screening logic.

#### Exceptional Ability vs. Practical Experience
This module also tested whether academic pedigree translates into better workforce outcomes relative to hands-on experience.

In the Tesla-style framing, lower-degree, higher-experience candidates at Job Levels 1-2 outperformed higher-degree, lower-experience peers in observed outcomes:
* **18.7% vs. 10.2%** outcome split referenced in the project summary.

**Interpretation:** The analysis suggests that academic pedigree alone may not be the strongest predictor of success in operational or execution-heavy roles. Experience appears to matter more in certain workforce segments.

---

## Strategic Takeaways

Across the five modules, several broad lessons emerged:

1. **Burnout is measurable:** Overtime and commute distance combine into a statistically meaningful attrition-risk signal.
2. **Compensation is not one-dimensional:** Pay, equity, and tier position do not affect all employees equally. Their impact depends on role, overtime load, and commute burden.
3. **Satisfaction can offset pay pressure:** Among lower-paid employees, work environment and job satisfaction showed meaningful relationships with retention.
4. **Not every intuitive HR story survives testing:** Several plausible ideas—like manager tenure, role tenure, promotion timing, training frequency, and overtime improving performance—did not hold up statistically in this sample.
5. **Hiring quality is segmentable:** Early attrition risk appears meaningfully related to prior-company history, suggesting that candidate stability can be evaluated more precisely than simple pedigree filters.

---

## What This Project Demonstrates

This project demonstrates the ability to:
* Build end-to-end analytics workflows using SQL and Python.
* Transform a raw HR dataset into decision-oriented workforce analysis.
* Apply statistical testing instead of relying on descriptive patterns alone.
* Translate analytical results into business-facing retention and hiring insights.
* Simulate how a People Analytics team might support decisions across the employee lifecycle.

---

## Limitations

* The dataset is IBM HR sample data, not real Tesla employee data.
* Tesla-specific job labels and workforce interpretations are analytical simulations, not internal Tesla definitions.
* Some subgroup analyses likely contain small sample sizes, so certain role-level findings should be treated as directional.
* Some very strong patterns, especially around salary hikes and performance, may reflect source-data structure rather than naturally occurring workforce behavior.

---



