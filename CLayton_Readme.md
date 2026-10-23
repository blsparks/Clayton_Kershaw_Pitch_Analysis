# Clayton Kershaw Pitch Performance Analysis (2015–2019)

## Project Overview

This project analyzes how MLB pitcher **Clayton Kershaw's performance and pitching approach changed from 2015 through 2019** using pitch-level Statcast data. The analysis examines pitch velocity, pitch selection, opposing contact quality, pitch movement, release position, and recorded plate-appearance outcomes.

**Objective:** Identify meaningful year-over-year trends and explain what they suggest about Kershaw's evolving pitching strategy and effectiveness.

**Tools:** Python, pandas, NumPy, Matplotlib, Seaborn, Plotly, statsmodels, pybaseball, Jupyter Notebook.

## Data

- **Source:** MLB Statcast data, accessed with `pybaseball.statcast_pitcher()` (Baseball Savant).
- **Player:** Clayton Kershaw (MLBAM ID: `477132`).
- **Period:** March 31–October 31 of each year from 2015 to 2019.
- **Records retrieved:** 14,572 pitch records across all five years.
- **Contact analysis sample:** 2,452 balls in play with recorded positive exit velocity.
- **Scope note:** The default notebook includes any game types returned within the date windows; set `REGULAR_SEASON_ONLY = True` to exclude postseason games.

The notebook downloads one season at a time and caches the results in `data/` so subsequent runs do not have to retrieve the data again.

## Analysis Workflow

1. **Collect and validate data:** Retrieve Statcast records and check required fields.
2. **Clean and segment:** Convert dates and numeric columns; create distinct samples for all pitches, pitches with identified types, measured batted balls, and recorded plate-appearance outcomes.
3. **Analyze trends:** Calculate annual metrics for release speed, effective speed, exit velocity, launch angle, hard-hit rate, and pitch mix.
4. **Visualize patterns:** Build line charts, stacked bar charts, game-level LOWESS trends, and interactive 3D release-position charts.
5. **Interpret results:** Compare changes over time and describe implications without claiming a causal relationship.

## Key Findings

| Metric | 2015 | 2019 | Change |
|---|---:|---:|---:|
| Average release velocity | 89.03 mph | 86.21 mph | −2.82 mph |
| Opponents' average exit velocity | 85.20 mph | 88.13 mph | +2.93 mph |
| Opponents' hard-hit rate (95+ mph) | 25.82% | 35.93% | +10.11 percentage points |
| Four-seam fastball usage | 53.3% | 43.5% | −9.8 percentage points |
| Slider usage | 28.0% | 39.6% | +11.6 percentage points |

- **Velocity decreased:** Kershaw's overall average release velocity fell by 2.82 mph between 2015 and 2019. Because the average combines pitch types, pitch-mix changes may contribute to this decline.
- **Contact quality increased:** Opponents hit the ball harder on average, and the share of measured batted balls hit at 95+ mph rose by 10.11 percentage points.
- **Pitch selection shifted:** Kershaw used fewer four-seam fastballs and more sliders, indicating a changing approach during the period analyzed.

### Practical Takeaway

**Tracking velocity alone is insufficient to assess pitcher performance.** Combining pitch-mix trends with exit velocity and hard-hit rate offers a more informative view of how a pitcher is adapting and how opposing hitters are responding. Kershaw's increased slider usage coincided with lower overall velocity and harder opposing contact; the analysis does not establish that one caused the other.

## How to Run

1. Install Python 3.10 or newer.
2. Install dependencies from the project folder:
   ```bash
   pip install -r requirements.txt
   ```
   In Jupyter, use `%pip install -r requirements.txt`. If the requirements file is not in your notebook environment, install the key packages directly:
   ```python
   %pip install pybaseball pandas numpy matplotlib seaborn plotly statsmodels
   ```
3. Open `Clayton_Kershaw_Python_Analysis.ipynb` in Jupyter Notebook, JupyterLab, VS Code, or Google Colab.
4. Run the notebook cells from top to bottom. An internet connection is required on the first run to download the Statcast records.

## Project Structure

```text
Clayton_Kershaw_Python_Analysis.ipynb   # Complete analysis and visualizations
requirements.txt                       # Python dependencies
README.md                              # Project documentation
data/                                  # Cached Statcast CSVs (created on run)
outputs/                               # Summary CSVs and chart PNGs (created on run)
```

## Limitations

- This is an observational study of one pitcher over five years; it cannot determine why observed performance metrics changed.
- Average release velocity includes multiple pitch types, so changes in pitch mix can influence the overall trend.
- Exit-velocity and hard-hit results include only batted balls with usable measurements.
- The notebook's recorded plate-appearance event shares should not be interpreted as official MLB season-level strikeout rates, ERA, or on-base percentages.
- Statcast data coverage and tracking measurements may vary across seasons.

## Data Reference

- [Baseball Savant — Statcast](https://baseballsavant.mlb.com/)
- [pybaseball documentation](https://github.com/jldbc/pybaseball)
