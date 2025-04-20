# Aspergillus Germination Dynamics

**Custom R scripts for analyzing phenotypic heterogeneity and germination dynamics in *Aspergillus niger* spores using oCelloScope time-lapse imaging.**

## 📚 Background & Scientific Rationale
Phenotypic heterogeneity plays a central role in the germination behavior of Aspergillus spores. Earlier methods (Chapters 2–4) relied on fixed area and circularity thresholds, which introduced bias across species and subpopulations. The improved pipeline (Chapter 5) defines germination relative to initial spore size and shape, accommodating asynchronous germination and subpopulation differences.

This method:

Removes the need for species-specific thresholds

Is robust against size-related artifacts

Is applicable to mixed populations (e.g., environmental spores or co-cultures)

The revised pipeline enhances reproducibility and reflects biological variation, not just population averages.
---

## 📚 Overview

This repository contains R scripts and data-processing pipelines developed during my PhD research to study fungal spore germination dynamics. The goal was to analyze phenotypic heterogeneity in swelling and germ tube formation across various *A. niger* spore populations, using a novel classification method based on relative changes in spore morphology.

### 🧪 Key Concepts:
- **Spore phenotypic heterogeneity** affects germination timing and dynamics.
- **Germination is analyzed in two phases**: swelling and germ tube formation.
- **Maturity of spores** (e.g., 8-day-old vs. 38-hour-old) significantly impacts nutrient response.
- **Compatible solute-deficient mutant (SJS128)** Hypothesised to have the same germination dynamics as immature A. niger reference strain. 

---

## 🧬 Data & Conditions

The datasets were generated using **oCelloScope time-lapse imaging** to track the germination of individual spores across 24 hours.

### Strains:
- `N402` – reference strain mature spores (8 days)
- `N402 38h` – Immature spores (harvested at 38 hours)
- `SJS128` – Mutant lacking biosynthesis of compatible solutes genes

### Nutrient Treatments:
- Amino acids: `Proline`, `Alanine`, `Arginine`
- Sugar: `Glucose`
- Each tested at `10 mM` and `1 mM`

---

## 🔍 Analysis Pipeline

### 1. **Preprocessing**
- Clean and merge `.csv` files exported from oCelloScope.
- Track spores by `ObjectId` and calculate:
  - Initial area
  - Initial circularity
  - Relative increases over time

### 2. **Germination Phase Assignment**
- **Resting (R):** No significant area or circularity change
- **Swelling (S):** Area ↑ ≥ 10%, circularity ~ stable
- **Germ Tube (G):** Area ↑ ≥ 50%, circularity ↓ ≥ 10%

### 3. **Metrics Extraction**
Using the `germinationmetrics` R package:
- Germination % (`Pmax`)
- Time to 50% germination (`t50_coolbear`)
- Germination heterogeneity (`GermUncertainty`, `d`)
- Coefficient of Velocity of Germination (`CVG`)
- Weighted Germination Percentage (`WGP`)

### 4. **Curve Fitting & Visualization**
- Modeled germination using 4-parameter Hill functions (`FourPHFfit.bulk`)
- Swelling and germ tube formation plotted with overlaid replicate dots

---
## 🧠 Acknowledgements
Some part of this pipeline builds on the germinationmetrics R package (Aravind et al., 2024), originally designed for plant seed germination. It was adapted for fungal spores to offer a universal and unbiased analysis framework.

## ✉️ Contact
For questions or collaborations:

Maryam Ijadpanahsaravi

✉️ m.ijadpanahsaravi@uu.nl

🔬 PhD Candidate, Microbiology, Utrecht University
