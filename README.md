# Automated Parameter Tuning for Timing Closure in OpenROAD/OpenLane

**A Grid Search Framework on the SkyWater 130 nm PDK**

## Overview

This repository contains the paper, LaTeX source, and figures for:

> **"Automated Parameter Tuning for Timing Closure in OpenROAD/OpenLane: A Grid Search Framework on the SkyWater 130 nm PDK"**

The work presents an automated grid search framework that systematically explores the parameter space of the OpenROAD/OpenLane RTL-to-GDSII flow targeting the SkyWater 130 nm process design kit (SKY130A).

## Key Contributions

- **Python-based grid search framework** that drives the full OpenLane Docker flow without human intervention, varying clock period, core utilization, and placement density across a 6×5×3 parameter grid (90 runs per design).
- **Fault-tolerant metrics extraction pipeline** that parses OpenLane timing reports and logs WNS, TNS, post-SPEF WNS, area, cell count, critical path delay, and power to a CSV after each run.
- **Quantitative characterization** of the timing–area–power tradeoff space for the *spm* benchmark on SKY130A.
- **Open-source release** of all sweep scripts, configuration files, and raw results for full reproducibility.

## Key Results

| Frequency | Timing Closure | Best WNS |
|-----------|----------------|----------|
| 100 MHz   | ✅ All pass    | 0.0 ps   |
| 125 MHz   | ✅ All pass    | 0.0 ps   |
| 143 MHz   | ✅ All pass    | 0.0 ps   |
| 167 MHz   | ✅ All pass    | 0.0 ps   |
| 200 MHz   | ✅ All pass    | 0.0 ps   |
| 250 MHz   | ❌ All fail    | −50 ps   |

- **37.2% area reduction** by increasing core utilization from 35% to 55% at 200 MHz
- **51.6% dynamic power reduction** from 250 MHz to 125 MHz (near-linear scaling)

## Repository Contents

```
├── main.tex              # LaTeX source of the paper
├── paper.pdf             # Compiled paper (PDF)
├── fig1_framework.png    # Framework flow diagram
├── fig2_wns_freq.png     # WNS vs. frequency results
├── fig3_area_util.png    # Area vs. utilization at 200 MHz
├── fig4_power_freq.png   # Power vs. frequency scaling
└── README.md             # This file
```

## Tools & Environment

- **OpenLane** v1.0.2 (commit `ff5509f`) with SKY130A PDK
- **Standard cell library**: `sky130_fd_sc_hd` (high-density)
- **Host**: Ubuntu 22.04, Intel CPU, 16 GB RAM
- **Python** 3.8 via `subprocess.run()` for Docker orchestration

## Parameter Search Space

| Parameter | Values |
|-----------|--------|
| `CLOCK_PERIOD` | 4.0, 5.0, 6.0, 7.0, 8.0, 10.0 ns |
| `FP_CORE_UTIL` | 35%, 40%, 45%, 50%, 55% |
| `PL_TARGET_DENSITY` | 0.4, 0.5, 0.6 |

**Total configurations**: 6 × 5 × 3 = **90 runs**

## Citation

If you use this work, please cite:

```bibtex
@inproceedings{openlane_gridsearch,
  title     = {Automated Parameter Tuning for Timing Closure in OpenROAD/OpenLane: A Grid Search Framework on the SkyWater 130 nm PDK},
  author    = {[Your Full Name]},
  booktitle = {[Conference/Journal]},
  year      = {2025}
}
```

## License

This project is released as open source to support reproducible research in open-source EDA.
