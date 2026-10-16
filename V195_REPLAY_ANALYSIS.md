# Alpha Radar V19.5 | Development replay and model-design corrections

## Decision summary

V19.5 is a selection/cohort/validation correction, not a proven performance upgrade. The 20-session adopted strategy improves relative to V19.4 on this replay, the 5-session strategy deteriorates, and the 60-session adopted strategy is unchanged. All three still trail their matched 0050 reference means. The latest fitted candidates are not approved by the final past-block adoption checks.

The current upload was a source-code ZIP, NOT a new market report. The earlier user-supplied Yahoo_daily snapshots were reused for development. No new weight, threshold or feature was selected after observing this new outer replay.

## Inputs and comparison integrity

- Source archive: user-uploaded V19.4 full 99-file package.
- Base SHA256: `7095b01b47f5f0541d256281c4f5de864d99693c0c04a4464be9e43e4acb0f12`.
- Prices: 63,928 rows, 92 symbols including 0050, hence 91 equities.
- Dates: 2023-10-16 through 2026-10-15; the same 100 previously exposed cutoffs.
- Horizons: 5, 20 and 60 trading sessions; 300 outer cases.
- Same entry, exit, cost, liquidity, price-basis and gap conventions as the previous run.
- Original fixed-control status/return replay: 300 matching completeness states; 294 finite returns; maximum difference zero.
- Optional fundamental/ownership source records: absent. Their empirical benefit remains untested.
- Exported price snapshots were compared by ticker/date, all columns and provenance. They match within CSV floating representation tolerance (rtol 1e-12, atol 1e-10). Stored in-memory data_hash strings differ; this is explicitly recorded rather than described as cryptographically identical inputs. The comparison tool refuses differing snapshots.
- Price sources were not independently checked against the exchange in this turn.

## Adopted strategy: same-date paired net means

These are arithmetic means across valid paired cutoff cases, NOT cumulative or annualized returns. Missing returns are not zeros. Adopted includes the original control when a candidate fails the final gate.

| Horizon | Paired cases | V19.4 | V19.5 | Change (percentage points) |
|---|---:|---:|---:|---:|
| 5 | 98 | -0.2158% | -0.3011% | -0.0853 |
| 20 | 96 | +1.1719% | +2.0495% | +0.8776 |
| 60 | 100 | +1.7600% | +1.7600% | +0.0000 |

The 20-session V19.5 adopted mean (+2.0495%) remains slightly below the unchanged original fixed-control mean (+2.0793%). This is not evidence of an optimum.

## Candidate-only comparison (different, smaller denominators)

Only dates where both versions formed candidates and both outcomes were observable are paired. Do not compare these means with all-100-case means.

| Horizon | Paired candidates | V19.4 | V19.5 | Change (percentage points) |
|---|---:|---:|---:|---:|
| 5 | 82 | -0.1404% | -0.2350% | -0.0946 |
| 20 | 59 | +0.5796% | +1.1758% | +0.5962 |
| 60 | 2 | -8.5036% | -14.7917% | -6.2881 |

The two matched 60-session candidate cases deteriorate. That tiny subset is not a reliable estimate of long-run performance, but it is retained rather than hidden.

## V19.5 versus 0050 (matched within the new report)

This table uses a different denominator from the old/new table: new-model and reference outcomes both observable and price bases comparable.

| Horizon | Pairs | Adopted model | 0050 | Excess (percentage points) |
|---|---:|---:|---:|---:|
| 5 | 97 | -0.3175% | +0.2615% | -0.5789 |
| 20 | 94 | +2.0865% | +3.2379% | -1.1514 |
| 60 | 99 | +1.8211% | +12.3112% | -10.4901 |

## Training success is not investment success

| Horizon | Old fitted | New fitted | Old final-gate passes | New final-gate passes |
|---|---:|---:|---:|---:|
| 5 | 88 | 91 | 5 | 8 |
| 20 | 74 | 70 | 8 | 4 |
| 60 | 3 | 17 | 0 | 0 |

Long-horizon fitted candidates increase from 3 to 17 because past-history allocation and support-local completeness are corrected. Zero long-horizon candidates pass the final gate. More fits do not mean higher returns.

## Latest candidate weights: NOT adopted

As of 2026-10-15:
- 5 sessions: accumulation 100%; one ranking score, not 100% capital allocation.
- 20 sessions: trend, trend_efficiency, liquidity_quality, orderly_pullback at 25% each.
- 60 sessions: trend, volume, trend_efficiency, momentum_persistence at 25% each.
All three latest adopted rankings still use the explicitly identified original control. The CSVs and JSON include failed checks; do not promote a candidate simply because it exists.

## Why the source changed

1. The old coefficient-fitting preparation could delete rows for missing unused columns. TrainingMoments now conditions on the exact selected support. Missing selected factors still exclude observations; no neutral-value imputation.
2. Old scoring folds could use overlapping holding intervals across fold boundaries. New inner folds make scoring intervals disjoint globally and purge training label end dates.
3. Final validation now reserves exactly the configured four blocks, rather than greedily reserving four to six. Development history expands with the horizon, up to max(252, 8*h+train_dates) decision dates within the supplied history. Risk/acceptance thresholds are unchanged, but data allocation IS different.
4. Equal-within-support versus nonnegative-ridge coefficients compete inside chronological development CV. The 160-candidate limit counts support/method combinations, not exhaustive combinations.
5. Depth-specific frontiers allow additions/removals/swaps even when singleton candidates dominate the general leaderboard. Composite/interaction parent conflicts are checked semantically.
6. Candidate missing outcomes cannot filter final validation to a more favorable subset. The reference cohort is fixed before comparing the selected candidate.
7. All selected inputs are now required for both sparse ranking and similar-history statistics. Training dates, failure reasons, and compatibility checks are shared between ranking and allocation UI.
8. Infinite values are missing in field-health reports. An outdated risk setting or model design cannot silently reuse a prior approved report.

The 34-column feature library is unchanged. Original models are retained as explicit controls, not compulsory inputs in each new support. No arbitrary new factor allocation was inserted.

## Separate cash policy

The guarded strategy can hold cash on predefined evidence failures. Its results are exported separately. A cash return of zero is not reclassified as improved stock selection, and missing prices are never replaced with cash after seeing the outcome.

## Verification limits

- This is a development replay using already-examined dates, NOT a fresh blind holdout. Outer holding windows overlap; 100 dates are not 100 independent experiments.
- No optional fundamental or ownership raw data in this input, so no claim that financial factors, institutional flow, margin or large-holder effects were empirically validated.
- Original release/publication/revision ledgers, delisted historical membership and real execution paths remain incomplete.
- No calibrated rise or limit-up probability, optimal-weight proof, current stock recommendation, live orders, or profit guarantee.
- Page verification used real supplied data with a fake Streamlit object. Real browser, mobile, Streamlit Cloud, and live endpoints were not verified.
- See V195_QA_STATUS.md for tests actually run. Synthetic tests validate behavior, not trading profit.

## Reproduce

```bash
python run_v19.py --replay-bundle OLD_REPLAY.zip --as-of 2026-10-15 --dates 100 --seed 1920 --output results_v195 --data data/v19
python compare_v195.py --old OLD_REPLAY.zip --new results_v195/v19_results.json --output paired_comparison
```

The original dataset must be retained with the report. Do not change seeds, stock pools, prices or costs and call that a same-input version comparison.
