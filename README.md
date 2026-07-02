# Within-subject biomarker tracking in early Parkinson's disease

Analysis code for a Bachelor's thesis (TFG) examining whether blood neurofilament
light chain (NfL) and DAT-SPECT imaging track motor worsening within the same
patient in early Parkinson's disease, using longitudinal data from the
Parkinson's Progression Markers Initiative (PPMI).

## Notebooks

All three notebooks live in `notebooks/` and are meant to be run in this order:

1. **`EDA_NfL_v4.ipynb`** — SAA+ stratification, NfL cohort construction
   (log2 transform, ≥3 visits), linear mixed-effects model (NfL vs MDS-UPDRS
   Part III), and the within-between (Mundlak) decomposition.
2. **EDA_DaTscan_v3.ipynb** — DAT-SPECT cohort construction, lateralization
   (tracking the less-affected/contralateral putamen), LMM (SBR vs motor
   score), and within-between decomposition.
3. **`EDA_NfL_DaTscan_Crossover.ipynb`** — combines the two cohorts above:
   patients with both NfL and DAT-SPECT data, aligned by visit date
   (≤180 days apart), and the three-way comparison (NfL–UPDRS, DAT-SPECT–UPDRS,
   NfL–DAT-SPECT).

Each notebook saves its filtered/processed dataset and figures under
`../04_Data/Results/` (relative to the notebook's own location), so the three
can be re-run independently once the raw data is in place.

## Data access

This repository does **not** include any PPMI data (raw or processed), per the
PPMI Data Use Agreement. To reproduce the analysis:

1. Register for a PPMI account and request data access at
   [ppmi-info.org](https://www.ppmi-info.org/access-data-specimens/download-data).
   Access is granted through the LONI Image & Data Archive (IDA) after
   agreeing to the Data Use Agreement; some data types may require a short
   research use description. Check the site for the current process, as it
   can change.
2. Once approved, download the following study files from the IDA:
   - `Current_Biospecimen_Analysis_Results_*.csv` (includes NfL)
   - `SAA_Biospecimen_Analysis_Results_*.csv`
   - `MDS-UPDRS_Part_III_*.csv` (and Parts I, II, IV if reproducing the total
     UPDRS analysis in `EDA_NfL_v4.ipynb`)
   - `Xing_Core_Lab_-_Quant_SBR_*.csv` (DAT-SPECT striatal binding ratios)
   - `Age_at_visit_*.csv`
3. Place them in `04_Data/Raw/` at the project root (i.e. one level above
   `05_Code/`), keeping the original PPMI filenames — the notebooks read from
   `../../04_Data/Raw` relative to their own folder.
4. Run the notebooks top to bottom in Jupyter; each one creates its own
   `04_Data/Results/results_*/` output folder automatically.

## Requirements

Python 3, with `pandas`, `numpy`, `matplotlib`, `seaborn`, `statsmodels`, and
`scipy`.
