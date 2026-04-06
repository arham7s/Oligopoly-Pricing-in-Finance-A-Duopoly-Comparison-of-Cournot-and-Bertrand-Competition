# Oligopoly Pricing in Finance: A Duopoly Comparison of Cournot and Bertrand Competition

![Python](https://img.shields.io/badge/Python-3.8%2B-blue?logo=python&logoColor=white)
![Platform](https://img.shields.io/badge/Platform-Google%20Colab-orange?logo=googlecolab&logoColor=white)
![Domain](https://img.shields.io/badge/Domain-Economics%20%7C%20Game%20Theory%20%7C%20Finance-green)
![Status](https://img.shields.io/badge/Status-Complete-brightgreen)
![License](https://img.shields.io/badge/License-MIT-lightgrey)

---

## Table of Contents

1. [Project Overview](#1-project-overview)
2. [Why This Project Matters](#2-why-this-project-matters)
3. [Economic Background](#3-economic-background)
4. [Mathematical Framework](#4-mathematical-framework)
5. [Project Structure](#5-project-structure)
6. [Notebook Sections](#6-notebook-sections)
7. [Key Results and Findings](#7-key-results-and-findings)
8. [Visualisations](#8-visualisations)
9. [Finance Applications](#9-finance-applications)
10. [How to Run](#10-how-to-run)
11. [Dependencies](#11-dependencies)
12. [Parameter Reference](#12-parameter-reference)
13. [Extensions](#13-extensions)
14. [Outputs and Exports](#14-outputs-and-exports)
15. [Resume Bullets](#15-resume-bullets)
16. [Alternative Project Titles](#16-alternative-project-titles)
17. [References](#17-references)

---

## 1. Project Overview

This project builds a **complete simulation-based study of oligopoly pricing** under two foundational game-theoretic frameworks — **Cournot competition** (quantity-setting) and **Bertrand competition** (price-setting) — and connects both models directly to real-world finance and business settings.

The notebook is written entirely in Python, runs top-to-bottom in Google Colab with no external dataset required, and produces publication-quality tables, charts, sensitivity analyses, and welfare decompositions. It is designed to be accessible to beginners while being analytically rigorous enough for academic showcase, case competitions, and professional portfolios.

> **One-line summary:** Two firms. Two strategies. Completely different market outcomes. Here is the full maths, simulation, and finance interpretation — end to end.

---

## 2. Why This Project Matters

### In Economics
Oligopoly markets — where a small number of firms dominate — are the norm in modern economies. Understanding how firms compete strategically is central to industrial organisation, antitrust policy, and regulatory economics.

### In Finance and Business

The same game-theoretic logic that governs quantity and price competition in a textbook duopoly maps directly onto real financial markets:

| Financial Market | Competition Type | Model Analogy |
|---|---|---|
| Banks competing on loan / deposit rates | Rate-undercutting | Bertrand |
| Brokers competing on trading fees | Fee war, zero-commission race | Bertrand |
| Investment banks managing deal volume | Pipeline and capacity discipline | Cournot |
| Insurers setting premiums | Price or volume competition | Both |
| Fintechs disrupting legacy incumbents | Cost advantage leading to undercutting | Asymmetric Bertrand |
| Lenders controlling credit supply | Volume-based rivalry | Cournot |

This project shows — with clean numerical evidence — **why Bertrand competition collapses margins, why Cournot preserves them, and what a cost advantage means in a disruption scenario.**

---

## 3. Economic Background

### What is a Duopoly?
A duopoly is a market with exactly two competing firms. It is the simplest form of oligopoly and lets us study strategic interaction in its purest form — each firm's optimal decision depends on what it expects its rival to do.

### Cournot Competition (1838)
Proposed by Antoine Augustin Cournot. Each firm simultaneously chooses **how much to produce**. The market price adjusts downward based on total industry output. Neither firm observes the rival's decision beforehand — they best-respond to expectations.

**Core prediction:** Both firms produce a positive quantity. Price settles above marginal cost. Both firms earn positive economic profit. The outcome is less efficient than perfect competition but better for consumers than monopoly.

### Bertrand Competition (1883)
Proposed by Joseph Bertrand as a critique of Cournot. Each firm simultaneously chooses **what price to charge**. Consumers are rational and always buy from the cheapest firm.

**Core prediction:** With identical products and identical costs, price competition drives equilibrium price all the way down to marginal cost. Both firms earn zero profit. This is known as the **Bertrand Paradox** — just two firms are enough to replicate the perfectly competitive outcome.

### Nash Equilibrium
Both models are solved using the **Nash Equilibrium** — a strategy profile where no firm can improve its own profit by unilaterally changing its decision, given the other firm's strategy. In Cournot this means both firms are simultaneously on their best-response curves. In Bertrand this means neither firm gains by raising or lowering its price.

---

## 4. Mathematical Framework

### Demand
Linear inverse demand function:

```
P = a - b·Q        where Q = q1 + q2
```

| Symbol | Meaning | Baseline |
|---|---|---|
| `P` | Market price | Endogenous |
| `Q` | Total output | Endogenous |
| `a` | Demand intercept (max willingness to pay) | 100 |
| `b` | Demand slope | 1 |

### Cost Functions

```
C1(q1) = c1 · q1
C2(q2) = c2 · q2
```

| Symbol | Meaning | Baseline |
|---|---|---|
| `c1` | Marginal cost Firm 1 | 20 |
| `c2` | Marginal cost Firm 2 | 20 |

### Cournot Equilibrium

**Profit functions:**
```
π1 = (a - b(q1+q2) - c1) · q1
π2 = (a - b(q1+q2) - c2) · q2
```

**First-order conditions (set ∂π/∂q = 0):**
```
a - 2b·q1 - b·q2 - c1 = 0
a - 2b·q2 - b·q1 - c2 = 0
```

**Best-response functions:**
```
BR1(q2) = (a - c1 - b·q2) / (2b)
BR2(q1) = (a - c2 - b·q1) / (2b)
```

**Analytical Nash equilibrium (general asymmetric case):**
```
q1* = (a - 2c1 + c2) / (3b)
q2* = (a - 2c2 + c1) / (3b)
Q*  = (2a - c1 - c2) / (3b)
P*  = (a + c1 + c2) / 3
π1* = b · (q1*)²
π2* = b · (q2*)²
```

**Baseline numerical results (a=100, b=1, c1=c2=20):**
```
q1* = q2* = 26.67    Q* = 53.33    P* = 46.67
π1* = π2* = 711.11   Total profit  = 1422.22
```

### Bertrand Equilibrium

**Demand allocation rule:**
```
p1 < p2  →  Firm 1 serves Q = a - b·p1,   Firm 2 serves 0
p2 < p1  →  Firm 2 serves Q = a - b·p2,   Firm 1 serves 0
p1 = p2  →  Market split equally
```

**Equilibrium (symmetric costs) — Bertrand Paradox:**
```
p* = MC = c
Q* = a - b·c
π1* = π2* = 0
```

**Baseline numerical results:**
```
P* = 20.00    Q* = 80.00    π1* = π2* = 0.00
```

### Welfare Measures

```
Consumer Surplus   CS  = 0.5 · (a - P*) · Q*
Producer Surplus   PS  = Total industry profit
Total Welfare      TW  = CS + PS
Deadweight Loss    DWL = TW_competitive - TW_actual
```

---

## 5. Project Structure

```
oligopoly-duopoly-model/
│
├── Oligopoly_Pricing_Duopoly_Model.ipynb     ← Main notebook (run in Colab)
│
├── Images/
│   ├── 01_cournot_best_response.png
│   ├── 02_bertrand_heatmaps.png
│   ├── 03_bertrand_undercutting.png
│   ├── 04_cournot_vs_bertrand_comparison.png
│   ├── 05_sensitivity_a.png
│   ├── 06_sensitivity_b.png
│   ├── 07_sensitivity_c1.png
│   ├── 08_sensitivity_c2.png
│   ├── 09_asymmetric_cournot.png
│   └── 10_welfare_analysis.png
│
└── README.md
```

---

## 6. Notebook Sections

| # | Section | What it does |
|---|---|---|
| 1 | Introduction and Imports | Project header, library imports, matplotlib style configuration |
| 2 | Baseline Parameters | Single block to set `a`, `b`, `c1`, `c2` — change here to re-run everything |
| 3 | Cournot Model | SymPy symbolic derivation, best-response curves, analytical equilibrium, output table |
| 4 | Bertrand Model | Demand allocation logic, profit heatmaps, undercutting dynamics |
| 5 | Model Comparison | Head-to-head comparison table, four-panel bar chart, finance interpretation |
| 6 | Sensitivity Analysis | Four parameter sweeps, line plots, directional summary, 2D price-gap heatmap |
| 7 | Asymmetric Firms | Scenarios with c1 not equal to c2, fintech vs incumbent case study |
| 8 | Extensions | Capacity constraints, product differentiation, repeated interaction, welfare analysis |
| 9 | Export | Save all charts as PNG and combined PDF, export all results to CSV |

---

## 7. Key Results and Findings

### Baseline Comparison (a=100, b=1, c1=c2=20)

| Metric | Cournot | Bertrand | Direction |
|---|---|---|---|
| Market Price P* | 46.67 | 20.00 | Bertrand 57% lower |
| Total Quantity Q* | 53.33 | 80.00 | Bertrand 50% higher |
| Firm 1 Profit | 711.11 | 0.00 | Cournot preserves margins |
| Firm 2 Profit | 711.11 | 0.00 | Cournot preserves margins |
| Total Industry Profit | 1422.22 | 0.00 | Cournot wins for producers |
| Consumer Surplus | 1422.22 | 3200.00 | Bertrand 125% higher |
| Total Welfare | 2844.44 | 3200.00 | Bertrand socially superior |
| Deadweight Loss | 355.56 | 0.00 | Cournot creates inefficiency |
| Price minus MC Markup | 26.67 | 0.00 | Cournot has market power |

### Finding 1 — The Bertrand Paradox holds numerically
With identical products and identical costs, two firms competing on price replicates perfect competition. Price equals marginal cost. Profit is zero. Confirmed analytically and shown via heatmap simulation.

### Finding 2 — Cournot preserves meaningful market power
Under quantity competition, both firms earn significant positive profit (711 each at baseline). The markup of 26.67 over marginal cost survives with only two competitors — this is the Cournot market power premium.

### Finding 3 — Sensitivity to market size
As demand intercept `a` rises, Cournot profits rise steeply while Bertrand profits stay flat at zero. The gap between models widens in larger markets, making the competition mode increasingly consequential in high-growth industries.

### Finding 4 — Cost asymmetry has opposite effects under each model
Under Cournot, a cost-efficient firm gains market share and higher profit but the rival always survives with positive profit. Under Bertrand, the efficient firm eliminates the rival entirely — winner-takes-all dynamics emerge.

### Finding 5 — Product differentiation rescues Bertrand firms
Even slight product differentiation (substitutability parameter γ < 1) restores positive profit under price competition. This is the economic rationale for brand investment and product differentiation in banking, insurance, and fintech.

### Finding 6 — Capacity constraints raise prices
When both firms face binding capacity caps in Cournot, total supply falls and market price rises above the unconstrained equilibrium. Models the effect of capital requirements (Basel III) on bank lending rates.

### Welfare Ranking
```
Perfect Competition = Bertrand Duopoly > Cournot Duopoly > Monopoly

TW:    3200  (DWL = 0)   |   3200  (DWL = 0)   |   2844  (DWL = 356)   |   2400  (DWL = 800)
```

---

## 8. Visualisations

### Chart 1 — Cournot Best Response Curves
Two downward-sloping best-response lines intersecting at the Nash equilibrium. The intersection is the unique (q1, q2) pair where both firms are simultaneously on their best-response curve — neither wants to deviate.

![Cournot Best Response](https://github.com/arham7s/Oligopoly-Pricing-in-Finance-A-Duopoly-Comparison-of-Cournot-and-Bertrand-Competition/blob/main/Outputs/01_cournot_best_response.png)

---

### Chart 2 — Bertrand Profit Heatmaps
Side-by-side profit heatmaps across all (p1, p2) price combinations for each firm. Bright regions indicate high profit — they appear when a firm prices low while the rival prices high. This is the visual engine of Bertrand undercutting incentives.

![Bertrand Heatmaps](https://github.com/arham7s/Oligopoly-Pricing-in-Finance-A-Duopoly-Comparison-of-Cournot-and-Bertrand-Competition/blob/main/Outputs/02_bertrand_heatmaps.png)

---

### Chart 3 — Bertrand Undercutting Dynamics
For three fixed levels of the rival's price, shows how Firm 1's profit jumps discontinuously just below the rival's price, then collapses to zero at and above it. This discontinuity drives the Bertrand race to the bottom.

![Bertrand Undercutting](https://github.com/arham7s/Oligopoly-Pricing-in-Finance-A-Duopoly-Comparison-of-Cournot-and-Bertrand-Competition/blob/main/Outputs/03_bertrand_undercutting.png)

---

### Chart 4 — Cournot vs Bertrand Four-Panel Comparison
Bar charts comparing market price, total quantity, firm-level profits, and welfare (consumer and producer surplus stacked) side by side across both models at baseline parameters.

![Model Comparison](https://github.com/arham7s/Oligopoly-Pricing-in-Finance-A-Duopoly-Comparison-of-Cournot-and-Bertrand-Competition/blob/main/Outputs/04_cournot_vs_bertrand_comparison.png)

---

### Chart 5 — Sensitivity to Demand Intercept (a)
As market size grows, Cournot profits rise steeply and the Cournot-Bertrand price gap widens. Bertrand profits remain flat at zero regardless of market size.

![Sensitivity a](https://github.com/arham7s/Oligopoly-Pricing-in-Finance-A-Duopoly-Comparison-of-Cournot-and-Bertrand-Competition/blob/main/Outputs/05_sensitivity_a.png)

---

### Chart 6 — Sensitivity to Demand Slope (b)
Steeper demand (higher b) compresses equilibrium prices and quantities in both models. The markup gap between Cournot and Bertrand narrows as demand becomes more inelastic.

![Sensitivity b](https://github.com/arham7s/Oligopoly-Pricing-in-Finance-A-Duopoly-Comparison-of-Cournot-and-Bertrand-Competition/blob/main/Outputs/06_sensitivity_b.png)

---

### Chart 7 — Sensitivity to Firm 1 Marginal Cost (c1)
Higher Firm 1 cost shrinks its output and profit under Cournot. Under Bertrand, the equilibrium price rises exactly with MC — confirming p* = MC holds always.

![Sensitivity c1](https://github.com/arham7s/Oligopoly-Pricing-in-Finance-A-Duopoly-Comparison-of-Cournot-and-Bertrand-Competition/blob/main/Outputs/07_sensitivity_c1.png)

---

### Chart 8 — Sensitivity to Firm 2 Marginal Cost (c2)
As Firm 2 becomes more expensive, Firm 1 gains Cournot market share. Under Bertrand, market leadership shifts to Firm 1 once c1 is below c2.

![Sensitivity c2](https://github.com/arham7s/Oligopoly-Pricing-in-Finance-A-Duopoly-Comparison-of-Cournot-and-Bertrand-Competition/blob/main/Outputs/08_sensitivity_c2.png)

---

### Chart 9 — Asymmetric Firms: Cournot Quantities and Profits
As the cost gap widens from symmetric (c1=c2=20) to extreme asymmetry (c1=5, c2=45), Firm 1 increasingly dominates quantity and profit. Firm 2 shrinks but always survives under Cournot — unlike under Bertrand.

![Asymmetric Cournot](https://github.com/arham7s/Oligopoly-Pricing-in-Finance-A-Duopoly-Comparison-of-Cournot-and-Bertrand-Competition/blob/main/Outputs/09_asymmetric_cournot.png)

---

### Chart 10 — Welfare Analysis Across Market Structures
Left panel: stacked bar chart of consumer surplus, producer surplus, and deadweight loss for all four market structures. Right panel: demand-curve geometry showing the CS triangle, PS rectangle, and DWL triangle for Cournot vs perfect competition.

![Welfare Analysis](https://github.com/arham7s/Oligopoly-Pricing-in-Finance-A-Duopoly-Comparison-of-Cournot-and-Bertrand-Competition/blob/main/Outputs/10_welfare_analysis.png)

---

## 9. Finance Applications

### Banks Competing on Loan Rates — Bertrand Logic
Two banks offering identical mortgage products compete by setting interest rates. The lower-rate bank captures all borrowers. Undercutting drives rates toward the cost of funds — net interest margin collapses to zero. This is precisely the Bertrand equilibrium outcome with p approaching MC.

If banks cannot differentiate their products, rate competition is a Bertrand game and NIM compression is the predicted equilibrium result.

### Brokerage Fee Wars — Bertrand Logic
The shift to zero-commission trading is a real-world Bertrand equilibrium in slow motion. When brokerage services are homogeneous, fee competition is intense and equilibrium fees approach the marginal cost of execution. A new entrant with lower unit costs can set fees below the incumbent's cost floor, capture the entire market, and still earn positive profit — the asymmetric Bertrand outcome.

### Investment Banking Deal Volume — Cournot Logic
Investment banks managing underwriting pipelines compete on relationships and capacity allocation, not headline fees. Each bank decides how many deals to pursue (quantity), not what fee to charge (price). This is Cournot competition. Volume discipline preserves spreads. When all banks constrain deal flow simultaneously in a risk-off environment, underwriting fees widen — the capacity-constrained Cournot result.

### Insurance Premium Competition — Both Models Apply
When two insurers cover identical risks, premium competition is Bertrand — prices fall toward actuarial cost. When products are differentiated by coverage scope, service quality, or brand reputation, firms escape the paradox and retain pricing power. The product differentiation extension models this transition precisely via the γ parameter.

### Fintech Disruption of Incumbents — Asymmetric Bertrand
A fintech with lower unit costs (no branch network, automated processes, cheaper capital) enters against a legacy incumbent. With c1 less than c2, the fintech prices just below the incumbent's marginal cost, captures the entire market, and earns (c2 minus c1) times Q as profit. The larger the cost gap, the higher the fintech's profit at equilibrium. The incumbent is eliminated unless it cuts costs or meaningfully differentiates its product. This is the disruption playbook in precise mathematical form.

---

## 10. How to Run

### Google Colab (Recommended — No Setup Required)

1. Open [Google Colab](https://colab.research.google.com)
2. Click **File → Upload notebook** and upload the `.ipynb` file
3. Click **Runtime → Run all**
4. All charts appear inline; exported files appear in the Files panel on the left sidebar

### Local Jupyter

```bash
# Clone the repository
git clone https://github.com/YOUR_USERNAME/oligopoly-duopoly-model.git
cd oligopoly-duopoly-model

# Install dependencies
pip install numpy pandas matplotlib seaborn sympy

# Launch notebook
jupyter notebook Oligopoly_Pricing_Duopoly_Model.ipynb
```

### Changing Parameters

All parameters live in a single block at the top of the notebook. Edit and re-run all cells:

```python
a  = 100   # demand intercept
b  = 1     # demand slope
c1 = 20    # marginal cost Firm 1
c2 = 20    # marginal cost Firm 2
```

### Downloading Outputs from Colab

```python
from google.colab import files
import shutil

# Download the combined PDF of all 10 charts
files.download('oligopoly_charts/oligopoly_all_charts.pdf')

# Download all charts and CSVs as a ZIP archive
shutil.make_archive('oligopoly_output', 'zip', 'oligopoly_charts')
files.download('oligopoly_output.zip')
```

---

## 11. Dependencies

All libraries are available by default in Google Colab — no installation required.

| Library | Purpose |
|---|---|
| `numpy` | Numerical arrays, grid simulations |
| `pandas` | DataFrame outputs, CSV exports |
| `matplotlib` | All charts and visualisations |
| `seaborn` | Colour palettes, heatmap styling |
| `sympy` | Symbolic algebra — best-response derivation, equilibrium solving |
| `itertools` | Combinatorial utilities |
| `warnings` | Suppress non-critical warnings |

For local environments:
```bash
pip install numpy pandas matplotlib seaborn sympy
```

---

## 12. Parameter Reference

| Parameter | Symbol | Default | Effect of Increase |
|---|---|---|---|
| Demand intercept | `a` | 100 | Larger market; higher prices and profits in both models |
| Demand slope | `b` | 1 | Steeper demand; lower equilibrium prices and quantities |
| Firm 1 marginal cost | `c1` | 20 | Firm 1 shrinks output and profit; Bertrand price rises with MC |
| Firm 2 marginal cost | `c2` | 20 | Firm 2 shrinks; Firm 1 gains Cournot share |
| Capacity cap Firm 1 | `K1` | unlimited | Binding cap raises price; shifts output share to Firm 2 |
| Capacity cap Firm 2 | `K2` | unlimited | Binding cap raises price; shifts output share to Firm 1 |
| Substitutability | `γ` | 0 to 1 | Higher γ means more intense price competition and lower profit |
| Simulation periods | `T` | 25 | Longer horizon for repeated game convergence |

### Useful Parameter Combinations

```python
# Symmetric baseline
a, b, c1, c2 = 100, 1, 20, 20

# Large growing market
a, b, c1, c2 = 150, 1, 20, 20

# Highly price-sensitive customers
a, b, c1, c2 = 100, 2, 20, 20

# Fintech vs incumbent (cost disruption)
a, b, c1, c2 = 100, 1, 10, 30

# Both firms capacity-constrained
K1, K2 = 15, 15
```

---

## 13. Extensions

### Extension 1 — Capacity-Constrained Cournot
Each firm has a maximum production capacity K. When the unconstrained optimum exceeds K, the firm produces at its cap and the rival best-responds to the constrained quantity. Iterates until no new constraint becomes binding.

**Key result:** When both firms are tightly capped, total supply falls and market price rises above the unconstrained Cournot level — scarcity rents accrue to producers. Directly models the effect of Basel III capital requirements on bank lending rates and volumes.

### Extension 2 — Differentiated Bertrand Competition
Products are imperfect substitutes. Each firm's demand depends on its own price and the rival's price, governed by a substitutability parameter γ. As γ approaches 1 the model converges to the Bertrand paradox. As γ approaches 0 each firm behaves like a monopolist.

**Key result:** Even slight differentiation (γ < 1) restores positive profit under price competition. This quantifies the economic value of brand, product features, and switching costs — and explains why banks and insurers invest so heavily in these dimensions.

### Extension 3 — Repeated Cournot Competition
Firms interact over T periods with three strategies: static Nash (same equilibrium every period), collusive (jointly restrict output to maximise combined profit), and adaptive (best-respond to rival's last-period output). The adaptive strategy converges to the one-shot Nash equilibrium within approximately 10 periods.

**Key result:** Repeated interaction can sustain tacit collusion above the one-shot Nash outcome if firms coordinate on the collusive path — directly relevant to understanding persistent above-normal margins in banking and insurance oligopolies.

### Extension 4 — Full Welfare Analysis
Computes consumer surplus, producer surplus, total welfare, and deadweight loss for all four market structures: perfect competition, Bertrand duopoly, Cournot duopoly, and monopoly.

**Key result:**
```
Market Structure         Total Welfare    Deadweight Loss
Perfect Competition         3200.00              0.00
Bertrand Duopoly            3200.00              0.00
Cournot Duopoly             2844.44            355.56
Monopoly                    2400.00            800.00
```

Bertrand achieves first-best welfare. Cournot generates about 44% of the monopoly deadweight loss.

---

## 14. Outputs and Exports

### Charts — 10 PNG files plus 1 combined PDF

| File | Description |
|---|---|
| `01_cournot_best_response.png` | Best-response curves and Nash equilibrium intersection |
| `02_bertrand_heatmaps.png` | Profit heatmaps across all price combinations |
| `03_bertrand_undercutting.png` | Firm 1 profit vs own price for three rival price levels |
| `04_cournot_vs_bertrand_comparison.png` | Four-panel: price, quantity, profit, welfare |
| `05_sensitivity_a.png` | Sensitivity to demand intercept a |
| `06_sensitivity_b.png` | Sensitivity to demand slope b |
| `07_sensitivity_c1.png` | Sensitivity to Firm 1 marginal cost |
| `08_sensitivity_c2.png` | Sensitivity to Firm 2 marginal cost |
| `09_asymmetric_cournot.png` | Cournot outcomes across six asymmetric cost scenarios |
| `10_welfare_analysis.png` | Stacked welfare bars and demand-curve geometry |
| `oligopoly_all_charts.pdf` | All 10 charts bundled in one PDF |

### Data Tables — CSV files

| File | Contents |
|---|---|
| `cournot_equilibrium.csv` | q1*, q2*, Q*, P*, profit1, profit2 |
| `bertrand_equilibrium.csv` | p*, Q*, profit1, profit2, winner |
| `model_comparison.csv` | Full side-by-side Cournot vs Bertrand comparison |
| `sensitivity_a.csv` | Both models across range of a values |
| `sensitivity_b.csv` | Both models across range of b values |
| `sensitivity_c1.csv` | Both models across range of c1 values |
| `sensitivity_c2.csv` | Both models across range of c2 values |
| `asymmetric_scenarios.csv` | Six cost-gap scenarios under both models |
| `welfare_analysis.csv` | CS, PS, DWL, TW for all four market structures |

---

## 15. Resume Bullets

**Quantitative and Economics framing:**
- Built a complete Python simulation of Cournot and Bertrand duopoly competition, deriving Nash equilibria symbolically via SymPy and validating numerically; demonstrated that Bertrand equilibrium achieves first-best total welfare (TW = 3200) while Cournot generates a deadweight loss of 355 at baseline parameters
- Conducted full sensitivity analysis across four demand and cost parameters, producing 200+ simulated equilibria and quantifying that Cournot industry profit grows from 111 to 2978 as market size doubles while Bertrand profit remains anchored at zero throughout
- Modelled asymmetric firm competition (fintech vs incumbent) showing winner-takes-all Bertrand dynamics when cost gap exceeds zero, and gradual share reallocation under Cournot — with direct mapping to zero-fee brokerage disruption and NIM compression in banking

**Finance and Strategy framing:**
- Applied Cournot and Bertrand game-theoretic models to banking, brokerage, insurance, and fintech pricing strategy; showed that a fintech with a 10-unit cost advantage over an incumbent captures 100% market share and earns positive profit under Bertrand price competition while the incumbent earns zero
- Extended the core model with capacity constraints (Basel III analogy), product differentiation (bank brand value modelled via substitutability parameter), repeated interaction (tacit collusion dynamics), and full welfare decomposition across four market structures
- Produced 10 publication-quality visualisations including best-response curve diagrams, profit heatmaps across price grids, sensitivity line plots with shaded model gaps, and welfare geometry charts; exported as high-resolution PNG files and a combined PDF

**Academic and Research framing:**
- Designed and implemented a theory-driven simulation project studying strategic interaction under linear demand and constant marginal cost, covering symmetric and asymmetric Nash equilibria, capacity-constrained Cournot, differentiated-product Bertrand, and multi-period adaptive dynamics
- Validated the analytical Cournot equilibrium formula q* = (a − 2c1 + c2) / 3b and the Bertrand paradox p* = MC numerically and graphically; conducted 2D price-gap heatmap analysis across joint (a, c1) parameter space identifying regions of maximum competitive divergence

---

## 16. References

- Cournot, A. A. (1838). *Researches into the Mathematical Principles of the Theory of Wealth*. Translated by N. T. Bacon (1897).
- Bertrand, J. (1883). Review of Walras and Cournot. *Journal des Savants*, 67, 499–508.
- Nash, J. (1951). Non-cooperative games. *Annals of Mathematics*, 54(2), 286–295.
- Tirole, J. (1988). *The Theory of Industrial Organization*. MIT Press.
- Varian, H. R. (2014). *Intermediate Microeconomics: A Modern Approach* (9th ed.). W. W. Norton.
- Mas-Colell, A., Whinston, M. D., and Green, J. R. (1995). *Microeconomic Theory*. Oxford University Press.
- Shubik, M. (1980). *Market Structure and Behavior*. Harvard University Press.

---

## License

This project is released under the MIT License. You are free to use, adapt, and build on it with attribution.

---

## Author

Built as part of a quantitative economics and finance research portfolio.  
Feedback, issues, and forks are welcome.

> *"In theory there is no difference between theory and practice. In practice there is."*
