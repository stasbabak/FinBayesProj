# Finance basics

## Lesson 1: price, return, wealth, and portfolio weights

### Why start here?

Before discussing risk or optimization, we need an exact answer to a simpler question:

> Given some assets and their prices, how does our wealth change?

The equations in this lesson are accounting identities. They do not predict markets and they are not a trading strategy. Later models must obey them.

## 1. Price, quantity, and position value

Let

- $P_{i,t}$ be the price of one unit of asset $i$ at time $t$;
- $q_{i,t}$ be the number of units we hold;
- $A_{i,t}$ be the euro value of that position.

Then

$$
A_{i,t}=q_{i,t}P_{i,t}.
$$

The total portfolio value is

$$
V_t=\sum_{i=1}^{N} A_{i,t}
    =\sum_{i=1}^{N}q_{i,t}P_{i,t}.
$$

Fractional quantities are allowed for many assets. If Bitcoin costs EUR 90,000 and we invest EUR 200, then

$$
q_{\mathrm{BTC}}=\frac{200}{90{,}000}  \approx 0.002222\ \mathrm{BTC}.
$$

We do not need to buy one whole Bitcoin.

### Price is not return

A price has units, such as EUR per BTC. A return is a dimensionless relative change. An asset priced at EUR 100 is not intrinsically cheaper or more profitable than one priced at EUR 1,000.

## 2. Simple return

If an asset price moves from $P_{i,t}$ to $P_{i,t+1}$, its simple return is

$$
r_{i,t+1}
=\frac{P_{i,t+1}-P_{i,t}}{P_{i,t}}
=\frac{P_{i,t+1}}{P_{i,t}}-1.
$$

Equivalently,

$$
P_{i,t+1}=P_{i,t}(1+r_{i,t+1}).
$$

Example: if BTC moves from EUR 90,000 to EUR 94,500,

$$
r_{\mathrm{BTC}}
=\frac{94{,}500-90{,}000}{90{,}000}
=0.05=5\%.
$$

If it moves from EUR 90,000 to EUR 85,500, the return is $-5\%$.

For an asset that pays cash during the period, such as a dividend $D_{i,t+1}$, the total return is

$$
r_{i,t+1}^{\mathrm{total}} = \frac{P_{i,t+1}-P_{i,t}+D_{i,t+1}}{P_{i,t}}.
$$

Using adjusted price data often incorporates dividends and similar distributions. We must document which price definition a dataset uses.

## 3. Wealth evolution and compounding

If the whole portfolio earns return $R_{t+1}$, ignoring deposits and withdrawals,

$$
V_{t+1}=V_t(1+R_{t+1}).
$$

Across $T$ periods,

$$
V_T=V_0\prod_{t=1}^{T}(1+R_t).
$$

Therefore the total compounded return is

$$
R_{0:T}=\frac{V_T}{V_0}-1  =\prod_{t=1}^{T}(1+R_t)-1.
$$

Returns add only approximately when they are small. Wealth compounds multiplicatively.

For a constant monthly return $r$, the annual return is

$$
R_{\mathrm{annual}}=(1+r)^{12}-1.
$$

Thus $5$% every month would imply

$$
1.05^{12}-1\approx79.6\%
$$

$\approx 80$% per year before costs and taxes. This is why EUR 100 per month from EUR 2,000 is an ambitious target even though EUR 100 sounds modest.

### Gains and losses are asymmetric

A $50$% loss followed by a $50$% gain does not restore the initial value:

$$
1{,}000(1-0.5)(1+0.5)=750.
$$

After losing fraction $L$, the gain required to recover is

$$
G_{\mathrm{recovery}}=\frac{1}{1-L}-1.
$$

After a $50$% loss, the required gain is $100$%. This asymmetry is one reason drawdown control matters.

## 4. Log return

The log return is

$$
\ell_{i,t+1}
=\ln\left(\frac{P_{i,t+1}}{P_{i,t}}\right)
=\ln(1+r_{i,t+1}).
$$

Log returns add exactly across time:

$$
\ell_{0:T}=\sum_{t=1}^{T}\ell_t.
$$

The corresponding simple return is

$$
r=e^\ell-1.
$$

For small returns, $\ell\approx r$, but they are not identical. Simple returns are natural for portfolio accounting over one period; log returns are often convenient for time-series analysis. We will keep the distinction explicit.

## 5. Portfolio weights

The weight of asset $i$ at time $t$ is its fraction of total wealth:

$$
w_{i,t}=\frac{A_{i,t}}{V_t}
       =\frac{q_{i,t}P_{i,t}}{V_t}.
