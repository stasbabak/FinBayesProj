# Finance basics

## Lesson 1: price, return, wealth, and portfolio weights

### Why start here?

Before discussing risk or optimization, we need an exact answer to a simpler question:

> Given some assets and their prices, how does our wealth change?

The equations in this lesson are accounting identities. They do not predict markets and they are not a trading strategy. Later models must obey them.

## 1. Price, quantity, and position value

Let

- \(P_{i,t}\) be the price of one unit of asset \(i\) at time \(t\);
- \(q_{i,t}\) be the number of units we hold;
- \(A_{i,t}\) be the euro value of that position.

Then

\[
A_{i,t}=q_{i,t}P_{i,t}.
\]

The total portfolio value is

\[
V_t=\sum_{i=1}^{N} A_{i,t}
    =\sum_{i=1}^{N}q_{i,t}P_{i,t}.
\]

Fractional quantities are allowed for many assets. If Bitcoin costs EUR 90,000 and we invest EUR 200, then

\[
q_{\mathrm{BTC}}=\frac{200}{90{,}000}
                 \approx 0.002222\ \mathrm{BTC}.
\]

We do not need to buy one whole Bitcoin.

### Price is not return

A price has units, such as EUR per BTC. A return is a dimensionless relative change. An asset priced at EUR 100 is not intrinsically cheaper or more profitable than one priced at EUR 1,000.

## 2. Simple return

If an asset price moves from \(P_{i,t}\) to \(P_{i,t+1}\), its simple return is

\[
r_{i,t+1}
=\frac{P_{i,t+1}-P_{i,t}}{P_{i,t}}
=\frac{P_{i,t+1}}{P_{i,t}}-1.
\]

Equivalently,

\[
P_{i,t+1}=P_{i,t}(1+r_{i,t+1}).
\]

Example: if BTC moves from EUR 90,000 to EUR 94,500,

\[
r_{\mathrm{BTC}}
=\frac{94{,}500-90{,}000}{90{,}000}
=0.05=5\%.
\]

If it moves from EUR 90,000 to EUR 85,500, the return is \(-5\%\).

For an asset that pays cash during the period, such as a dividend \(D_{i,t+1}\), the total return is

\[
r_{i,t+1}^{\mathrm{total}}
=
\frac{P_{i,t+1}-P_{i,t}+D_{i,t+1}}{P_{i,t}}.
\]

Using adjusted price data often incorporates dividends and similar distributions. We must document which price definition a dataset uses.

## 3. Wealth evolution and compounding

If the whole portfolio earns return \(R_{t+1}\), ignoring deposits and withdrawals,

\[
V_{t+1}=V_t(1+R_{t+1}).
\]

Across \(T\) periods,

\[
V_T=V_0\prod_{t=1}^{T}(1+R_t).
\]

Therefore the total compounded return is

\[
R_{0:T}=\frac{V_T}{V_0}-1
       =\prod_{t=1}^{T}(1+R_t)-1.
\]

Returns add only approximately when they are small. Wealth compounds multiplicatively.

For a constant monthly return \(r\), the annual return is

\[
R_{\mathrm{annual}}=(1+r)^{12}-1.
\]

Thus \(5\%\) every month would imply

\[
1.05^{12}-1\approx79.6\%
\]

per year before costs and taxes. This is why EUR 100 per month from EUR 2,000 is an ambitious target even though EUR 100 sounds modest.

### Gains and losses are asymmetric

A \(50\%\) loss followed by a \(50\%\) gain does not restore the initial value:

\[
1{,}000(1-0.5)(1+0.5)=750.
\]

After losing fraction \(L\), the gain required to recover is

\[
G_{\mathrm{recovery}}=\frac{1}{1-L}-1.
\]

After a \(50\%\) loss, the required gain is \(100\%\). This asymmetry is one reason drawdown control matters.

## 4. Log return

The log return is

\[
\ell_{i,t+1}
=\ln\left(\frac{P_{i,t+1}}{P_{i,t}}\right)
=\ln(1+r_{i,t+1}).
\]

Log returns add exactly across time:

\[
\ell_{0:T}=\sum_{t=1}^{T}\ell_t.
\]

The corresponding simple return is

\[
r=e^\ell-1.
\]

For small returns, \(\ell\approx r\), but they are not identical. Simple returns are natural for portfolio accounting over one period; log returns are often convenient for time-series analysis. We will keep the distinction explicit.

## 5. Portfolio weights

The weight of asset \(i\) at time \(t\) is its fraction of total wealth:

\[
w_{i,t}=\frac{A_{i,t}}{V_t}
       =\frac{q_{i,t}P_{i,t}}{V_t}.
\]

