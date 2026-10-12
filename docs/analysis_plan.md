# Experiment Analysis Plan

## Version and Status

Version: 1.0.
Written before inspecting outcome summaries in this project.
This is a retrospective analysis plan for a published experiment,
not prospective registration of a new experiment.

## Population and Assignment

Analyze all supplied randomized records by assigned campaign.
Retain non-buyers and zero-spend customers.
Actual email delivery and opening information are unavailable.

Campaign labels:
- Mens E-Mail
- Womens E-Mail
- No E-Mail

Merchandise purchase flags and campaign names do not identify customer gender.

## Primary Outcome

Arithmetic mean of two-week spend per randomized customer, including zeros.
Use dataset monetary units until a specific currency is verified.

## Primary Comparison Family

1. Mens E-Mail minus No E-Mail.
2. Womens E-Mail minus No E-Mail.
3. Mens E-Mail minus Womens E-Mail.

Use two-sided Welch tests and Holm adjustment across these three comparisons.
Family significance level: 0.05.
Report mean differences and nominal 95% Welch confidence intervals.
Nominal intervals are not multiplicity-adjusted intervals.

Check spending-tail sensitivity using within-arm bootstrap:
5,000 replicates, seed 20261011, bounded memory allocation.
Do not remove large purchases to obtain favorable results.

## Secondary Outcomes

Conversion rate and visit rate, using all assigned customers as denominators.
Compare each email with control for each outcome: four comparisons.
Use a separate Holm family and label secondary findings exploratory.
Report absolute percentage-point differences and nominal 95% intervals.
Use Newcombe intervals based on Wilson score intervals for risk differences.

Do not restrict causal comparisons to buyers or visitors.
Revenue per buyer may be descriptive, but is not the primary estimand.

## Data and Assignment Diagnostics

Check schema, missingness, finite values, binary flags, and outcome consistency.
Report assignment counts and an approximately 1:1:1 sample-ratio diagnostic.
Examine pretreatment balance using distributions and standardized differences.
Do not deduplicate profiles without evidence of duplicate customer records.

If outcomes are missing or inconsistent, document the issue and amend the
handling plan before effect estimation. Do not silently drop or rewrite them.

## Exploratory Segments

Use purchase recency groups of 1-3, 4-6, and 7-12 months only if source
definitions and observed ranges support them.
Otherwise record revised boundaries before subgroup outcome summaries.

Report counts, effects, uncertainty, and declared multiplicity handling.
Use treatment-by-segment interactions to assess heterogeneity.
Significance in one subgroup and nonsignificance in another is not
evidence that subgroup effects differ.

## Economic Scenarios

Assumed contribution margins: 0.3, 0.5, and 0.7.
Assumed contact costs: 0.01, 0.05, and 0.10 dataset monetary units.

For broad email assignment:
incremental contribution per customer =
assumed margin * incremental spend - assumed contact cost.

Show effect uncertainty and hypothetical rollout assumptions.
Do not describe estimated revenue or contribution as realized business impact.

## Outcome Access and Targeting

A separate targeting plan will define train, validation, and test partitions.
Freeze and evaluate targeting policies before full-population outcome summaries.
Then complete the original experiment analysis using all randomized records.
Clearly distinguish full-population campaign effects from held-out policy value.

## Interpretation

A nonsignificant result does not establish no effect or equivalence.
A larger point estimate does not establish superiority without a direct comparison.
Exploratory segments are not confirmed targeting rules.

## Amendments

Record changes, reasons, and outcome exposure before implementing amendments.
No amendments at version 1.0.
