# Alpha Radar V19.5 | Verification status

## Actually completed this turn

- Final complete source test suite: **294 passed in 129.48 seconds**.
- The new V19.5 regression file contributes 33 tests (parameterized cases included).
- Earlier 291/292-test runs are intermediate subsets, NOT extra independent tests.
- All Python source parsed using Python 3.11 grammar; actual runtime Python 3.13.5.
- 100 supplied historical cutoffs x 3 horizons = 300 cases completed with the new numerical engine.
- Original fixed-control outcomes reproduced: 294 finite returns and 6 missing states; numeric difference zero.
- Actual supplied data: 63,928 daily observations, 92 symbols including 0050.
- Data are user-supplied Yahoo_daily observations, not independently exchange-verified in this turn.
- Earlier and new exported input snapshots match with explicit CSV floating tolerance. Stored frame hashes differ; see comparison JSON for both facts.
- No optional fundamental/ownership raw evidence is in this replay. Their investment effectiveness was NOT tested.
- Numerical source digest was checked against the replay checkpoint manifest.

## What the 33 new tests cover

- Missing UNUSED inputs cannot remove training rows; selected missing inputs are not imputed.
- Cached support moments match a direct selected-input reference calculation.
- Unknown price bases cannot be used to fit coefficients.
- Inner scoring holding intervals are disjoint across folds; fit labels precede scoring.
- Final configured blocks are reserved before candidate scoring and fitting.
- Indirect composite/parent interaction overlap is rejected.
- Equal weights and fitted coefficients are compared within development CV.
- A constructed synthetic signal can pass the final gate; this is NOT a market return claim.
- Changing outer future outcomes cannot alter prior training; insufficient evidence creates no invented weights.
- Constant scores cannot become predictive singleton models.
- UI uses current design/version, displays fit dates and rejects incompatible risk settings.
- Similar-history summaries require ALL selected inputs; numeric infinity is not AVAILABLE.
- Checkpoint fingerprint includes the new numerical source.
- Comparator validates input snapshots instead of trusting inconsistent serializer hashes.

## UI evidence

The three main page functions were exercised with the actual supplied price panel
and the new report using a fake Streamlit implementation. All three emitted zero
error calls. The included tables contained actual factor/weight/result data, not
only empty or synthetic placeholders. The detailed JSON is in the results archive.

This is **NOT browser/Streamlit Cloud/mobile testing**. Streamlit is absent in this
runtime; the installation attempt could not obtain a matching distribution from
the configured package index. Actual deployment dependencies and live endpoints
remain to be checked in their execution environment.

## Numerical outcomes: unfavorable results retained

- Adopted 5-session paired mean: V19.4 -0.2158%, V19.5 -0.3011% (worse).
- Adopted 20-session paired mean: +1.1719% to +2.0495% (better than V19.4,
  but below the original fixed-control +2.0793%).
- Adopted 60-session paired mean: +1.7600% in both versions.
- Long-horizon candidates fitted: 3 to 17; final adopted long-horizon candidates: zero.
- All three latest candidates at 2026-10-15 failed adoption; old control remains explicit.
- All three adopted horizons still trail matched 0050 mean returns.

These are arithmetic means of overlapping development cases, NOT compounded
portfolio returns, actual fills, new blind tests, or proof of optimal weights.

## Design changes and boundaries

The final-validation allocation now uses exactly the configured four blocks rather
than a greedy four-to-six, and the development window grows with the horizon.
This is an explicit methodological change. The improvement, positive-net-return,
benchmark, pool-reference, tail-risk and fill thresholds were NOT weakened.

No new indicators were added; the 34-column candidate library and price/outcome
cost rules are preserved. Optional data is supported only when actually available
and properly timed. No original disclosure/revision ledger, delisted universe,
verified live reversal path or official historical limit-up series is fabricated.

## Package checks

The deliverable is self-contained code, not a price database or a secret/token dump.
Old numerical engines remain for comparisons. Fourteen obsolete documentation files
are retained inside legacy_release_notes.zip; this reduces root upload file count
without removing model code or the source tests.

Final complete archive: **92 root files**, below the 100-file upload limit.
Archive CRC, manifest hashes and extracted Python 3.11 grammar/compilation: PASS.
New tests rerun FROM the extracted archive: **33 passed in 8.60 seconds**.
These 33 are a repeat subset of the 294 unique tests, not additional market trials.
The final actual-data three-page fake-Streamlit check also emitted no errors.
The QA note and manifest were then updated; numerical code did not change.
Final source and extracted numerical digests both match the completed replay.
