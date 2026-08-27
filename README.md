# Casablanca stock exchange Income Planner

**How much capital do you need to invest in the Casablanca Stock Exchange to generate a target monthly income?**

This project answers that question rigorously, using real market data from the Bourse de Casablanca and two complementary financial models: a **dividend-based approach** (passive income, capital preserved) and a **withdrawal-based approach** (Monte Carlo simulation of share sales over a chosen horizon).

## Motivation

- Where people and organisation could put their money ?
- The native response is gold or real estate for large amount of money, these are basic investement and their is better alternatives of it such as stocks, wich they have the ability to make revenues by giving divident.
- According to the latest official data from the US Federal Reserve’s Survey of Consumer Finance, 21% of US families own stocks. instead in morrocco it is less than 1%.
- Personal finance calculators built for US or European markets don't apply cleanly to Morocco: dividend yields, tax treatment (15% withholding on dividends, capital gains exempt after 12 months), inflation, and market volatility on the MASI are all different. This tool is built specifically for the Moroccan context, using MASI historical data and the dividend profiles of the largest listed companies (Attijariwafa, Maroc Telecom, BCP, Managem, etc.).

## What the tool answers

Given a target monthly income and a few assumptions, it computes:

- The **capital required via dividends alone**, using either the MASI average yield or a user-selected basket of high-dividend stocks
- The **capital required via periodic withdrawals**, accounting for expected return, volatility, and inflation
- The **probability of portfolio survival** over the chosen horizon (sequence-of-returns risk)
- **Sensitivity analysis**: how the answer changes under optimistic, base, and pessimistic scenarios

## Approach

- **Data layer** — historical MASI prices and per-stock dividend yields (CSV + scraper)
- **Dividend model** — closed-form capital requirement, net of Moroccan withholding tax
- **Monte Carlo engine** — simulates N portfolio paths under a chosen return distribution, reports success rate and percentile outcomes
- **CLI + notebook demo** — reproducible examples with charts

## Key insight

The dividend approach and the withdrawal approach give very different answers for the same target income. Which one is "right" depends on assumptions the user rarely questions — this tool makes those assumptions explicit and lets you stress-test them.

## Tech stack

Python 3.11 · pandas · numpy · scipy · matplotlib · pytest · streamlit

## Disclaimer

This is an educational project. It is not investment advice. Historical returns do not guarantee future performance, and the MASI has a limited history compared to developed-market indices — model outputs should be treated as orders of magnitude, not precise forecasts.