$$

For a fully invested long-only portfolio,

$$
w_{i,t}\ge 0,
\qquad
\sum_{i=1}^{N}w_{i,t}=1.
$$

These weights are our principal decision variables. The future asset returns are not decision variables: we observe or model them, but cannot choose them.

If holdings remain unchanged during one period and we ignore costs, the portfolio's simple return is

$$
R_{p,t+1}=\sum_{i=1}^{N}w_{i,t}r_{i,t+1}.
$$

Notice the timing: weights are known at the beginning of the period; returns are realized at its end. Using end-of-period information to choose beginning-of-period weights would introduce look-ahead bias.

## 6. A EUR 2,000 example

Suppose the initial allocation is:

| Asset | Amount | Initial weight |
|---|---:|---:|
| EUR cash | EUR 1,000 | $0.50$ |
| Global equities | EUR 600 | $0.30$ |
| Gold | EUR 200 | $0.10$ |
| BTC | EUR 200 | $0.10$ |
| **Total** | **EUR 2,000** | **$1.00$** |

Assume hypothetical one-month returns:

| Asset | Return |
|---|---:|
| EUR cash | $0\%$ |
| Global equities | $+2\%$ |
| Gold | $-1\%$ |
| BTC | $+12\%$ |

Then

$$
\begin{aligned}
R_p
&=0.50(0)+0.30(0.02)+0.10(-0.01)+0.10(0.12)\\
&=0.017=1.7\%.
\end{aligned}
$$

The new value before costs is

$$
V_1=2{,}000(1.017)=\mathrm{EUR}\ 2{,}034.
$$

The contributions to profit are EUR 0 from cash, EUR 12 from equities, EUR $-2$ from gold, and EUR 24 from BTC.

This example also shows an important distinction:

- BTC returned $12\%$;
- because BTC was only $10\%$ of the portfolio, it contributed $1.2$ percentage points to the portfolio return.

## 7. Costs, deposits, and withdrawals

Let $C_{t+1}$ be trading costs and other charges paid during the period, and let $F_{t+1}$ be external cash flow into the portfolio. We define $F>0$ for a deposit and $F<0$ for a withdrawal. Then

$$
V_{t+1} = V_t(1+R_{p,t+1}) - C_{t+1} + F_{t+1}.
$$

For performance measurement, deposits must not be mistaken for investment profit. A basic net return excluding external cash flow is

$$
R_{t+1}^{\mathrm{net}} = \frac{V_{t+1}-V_t-F_{t+1}}{V_t}.
$$

Later we will model transaction fees, bid/ask spread, slippage, taxes, and interest on cash more carefully.

## 8. What this gives our optimization problem

We can now separate four kinds of quantity:

1. **State/observations:** prices $P_{i,t}$, past returns, volatility, rates, and other data available at time $t$.
2. **Decision variables:** portfolio weights $\mathbf w_t$.
3. **Constraints:** capital, $w_i\ge0$, $\sum_i w_i=1$, accessible assets, and later risk limits.
4. **Outcomes:** future portfolio return, wealth, and drawdown.

Schematically,

$$
\text{information available at }t
\longrightarrow
\mathbf w_t
\longrightarrow
\text{future asset returns}
\longrightarrow
V_{t+1}.
$$

The unknown future returns sit between our decision and its outcome. That is what makes the problem stochastic.

## 9. Checks for understanding

### Check 1

An asset rises from EUR 80 to EUR 92. What is its simple return?

$$
r=\frac{92-80}{80}=0.15=15\%.
$$

### Check 2

A portfolio loses $20\%$. What gain restores it?

$$
G_{\mathrm{recovery}} =\frac{1}{1-0.20}-1 =0.25=25\%.
$$

### Check 3

A portfolio holds $60\%$ cash returning $0\%$ and $40\%$ BTC returning $-10\%$. What is the portfolio return?

$$
R_p=0.60(0)+0.40(-0.10)=-0.04=-4\%.
$$

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


---

## Lesson 2: expected return, uncertainty, and portfolio risk

### 1. From an observed return to an uncertain return

Recall the definition of the return of the whole portfolio, with no external deposits or withdrawals:

$$
R_p=\frac{V_{t+1}-V_t}{V_t}.
$$

For unchanged holdings and no costs, this becomes

$$
R_p=\sum_i w_i r_i.
$$

We suppress time subscripts for this lesson. The weights are fixed at the beginning of one chosen period; the asset returns refer to that same period. Returns include distributions such as dividends, where applicable.

