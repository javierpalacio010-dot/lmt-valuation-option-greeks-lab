# Changelog / revision notes

## v2: model improvement (discrete dividends)
- **Change:** replaced the continuous 2.45% dividend yield with three dated $3.60 cash dividends (Dec 1 2026 declared; Mar 1 and Jun 1 2027 estimated) using an escrowed-dividend CRR lattice (`crr_discrete`, notebook Section 9). New input file: `data/dividends.csv`.
- **Why it is better:** LMT pays fixed quarterly cash dividends, and three ex-dates fall inside the option's life. For an American put, the timing of those cash drops changes both the value and the early-exercise decision. A smooth yield cannot capture either effect.
- **Effect:** CRR value $48.33 (v1) → $49.05 (v2). The gap to the $50.15 market midpoint narrows from $1.82 to $1.10, and the v2 value now sits inside the $48.70–$51.60 bid-ask range. The early-exercise premium falls from $0.60 to $0.50.
- **Also added:** American-exercise convergence (25–1,000 steps, N/N+1 averaging), implied volatility backed out of the bid/mid/ask with the v2 lattice, an analyst-horizon alignment warning (12-month targets vs 0.60-year option) with a disclosed horizon-scaled alternative, and new checks (American ≥ European, put ≥ intrinsic, p*, bid ≤ ask, decimal scaling).
- **Unchanged:** the template CRR function, the validation assertions, the workflow and `requirements.txt`. The v1 results are still produced and exported.

## v1: initial model
- Course template run on real LMT inputs (spot, listed put, Treasury rate, implied volatility, 15 dated analyst targets).
- One template edit: blank DCF/comps inputs are exported as `null` (not `0`), and the dashboard shows "Pending" instead of plotting $0.
