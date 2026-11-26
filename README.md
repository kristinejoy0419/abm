# ABM Account Scoring and Activation

A single-page dashboard for account-based growth. It scores target accounts, tiers them, shows which play to run at each engagement level, and tracks buying committee coverage and pipeline.

**Status: illustrative mock.** All companies, people and numbers are fictional sample data.

## What's in it

- **Exec summary tab:** headline numbers, how the score works (adjustable weights), the activation plan by tier and engagement level, pipeline and win rate by tier, typical path to a win, new logos, and pipeline coverage by cohort and by rep.
- **Working view tab:** "Act this week" actions, engagement tracker with automated triggers, buying committee coverage, competitor evaluation alerts, and the account list with account detail.

## Scoring model

`Score = Fit × w1 + Product usage × w2 + Intent × w3` (weights add up to 100%).

- **Fit (account traits only):** AI maturity (engineering hiring rate, AI and dev tools in use, teams using them) plus firmographics (eng headcount, code platform, industry, region).
- **Product usage (PQA):** active seats, PRs reviewed, repos connected, teams on the product, engineers using it on open source or personal projects.
- **Intent and engagement:** intent surge (6sense or Demandbase), G2 visits, pricing and docs visits, community, events and ads.

Stages: **active evaluator** (score 62+ with strong usage or intent), **hidden evaluator** (strong intent, no usage), **warming**, **not engaged**.

Tiers by fit rank: Tier 1 (1:1, ~100), Tier 2 (1:few, ~400), Tier 3 (1:many, ~3,000), plus Tier 0 evergreen growth for the whole market.

## Run it

Open `index.html` in a browser. No build step.

## Load your own data

Use **Upload your data (CSV)** in the header. The file is read in the browser only and is never sent anywhere. Column format: [`data/abm-account-template.csv`](data/abm-account-template.csv).

## Making it live (next step)

1. Connectors (Fivetran or Airbyte) land Salesforce, intent, G2 and marketing automation data in a warehouse.
2. A scheduled model (dbt) builds one account table with the template's columns plus scores, tiers and stages.
3. A small API serves that table to this page behind company sign-in.
4. Reverse ETL (Hightouch or Census) pushes scores and tiers back to Salesforce, ad audiences and sequences.
