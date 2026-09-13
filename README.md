# FinBayesProj

A research and learning project for studying adaptive portfolio allocation under changing market, macroeconomic, and geopolitical regimes.

The project has two parallel tracks:

1. derive and understand the financial mathematics;
2. implement and test each idea against simple baselines.

The initial investable universe is EUR cash, short-duration bonds, global equities, gold, and Bitcoin. The initial capital constraint is EUR 1,000–2,000. The desired EUR 100 monthly return is a hypothesis to test, not an assumed or guaranteed outcome.

No live trading is planned until the project has a precise objective, realistic costs, risk limits, and credible out-of-sample evidence.

## Structure

- `notes/` — project definition, finance foundations, mathematical derivations, and model assumptions
- `data/` — local raw and processed data (large or sensitive files are ignored)
- `notebooks/` — exploratory and reproducible research
- `src/` — reusable data, return, risk, portfolio, and regime-model code
- `tests/` — focused checks for the reusable code
- `results/` — generated tables, figures, and experiment summaries

Start with [`notes/00_project_definition.md`](notes/00_project_definition.md).

## Safety

Never commit passwords, API keys, authentication tokens, wallet seed phrases, or private keys. Keep credentials in environment variables or a local `.env` file, which is ignored by Git.
