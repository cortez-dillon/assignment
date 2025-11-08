Created by: Dillon Cortez  
Updated by: Dillon Cortez	  
Date Created: 11/06/2025  
Date Updated: 11/07/2025  
Version: 1  
LLM Used: Perplexity

**Role**: Financial Analyst / Treasury Analyst  
**Audience**: CFO or Director of Treasury  
**Purpose**: Provide a professional, quantitative specification outlining the analytical structure for evaluating, comparing, and recommending foreign exchange (FX) hedging alternatives to manage the USD value risk of a EUR-denominated receivable due in one year.

## **Problem Statement**

Our company anticipates receiving EUR 20,000,000 in one year, exposing us to potential foreign exchange risk due to fluctuations in the EURUSD exchange rate. The objective is to analyze and evaluate alternative hedging strategies to protect the USD value of this receivable, balancing cost, certainty, and optionality. This report targets corporate treasury for strategic decision-making on FX risk management.

| Variable | Description | Unit | Value / Source |
| :---- | :---- | :---- | :---- |
| FCAMT | Foreign currency receivable | EUR | 20,000,000 (Company data) |
| S | Current EURUSD spot rate | USD per EUR | 1.1539 (Market data, Nov 7, 2025\) |
| F | 1-year EURUSD forward rate | USD per EUR | 1.0935 (Provided scenario) |
| rUSD | 1-year USD interest rate | % per annum | 3.7% (Federal Reserve data, Nov 2025\) |
| rEUR | 1-year EUR interest rate | % per annum | 2.2% (Euribor proxy, Nov 2025\) |
| t | Time to maturity | Years | 1 |
| Kput | Strike price for EUR put option | USD per EUR | 1.1539 (Set at spot) |
| Premiumput | Put option premium | USD per contract | 0.019 (Scenario) |
| Kcall | Strike price for EUR call option | USD per EUR | 1.1539 (Set at spot) |
| Premium call | Call option premium | USD per contract | 0.024 (Scenario) |

## **Conventions and Assumptions**

* Interest rates are quoted on a simple annual basis.  
* Forward rate corresponds to contract maturity in 1 year.  
* Premiums are paid upfront in USD.  
* Exchange rates expressed as USD per EUR.  
* Transaction and credit costs excluded.  
* No multipliers on option contracts, premium per EUR unit.

## **Calculation Flow**

1. Compute USD proceeds if the receivable is hedged via the forward contract at the forward rate ***F***   
2. Validate forward rate with synthetic forward calculation using money market parity:    Fcalc \= S x 1+rUSD x  T/1+rEUR x T  
3. Calculate USD proceeds from the put option hedge considering exercise and premium costs across a range of possible spot rates at maturity ***St***  
4. Calculate USD proceeds from the call option hedge similarly, capturing upside potential protection.  
5. Compare USD outcomes from forward, money market, put option, and call option hedges for base case and sensitivity scenarios (varying ***St*** from 0.95 x ***S*** in 0.01 increments).  
6. Summarize tradeoffs in cost, risk reduction, and optionality.

## **Outputs**

| Output Variable | Description | Format | Purpose |
| :---- | :---- | :---- | :---- |
| USDforward | USD proceeds via forward hedge | Numeric | Confirmed cash inflow certainty |
| USDmm | USD proceeds via money market hedge | Numeric | Cross-check forward rate viability |
| USDput | USD proceeds via put option hedge | Table | Protection at downside spot prices |
| USDcall | USD proceeds via call option hedge | Table | Upside protection scenarios |
| Summary Chart | Hedge outcomes vs. spot price | Line chart | Visualize comparative results |
| Executive Summary | Strategic recommendation summary | Text | Treasury decision support |

## **Sensitivity Plan**

* Analyze hedge outcomes across spot rate range 0.95 ***S*** to 1.05 ***S*** with increments of 0.01  
* Evaluate sensitivity of USD proceeds to changes in spot rate at maturity.  
* Test robustness of hedging decisions amid market volatility.

## **Limitations and Next Steps**

* Current specification ignores transaction costs, bid-ask spreads, and counterparty credit risk.  
* Implied volatility effects on option pricing not incorporated; premiums are fixed per scenario inputs.  
* The next phase involves coding a spreadsheet model or software implementation to quantify outcomes under varying scenarios for informed risk management.