After the period, $r_i$ and $R_p$ are observed numbers. Before the period, we describe them as random variables with a joint probability distribution. That distribution is a model of our uncertainty.

This distinction should feel familiar from statistical inference: an observation, a model parameter, and an estimate of that parameter are different objects.

All numerical examples below are hypothetical, not forecasts or proposed allocations.

### 2. Expected return: averaging over possible outcomes

Suppose a return $r$ has possible outcomes $r_s$ with probabilities $p_s$. Its expectation is

$$
\mu=\mathbb E[r]=\sum_s p_s r_s,
\qquad \sum_s p_s=1.
$$

For a continuous distribution with density $f(r)$, the sum becomes an integral:

$$
\mu=\int r f(r)\,dr.
$$

Expectation is a probability-weighted average. It need not equal any actual outcome.

Consider two hypothetical one-month investments:

| Investment | Outcome 1, probability 1/2 | Outcome 2, probability 1/2 | Expected return |
|---|---:|---:|---:|
| A | 0% | 2% | 1% |
| B | -9% | 11% | 1% |

Both have the same expected return. Their possible losses are very different. With EUR 2,000 invested entirely in either one, expected ending wealth is EUR 2,020, but the possible ending values are:

- A: EUR 2,000 or EUR 2,040;
- B: EUR 1,820 or EUR 2,220.

Expected wealth is not a promised outcome. Maximizing it alone does not express how much uncertainty or loss we are willing to accept.

### 3. Variance and volatility

To measure dispersion around the expected return, start with the deviation $r-\mu$. Its expectation is zero, so simply averaging deviations cannot measure dispersion.

Instead, square them:

$$
\sigma^2=\operatorname{Var}(r)
=\mathbb E[(r-\mu)^2].
$$

Variance is nonnegative. Squaring gives larger deviations more weight and treats deviations above and below the mean symmetrically.

The standard deviation of returns is called volatility:

$$
\sigma=\sqrt{\operatorname{Var}(r)}.
$$

For investment A, the deviations from its mean $0.01$ are $-0.01$ and $+0.01$:

$$
\sigma_A^2
=\tfrac12(-0.01)^2+\tfrac12(0.01)^2
=0.0001,
\qquad \sigma_A=0.01=1\%.
$$

For B, they are $-0.10$ and $+0.10$:

$$
\sigma_B^2=0.01,
\qquad \sigma_B=0.10=10\%.
$$

Here “10% volatility” means a standard deviation of 10 percentage points in the one-month return. We calculate using decimal returns throughout.

For fixed starting wealth and no external flows,

$$
V_{t+1}=V_t(1+R_p)
\quad\Longrightarrow\quad
\operatorname{SD}(V_{t+1})=V_t\sigma_p.
$$

A portfolio volatility of 10% therefore corresponds to EUR 200 standard deviation in ending wealth when $V_t=2000$.

This is not a maximum loss, nor does it by itself specify a probability of loss. Probabilities require the return distribution, not just its standard deviation. We have not assumed Gaussian returns.

### 4. Expected portfolio return

Linearity of expectation gives

$$
\mu_p=\mathbb E[R_p]
=\mathbb E\!\left[\sum_i w_i r_i\right]
=\sum_i w_i\mu_i
=\mathbf w^\mathsf T\boldsymbol\mu.
$$

This does not require independent asset returns.

We treat the weights as fixed for this one-period calculation. Later, when weights depend on market information, the corresponding expectations and covariances can be conditioned on that information.

Portfolio variance takes more work because it depends on how asset returns move together.

### 5. Covariance: do deviations occur together?

For assets $i$ and $j$, define

$$
\Sigma_{ij}
=\operatorname{Cov}(r_i,r_j)
=\mathbb E[(r_i-\mu_i)(r_j-\mu_j)].
$$

If both tend to be above their respective means together, and below them together, the products tend to be positive. If one tends to be above its mean while the other is below, they tend to be negative.

Thus covariance measures co-movement of deviations from the means. It does not mean that prices always move in the same direction.

For $i=j$,

$$
\Sigma_{ii}=\sigma_i^2.
$$

The covariance matrix collects these quantities:

$$
\boldsymbol\Sigma=
\begin{pmatrix}
\sigma_1^2 & \operatorname{Cov}(r_1,r_2) & \cdots\\
\operatorname{Cov}(r_2,r_1) & \sigma_2^2 & \cdots\\
\vdots & \vdots & \ddots
\end{pmatrix}.
$$

