# Discordance Between Self-Reported Gallstone Diagnosis and Gallbladder Surgery: Analysis of NHANES 2017-2023
## Team: 
- Nicole Tesla Kreimer
- Erna Jiraskova
- Pavel Eidelman

---

## Dataset  
### Source: NHANES (open dataset)  
### Size:  
| Population | N |
|---|---:|
| Total participants (all ages) | 27,493 |
| Merged variables (columns) | 212 |
| Adults ≥20 with valid responses | 16,989 |
| Gallbladder surgery with valid gallstone history | 1,935 |
| 2017–2020 cycle | 1,016 |
| 2021–2023 cycle | 919 |
| Concordant (surgery + gallstones) | 1,426 (73.7%) |
| Discordant (surgery + no reported gallstones) | 509 (26.3%) |

### Key Variables:
* Outcome & Cohort: Ever had gallbladder surgery; ever told by a doctor of gallstones (Medical Conditions Questionnaire).
* Candidate features: Demographics (age, sex, race/ethnicity), socioeconomic/access factors (education, family income-to-poverty ratio, health insurance, routine healthcare access), and clinical/metabolic measures (BMI, waist circumference, diabetes, time since surgery, and laboratory measurements).

## Research question:  
Among adults reporting previous gallbladder surgery in NHANES 2017-2023, which demographic, socioeconomic, metabolic, clinical, and laboratory charachteristics distinguish those with and without a self-reported history of gallstones?*

## Literature background:

### Paper 1, same data: 
**Wang et al. Relationship of triglyceride-glucose index to gallstone prevalence and age at first gallstone surgery in American adults.**
Scientific Reports. 2024;14:16749.
([PMC11271289](https://pmc.ncbi.nlm.nih.gov/articles/PMC11271289/))  

| Field | Summary |
|---|---|
| **Question** | Is the triglyceride-glucose (TyG) index associated with gallstone prevalence and age at first gallbladder surgery? |
| **Data** | NHANES 2017–March 2020; 3,905 adults, including 421 reporting gallstones. |
| **Method** | Multivariable logistic regression, generalized additive models, dose–response analysis and subgroup analysis. |
| **Validation** | Sensitivity and subgroup analyses within the same dataset. No independent validation cohort. |
| **Result** | Higher TyG was associated with gallstone prevalence (adjusted OR 1.25; 95% CI 1.04–1.51 per unit increase). |
| **Left open** | Did not specifically characterize patients with previous gallbladder surgery according to their reported gallstone history. |

### Paper 2, related\same question:
**Alli et al. Nineteen-year trends in incidence and indications for laparoscopic cholecystectomy: the NY State experience.**
Surgical Endoscopy. 2017;31:1651–1658. 
(https://link.springer.com/article/10.1007/s00464-016-5154-9)
| Field | Summary |
|---|---|
| **Question** | Have the frequency and indications for laparoscopic cholecystectomy changed over time? |
| **Data** | New York SPARCS administrative database, 1995–2013; 711,406 cholecystectomies, including 637,308 laparoscopic procedures. |
| **Method** | Retrospective analysis using ICD-9 and CPT codes; log-linear Poisson regression for temporal trends. |
| **Validation** | Additional analysis accounting for population changes. No independent validation or confirmation against pathology or imaging. |
| **Result** | Calculous cholecystitis decreased by 20.1%, while acalculous cholecystitis and biliary dyskinesia increased by 94.2% and 331.7%, respectively, in relative frequency per 1,000 laparoscopic procedures. |
| **Left open** | Baseline characteristics across surgical indications were described but limited to demographic and insurance data, without formal statistical comparisons or comprehensive clinical, metabolic and laboratory characterization. Discordance between surgical and diagnostic histories was not assessed. |

**The gap our project fills:** Despite extensive research on gallstone disease and management, studies comparing patients undergoing cholecystectomy with and without gallstones have largely focused on surgical indications and postoperative outcomes, with limited comprehensive patient characterization. To our knowledge, no previous NHANES study has specifically characterized patients reporting gallbladder surgery without a history of diagnosed gallstones.
  
## Approach:
### Descriptive Analysis 
Descriptive epidemiology to estimate the national prevalence of discordance and compare demographic, clinical, and socioeconomic distributions between concordant and discordant groups.  
### Baseline Model: 
Logistic regression using age and sex followed by multivariable analysis with additional features.
### Machine Learning & Explainability: 
Compare multivariable logistic regression with tree based classification models such as gradient boosting (`XGBoost`) to capture non-linear relationships and interactions, paired with predictor importance and `SHAP` analysis to interpret global and individual features associated with model predictions.  
  
## Validation Strategy:
### Temporal Validation: 
Train models on NHANES 2017–2020 (n = 1,016) and evaluate on NHANES 2021–2023 (n = 919).
### Pipeline Testing: 
Automated `pytest` unit tests verifying zero participant leakage (`SEQN` disjointness), valid physiological/questionnaire value ranges, and proper handling of missingness and survey weights.  
### Metrics: 
ROC-AUC, PR-AUC, calibration plots, and subgroup performance across demographic and socioeconomic strata.  
    
## Timeline:  
| Week | Date | Course Milestone | Team Deliverable |
| :--- | :--- | :--- | :--- |
| **Week 6** | Nov 25 | Project approval | Finalize `README.md`, verify 2017–2023 counts, add first weighted/unweighted summary table |
| **Week 7** | Dec 2 | Requirements due | Complete `requirements.md` in Kiro; freeze cohort, missingness, and feature definitions |
| **Week 8** | Dec 9 | Design spec due | Complete `design.md`; finalize merged analytic dataset and survey-weighted Table 1 |
| **Week 9** | Dec 16 | EDA & task list | Complete EDA and `tasks.md`; run age/sex baseline and multivariable weighted logistic regression |
| **Week 10** | Dec 23 | Tests & draft results | Train/tune XGBoost, run 2021–2023 temporal validation + SHAP, pass all `pytest` checks |
| **Week 11** | Dec 30 | Final submission | Code cleanup, reproducibility check, final report, and AI-use statement on Moodle |
| **Week 12** | Jan 6/13 | Presentations | Present findings and clinical interpretation |
