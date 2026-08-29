# Casablanca stock exchange Income Planner

**How much capital do you need to invest in the Casablanca Stock Exchange to generate a target monthly income?**

This project answers that question rigorously, using real market data from the Bourse de Casablanca and two complementary financial models: a **dividend-based approach** (passive income, capital preserved) and a **withdrawal-based approach** (Monte Carlo simulation of share sales over a chosen horizon).

## Motivation

- Where people and organisation could put their money ?
- The native response is gold or real estate for large amount of money, these are basic investement and their is better alternatives of it such as stocks, wich they have the ability to make revenues by giving divident.
- According to the latest official data from the US Federal Reserve’s Survey of Consumer Finance, 21% of US families own stocks. instead in morrocco it is less than 1%.
- Personal finance calculators built for US or European markets don't apply cleanly to Morocco: dividend yields, tax treatment (15% withholding on dividends, capital gains exempt after 12 months), inflation, and market volatility on the MASI are all different. This tool is built specifically for the Moroccan context, using MASI historical data and the dividend profiles of the largest listed companies (Attijariwafa, Maroc Telecom, BCP, Managem, etc.).

## What the tool answers

**Income mode** — given a lump-sum capital available today:
- What monthly (after-tax) income can it generate through dividends?
- Inversely, what capital is needed for a target monthly income?

**Accumulation mode** — given a monthly savings capacity:
- How large will the capital grow over T years, accounting for reinvested dividends and price appreciation (net of tax)?
- What monthly income will that final capital produce?

**Portfolio tools:**
- **Screen** stocks by yield, sector, or market capitalization
- **Suggest** a diversified portfolio for a target income (greedy heuristic with concentration limits) 

## Mathematical model

**Income mode (Model A):**

$$M = \frac{C \cdot y_{\text{net}}}{12} \qquad C = \frac{12 \cdot M}{y_{\text{net}}}$$

where $y_{\text{net}} = y_{\text{gross}} \cdot (1 - \tau_d)$ and $\tau_d = 0.15$.

**Accumulation mode (Model B):**

$$C(T) = s \cdot \frac{(1 + r_{m,\text{net}})^{12T} - 1}{r_{m,\text{net}}}$$

with $r_{\text{net}} = y(1 - \tau_d) + g$ and $r_{m,\text{net}} = (1 + r_{\text{net}})^{1/12} - 1$.

Non-dividend-paying stocks are supported in the dataset but only contribute to capital growth ($g$), never to income ($y = 0$).

## Approach

- **Data layer** — historical MASI prices and per-stock dividend yields (CSV + scraper)
- **Dividend model** — closed-form capital requirement, net of Moroccan withholding tax
- **CLI + notebook demo** — reproducible examples with charts

## Roadmap

- Historical scenario analysis (pessimistic / base / optimistic percentiles)
- Monte Carlo simulation with probability-of-ruin
- Markowitz mean-variance portfolio optimization
- Live data scraper for BVC / Wafabourse
- Streamlit web interface
- Multi-phase accumulation (partial retirement, phased transitions)
- Dividend sustainability scoring

## Key insight

The dividend approach and the withdrawal approach give very different answers for the same target income. Which one is "right" depends on assumptions the user rarely questions — this tool makes those assumptions explicit and lets you stress-test them.

## Tech stack

Python 3.11 · pandas · numpy · scipy · matplotlib · pytest · streamlit

## Disclaimer

This is an educational project. It is not investment advice. Historical returns do not guarantee future performance, and the MASI has a limited history compared to developed-market indices — model outputs should be treated as orders of magnitude, not precise forecasts.