### 6. Correlation: normalized covariance

When both standard deviations are nonzero, correlation is

$$
\rho_{ij}
=\frac{\Sigma_{ij}}{\sigma_i\sigma_j},
\qquad -1\le \rho_{ij}\le 1.
$$

Equivalently,

$$
\Sigma_{ij}=\rho_{ij}\sigma_i\sigma_j.
$$

- $\rho=1$: perfect positive linear relationship between returns.
- $\rho=0$: zero linear correlation; other dependence can remain.
- $\rho=-1$: perfect negative linear relationship.

Zero correlation does not generally imply independence. Correlation also does not establish causation.

If an idealized cash asset has a deterministic return, its volatility and covariance with risky returns are zero. Its correlation is undefined because the denominator is zero; we do not need a correlation value to include it in the covariance matrix.

### 7. Deriving portfolio variance

Subtract the expected portfolio return:

$$
R_p-\mu_p=\sum_i w_i(r_i-\mu_i).
$$

Square and take the expectation:

$$
\begin{aligned}
\sigma_p^2
&=\mathbb E\!\left[
\left(\sum_i w_i(r_i-\mu_i)\right)
\left(\sum_j w_j(r_j-\mu_j)\right)
\right]\\
&=\sum_i\sum_j w_iw_j
\mathbb E[(r_i-\mu_i)(r_j-\mu_j)]\\
&=\sum_i\sum_j w_iw_j\Sigma_{ij}\\
&=\boxed{\mathbf w^\mathsf T\boldsymbol\Sigma\mathbf w}.
\end{aligned}
$$

For two assets:

$$
\boxed{
\sigma_p^2
=w_1^2\sigma_1^2+w_2^2\sigma_2^2
+2w_1w_2\rho_{12}\sigma_1\sigma_2.
}
$$

The factor of two appears because the double sum contains both $(i,j)=(1,2)$ and $(2,1)$.

Expected returns are weighted averages. Volatility is generally not a weighted average: the cross terms matter.

### 8. A worked diversification example

Suppose two hypothetical assets each have:

- expected monthly return 1%;
- monthly volatility 10%.

Allocate half the portfolio to each. For any correlation, expected portfolio return is

$$
\mu_p=0.5(0.01)+0.5(0.01)=0.01.
$$

Its variance is

$$
\sigma_p^2
=(0.5)^2(0.10)^2+(0.5)^2(0.10)^2
+2(0.5)(0.5)\rho(0.10)(0.10)
=0.005(1+\rho).
$$

| Correlation | Portfolio monthly volatility | Standard deviation of ending wealth, starting at EUR 2,000 |
|---:|---:|---:|
| 1 | 10.00% | EUR 200.00 |
| 0.5 | 8.66% | EUR 173.21 |
| 0 | 7.07% | EUR 141.42 |
| -1 | 0.00% | EUR 0.00 |

The zero-volatility case is an idealized mathematical limit: equal volatilities and perfectly opposite deviations cancel exactly. It is not a claim that we can obtain a reliable risk-free return this way in real markets.

With imperfect positive correlation, diversification already reduces volatility relative to either asset alone in this example. Negative correlation is not required.

Holding more asset names is insufficient if their returns are strongly correlated. Historical correlation can also change, so estimated diversification benefits are uncertain.

### 9. Population quantities versus estimates from data

The model quantities $\mu_i$ and $\Sigma_{ij}$ are unknown. With $n$ aligned historical return observations, common estimators are

$$
\widehat\mu_i=\frac{1}{n}\sum_{k=1}^{n}r_{i,k}
$$

and

$$
\widehat\Sigma_{ij}
=\frac{1}{n-1}\sum_{k=1}^{n}
(r_{i,k}-\widehat\mu_i)(r_{j,k}-\widehat\mu_j).
$$

The $n-1$ denominator accounts for estimating the means from the same sample; it gives an unbiased covariance estimator for independent, identically distributed observations with finite second moments. Market data may violate those assumptions.

We must align dates, use a common valuation currency, document distributions and missing observations, and never estimate inputs from data unavailable at the decision time.

Daily and monthly volatilities are different quantities. The familiar square-root scaling holds for a sum of uncorrelated returns with equal variance:

$$
\operatorname{Var}\!\left(\sum_{k=1}^{m}r_k\right)=m\sigma^2.
$$

For compounded simple returns this is generally an approximation. For sums of log returns it is exact under the stated covariance assumptions. We will initially report volatility at the actual sampling frequency.

### 10. Drawdown: loss relative to an earlier peak

