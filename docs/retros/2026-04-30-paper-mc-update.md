# Retro: Paper MC Update - 2026-04-30

## What we did
Corrected the Monte Carlo sensitivity analysis results throughout the capstone paper after
discovering that the original p05 claims (>= 1.21 at days 0-13) were based on a run without
a minimum-event-count filter, making late-offset statistics unreliable.

## Changes made to paper
1. Section 5d: Updated MC claim to days 0-9, n >= 8 filter, day 5 marginal (p05 = 0.99)
2. Conclusion: Updated MC parenthetical to match corrected statistics
3. Fig. 4 caption: Updated to corrected language
4. Fig. 4 image: Swapped old figure (y-axis 0-5, days 0-13) for sensitivity_mc.png (y-axis 0-2.5, days 0-9)
5. Last appendix caption: Fixed "Fig. 1." to "Fig. 10." (numbering error from inserting Fig. 9 AO split)

## What we learned about the data
- Late CAO day offsets (10+) have very few contributing events - reporting MC bounds there is
  misleading. The n >= 8 threshold is a reasonable floor for composite credibility.
- Day 5 is consistently marginal (p05 near 1.0) across runs; the 25th percentile (1.43)
  confirms the full distribution still sits well above 1.0, so the result holds.
- AO phase split: positive n=11, negative n=19 (30 total identified, 27 used in main composite
  after 3 excluded). Confirmed from Cell 15 code, not paper text.

## Files changed
- `capstone_paper_draft CAO 4-27-26.docx` (in Research Paper/)
- `Capstone.ipynb` Cell 14: added n_events >= 8 filter to valid_days
