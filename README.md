# Cropland Mapping — Code Submission

Everything needed to run `Cropland_Mapping_Pipeline.ipynb` is in this folder.

## Setup

```
python -m venv venv
venv\Scripts\activate        # (Linux/Mac: source venv/bin/activate)
pip install -r requirements.txt
```

Then open `Cropland_Mapping_Pipeline.ipynb` in Jupyter and run all cells top to bottom.

## Two ways to run it

The notebook has one master switch near the top:

```python
RUN_EXPENSIVE_CELLS = False   # default
```

- **`False` (default, recommended):** loads the already-computed CSV outputs in this
  folder (feature tables, tuning results, CV scores, etc.) — the same files the
  dissertation's tables and figures were built from. Runs in under a minute.
- **`True`:** re-runs the full pipeline from scratch — Google Earth Engine feature
  extraction, hyperparameter search, and TempCNN training. Takes roughly 1–2 hours and
  requires:
  - A Google Earth Engine account with API access.
  - Editing the line `ee.Initialize(project="uosmc-490716")` in Section 3.1 to your own
    GEE-enabled Google Cloud project — `uosmc-490716` is the original author's project
    and will not work for anyone else.
  - `pip install earthengine-api` (commented out in `requirements.txt` since it's only
    needed in this mode) and running `earthengine authenticate` once beforehand.

## File manifest

| File(s) | Role |
|---|---|
| `Cropland_Mapping_Pipeline.ipynb` | The notebook — run this |
| `requirements.txt` | Python dependencies |
| `Train.csv`, `Test.csv` | Raw GeoAI Challenge data (all regions) — the notebook filters these to the Iran subset itself on the first run |
| `Train_Iran_features.csv` | Extracted satellite features (Sentinel-1/2, Landsat-8) for the Iran subset |
| `Train_Iran_features_year2.csv` | Second-season features, used in the temporal extendibility test |
| `Train_Iran_errors_by_landcover_tuned.csv` | ESA WorldCover land-cover class per point, cross-tabulated with model errors |
| `tuned_model_comparison_kappa_fixed.csv`, `repeated_cv_kappa.csv` | Cross-validated Kappa scores (5-fold and 15-split) |
| `feature_importance_tuned.csv`, `oof_predictions_all_models_tuned.csv`, `sensor_ablation_results.csv` | Supporting results used in the notebook's evaluation section |
