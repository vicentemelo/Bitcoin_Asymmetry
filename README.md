# Bitcoin Asymmetric Power Law

A Jupyter notebook that fits the Bitcoin Power Law to daily prices and draws it as charts you can read at a glance.

```
price ≈ A × (days since the genesis block) ^ n
```

The genesis block is day 0 (3 January 2009). On a log-log chart that curve becomes a straight line. The notebook fits the line, measures how well it holds, and shows where today's price sits against it. The fitted exponent comes out near `n ≈ 5.6`.

<img width="1638" height="652" alt="image" src="https://github.com/user-attachments/assets/181774cb-b66d-4a0d-a41c-96d6af1964ef" />


## Files

| File                      | What it is                              |
| ------------------------- | --------------------------------------- |
| `bitcoin_power_law.ipynb` | The notebook. Run this.                 |
| `BTC_daily.csv`           | Daily BTC closing prices (`Date,Price`) |
| `requirements.txt`        | Python packages it needs                |

<img width="1309" height="648" alt="image" src="https://github.com/user-attachments/assets/7a53d8f2-fd39-4bb7-8ade-af0156986699" />

## How to run

```bash
# 1. (optional) make an isolated environment
python3 -m venv .venv
source .venv/bin/activate          # Windows: .venv\Scripts\activate

# 2. install packages
pip install -r requirements.txt

# 3. open the notebook
jupyter notebook bitcoin_power_law.ipynb
```

Run the cells from top to bottom with Shift+Enter.

When you open it, the first cell checks the CSV's last date. If it is behind, it pulls the missing days from Yahoo Finance up to today, adds them to the file, and keeps going. If you are offline it just uses the data already in the CSV.

<img width="1270" height="636" alt="image" src="https://github.com/user-attachments/assets/699ae9a2-4b4b-4688-b970-eb52bc3d37d6" />


## What each section shows

1. **Load the data.** Read the prices and count days since the genesis block.
2. **Fit the line.** Fit a straight line to `log(price)` vs `log(days)`. The slope is the exponent `n`, the intercept gives `A`, and `R²` says how closely the prices hug the line.
3. **The headline chart.** The price dots scatter around one straight line across six orders of magnitude.
4. **The corridor.** A band around the trend, with a support line (the 1st percentile of past gaps) and a resistance line (the 99th percentile), projected out to 2035. Today's support, fair value, and resistance prices show in the legend.
5. **Histogram.** How many days Bitcoin traded at each distance from the trend, measured in standard deviations. Below trend is green, above trend is red.
6. **Oscillator.** The same distances plotted over time so you can watch Bitcoin swing above and below the trend year by year.
7. **Percentile bands.** Asymmetric 67% and 95% bands, since the gaps are wider above the trend than below. It also notes a handy rule: the trend price doubles roughly every time Bitcoin's age grows about 13%.
8. **Skew-normal bands.** A fitted curve for the lopsided gaps, plus a close-up of the last 12 months.
9. **Risk metric.** For each day, rank today's gap against every gap up to that day and squash it to a 0 to 1 score. 0 is the lowest Bitcoin has ever been against the trend, 1 is the highest. A smoothed version follows, and you can change the `SMOOTH` window to taste.

## Disclaimer

This is an educational visualization, not financial advice. The power law is a descriptive trend, not a law of nature. A high `R²` partly comes from two things both growing over time, the exponent is uncertain (about 5.6 give or take 0.4) and shifts with the chosen start date, and Bitcoin only has one short history. The line can bend or break.
