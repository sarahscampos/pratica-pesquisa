# DARA — Divergent Association Rules Analysis

## Objective
- Reproduce and illustrate the DARA idea over categorized health data, comparing frequency distributions between the full dataset and rule-induced subsets to highlight divergent value rankings.
- Based on the study:
  - Baroni, L., Salles, R., Salles, S., Guedes, G., Porto, F., Bezerra, E., Barcellos, C., Pedroso, M., Ogasawara, E. [An analysis of malaria in the Brazilian Legal Amazon using divergent association rules](https://doi.org/10.1016/j.jbi.2020.103512). Journal of Biomedical Informatics, 2020. DOI: 10.1016/j.jbi.2020.103512.

## Workflow (Semantic Numbering)
- `1-generate-rules.R`
  - Loads `dara/rj.cat.csv`, generates association rules targeting `tmn.geral=alto`, computes interest measures, filters weak/redundant rules, and exports a tidy `dara/dataset.csv` used downstream.
- `2-divergent-ranking.R`
  - Loads `dara/rj.cat.csv` and `dara/dataset.csv`, restricts the dataset to `tmn.geral=="alto"`, and computes per-attribute divergent rankings by comparing the ordering of value frequencies between dataset and rules.

## Data
- `dara/rj.cat.csv`: Categorized dataset (input).
- `dara/dataset.csv`: Rules summary produced by Step 1 (output, also input to Step 2).
- `dara/dataset.RData`: Auxiliary data (not required by the scripts above, kept for reference).

## Usage
- Run from the repository root or from within `dara/`:
  - R: `Rscript dara/1-generate-rules.R`
  - R: `Rscript dara/2-divergent-ranking.R`
- The scripts resolve input/output paths to `dara/` automatically.

## Notes
- No Jupyter notebooks were found in this folder.
- Scripts were refactored with English, didactic comments and consistent file paths.
- If you add new steps (e.g., `3-visualization.R`), follow the same naming pattern.
