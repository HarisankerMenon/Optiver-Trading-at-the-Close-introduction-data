# Optiver — Closing Auction: Baseline Analysis

Exploring order-book behaviour during the Nasdaq closing auction
(Kaggle: *Optiver – Trading at the Close*).

**This is a baseline study that stops at a negative result** — deliberately.

---

## What I did

Visualised how bid/ask/WAP, near/far/reference prices, and imbalance/matched
size evolve across the auction window for a single stock-day. Then established a
zero-prediction baseline and tested whether the obvious naive rule beats it.

## What I found

| Prediction | MAE |
|---|---:|
| Always 0 (baseline) | 6.40777 |
| Imbalance flag → ±0.1 | 6.40706 |
| **Improvement** | **0.00071 (0.011%)** |

A 0.011% improvement is indistinguishable from noise. **The auction imbalance
buy/sell flag alone carries no usable directional signal at this magnitude.**

## Why this is worth committing

Establishing what a trivial predictor achieves comes before fitting anything.
Without that number, a model's score is unreadable — an R² or an MAE means
nothing until you know what predicting zero would have got you.

This result also says something specific: any model built on this data has to
beat **6.40777**, and the imbalance direction is not the feature that will do it.
The flag most likely matters only in interaction with size and time-to-close,
not on its own.

## Limits

- The three plots cover **one stock on one day** — illustrative, not representative
- No model fitted. No feature engineering. Baseline only.
- Single metric (MAE), evaluated in-sample on the training set
- The ±0.1 magnitude is arbitrary and untested

## What I'd do next

Sweep the magnitude before adding anything else:

```python
for m in [0.01, 0.05, 0.1, 0.5, 1.0, 2.0]:
    mae = (train["imbalance_buy_sell_flag"] * m - train["target"]).abs().mean()
    print(f"magnitude {m:<5} MAE {mae:.5f}")
```

If no scaling beats 6.40777, the flag is uninformative alone — useful to know
before building features on top of it.

## Data

Kaggle competition data (~611 MB), **not redistributed here** — see
[`data/README.md`](data/README.md).

## Run it

```bash
pip install -r requirements.txt
# place train.csv in data/ — see data/README.md
jupyter notebook optiver_auction_baseline.ipynb
```

`train.csv` is ~611 MB and loads into roughly 2 GB of memory.

---

**V. Harisanker** · Michelstadt, Germany
[Portfolio](https://harisankermenon.github.io) · [LinkedIn](https://www.linkedin.com/in/v-harisanker-0537302b0) · vharisankermenon@gmail.com
