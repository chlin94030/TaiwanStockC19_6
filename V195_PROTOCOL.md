# V19.5 development protocol - frozen before supplied-price replay

Scope: user-uploaded V19.4 full 99-file archive with SHA256
7095b01b47f5f0541d256281c4f5de864d99693c0c04a4464be9e43e4acb0f12.
No new performance report accompanied this upload. Reuse the prior supplied
price bundle only for development comparisons, never as a new blind test.

Changes fixed before looking at new replay outcomes:
- Retain the 34-column feature library, original controls, cost and entry rules.
- Fit each candidate on its own selected inputs; missing unused columns cannot
  remove rows. No imputation of selected factors.
- Use non-overlapping scoring windows across ALL chronological inner folds;
  purge fit labels relative to each fold start.
- Reserve exactly the configured final validation block count (default 4),
  not opportunistically 4-6; longer-horizon development window uses up to
  max(252, 8*h+train_dates) past decision dates, retaining the 3-year input limit.
- Compare equal-within-support versus fitted nonnegative-ridge weights inside
  the search folds. Deleted factors are never restored. Budget counts candidates,
  not subset names; default 160, at most 6 underlying inputs.
- Search depth-specific frontiers, with bounded additions, removals and swaps.
- Reject semantic overlap between composite, interaction and parent inputs.
- Final selection is ONE candidate before final-block inspection. Candidate
  missing data cannot choose a more favorable subset of reference dates.
- Do not weaken existing improvement, benchmark, risk and fill gates.
- Sparse UI and similar-history displays require ALL selected inputs.
- Report gate failures, data coverage, search alternatives and replay matching.

Outcome plan: baseline V19.4 versus V19.5 on the same 100 exposed dates,
5/20/60-day paired means, accepted counts, candidate counts, and cash separate.
No coefficient or threshold is chosen from this outer replay's results.
No claim that optimal weights or future returns have been established.
