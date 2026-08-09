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

## Does any magnitude work?

The result above tested a single magnitude (±0.1). That isn't enough to call the
flag useless — the magnitude itself might have been wrong. So: nine values,
0.001 to 2.0, against the same baseline.

| Magnitude | MAE | vs baseline |
|---|---:|---:|
| 0.001 | 6.407759 | −0.000012 |
| 0.005 | 6.407713 | −0.000058 |
| 0.010 | 6.407655 | −0.000116 |
| 0.050 | 6.407288 | −0.000482 |
| **0.100** | **6.407057** | **−0.000714** |
| 0.200 | 6.407335 | −0.000436 |
| 0.500 | 6.414123 | +0.006352 |
| 1.000 | 6.445199 | +0.037429 |
| 2.000 | 6.579970 | +0.172200 |

Baseline (predict 0): **6.40777**

**MAE improves steadily up to 0.1, then reverses.** The optimum is interior, not
at the boundary — which means the flag does carry directional information. If it
carried none, any step away from zero would have hurt immediately.

Checking direction directly, on the 4,106,386 rows with a non-zero flag:

| | |
|---|---|
| Correct direction | **50.74%** |
| 95% CI | [50.69%, 50.79%] |
| Distance from chance | ~30 standard errors |
| MAE improvement | **0.0111%** |

**The edge is statistically certain and economically worthless.** That gap is the
finding. With four million rows you can establish a signal beyond any doubt and
still find it far too small to act on — and the penalty for overshooting dwarfs
the reward: magnitude 2.0 is 2.69% *worse* than predicting nothing at all.

Significance was never the question. Effect size was.

## Limits

- The three plots cover **one stock on one day** — illustrative, not representative
- No model fitted. No feature engineering. Baselines only.
- Single metric (MAE), evaluated in-sample on the training set
- Nine magnitudes tested on a linear scale of the flag; no interaction terms

## What I'd do next

Test whether `imbalance_size` carries what the flag doesn't. Direction alone is
near-worthless, but magnitude and time-to-close may not be — and the flag most
likely only matters in interaction with them, not on its own.

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
