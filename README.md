# Hillstrom Email Experiment Analysis

A portfolio project analyzing a published randomized retail email experiment.

## Business Questions

- Did either email campaign increase spending per assigned customer?
- How uncertain are the estimated effects?
- Can targeting improve incremental value under a contact budget?
- What action is justified under explicit margin and contact-cost assumptions?

## Planned Workflow

Python, SQL, BigQuery, randomized experiment analysis,
held-out targeting-policy evaluation, and a Tableau decision dashboard.

## Planned Deliverables

- Reproducible code and SQL queries
- Data provenance, data dictionary, and locked analysis plans
- Campaign effects with uncertainty and multiple-testing correction
- Held-out targeting-policy comparisons
- Cost and margin sensitivity analysis
- Tableau dashboard and one-page decision memo

## Current Status

Initial setup completed. A dataset mirror has been downloaded and verified:
64,000 records, 12 fields, and a matching source-loader checksum.

Experiment and targeting analysis plans have been written before outcome summaries.
No campaign effects, targeting models, or business results have been estimated.

## Project Documents

- [Data provenance](reports/data_provenance.json)
- [Experiment analysis plan](docs/analysis_plan.md)
- [Targeting policy plan](docs/targeting_plan.md)
- [Project progress](docs/progress.md)

This project analyzes a published experiment.

## Environment

Python 3.11.
Install dependencies using: python -m pip install -r requirements.txt
