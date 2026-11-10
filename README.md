# Engineering-Constrained Agentic AI and Multi-Agent Decision Support for Mission-Critical Data Centers

**A Reproducible Simulation Study**

Companion repository for the paper published in **IEEE Access** (November 2026).

- **Author:** Raja Kumara Swamy Donthula, Senior Member, IEEE (Independent Researcher, Alpharetta, GA, USA)
- **ORCID:** [0009-0005-6061-3989](https://orcid.org/0009-0005-6061-3989)

---

## Overview

Data centers running large AI/GPU workloads must coordinate electrical power, cooling, reliability, commissioning, and safety under tight redundancy and safety constraints. This paper presents an **engineering-constrained Agentic AI / Multi-Agent System (MAS) architecture** for decision support in mission-critical data-center operations, evaluated with a simplified, physics-informed **digital-twin-style simulation**.

> **Scope note:** This work contributes a reproducible architecture and evaluation methodology. It does **not** claim validated field performance. All results come from first-pass computational simulations, and the full six-agent runtime was not built or field-validated.

## Key Contributions

- A reference architecture applying Agentic AI and MAS concepts to mission-critical data-center operations
- A domain-decomposed **six-agent model**
- A **three-level human-in-the-loop (HITL) authorization model**
- A digital-twin-style evaluation strategy for repeatable fault injection and cross-domain coordination experiments
- A reproducible experimental methodology and metric set, including a fair, constraint-matched comparator for cross-agent arbitration

## Architecture

| Agent | Domain | Role |
|---|---|---|
| **EPA** | Electrical power | Power-state analysis; constrained electrical recommendations |
| **CTA** | Cooling / thermal | Thermal monitoring and cooling optimization |
| **RFDA** | Reliability | Fault/anomaly detection and diagnosis |
| **CORA** | Commissioning | Readiness and test-sequencing (FAT/SAT/IST) support |
| **SVA** | Safety | Constraint and authorization verification |
| **ODSA** | Orchestration | Coordination, arbitration, and provenance logging |

### Human-in-the-loop authorization levels

| Level | Description |
|---|---|
| **1: Autonomous Monitoring and Reporting** | Telemetry interpretation, alerts, dashboards. No direct equipment control. |
| **2: Supervised Operational Adjustment** | Low-consequence, reversible setpoint recommendations within defined limits. |
| **3: Explicit Human Authorization** | Safety-critical actions (switching, generator transfer, ATS, UPS bypass) require explicit operator approval. |

These levels are design constructs of the framework, not categories defined by NFPA 70E, IEEE standards, or the NIST AI RMF.

## Experiments and Headline Results

Each experiment used **N = 300 matched Monte Carlo replications**, paired inference, effect sizes, and 95% bootstrap confidence intervals.

| # | Experiment | Hypothesis | Headline result | Status |
|---|---|---|---|---|
| 1 | UPS battery fault detection (RFDA, CUSUM vs. static threshold) | H1 | MTTD 56.19 h → 6.81 h (**87.9% shorter**) | Supported |
| 2 | MV feeder overload response (EPA/ODSA vs. reactive rules) | H2 | Compliance 99.2% vs. 90.0%, at the cost of 52.5% more load shed | Partially supported |
| 3 | Cooling-capacity degradation under GPU load (CTA+EPA) | H3 | **61.2% fewer** thermal-limit violation timesteps; 84.4% lower severity | Supported |
| 4 | IST / commissioning sequencing (CORA, four-arm comparator) | H4 | Completeness 97.6% vs. 61.5% for rigid manual plan (+36.1 pp) | Supported |
| 5 | Cross-agent EPA/CTA arbitration (three-arm, **exploratory**) | H5 | Residual bus-capacity violations 0.627 → 0.000 timesteps/trial vs. a fair constrained controller, at ~5.2% more compute curtailment | Scoped support |

H1–H4 were pre-specified; H5 was added after Experiments 1–4 and is labeled exploratory in the paper.

## Reproducing the Results

Per the paper's Data and Code Availability statement:

- Python with **NumPy, SciPy, and Matplotlib** only
- Scripts: `sim.py` and `make_numbers.py` (regenerates Tables V–IX, Supplementary Table S2, and Fig. 4)
- Fixed seeds: master seed `20261014`; seed families `master+1` to `master+5`
- Parameter provenance: Supplementary Table S1

```bash
python -m venv .venv
source .venv/bin/activate
pip install numpy scipy matplotlib
python make_numbers.py
```

> [Update this section to match whether the simulation code is released in this repository.]

## Limitations

- Simulated environment; **not field-validated** against physical hardware
- One representative topology; parameters are illustrative or practice-informed, not calibrated to a specific facility
- Each agent role is a single prototype component, not the full multi-model agent runtime
- The agent-trust verification mechanism was proposed but not implemented
- HITL authorization and operator-facing effectiveness were specified, not evaluated
- Cybersecurity aspects are out of scope
- The Experiment 5 benefit is close to a mechanical consequence of look-ahead timing and should not be generalized to agentic AI being superior to deterministic control

This work uses standards for engineering context only and does not warrant any specific action in real facilities. Safety-critical operations must follow site-specific electrical-safety procedures, LOTO, interlocks, and qualified-person authority.

## Citation

```bibtex
@article{donthula2026engineering,
  author  = {Donthula, Raja Kumara Swamy},
  title   = {Engineering-Constrained Agentic {AI} and Multi-Agent Decision Support for Mission-Critical Data Centers: A Reproducible Simulation Study},
  journal = {IEEE Access},

```

## Contact

Corresponding author: Raja Kumara Swamy Donthula, rajakumaraswamydonthula@gmail.com

## License

MIT 
