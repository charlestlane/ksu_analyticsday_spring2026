# Zero-Inflated Poisson Modeling of NCAA Postseason Awards

**Authors:** Kyle Bresko, Charles Lane, Kaleb Treangen

**Course:** DATA 4990 — Capstone

**Department:** School of Data Science and Analytics, Kennesaw State University

**Term:** Spring 2026

---

This notebook contains the analysis code for our capstone project. We model individual player award counts in NCAA Conference USA men's basketball using game-level box score statistics. A Zero-Inflated Poisson (ZIP) regression is employed to handle the excess zeros inherent in award count data, and model performance is evaluated against several baseline regressors using Spearman rank correlation.

# Summary

## Objective
This project predicts individual player award counts for NCAA Conference USA men's basketball using game-level box score statistics. The goal is to identify which statistical performance metrics best predict end-of-season award recognition.

## Data
- **Box scores** were collected via the ncaahoopR R package for three Conference USA seasons: 2023-24, 2024-25, and 2025-26.
- **Awards** data was gathered from conference award announcements for the same seasons.
- Player names were normalized and matched across both sources. Coach awards were excluded.

## Feature Engineering
- Per-game statistics were aggregated at the player-season level, including points, rebounds, assists, steals, blocks, field goals, free throws, and turnovers.
- Derived features include shooting efficiency, usage rate, and team-level totals (FGA, FTA, TOV).
- Features were standardized using StandardScaler prior to modeling.

## Train/Test Split
- **Training:** 2023-24 and 2024-25 seasons
- **Testing:** 2025-26 season

## Modeling
- Several regression models were evaluated via grid search with cross-validation, including Linear Regression, Poisson Regression, Ridge, Lasso, Random Forest, Gradient Boosting, and KNN.
- A **Zero-Inflated Poisson (ZIP)** model was selected as the primary model to account for the large number of players who receive zero awards (excess zeros in the target distribution).
- Model diagnostics included VIF checks for multicollinearity and a dispersion test comparing Poisson vs. Negative Binomial assumptions.

## Evaluation
- Models were compared using Spearman rank correlation, which measures how well predicted values preserve the relative ordering of players by award count.
- The ZIP model was benchmarked against the sklearn regression candidates.
- Residual plots and actual-vs-predicted scatter plots were used for visual assessment.

## Predictions and Analysis
- The ZIP model generated predicted award counts for all players in the 2025-26 test season.
- Rolling prediction windows and games-to-date analyses tracked how player rankings evolved over the course of the season.
- Key players such as R. Johnson, Z. Cleveland, C. Bliss, and K. Natt were profiled across game windows to observe prediction stability.
