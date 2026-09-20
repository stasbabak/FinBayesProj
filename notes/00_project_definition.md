# Project definition

## Research question

Can an adaptive portfolio produce credible evidence of positive expected return, after realistic costs, while keeping the risk of severe loss within an explicitly chosen limit?

The target of EUR 100 per month is an outcome to evaluate, not a return that the model must force every month.

## Provisional scope

These values record our starting point and must be reviewed before modelling or trading.

- Initial capital: EUR 1,000–2,000
- Initial asset universe: EUR cash, short-duration bonds, global equities, gold, and BTC
- Position direction: long-only
- Leverage and borrowed money: excluded
- Live trading: excluded until research and paper-trading gates are passed

## Mathematical objects

The decision vector at time \(t\) is

$$
\mathbf w_t =
(w_{\mathrm{cash}}, w_{\mathrm{bonds}}, w_{\mathrm{equities}},
w_{\mathrm{gold}}, w_{\mathrm{BTC}}),
$$

subject initially to

$$
\sum_i w_{i,t}=1,\qquad w_{i,t}\geq 0.
$$

The observed state \(\mathbf X_t\) may include prices, returns, volatility, interest rates, EUR/USD, oil, market stress, and measured geopolitical risk.

A candidate objective is to maximize expected return subject to explicit drawdown and severe-loss constraints. We will select the exact objective only after studying the alternatives and their consequences.

## Decisions still required

- evaluation horizon;
- maximum tolerable temporary drawdown;
- maximum tolerable permanent loss;
- probability allowed for breaching either limit;
- whether profits are reinvested or withdrawn;
- trading frequency and minimum rebalance size;
- exact instruments that make each asset class accessible;
- taxes, fees, spreads, and slippage assumptions;
- criteria for passing from backtesting to paper trading and then to small live positions.

## Scientific workflow

1. Define the objective, constraints, and success criteria.
2. Establish cash and buy-and-hold baselines.
3. Derive each risk and portfolio quantity before implementing it.
4. Separate training, validation, and untouched test periods.
5. Include costs and test sensitivity to assumptions.
6. Reject results that do not survive out-of-sample and robustness checks.
