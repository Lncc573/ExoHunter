# ExoHunter: ML Ranking of TESS Exoplanet Candidates

Can machine learning combine transit characteristics to rank exoplanet candidates better than a conventional baseline, and explain why each candidate gets its score?

Data: NASA Exoplanet Archive, TESS Object of Interest (TOI) table. Runs in Google Colab; all outputs save to Google Drive so a disconnect never loses progress.

## Key results

| Method (exam-set ROC-AUC) | Transit only | Transit + star | All clues |
|---|---|---|---|
| Depth baseline | 0.552 | | |
| Logistic regression | 0.648 | 0.735 | 0.770 |
| XGBoost | 0.759 | 0.898 | 0.924 |

- **Explainable:** SHAP shows how each clue pushes a candidate's score up or down.
- **Bias measured:** the fraction of real planets falls from 0.86 (closest stars) to 0.21 (farthest). A distance-matched model keeps similar AUC (0.875 vs 0.870 on a balanced exam) but only 21 of its top 100 candidates overlap with the original model's.
- **Real-data check:** 30 top candidates were folded on TESS light curves. All 24 testable ones showed a dip; none showed a large eclipsing-binary signature. This is a sanity check, not confirmation.
- **Light-curve features pilot (275 candidates):** AUC 0.675 to 0.765 on transit-only clues; cause of the gain not established.

## Limitations (important)

Scores order candidates; they are **not** probabilities of being a planet. Labels reflect which candidates astronomers chose to follow up (selection bias), undecided candidates are farther and fainter than labeled ones, and the vetting sample is small and not random. See the full report.

## Repository contents

- `notebooks/ExoHunter_clean.ipynb`: the whole project, top to bottom
- `docs/ExoHunter_Report.pdf`: final report

## How to run

1. Open the notebook in Google Colab (File > Open notebook > GitHub tab, or upload it).
2. Run Section 0 first, then the sections in order. After a disconnect, rerun Section 0 and continue from where you were.
3. Slow sections (light-curve vetting and the pilot) save after every star and stop after 25 minutes; press play again to continue.

## Next steps

Compare the saved prediction snapshot with NASA's future verdicts; vet lower-ranked candidates too; refit timing with BLS for the pilot candidates.
