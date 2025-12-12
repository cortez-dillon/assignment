### **A. Scenario-Specific Variables (Inputs)**

The model will use the following specific input values derived from the scenario provided:

| Variable | Description | Unit | Value | Named Range |
| :---- | :---- | :---- | :---- | :---- |
| **FC\_AMT** | Foreign currency receivable | EUR | 20,000,000 | FC\_AMT |
| **S0\_in** | Current EUR/USD Spot Rate | USD/EUR | 1.1539 | S0\_in |
| **F0\_in** | 1-year EUR/USD Forward Rate | USD/EUR | 1.0935 | F0\_in |
| **R\_USD** | 1-year USD Interest Rate | % p.a. | 3.7% | R\_USD |
| **R\_FC** | 1-year EUR Interest Rate | % p.a. | 2.2% | R\_FC |
| **T\_DAYS** | Time to Maturity (in Days) | Days | 365 | T\_DAYS |
| **T\_YRS** | Time to Maturity (in Years) | Years | 1 | T\_YRS |
| **K\_PUT** | Put Option Strike Price | USD/EUR | 1.1539 | K\_PUT |
| **PREM\_PUT** | Put Option Premium | USD/EUR | 0.019 | PREM\_PUT |
| **K\_CALL** | Call Option Strike Price | USD/EUR | 1.1539 | K\_CALL |
| **PREM\_CALL** | Call Option Premium | USD/EUR | 0.024 | PREM\_CALL |

---

### **B. Excel Spreadsheet Requirements**

The AI must generate a professional, downloadable spreadsheet model (.xlsx file) with the following structure and components:

#### **1\. Named Ranges**

Create the following exact Named Ranges, ensuring they correspond to the input cells:

FC\_AMT, S0\_in, F0\_in, R\_USD, R\_FC, K\_PUT, K\_CALL, PREM\_PUT, PREM\_CALL, T\_DAYS, T\_YRS.

#### **2\. Color Coding**

Strictly apply the following color convention across the model:

* **Yellow Fill:** All **Input Variables** and **Decision Variables** (e.g., FC\_AMT, S0\_in, K\_PUT).  
* **Blue Fill:** **Assumptions** and derived time variables (e.g., T\_DAYS, T\_YRS).  
* **Green Fill:** Cells containing **Formulas** or calculations (e.g., Hedge outcomes, Parity Check).  
* **Gray Fill:** Final **Outputs** / Key Performance Indicators (KPIs) (e.g., USDforward, Summary Results).

#### **3\. Model Components and Calculations**

Organize the spreadsheet into the following distinct, clearly labeled sections:

**I. Inputs and Assumptions**

* Display all variables from Section A in a clearly labeled table.  
* Ensure T\_YRS is calculated as T\_DAYS / 365.

**II. Forward Hedge Calculation**

* **Output:** USDforward (Total USD proceeds)  
* **Formula:** $USD\_{forward} \= FC\_{AMT} \\times F0\\\_in$

**III. Money Market (MM) Hedge Calculation (3-Step Logic)**

* Step 1: Borrow FC Today (in EUR):  
  $$Borrow\_{FC} \= \\frac{FC\_{AMT}}{1 \+ R\_{FC} \\times T\_{YRS}}$$  
* Step 2: Convert to USD Today:  
  $$USD\_{Invest} \= Borrow\_{FC} \\times S0\\\_in$$  
* **Step 3: Future USD Proceeds:**  
  * Output: USDmm (Total USD proceeds)  
    $$USD\_{MM} \= USD\_{Invest} \\times (1 \+ R\_{USD} \\times T\_{YRS})$$

**IV. Synthetic Forward Rate (Parity Check)**

* Formula:  
  $$F\_{calc} \= S0\\\_in \\times \\frac{1 \+ R\_{USD} \\times T\_{YRS}}{1 \+ R\_{FC} \\times T\_{YRS}}$$  
* **Cross-Check:** Include a cell that computes the difference between $F\_{0\\\_in}$ and $F\_{calc}$ and label it **Parity Deviation**.

**V. Sensitivity Analysis and Option Payoff Table**

* Create a table spanning 11 rows of scenarios.  
* **Column A: Future Spot Rate ($S\_T$)**: Start at $0.95 \\times S0\\\_in$ and increase in increments of **0.01 USD/EUR** until $1.05 \\times S0\\\_in$.  
* **Column B: Unhedged Proceeds**: Calculate $FC\_{AMT} \\times S\_T$.  
* **Column C: Forward Hedge Proceeds**: Should be a fixed value (USDforward) across all rows.  
* **Column D: Money Market Hedge Proceeds**: Should be a fixed value (USDmm) across all rows.  
* **Column E: Put Option Hedge Proceeds**:  
  * **Logic:** The Put Option grants the right to sell EUR at $K\_{PUT}$ or at the market rate ($S\_T$) if $S\_T \> K\_{PUT}$. The premium is paid upfront.  
  * Formula:  
    $$USD\_{put} \= (FC\_{AMT} \\times \\max(K\_{PUT}, S\_T)) \- (FC\_{AMT} \\times PREM\_{PUT})$$

**VI. Summary Outputs**

* Create a final table summarizing the certainty of cash flows for the **Forward** and **MM** hedges, and the minimum/maximum possible USD proceeds for the **Put Option** hedge based on the sensitivity table.

#### **4\. Verification Instructions**

The AI must explicitly perform and report the following verification steps:

1. **Validate Parity:** Report the Parity Deviation value and comment on whether the input forward rate ($F\_{0\\\_in}$) is close to the theoretical rate ($F\_{calc}$).  
2. **Confirm Named Ranges:** Explicitly list all 11 created Named Ranges (e.g., FC\_AMT, S0\_in, etc.) and the cell addresses they refer to for auditability.  
3. **Formula Mapping:** Provide a full, separate list showing the exact Excel formula used for all Green-colored calculation cells, mapping them to their specific cell addresses (e.g., Cell B10 (USDforward): \=FC\_AMT \* F0\_in).  
4. **Deliverable:** **Provide the complete model as a downloadable .xlsx file.**
