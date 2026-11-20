# Can Investor Attention Be Traded?
### Search-attention signals and two-week returns in the S&P 100

This project tests whether a sudden rise in Google searches for a company predicts its stock
return over the next two weeks, building on Da, Engelberg & Gao (2011), *In Search of Attention*.

## The question
Investors pile into whatever is popular, especially during the current AI boom. Can an
outsider make money by spotting that attention and following the crowd?

## Method
- **Universe:** 101 current S&P 100 constituents, Oct 2021 – Aug 2026 (258 weeks)
- **Signal:** a "spike" is a week when search interest is more than 2 standard deviations above
  the stock's own trailing 52-week average (1,370 signals)
- **Trading:** buy every spiking stock at equal weight and hold for two weeks, paying 5 bps on
  entry and exit. Signals are lagged 14 days to avoid look-ahead bias
- **Benchmark:** an equal-weighted basket of the same stocks with no trading costs
- **Inference:** weekly cross-sectional return gap with Newey-West (HAC) t-statistics,
  checked separately before and after a fixed split on 1 June 2024

## Key results
| Period | Strategy (net) | Benchmark | Sharpe (strat / bench) 
| In-sample | 59.0% | 29.7% | 0.98 / 0.76 |
| Out-of-sample | 108.8% | 77.1% | 1.79 / 1.87 |

The strategy beat the benchmark in both periods, but neither the return gap nor the active
return was significant at the 5% level (HAC t = 1.65 and 1.22). The sector split shows the
edge is partly driven by the tech/semiconductor cycle. **Conclusion: the trading claim is not
supported.**

## Robustness and pitfalls addressed
- Good-news filter (spikes where the price also rose that week)
- IT vs non-IT sector split
- Truncation tests: 0 of 53,867 z-scores changed, so no future data leaks into the signal
- Google Trends rescaling/rounding noise: 20 re-rounding tests
- Bugs found and fixed: a monthly-vs-weekly data mix-up, early signal timing, look-ahead in
  the filter, and inflated pooled t-statistics (3.81 → 1.22)
- Known limitation: survivorship bias from using today's index members

## Files
- `notebook.ipynb`: full pipeline (data → cleaning → strategy → backtest → risk diagnostics)
- `report.pdf`: write-up with hypothesis, methodology defence and pitfall checklist
- `data/`: cached snapshot so the results reproduce exactly (`USE_CACHE = True`)

## Tools
Python, pandas, NumPy, statsmodels, matplotlib, pytrends, yfinance

**Author:** Nada Zueter · October 2026
