# TCGA-LUAD Survival Analysis

Bioinformatics project analyzing somatic mutation data from the TCGA Lung Adenocarcinoma (LUAD) cohort to find which driver gene mutations are associated with patient survival outcomes.

---

## Overview
This project asks a simple question: do patients with mutations in known LUAD driver genes survive longer or shorter than those without? Using publicly available genomic and clinical data, I built a pipeline that screens 8 driver genes across 680 patients and runs Kaplan-Meier survival analysis to find statistically significant associations.

---

## Data
All data sourced from the **UCSC Xena Functional Genomics Explorer** (xena.ucsc.edu):

- **Somatic mutations:** TCGA-LUAD Ensemble Somatic Mutation dataset — 194,731 mutation records across 575 patients
- **Survival data:** TCGA-LUAD phenotype file — OS.time (days) and OS event flag for 721 patients

No account or controlled access required since both files are publicly available.

---

## Methods
1. Loaded and merged mutation and survival datasets, aligning on 12-character TCGA patient IDs
2. Built a binary mutation matrix for 8 established LUAD driver genes: TP53, KRAS, EGFR, STK11, KEAP1, RBM10, BRAF, NF1
3. For each gene, split patients into mutated vs. not mutated groups and ran Kaplan-Meier survival estimation with log-rank hypothesis testing using the `lifelines` library

---

## Results

Of the 8 driver genes tested, **RBM10** was the only statistically significant finding (log-rank p = 0.0228).

Patients with RBM10 mutations (n=44) had noticeably worse overall survival compared to wild-type patients (n=636). RBM10 is an RNA splicing regulator and loss-of-function mutations likely disrupt normal mRNA processing in tumor suppressor transcripts, contributing to more aggressive disease progression.

STK11 trended toward significance (p=0.0842) but didn't cross the threshold.

![RBM10 Kaplan-Meier Curve](https://github.com/user-attachments/assets/b24f0721-a583-464c-b705-58dffaed230f)

---

## Limitations
- RBM10 mutated group is small (n=44), so confidence intervals are wide
- No multivariate adjustment — age and tumor stage could be confounding the result
- Analysis limited to 8 pre-selected genes

---

## Next Steps
- Cox proportional hazards regression to control for age and AJCC stage
- Expand to all genes mutated in >30 patients with FDR correction for multiple testing
- Validate RBM10 finding in an independent cohort (CPTAC-LUAD)

---

## Stack
Python — `pandas`, `matplotlib`, `lifelines`
