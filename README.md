# 2026-27 Bundesliga Predictor

This is an end-to-end predictive analytics project designed to forecast the **2026/27 Bundesliga season**, from match-level predictions through to an expected final league table.

## Project Overview

The model combines **Dixon-Coles (DC) statistical modelling** with **XGBoost** to estimate expected home and away goals for each fixture. The DC model captures underlying team attacking and defensive strengths while accounting for home advantage, while XGBoost provides a machine-learning approach using engineered team and match-level features.

The resulting goal expectations are converted into scoreline probability distributions and used in a **10,000-run Monte Carlo simulation** of the full season. The simulations are aggregated to estimate expected points and finishing positions, alongside probabilities for outcomes such as winning the title, finishing in the top four, and relegation.

## Data

Historical Bundesliga data was collected from:

- **FBref** — team and player performance statistics
- **Understat** — expected goals (xG) and match-level attacking data
- **Transfermarkt** — supplementary squad and transfer information

Data was cleaned, standardised and merged across seasons before being used for feature engineering and modelling.

## Feature Engineering

Features were engineered to capture both recent form and longer-term team strength. The final feature set was grouped into four main areas:

- **Performance & Form:** Goals, goals conceded, xG, xGA, non-penalty xG, non-penalty xGA, non-penalty xG difference, points, PPDA and deep completions. These were calculated over the last 5 matches, last 10 matches, season-to-date and the team's previous 5 matches at the relevant venue.
- **Attacking & Defensive Strength:** Weighted measures combining recent and season-to-date xG and xGA, giving greater weight to recent performance.
- **Squad Value:** Team market value, changes in market value, percentage changes and log-transformed market values.
- **Head-to-Head:** Historical win rates, average goals scored by each team and average goal difference from previous meetings.

Additional indicators were included to account for promoted teams when generating predictions.

This feature set was used to train separate home-goal and away-goal XGBoost regression models.

## Modelling Pipeline

1. Collect and clean historical Bundesliga data.
2. Merge data from FBref, Understat and Transfermarkt.
3. Engineer team-level feature groups.
4. Estimate team attacking and defensive parameters using a **Dixon-Coles model**.
5. Train **XGBoost regression models** for home and away goals.
6. Evaluate model performance using the **2025/26 Bundesliga season** as an out-of-sample test set.
7. Combine model outputs to generate expected goals for each fixture.
8. Convert expected goals into scoreline probability matrices.
9. Run **10,000 Monte Carlo simulations** of the complete season.
10. Aggregate the simulations to estimate the expected final league table and finishing probabilities.

## Predicted 2026/27 Bundesliga Table

| Predicted Position | Team | Expected Points |
|---:|---|---:|
| 1 | Bayern Munich | 80.95 |
| 2 | Borussia Dortmund | 65.12 |
| 3 | Bayer Leverkusen | 64.92 |
| 4 | RB Leipzig | 59.71 |
| 5 | Stuttgart | 57.95 |
| 6 | Eintracht Frankfurt | 50.38 |
| 7 | Hoffenheim | 47.17 |
| 8 | Mainz | 46.31 |
| 9 | Freiburg | 45.85 |
| 10 | Borussia Monchengladbach | 43.18 |
| 11 | Union Berlin | 41.44 |
| 12 | Werder Bremen | 40.40 |
| 13 | Hamburger SV | 39.11 |
| 14 | Augsburg | 38.91 |
| 15 | Koln | 38.84 |
| 16 | Elversberg | 30.05 |
| 17 | Schalke | 29.09 |
| 18 | Paderborn | 26.35 |

## Tools

**Python · pandas · NumPy · scikit-learn · XGBoost · statsmodels · Jupyter**

*Predictions represent model estimates rather than guaranteed outcomes.*
