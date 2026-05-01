# Research Notes - Capstone Gotchas

## Monte Carlo valid_days filter (2026-04-30)

**Bug:** The original MC sensitivity analysis (Cell 14 of Capstone.ipynb) computed p05 for all
day offsets 0-13, including late offsets (days 10+) where very few events contribute to the
composite. This produced artificially stable-looking p05 values (reported as >= 1.21) that
were not statistically meaningful due to low n.

**Fix:** Filter `valid_days` by a minimum event count before running the MC loop:

```python
n_events_per_day = px_df.groupby('day_offset')['onset'].nunique()
valid_days = bowen_mc_df.columns[bowen_mc_df.columns.isin(n_events_per_day[n_events_per_day >= 8].index)]
```

Note: `valid_days` must be initialized from `bowen_mc_df.columns` - do not filter an undefined variable.

This drops days 10+ from the analysis. Seed set to `np.random.seed(42)` for reproducibility.

**Corrected statistics:**
- Days reported: 0-9 (n >= 8 at each offset)
- Day 5 is marginal: p05 = 0.99, but 25th percentile = 1.43
- Minimum robust p05: 1.14 at day 9
- p05 > 1.0 at all offsets except day 5

**Paper language (corrected):**
> p05 exceeded 1.0 at all post-onset day offsets 0-9 with adequate composite sample sizes
> (n >= 8), with the marginal exception of day 5 (p05 = 0.99; 25th percentile = 1.43).
> Minimum p05 at unambiguously robust offsets was 1.14 at day 9.

**Lesson:** Always check n per day offset before reporting MC bounds at late offsets in
event-composite studies. Low-n tails can produce misleadingly stable percentile bounds.
