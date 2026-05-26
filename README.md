# annae_2026_status
Data and code used in the paper Acosta-Chaves et al. From Protected Areas To Urban Refuges: The Status Of The Blue-Sided Leaf Frog (Agalychnis Annae) In Costa Rica 
README – Supplementary R Scripts for Agalychnis annae Distribution Analysis
Authors: Hector Zumbado, Victor Acosta
Standardization and improvement: DeepSeek (AI assistant)
Date: 2026-05-25

This repository contains four standardized R scripts that perform the complete data cleaning, spatial analysis, environmental mapping, population PCA, and protected‑area assessment for the frog Agalychnis annae in Costa Rica.

Data access note:
Some occurrence localities have been obscured because the species is sensitive to collection or disturbance. The full, precise coordinates are not included in this public repository. They can be obtained upon reasonable request to the corresponding authors, provided the requester holds a valid research permit from the relevant Costa Rican authorities (SINAC, MINAE, CONAGEBIO). The cleaned, aggregated data that are already anonymised are provided in the data/processed/ folder after running the scripts.

Scripts overview
Script	Description
Supplementary_Code_1_Data_Cleaning_and_Full_Dataset.R	Downloads (optional), cleans, and merges occurrence records from GBIF, iNaturalist, UCR, citizen science, and Panama. Creates the full dataset and temporal subsets (pre‑2000 / post‑2000).
Supplementary_Code_2_County_Analysis.R	Performs county‑level (cantonal) analyses: maps of observation counts, bar charts, latitudinal/longitudinal trends, first observation year, and density plots.
Supplementary_Code_3_Environmental_Maps_and_Population_PCA.R	Generates publication‑quality maps for 22 environmental variables (19 bioclimatic + elevation + HFI + coffee) at 30‑arc‑second resolution, plus a PCA of three geographic populations and background points.
Supplementary_Code_4_Protected_Areas_and_Corridors.R	Quantifies occurrence overlap with Costa Rican protected areas and biological corridors (including the 2024 Cubujuquí corridor). Produces four map variants (labeled, clean, numbered, patterned) and summary tables.
Required R packages
All scripts rely on the following packages. They are automatically installed if missing (except rgdal which is deprecated – we use sf and terra).

r
pkgs <- c("sf", "ggplot2", "dplyr", "tidyr", "readr", 
          "ggspatial", "ggrepel", "patchwork", "cowplot",
          "terra", "FactoMineR", "factoextra", "writexl",
          "ggpattern", "gridExtra")
Folder structure
Before running the scripts, create the following directory structure relative to your working directory:

text
your_project/
├── data/
│   ├── raw/                    # Place raw input files here
│   │   ├── Agalychnis_annae_gbif_raw.rds
│   │   ├── inat_annae.rds
│   │   ├── Agalychnis_annae_ucr.rds
│   │   ├── Agalychnis_annae_raw_media.rds
│   │   └── Agalychnis_annae_panama.csv
│   └── processed/              # Created automatically; cleaned outputs go here
├── shapefiles/
│   ├── costa_rica_wgs84.gpkg   # Costa Rica boundary
│   ├── area_silvestre_protegida.gpkg
│   ├── corredores_biologicos.gpkg
│   ├── Corredor_Cubujuqui.shp  # 2024 corridor (optional)
│   └── (other administrative layers: counties, provinces, etc.)
├── rasters/
│   └── env_stack_annae_30s.tif # 22‑layer environmental stack (30 arc‑sec)
└── output/
    ├── figures/                # Maps and plots
    └── protected_areas_mainland/
        ├── tables/
        └── maps/
Note: The environmental stack and shapefiles are not provided in this repository because of their large size. They can be obtained from public sources (WorldClim, HFI, ICAFE, SINAC).

Running the scripts
Execute the scripts in numerical order because later scripts depend on outputs from earlier ones (e.g., the full dataset is created in Code 1 and used in Codes 2‑4).

bash
Rscript Supplementary_Code_1_Data_Cleaning_and_Full_Dataset.R
Rscript Supplementary_Code_2_County_Analysis.R
Rscript Supplementary_Code_3_Environmental_Maps_and_Population_PCA.R
Rscript Supplementary_Code_4_Protected_Areas_and_Corridors.R
Each script will:

Check for required directories and create them if missing.

Load necessary libraries (install if absent).

Run the analysis and save outputs (tables, figures) into the output/ folder.

Print progress messages to the console.

Expected outputs
Code 1
data/processed/Agalychnis_annae_full_dataset.rds – merged occurrences.

data/processed/Agalychnis_annae_predecline.rds – pre‑2000 subset.

data/processed/Agalychnis_annae_postdecline.rds – post‑2000 subset.

Maps: output/figures/Agalychnis_annae_*.jpg.

Code 2
data/processed/Agalychnis_annae_total_obs.csv – counts per county and time period.

output/figures/Agalychnis_annae_*.jpg – county bar charts, lat/long trends, first observation plots.

Code 3
output/figures/maps_30s/individual/ – one map per variable (PNG, PDF, SVG).

output/figures/maps_30s/variations/ – alternative backgrounds and HFI palettes.

output/figures/population_pca/ – PCA biplot, boxplots, density plots, variable contributions, and pca_results.xlsx.

Code 4
output/protected_areas_mainland/tables/ – CSV summaries of points in PAs and corridors.

output/protected_areas_mainland/maps/ – four map variants (PNG, PDF).

License and citation
These scripts are provided for reproducible research. If you use them, please cite the paper.

Session info
All scripts were tested with R version 4.3.2 and package versions current as of May 2026. A sessionInfo() log is saved with each run.
