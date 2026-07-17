# STB-0 — Successful Translation Benchmark

## Status

**PRELIMINARY SUPPORT.** Executed cross-rater construct-validity pilot; not an automatic translation metric or full RC validation.

## Design

- WMT20 professional MQM annotations: en-de, zh-en.
- 34,171 unique system–segment translations; 110,640 leave-one-rater-out examples; 53 documents.
- Held-out rater supplies success outcome. Other raters supply two coordinates.
- S = Accuracy + Non-translation penalty. B = all target-regime boundary/realization penalties (Terminology, Style, Locale, Fluency, other).
- Primary success: held-out weighted MQM penalty = 0. Secondary usable success: penalty <= 1.

## Results

1. S/B Spearman correlation: 0.211.
2. Boundary-only cases S=0,B>0: 19.4%.
3. Held-out strict success: S=0,B=0 = 64.4%; S=0,B>0 = 34.2%.
4. False-success rate: semantic-only = 52.7%; typed 2D = 35.6%; reduction = 17.0 points, document-bootstrap 95% CI [15.5, 18.5].
5. Strict-success grouped OOF ROC-AUC: semantic-only 0.730, collapsed scalar 0.774, typed 2D 0.773.

## Rule-based admission

| Rule | Coverage | Precision | Recall | False-success |
|---|---:|---:|---:|---:|
| S=0 | 34.4% | 47.3% | 60.0% | 52.7% |
| S=0 and B=0 | 15.0% | 64.4% | 35.5% | 35.6% |

McNemar exact p=0.

## Model comparison

| outcome               | model                |   roc_auc |   average_precision |    brier |   spearman |      mae |
|:----------------------|:---------------------|----------:|--------------------:|---------:|-----------:|---------:|
| strict_success        | semantic_only_1d     |    0.7299 |              0.4376 |   0.1739 |     0.3545 | nan      |
| strict_success        | collapsed_total_1d   |    0.7736 |              0.5344 |   0.1652 |     0.4216 | nan      |
| strict_success        | typed_2d             |    0.7725 |              0.5339 |   0.1650 |     0.4199 | nan      |
| strict_success        | typed_2d_interaction |    0.7713 |              0.5332 |   0.1645 |     0.4180 | nan      |
| usable_success        | semantic_only_1d     |    0.7458 |              0.6872 |   0.2039 |     0.4260 | nan      |
| usable_success        | collapsed_total_1d   |    0.7871 |              0.7552 |   0.1915 |     0.4973 | nan      |
| usable_success        | typed_2d             |    0.7866 |              0.7556 |   0.1914 |     0.4965 | nan      |
| usable_success        | typed_2d_interaction |    0.7855 |              0.7552 |   0.1907 |     0.4945 | nan      |
| heldout_total_penalty | semantic_only_1d     |  nan      |            nan      | nan      |     0.5097 |   2.6821 |
| heldout_total_penalty | collapsed_total_1d   |  nan      |            nan      | nan      |     0.5811 |   2.5243 |
| heldout_total_penalty | typed_2d             |  nan      |            nan      | nan      |     0.5812 |   2.5244 |
| heldout_total_penalty | typed_2d_interaction |  nan      |            nan      | nan      |     0.5810 |   2.5188 |

## Interpretation boundary

This run can establish that professional human translation judgments contain two non-identical coordinates and that a two-coordinate admission rule is safer than semantic-only admission. It does not establish automatic computation of B, calibrated POINT/RE-DERIVE/BORROW/WEAK/REFUSE thresholds, function-relative fans, PackSpec verdict preservation, or full Regime Convergence.

If typed 2D merely matches the collapsed scalar, its demonstrated advantage is auditability and typed remediation rather than predictive accuracy.
