# Harvard-Yale Scoring Model

A least-squares model of how many points Yale and Harvard each score in a football game, fit on Ivy League game data from 2016-2025. The end goal is to use each team's current season form to predict the score of the upcoming Harvard-Yale game.

See `model.ipynb` for the full write-up of the math and the code.

## Repo layout

```
.
├── model.ipynb   # the model: data loading, fitting, and (soon) evaluation
├── data/
│   └── ivy_team_games_2016_2025.csv   # game log the model is fit on
├── requirements.txt
└── README.md
```

## Requirements

- Python 3.10+
- `pandas`
- `numpy`
- `jupyter` (to open and run the notebook)

Install everything with:

```bash
pip install -r requirements.txt
```

(or just `pip install pandas numpy jupyter` if you'd rather skip the requirements file)

## Running it

1. Clone the repo and `cd` into it.
2. Install the requirements above.
3. Launch Jupyter from the **repo root** — the notebook loads the data with a relative path (`data/ivy_team_games_2016_2025.csv`), so it has to be run from there:
   ```bash
   jupyter notebook model.ipynb
   ```
4. Run all cells top to bottom (Run → Run All Cells, or Shift+Enter through each cell). The last cell prints the fitted coefficients for both teams:
   ```
   Yale Coefficients: [...]
   Harvard Coefficients: [...]
   ```

## Data

`data/ivy_team_games_2016_2025.csv` has one row per **team-game** (so each game appears twice, once from each team's point of view), covering all 8 Ivy League teams from the 2016 through 2025 seasons (2020 is absent — no season was played that year).

| Column                                        | Meaning                                                |
| --------------------------------------------- | ------------------------------------------------------ |
| `team`, `opponent`                            | team names, e.g. `yale`, `harvard`                     |
| `season`, `date`                              | season year, and the game date (`YYYY-MM-DD`)          |
| `home`                                        | 1 if `team` played at home, 0 otherwise                |
| `team_pts`                                    | points scored by `team`                                |
| `team_total_yds`, `team_total_plays`          | offensive yards and play count for `team`              |
| `team_third_down_conv`, `team_third_down_att` | third downs converted and attempted by `team`          |
| `team_turnovers`                              | turnovers committed by `team`                          |
| `opp_total_yds`, `opp_total_plays`            | yards and plays allowed by the defense of `team`       |
| `opp_third_down_conv`, `opp_third_down_att`   | third downs allowed and faced by the defense of `team` |
| `opp_turnovers`                               | turnovers forced by the defense of `team`              |

## Status

The model is fit, but not yet evaluated. See the "Next Steps" section at the end of `model.ipynb` for what's left: backtesting against 2016-2025, validating against 2026 results, and using the validated model to predict the upcoming Harvard-Yale game.