Volatility describes dispersion of returns. Drawdown describes a trajectory of wealth.

Assume positive portfolio value with no external deposits or withdrawals. Define its running peak:

$$
H_t=\max_{0\le s\le t}V_s.
$$

Define drawdown as a nonnegative loss fraction:

$$
D_t=1-\frac{V_t}{H_t}.
$$

Maximum drawdown over the observed interval is

$$
D_{\max}=\max_{0\le t\le T}D_t.
$$

For example:

| Time | Portfolio value | Running peak | Drawdown |
|---:|---:|---:|---:|
| 0 | EUR 2,000 | EUR 2,000 | 0% |
| 1 | EUR 2,200 | EUR 2,200 | 0% |
| 2 | EUR 1,980 | EUR 2,200 | 10% |
| 3 | EUR 2,090 | EUR 2,200 | 5% |
| 4 | EUR 2,310 | EUR 2,310 | 0% |

Maximum drawdown is 10%, even though the final cumulative return is

$$
\frac{2310}{2000}-1=15.5\%.
$$

At time 2, the loss relative to initial capital is only 1%, but the drawdown from the earlier peak is 10%. Those answer different questions.

A historical maximum drawdown is not a bound on future losses. A new path may exceed it. With deposits or withdrawals, we should measure drawdown on a performance index adjusted for external cash flows.

### 11. Why the order of returns matters

Consider the same four returns in two different orders, starting from EUR 2,000:

| Path | Return sequence | Wealth sequence, including initial value | Maximum drawdown |
|---|---|---|---:|
| A | +10%, +10%, -10%, -10% | 2000, 2200, 2420, 2178, 1960.20 | 19% |
| B | +10%, -10%, +10%, -10% | 2000, 2200, 1980, 2178, 1960.20 | 10.9% |

Both have the same arithmetic mean, sample volatility, and final value. Their maximum drawdowns differ.

The final values agree because multiplication is commutative:

$$
V_4=2000(1.1)^2(0.9)^2=1960.20.
$$

The peaks and subsequent troughs depend on the order. A variance limit therefore cannot, by itself, guarantee a drawdown limit.

### 12. Connecting these quantities to optimization

We now have a candidate mathematical problem for fixed one-period weights:

$$
\max_{\mathbf w}\ \mathbf w^\mathsf T\boldsymbol\mu
$$

subject to

$$
\mathbf w^\mathsf T\boldsymbol\Sigma\mathbf w
\le \sigma_{\mathrm{allowed}}^2,
\qquad
\sum_i w_i=1,
\qquad
w_i\ge0.
$$

This asks for the highest expected return within a chosen volatility limit. It is one possible formulation, not yet our selected objective.

The inputs $\boldsymbol\mu$ and $\boldsymbol\Sigma$ must be estimated. The risk limit expresses a preference. Neither is supplied by the optimizer itself.

For drawdown control, we would instead need a model for entire return paths. For example,

$$
\Pr(D_{\max}>d_{\mathrm{allowed}})\le\alpha
$$

specifies an allowed probability $\alpha$ of exceeding drawdown $d_{\mathrm{allowed}}$ over a stated horizon. Its validity depends on the path model and its estimated uncertainty.

Volatility and drawdown each capture part of risk. Neither fully describes rare losses, liquidity, or counterparty failure.

### 13. Checks for understanding

Try these before opening the answers.

1. An asset returns -4% or +6%, each with probability one half. What are its expected return and volatility?
2. Two assets each have volatility 8%. With equal weights and zero correlation, what is portfolio volatility?
3. A portfolio rises from EUR 2,000 to EUR 2,500 and falls to EUR 2,100. What is its current drawdown, and what is its cumulative return from the start?
4. Can two return sequences have the same mean and volatility but different maximum drawdowns?

<details>
<summary>Answers</summary>

1. The mean is 1%. Deviations from it are -5 and +5 percentage points, so volatility is 5%.

2. The variance is $2(0.5)^2(0.08)^2=0.0032$, giving volatility $\sqrt{0.0032}\approx0.05657=5.66\%$.

3. Drawdown is $1-2100/2500=16\%$. Cumulative return is $2100/2000-1=5\%$.

4. Yes. Reordering the same returns leaves their mean and volatility unchanged but can change the sequence of peaks and troughs, as in section 11.

</details>

### Next discussion

Before choosing an optimizer, we should distinguish the risk measures we can estimate from the losses we would actually tolerate. Then we can derive a two-asset allocation problem and examine how uncertainty in the estimated inputs changes its answer.
