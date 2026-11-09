# LMT Valuation-to-Option Pricing Lab: v1 initial model

Course template applied to **Lockheed Martin (LMT)** and the listed **June 17, 2027 $580 American put**, valued on **November 9, 2026**.

- `valuation_option_lab.ipynb` validates the CSV inputs, builds five analyst-informed states, prices the put with a 200-step CRR lattice (continuous 2.45% dividend yield), runs the template checks and writes `docs/model_results.json`.
- `docs/index.html` renders the dashboard from that JSON.
- GitHub Actions executes the notebook before every Pages deployment.

Inputs and their sources are in `data/` (see `data/source_documentation.csv`). The DCF and comparable-company values come from my earlier LMT valuation.
