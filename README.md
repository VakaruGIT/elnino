# El Niño: exploring and forecasting the Oceanic Niño Index

Analysis of NOAA's [Oceanic Niño Index (ONI)](https://www.cpc.ncep.noaa.gov/data/indices/oni.ascii.txt), the 3-month running mean of sea-surface temperature anomalies in the Niño 3.4 region, 1950 to present.

## Status

- [x] EDA and event classification (`eda.ipynb`)
- [ ] Forecasting baselines (`forecasting.ipynb`)
- [ ] Extra predictors (SOI, MEI, ocean heat content)

## What the EDA covers

- Loads the live NOAA file and builds a monthly `DatetimeIndex`. Each 3-month season is dated to its **end month**, so JAS is September, and `NDJ` is shifted to the following year.
- Validates the series: sorted, unique index, no gaps, no missing values, known peak events present.
- Labels every season as El Niño, La Niña or Neutral (`PHASE`), and applies NOAA's stricter rule of 5 consecutive seasons beyond ±0.5 °C (`EVENT`).
- Builds a table of events with start, end, duration and peak.

## Findings

- 42 events since 1950: 22 El Niño and 20 La Niña.
- El Niño reaches higher extremes (peak +2.59 in 2015–16, vs −2.04 for the strongest La Niña, 1973–74), but La Niña episodes last longer on average (about 11 vs 10 seasons).
- The strongest events by peak: 2015–16, 1997–98, 1982–83, 1973–74 (La Niña), 2023–24.
- About 8% of the seasons beyond ±0.5 °C belong to short excursions that do not qualify as events.
- The latest event (2026) is still provisional: it needs 5 consecutive seasons to count.

## Setup

```bash
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
jupyter lab
```

The data is downloaded from NOAA when `eda.ipynb` runs, so it needs network access. The last cell saves `data/oni.csv` and `data/events.csv`. Results change as NOAA adds a new season each month.

## Data source

NOAA Climate Prediction Center, ONI. Public domain; please cite NOAA CPC.
