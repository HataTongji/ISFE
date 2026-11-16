# ISFE
ISFE v1.0: Informal-Settlement Flood Exposure workflow
# ISFE v1.0: Informal-Settlement Flood Exposure workflow

Code for: Katabarwa Murenzi Gilbert, Qian Shi. *An open machine-learning framework for flood-exposure assessment of informal settlements in data-scarce cities: evaluation across five East African cities.* Submitted to *Environmental Modelling & Software*.

- Code (this repository): https://github.com/HataTongji/ISFE
- Archived release: https://doi.org/10.5281/zenodo.[CODE-ID]
- Data (samples and output rasters): https://doi.org/10.5281/zenodo.[DATA-ID]
- Licence: MIT (code); CC BY 4.0 (data)
- Contact: hata2020@tongji.edu.cn; qianshi@tongji.edu.cn

## What it does
`M2_Final_Reproducible_Pipeline.ipynb` runs the full workflow for Nairobi, Kampala, Dar es Salaam, Kigali and Bujumbura:
1. Data preparation: flood and non-flood sampling (up to 2,500 points per class per city), extraction of 19 predictors, and VIF screening (VIF ≤ 10).
2. Seven learners: RF, XGBoost, CatBoost, LightGBM, ResNet1D, TabTransformer and stacking. They are tuned with Bayesian search under 3-fold spatial-block cross-validation and evaluated on a spatial-block hold-out (20% of each class, as whole ~1.1 km blocks).
3. Explanation: SHAP, accumulated local effects (ALE) and leave-one-covariate-out (LOCO) analysis.
4. Uncertainty: inter-model disagreement and Monte Carlo dropout.
5. Maps: susceptibility, 5-class (Jenks) and uncertainty GeoTIFFs, with figures.
6. External validation against the Global Flood Database (Google Earth Engine, optional).
7. Informal-settlement flood exposure: overlap area, chi-square test and Relative Flood Exposure Index (Cell 11).
8. Supplementary Tables S1, S2 and A1 (Cell 12).

## Installation
```
conda create -n isfe python=3.12
conda activate isfe
conda install -c conda-forge pytorch     # Windows: install PyTorch from conda-forge
pip install -r requirements.txt
```
Tested on Intel Core i7-8750H, 32 GB RAM, NVIDIA GTX 1050 (Windows), and on Google Colab. A CPU is sufficient.

## Data set-up
Download the data archive from https://doi.org/10.5281/zenodo.[DATA-ID] and unzip it. It contains one folder per city with the sample CSV and the predictor rasters. Set `LOCAL_BASE` in Cell 0 to the unzipped folder, or the Google Drive path in Colab.

## Running
Run all cells in order. Results are checkpointed city by city. Outputs are written to `M2_Final_Reproducible_Results/`:
- `Tables/`: metrics, sampling log, SHAP, ALE, LOCO, uncertainty and exposure tables
- `Figures/`: publication figures (300 dpi)
- `TIF_Maps/`: probability, 5-class and uncertainty GeoTIFFs, with QGIS `.qml` styles
- `Supplementary/`: Tables S1, S2 and A1

## Input data sources
Copernicus Sentinel-1/2, SRTM (USGS), the Global Flood Database, JRC Global Surface Water and GADM v4.0, all accessed through Google Earth Engine. GADM boundaries are not redistributed; download them from https://gadm.org.

## Citation
See `CITATION.cff`.
