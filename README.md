# tcga-luad-survival-analysis

A bioinformatics pipeline designed to identify and validate prognostic somatic mutation biomarkers in Lung Adenocarcinoma (LUAD) utilizing data from The Cancer Genome Atlas (TCGA).

---

## project overview
This project investigates the correlation between specific gene mutations and patient overall survival (OS) outcomes in LUAD. By extracting, cleaning, and merging large clinical and genomic datasets, this computational pipeline screens known driver genes to uncover statistically significant prognostic indicators.

This allows for more precise genomic risk stratification in clinical settings, potentially identifying high-risk patients who require aggressive therapeutic intervention or heightened post-treatment surveillance despite standard staging metrics.

---

## dataset & sources
Data was sourced publicly from the **UCSC Xena Functional Genomics Explorer**:
* **Somatic Mutations:** TCGA Lung Adenocarcinoma Ensemble Somatic Mutation dataset (comprising 194,731 mutation records across 12 feature columns).
* **Clinical/Phenotype Data:** TCGA LUAD survival dataset mapping overall survival tracking timelines (`OS.time` in days) and censorship events (`OS`) for 721 unique patients.

---

## computational workflow
1. **Data Cleaning & ID Alignment:** Parsed complicated multi-character TCGA sample barcodes down to the base 12-character participant identifier to easily cross-reference clinical metrics with genomic profiles.
2. **Feature Engineering:** Constructed a binary mutation matrix isolating 8 prominent LUAD driver genes (*TP53, KRAS, EGFR, STK11, KEAP1, RBM10, BRAF, NF1*).
3. **Survival Estimation:** Implemented Kaplan-Meier survival curves and conducted Log-Rank tests utilizing the Python `lifelines` library to evaluate statistical disparities between mutated and wild-type cohorts.

---

## key results

Of the 8 major driver genes evaluated, **RBM10** was identified as the sole statistically significant prognostic biomarker ($p = 0.0228$). 

### Kaplan-Meier Survival Analysis Summary:
* **RBM10 Finding:** Patients presenting with an *RBM10* mutation ($n = 44$) exhibited significantly accelerated mortality and worse overall survival profiles compared to the wild-type cohort ($n = 636$).
* **Biological Context:** *RBM10* (RNA Binding Motif Protein 10) acts as a critical tumor suppressor regulating alternative RNA splicing. The dramatic drop in survival suggests that the loss of this master genetic editor drives highly aggressive tumor progression.

<img width="1313" height="657" alt="Screenshot 2026-06-16 at 10 48 38 PM" src="https://github.com/user-attachments/assets/b24f0721-a583-464c-b705-58dffaed230f" />

---

## future plans
To prepare this work for formal academic conference submission, upcoming milestones include:
* **Multivariate Adjustment:** Upgrading from univariable Kaplan-Meier splits to a **Cox Proportional Hazards Model** to control for clinical confounding factors like age and tumor stage.
* **Multiple Testing Correction:** Implementing False Discovery Rate (FDR / Benjamini-Hochberg) adjustments to combat the statistical look-elsewhere effect across multi-gene screens.

---

## tech stack & libraries
* **Language:** Python
* **Data Manipulation:** `pandas`, `numpy`
* **Data Visualization:** `matplotlib`
* **Statistical Modeling:** `lifelines` (KaplanMeierFitter, logrank_test)
