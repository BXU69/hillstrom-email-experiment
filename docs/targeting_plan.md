# Targeting Policy Analysis Plan

## Version and Status

Version: 1.0.
Written before outcome summaries or model fitting in this project.
No targeting advantage or positive business result is assumed.

## Business Constraint

Contact at most 10,000 customers in the verified study population.
Budget fraction = 10,000 / verified population count.
Apply this same fraction to validation and test populations.
Broad-send policies are unconstrained reference policies.

## Stable Records and Splits

Create row_id from immutable CSV row order, starting at zero.
Tie row IDs to the recorded source SHA-256.
Do not treat row_id as a predictor or a verified customer identifier.

Split approximately 60% train, 20% validation, and 20% test.
Stratify only by randomized treatment arm.
Use random seed 20261011 and record the exact splitting procedure.
Do not stratify by outcomes.

Store customer-level assignments locally.
Commit only split rules, checksum, seed, and partition counts.

## Outcome Access

Train outcomes are available for fitting.
Validation outcomes are available for configuration selection.
Test outcomes remain excluded from development data-loading paths.

Test pretreatment features may be used to apply frozen policies.
Do not inspect test outcome summaries, full-population outcome summaries,
or full-population subgroup results during development.

Complete schema and outcome-validity checks without displaying outcome values
or outcome distributions. Document any prior outcome exposure.

## Features

Use only verified pretreatment attributes:
recency, history, history_segment, mens, womens,
newbie, channel, and zip_code.

Exclude visit, conversion, spend, row_id, and assignment as customer predictors.
Fit preprocessing using training data only.
Handle unseen categorical values explicitly.

## Bounded Modeling Approach

Use a three-arm T-learner: one Ridge regression per assignment arm.
Predict two-week spend under no email, men's email, and women's email.
Use the same preprocessing and model family across arms.

Candidate Ridge alpha values: 1, 10, and 100.
Use validation data to select one shared alpha.
Selection criterion: estimated incremental contribution of the uplift policy
at margin 0.5 and contact cost 0.05, under the contact cap.
Break ties by choosing the larger alpha.

Negative predicted spend will be clipped to zero for policy construction.
Record this rule; evaluate policies using actual unmodified outcomes.

After selection, refit preprocessing and models on train plus validation.
Freeze configuration, fitted models, and policy rules before test evaluation.

## Required Policies

1. No email.
2. Send men's email to everyone.
3. Send women's email to everyone.
4. Random targeting under the contact cap.
5. Response-based targeting under the contact cap.
6. Incremental-effect targeting under the contact cap.

For random targeting, choose the email arm on validation data using
estimated mean incremental contribution; break ties in favor of men's email.
Use seed 20261011 to select recipients independently of outcomes.

For response targeting, rank customers by the larger predicted spend
under the two email arms and send the corresponding email.
Contact up to the cap.

For incremental-effect targeting, choose the email with the larger predicted
contribution relative to no email:
margin * (predicted email spend - predicted no-email spend) - contact cost.
Contact customers with positive predicted contribution, up to the cap.

Break campaign ties in favor of men's email.
Break customer ranking ties by row_id.

## Final Evaluation

Evaluate frozen policies on randomized test records.
Use inverse-probability-weighted policy values with assignment probability
approximately 1/3 per arm, based on the published design.

If exact allocation probabilities are unavailable, disclose the approximation
and report a sensitivity analysis using observed test-arm proportions.

Estimate policy incremental spend relative to the no-email policy.
Apply margin and contact-cost assumptions to estimate contribution.
Contact cost applies only to customers assigned an email by the policy.

Do not evaluate only customers whose observed assignment matches the policy
without inverse-probability weighting.
Do not use predicted scores as evidence of realized policy value.

## Uncertainty and Comparisons

Primary policy comparisons at margin 0.5 and contact cost 0.05:
- Incremental-effect targeting minus response-based targeting.
- Incremental-effect targeting minus random targeting.

Use 5,000 paired within-arm bootstrap replicates, seed 20261012.
Hold fitted models and customer policy assignments fixed.
Report nominal 95% bootstrap percentile intervals.

For the two primary comparisons, use approximate two-sided normal tests
based on bootstrap standard errors, with Holm correction at family alpha 0.05.
Label this inference approximate and conditional on the fitted policies.
Do not claim it captures all model-training uncertainty.

Other policy comparisons and economic scenarios are descriptive sensitivity
analyses, not additional confirmed wins.

## Economic Sensitivity

Margins: 0.3, 0.5, and 0.7.
Contact costs: 0.01, 0.05, and 0.10 dataset monetary units.
Freeze scenario rules before opening test outcomes.

Keep primary policy assignments fixed for economic sensitivity.
Do not optimize new policies after inspecting test results.
Distinguish test-population value from hypothetical study-wide extrapolation.

## Interpretation and Amendments

Report all planned policies, including unfavorable or inconclusive results.
Do not retune after opening test outcomes.
Later policy changes are exploratory and need new confirmation data.
Unchanged reproducibility reruns are allowed and logged.

Individual predicted effects are not observed individual causal effects.
No amendments at version 1.0.
