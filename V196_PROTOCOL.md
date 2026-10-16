# V19.6 development protocol and change ledger

## Scope
Base: the V19.5 92-file release. Data: the user's previously exposed Yahoo_daily history; no new financial/flow records. This is not a new blind holdout, original disclosure ledger or an exhaustive optimizer. Numeric performance is computed, not promised.

## Investigations retained
The development session tested signed-rank regression, positive regression, shallow gradient boosting with rank targets, shallow gradient boosting with net-excess-return targets, symbol-specific historical-memory scores, and hypothetical initial/trailing stop overlays. Failures are retained in the delivered audit CSVs. They are NOT silently deployed into the main model. Several simple liquidity/turnover scorecards were also explored. Consequently the final scorecard library is a DEVELOPMENT choice informed by these same exposed data, not a pre-registered never-seen test.

## Deployed research algorithm
Default factor_design=tournament_v196. The existing sparse_v195 method remains an explicit alternative. The legacy fixed six-factor prior is an independent comparator; it is not the same as the V19.5 adopted adaptive series.

Eight price-only profiles: legacy fixed prior, turnover percentile alone, turnover plus downside resilience at 25/75,50/50,75/25, and turnover plus 60-session return at the same grid. Optional actual evidence permits three additional predeclared profiles: growth+valuation, trust+breakout, foreign+trust+pattern. No missing optional field becomes a zero/neutral score. The 10 r196_ columns are same-day percentile coordinates, not 10 independent new sources of information. Dollar turnover is NOT market capitalization.

A signal uses information through that day's close. Eligible same-day non-benchmark securities define the cross-section. No future return determines cutoff membership or replaces an unavailable selected stock. Existing universe, volume, price-anomaly, entry-gap, split-coordinate and transaction-cost assumptions remain. To prevent implicit double counting, the external legacy bias-score deduction is not reapplied to the new scorecards. It is retained exactly for the legacy control; this score-definition change is explicit.

Per horizon and cutoff, take up to eight most recent fully matured non-overlapping policy evaluation windows. Require at least four. Compare each profile against the original control on ALL of these fixed dates. Missing price outcomes or incompatible bases invalidate a profile for selection rather than choosing favorable replacement dates. The objective uses mean improvement minus 0.5 times the standard-error-shaped dispersion penalty. This is a regularizer, NOT a valid confidence lower bound after multiple comparisons. At least 60% of selection windows must improve and the penalized difference must reach improvement_floor (default0.002). No optimizer claims an unrestricted optimum; coefficients are the bounded stated grid.

Separate prequential check: on four prior disjoint dates, replay which profile this algorithm would have issued THEN, using only returns matured before each such date. Evaluate that sequence against the original control, 0050 and same-pool equal weight using the existing improvement, leave-one-block, majority, positive-net, tail-risk and fill checks. This evaluates the adaptive policy, not a permanently frozen vector. It is a methodological change from V19.5's nested sparse-support validation, not merely a new factor weight. No threshold was lowered. An accepted prior gate can still lose on the next outcome.

If the policy gate fails, adopted output retains the explicitly labeled original fixed control. The unapproved research choice remains visible. Cash policy is separately reported, never used to replace missing outcomes or fake stock-selection alpha. A rank weight is not a portfolio allocation or a probability.

## Evaluation
Same 100 exposed cutoffs, 5/20/60 sessions, next common session open to T+h close, same price snapshot and costs. Three independent comparisons: V19.5 versus V19.6 adopted output on identical dates; current model versus original fixed control; fixed simple profiles versus 0050 on paired compatible-price observations. Counts can differ. Report arithmetic means, not compounded/annualized returns or actual fills. No date is omitted because it loses. No new test-period tuning after the final 300-case replay.

Final replay disables the optional expensive per-factor removal audit; this is recorded as factor_audit=false. It still computes all seven price-only fixed profile controls and 300 policy cases. Existing detailed factor audit remains available from the command line/UI.

## Limitations
Same-stock-pool survivorship and source selection, corporate-action/dividend completeness, original financial filing timing/revisions, real intraday path, limit-order queues, capacity and live environment remain unverified. There are 91 equities, not the whole Taiwan market. Long-horizon windows across 100 sampled dates overlap. A later historical date not sampled previously is not automatically an independent blind holdout after repeated research.

## Method references (not evidence of profitability)
- https://scikit-learn.org/stable/modules/generated/sklearn.model_selection.TimeSeriesSplit.html
- https://scikit-learn.org/stable/common_pitfalls.html
- https://scikit-learn.org/stable/modules/generated/sklearn.ensemble.HistGradientBoostingRegressor.html
- https://finmind.github.io/tutor/TaiwanMarket/Fundamental/