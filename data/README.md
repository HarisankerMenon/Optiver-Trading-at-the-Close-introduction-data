# Data

Kaggle competition data is **not stored in this repository**. `train.csv` alone
is ~611 MB — above GitHub's 100 MB per-file limit — and the competition rules
restrict redistribution of competition data.

**Source:** https://www.kaggle.com/competitions/optiver-trading-at-the-close/data

Download from the competition page and place `train.csv` in this folder.

## Key columns

| Column | Meaning |
|---|---|
| `stock_id`, `date_id`, `seconds_in_bucket` | identifiers; `seconds_in_bucket` runs across the auction window |
| `imbalance_size`, `imbalance_buy_sell_flag` | auction imbalance size and direction (1 buy / 0 none / −1 sell) |
| `matched_size` | size matchable at the current reference price |
| `reference_price`, `near_price`, `far_price` | auction price signals |
| `bid_price`, `ask_price`, `bid_size`, `ask_size`, `wap` | order book |
| `target` | short-horizon return, basis points — the prediction target |

## Baseline to reproduce

```python
baseline_mae = train["target"].abs().mean()
print(baseline_mae)   # 6.40777...
```

Any model must beat **6.40777** to be worth anything.

## Note on the competition files

The Kaggle download also includes `competition.cpython-310-x86_64-linux-gnu.so`,
`__init__.py` and `public_timeseries_testing_util.py`. These are Kaggle's
compiled evaluation API — they only work inside a Kaggle notebook and are
deliberately excluded by `.gitignore`. Compiled binaries do not belong in a
portfolio repository.