For a fully invested long-only portfolio,

\[
w_{i,t}\ge 0,
\qquad
\sum_{i=1}^{N}w_{i,t}=1.
\]

These weights are our principal decision variables. The future asset returns are not decision variables: we observe or model them, but cannot choose them.

If holdings remain unchanged during one period and we ignore costs, the portfolio's simple return is

\[
R_{p,t+1}=\sum_{i=1}^{N}w_{i,t}r_{i,t+1}.
\]

Notice the timing: weights are known at the beginning of the period; returns are realized at its end. Using end-of-period information to choose beginning-of-period weights would introduce look-ahead bias.

## 6. A EUR 2,000 example

Suppose the initial allocation is:

| Asset | Amount | Initial weight |
|---|---:|---:|
| EUR cash | EUR 1,000 | \(0.50\) |
| Global equities | EUR 600 | \(0.30\) |
| Gold | EUR 200 | \(0.10\) |
| BTC | EUR 200 | \(0.10\) |
| **Total** | **EUR 2,000** | **\(1.00\)** |

Assume hypothetical one-month returns:

| Asset | Return |
|---|---:|
| EUR cash | \(0\%\) |
| Global equities | \(+2\%\) |
| Gold | \(-1\%\) |
| BTC | \(+12\%\) |

Then

\[
\begin{aligned}
R_p
&=0.50(0)+0.30(0.02)+0.10(-0.01)+0.10(0.12)\\
&=0.017=1.7\%.
\end{aligned}
\]

The new value before costs is

\[
V_1=2{,}000(1.017)=\mathrm{EUR}\ 2{,}034.
\]

The contributions to profit are EUR 0 from cash, EUR 12 from equities, EUR \(-2\) from gold, and EUR 24 from BTC.

This example also shows an important distinction:

- BTC returned \(12\%\);
- because BTC was only \(10\%\) of the portfolio, it contributed \(1.2\) percentage points to the portfolio return.

## 7. Costs, deposits, and withdrawals

Let \(C_{t+1}\) be trading costs and other charges paid during the period, and let \(F_{t+1}\) be external cash flow into the portfolio. We define \(F>0\) for a deposit and \(F<0\) for a withdrawal. Then

\[
V_{t+1}
=
V_t(1+R_{p,t+1})
-C_{t+1}
+F_{t+1}.
\]

For performance measurement, deposits must not be mistaken for investment profit. A basic net return excluding external cash flow is

\[
R_{t+1}^{\mathrm{net}}
=
\frac{V_{t+1}-V_t-F_{t+1}}{V_t}.
\]

Later we will model transaction fees, bid/ask spread, slippage, taxes, and interest on cash more carefully.

## 8. What this gives our optimization problem

We can now separate four kinds of quantity:

1. **State/observations:** prices \(P_{i,t}\), past returns, volatility, rates, and other data available at time \(t\).
2. **Decision variables:** portfolio weights \(\mathbf w_t\).
3. **Constraints:** capital, \(w_i\ge0\), \(\sum_i w_i=1\), accessible assets, and later risk limits.
4. **Outcomes:** future portfolio return, wealth, and drawdown.

Schematically,

\[
\text{information available at }t
\longrightarrow
\mathbf w_t
\longrightarrow
\text{future asset returns}
\longrightarrow
V_{t+1}.
\]

The unknown future returns sit between our decision and its outcome. That is what makes the problem stochastic.

## 9. Checks for understanding

### Check 1

An asset rises from EUR 80 to EUR 92. What is its simple return?

\[
r=\frac{92-80}{80}=0.15=15\%.
\]

### Check 2

A portfolio loses \(20\%\). What gain restores it?

\[
G_{\mathrm{recovery}}
=\frac{1}{1-0.20}-1
=0.25=25\%.
\]

### Check 3

A portfolio holds \(60\%\) cash returning \(0\%\) and \(40\%\) BTC returning \(-10\%\). What is the portfolio return?

\[
R_p=0.60(0)+0.40(-0.10)=-0.04=-4\%.
\]

## 10. Assumptions made in this lesson

The simple equations above temporarily assume:

- all assets use the same valuation currency, EUR;
- prices and cash flows are observed at consistent times;
- assets are divisible;
- no leverage or short selling;
- no taxes, spread, slippage, or trading fees unless written explicitly;
- no missing or stale prices;
- weights are chosen before the subsequent returns are known.

These assumptions are scaffolding. We will relax them deliberately rather than silently.

## Next lesson

The next step is risk:

- why average return alone is insufficient;
- variance and volatility;
- covariance and correlation;
- drawdown;
- why diversification depends on co-movement rather than the number of assets.
