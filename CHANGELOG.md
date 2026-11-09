# Changelog / revision notes

## v3: Module 5 Greeks extension
- **Greeks (notebook Section 10):** delta, gamma and theta read from the v2 lattice nodes; vega and rho from central-difference repricing (σ ± 1 vol point, r ± 10 bp). All use the same inputs, model and valuation date as the reported $49.05 value. Units: delta and gamma per $1, theta per year and per calendar day, vega and rho per 1.00 and per 1 point. Per-share and per-contract (×100) values are reported separately.
- **Validation (Section 11):** independent central finite differences (S ± 1%, valuation date + 1 day, σ ± 0.5 point, r ± 5 bp). All are within tolerance (largest relative difference 0.4%). A bump-size stability table shows lattice noise for bumps under 0.5%. A closed-form European benchmark on the escrowed spot explains the differences through the early-exercise right.
- **Approximations (Section 12):** delta-only vs delta-gamma vs full repricing for −20% to +20% moves; multi-factor (Δ, Γ, vega, θ, ρ) estimates vs full repricing for small, moderate and large combined shocks.
- **Visualizations (Section 13, `docs/greeks.html`):** Plotly charts of delta (three maturities), gamma, vega vs price and vs volatility, theta vs price and vs time to expiration, the approximation comparison and value vs stock price, with spot and strike marked. `docs/index.html` links to the new page.
- **Interpretation, checks and memo (Sections 14–16):** risk profile in contract terms (delta hedge and rebalancing), 12 Module 5 checks, the integrated decision memo and an AI-use disclosure.

## v2: model improvement (discrete dividends)
- **Change:** replaced the continuous 2.45% dividend yield with three dated $3.60 cash dividends (Dec 1 2026 declared; Mar 1 and Jun 1 2027 estimated) using an escrowed-dividend CRR lattice (`crr_discrete`, notebook Section 9). New input file: `data/dividends.csv`.
- **Why it is better:** LMT pays fixed quarterly cash dividends, and three ex-dates fall inside the option's life. For an American put, the timing of those cash drops changes both the value and the early-exercise decision. A smooth yield cannot capture either effect.
- **Effect:** CRR value $48.33 (v1) → $49.05 (v2). The gap to the $50.15 market midpoint narrows from $1.82 to $1.10, and the v2 value now sits inside the $48.70–$51.60 bid-ask range. The early-exercise premium falls from $0.60 to $0.50.
- **Also added:** American-exercise convergence (25–1,000 steps, N/N+1 averaging), implied volatility backed out of the bid/mid/ask with the v2 lattice, an analyst-horizon alignment warning (12-month targets vs 0.60-year option) with a disclosed horizon-scaled alternative, and new checks (American ≥ European, put ≥ intrinsic, p*, bid ≤ ask, decimal scaling).
- **Unchanged:** the template CRR function, the validation assertions, the workflow and `requirements.txt`. The v1 results are still produced and exported.

## v1: initial model
- Course template run on real LMT inputs (spot, listed put, Treasury rate, implied volatility, 15 dated analyst targets).
- One template edit: blank DCF/comps inputs are exported as `null` (not `0`), and the dashboard shows "Pending" instead of plotting $0.
