# Discordace Between Reported Gallstone Diagnosis and Gallbladder Surgery
## Team: 
- Nicole Tesla Kreimer
- Erna Jiraskova
- Pavel Eidelman

---

## Dataset  
### Source: NHANES (open dataset)  
### Size:  
Total participants (all ages):          27,493  
Merged features (columns):              212  
Adults (age >= 20) with valid Qs:       16,989  
Adults reporting gallbladder surgery:   1,935  
2017-2020 cycle:                    1,016  
2021-2023 cycle:                    919  
Concordant (Surgery + Gallstones):      1,426 (73.7%)  
Discordant (Surgery + NO Gallstones):   509 (26.3%)  
### Key Variables:
* Outcome & Cohort: Ever had gallbladder surgery; ever told by a doctor of gallstones (Medical Conditions Questionnaire).
* Predictors: Demographics (age, sex, race/ethnicity), socioeconomic/access factors (education, family income-to-poverty ratio, health insurance, routine healthcare access), and clinical/metabolic measures (BMI, waist circumference, diabetes, time since surgery, and laboratory lipids/glucose where sample coverage permits).

## Research question:  
*Among adults reporting previous gallbladder surgery, which demographic, metabolic, clinical and socioeconomic characteristics distinguish those with and without a reported history of gallstones?*
- In US adults reporting gallbladder surgery in NHANES (2017–2023), do demographic, clinical, metabolic, and socioeconomic characteristics modeled via survey-weighted multivariable logistic regression and gradient boosting predict discordant non-reporting of gallstones better than a survey-weighted age-and-sex-only baseline?  

### Literature background:
### Paper 1 (same data): NHANES 2017–2020 study of metabolic dysfunction-associated steatotic liver disease (MASLD) and gallstones ([PMC11704231](https://pmc.ncbi.nlm.nih.gov/articles/PMC11704231/))  
* what they did: analyzed NHANES 2017-2020 using the self-report gallstone questionnaire and propensity score matching.
* what they found: gallstones were more prevalent with MASLD with higher odds after matching.
* what they left open: treated self-reported gallstones strictly as the outcome and did not examine individuals who reported gallbladder surgery yet answered "no" to gallstones.

*Paper 2 (same question): NHANES 2017–March 2020 study of the triglyceride-glucose (TyG) index, gallstones, and age at first gallstone surgery ([PMC11271289](https://pmc.ncbi.nlm.nih.gov/articles/PMC11271289/))  
what they did: applied logistic regression and dose-response analysis using the same NHANES gallstone and gallbladder surgery questionnaire data.
what they found: a higher TyG index was associated with higher gallstone prevalence and earlier age at first surgery (without establishing causation).
what they left open: they did not evaluate the reliability or discordance of the self-reported gallstone response itself.*

### Paper 2, same question (reliability of self-reported gallstones versus surgery): E3N cohort, CMAJ, menopausal hormone therapy and cholecystectomy in French women. https://cmaj.ca/node/32619
* What they did: checked self-reports against documents in random samples of women.
* What they found: agreement was about 99% for cholecystectomy but only about 67% for gallstone disease, so surgery is reported reliably and gallstones less so.
* What they left open: this was a side check in a hormone therapy study, not an analysis of who gives discordant answers. Supporting: a Scottish study found about 99.6% agreement between self-reported cholecystectomy and hospital records.

**The gap our project fills:** Prior NHANES studies treat self-reported gallstone diagnosis and gallbladder surgery as aligned proxies for gallstone disease. Our project directly characterizes the discordant sub-population (gallbladder surgery without reported gallstones, representing 26.3% of surgical cases) across 2017-2023.   
  
## Approach:
### Descriptive Analysis: 
Survey-weighted descriptive epidemiology to estimate the national prevalence of discordance and compare demographic, clinical, and socioeconomic distributions between concordant and discordant groups.  
### Baseline Model: 
Multivariable Logistic Regression to establish an interpretable statistical benchmark (adjusted odds ratios, 95% CIs, and baseline ROC-AUC).  
### Machine Learning & Explainability: 
Gradient Boosting (`XGBoost`) to capture non-linear relationships and interactions, paired with predictor importance and `SHAP` analysis to interpret global and individual drivers of discordance.  
  
## Validation Strategy:
### Temporal Validation: 
Train models on NHANES 2017–March 2020 (n = 1,016) and evaluate out-of-time generalization on NHANES 2021–2023 (n = 919).  
### Pipeline Testing: 
Automated `pytest` unit tests verifying zero participant leakage (`SEQN` disjointness), valid physiological/questionnaire value ranges, and proper handling of missingness and survey weights.  
### Metrics: 
ROC-AUC, PR-AUC, calibration plots, and subgroup performance across demographic and socioeconomic strata.  
    
## Timeline:  
| :--- | :--- | :--- | :--- |
| **Week 6** | Nov 25 | Project approval; finalize NHANES 2017–2023 cohort extraction. |  
| **Week 7** | Dec 2 | Spec-driven development in Kiro: complete `requirements.md`. |  
| **Week 8** | Dec 9 | Data cleaning, EDA, and complete `design.md`. |  
| **Week 9** | Dec 16 | Finalize EDA + `tasks.md`; run survey-weighted descriptive analysis and Logistic Regression baseline. |  
| **Week 10** | Dec 23 | Train/tune `XGBoost`, run temporal validation + `SHAP` analysis, complete LLM-assisted pipeline tests and draft results. |  
| **Week 11** | Dec 30 | Code cleanup, reproducibility check, and **Final Submission (Moodle)**. |  
