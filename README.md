# NMD WAL Simulator — Behavioral Runoff Analytics for IRRBB

## Overview

This repository presents a simulation framework to estimate the **Weighted Average Life (WAL)** of Non-Maturing Deposits (NMDs) by GL Product Code, enabling product-level insights for **IRRBB (Interest Rate Risk in the Banking Book)**. 

By applying behavioral runoff assumptions, the model calculates WAL over a specified tenor horizon and flags products that **exceed regulatory or internal WAL policy thresholds** — supporting decision-making for product repricing, retention, or discontinuation.

---

## Business Context

Under Basel IRRBB guidelines, banks must estimate the repricing behavior of non-contractual deposits. WAL assumptions feed directly into:

- **Economic Value of Equity (EVE)** and **Net Interest Income (NII)** sensitivity  
- Capital allocation under interest rate risk buffers  
- Treasury and ALCO decisions on which products to **optimize, retain, or exit**

This simulation toolkit offers a modular engine to profile behavioral WAL across deposit segments like **Retail Savings, Corporate Sweeps, and SME Operating accounts**.

---

## Model Structure

| Component        | Description                                         |
|------------------|-----------------------------------------------------|
| `GL_Code`         | Product identifier from General Ledger             |
| `Decay_Type`      | Behavioral runoff assumption (`exponential`, `linear`, `custom_step`, etc.) |
| `Initial_Balance` | Simulated customer deposit balance (e.g. €100M)    |
| `WAL_Cap_Years`   | Internal/regulatory policy cap for acceptable WAL  |

The engine simulates runoff over 10 years, applies the decay curve, and computes:

$$
\text{WAL} = \frac{\sum_{t} t \cdot \text{Runoff}_t}{\sum_t \text{Runoff}_t}
$$

---

## Output Preview



The notebook generates a comparative bar chart:

- Bars: Actual computed WAL per GL product  
- Dashed Line: WAL policy cap  
- Inline Labels: WAL in years  
- Color-coded decisions:
  - **Continue**: WAL ≤ Cap
  - **Discontinue / Reprice**: WAL > Cap  

> Outcome: A simple yet powerful IRRBB signal to guide deposit product strategies.

---

## How to Use

- Clone the repo:
   ```bash
   git clone https://github.com/SanketSapre25/NMD-WAL-Profiler.git
   cd NMD-WAL-Profiler
   - Launch NMD_WAL_Analyzer.ipynb in Jupyter
- Edit the gl_data DataFrame with your product assumptions
- Run through the notebook:
- Behavioral decay simulation
- WAL computation
- Visualization + decisions

## Dependencies
- numpy
- pandas
- matplotlib


## Roadmap
- Add CSV import / export capability
- Support maturity bucketing (0–2Y, 2–4Y, etc.)

## Author
Sanket Sapre, a Senior Consutant in Model Risk and Regulatory Reporting, currently upskilling into Risk Data Product Management. This project is part of a broader portfolio of open prototypes aimed at modernizing capital and treasury risk workflows through product-led thinking.

## License
Licensed under the GNU General Public License v3.0 — see LICENSE for details.

