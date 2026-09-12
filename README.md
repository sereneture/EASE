# EASE: Continuous Simplex Commitment for Multi-Target Allocation and Motion Control

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Status: Under Review](https://img.shields.io/badge/Status-Under%20Review-orange.svg)]()
[![Venue: Robotics and Autonomous Systems](https://img.shields.io/badge/Venue-Robotics%20and%20Autonomous%20Systems-blueviolet.svg)]()
[![Domain: UAV Swarm Control](https://img.shields.io/badge/Domain-UAV%20Swarm%20Control-brightgreen.svg)]()
[![Dynamics: Acceleration-Bounded](https://img.shields.io/badge/Dynamics-Acceleration--Bounded%20Dynamics-informational.svg)]()
[![Scale Generalization: N=18--80](https://img.shields.io/badge/Scale%20Transfer-N%3D18%20%7C%2040%20%7C%2080-success.svg)]()

Official project repository and open-source visual evaluation suite for:

> **Continuous Simplex Commitment for Multi-Target Allocation and Motion Control**  
> *Under Review at Robotics and Autonomous Systems (Elsevier)*  
> *Authors: Wang Chen (王琛) et al.*

---

## 🌟 Research Highlights

- **Continuous Simplex Commitment Interface**: Replaces brittle discrete target assignments with continuous probability simplex dynamics $\mathbf{a}_i \in \Delta^{M-1}$. By continuously blending target-dependent guidance velocity fields $\mathbf{v}_i^{\text{des}} = \sum_{j=1}^M a_{ij} \mathbf{v}_{ij}$, the framework eliminates boundary chattering, target thrashing, and high-frequency combinatorial re-computations.
- **Count-Adaptive Standoff Formation**: Dynamically adjusts multi-target encirclement ring radii based on local target threat weights and assigned subgroup quotas ($n^*_j$), ensuring uniform chordal packing and balanced angular coverage across diverse target counts.
- **Deadlock-Free Circulation Bypass & Density-Gated Merging**: Introduces latched tangential circulation around static obstacles and foreign target exclusion zones to break collinear force deadlocks, coupled with density-gated spiral entry to guarantee rapid ring convergence without outer limit-cycle orbits.
- **Target-Core Standoff Safety Projection**: Integrates active acceleration barrier filtering that treats target entities as protected cores ($d_{\min} \ge \max(4r_{\text{body}}, 2r_{\text{body}} + V_{\max}\Delta t)$), preventing transient vehicle penetration and overshoot while preserving smooth asymptotic ring closure.
- **24-Dimensional Similitude Envelope via Active CMA-ES**: Normalizes vehicle kinematics and operational geometries through dimensionless $\Pi$-groups under similitude scaling. An offline Active CMA-ES calibration discovers globally robust envelope parameters under racing evaluations, enabling zero-shot transfer from nominal teams ($N=18, 40$) to ultra-dense large swarms ($N=80$) without re-tuning.

---

## 🌐 Synchronized Swarm Panoramas Across Evaluation Scenarios

The framework governs collective allocation and guidance across diverse swarm scales and target scenarios under planar acceleration-bounded dynamics. Below are the macro rollout evaluations on held-out benchmark scenarios:

### Scenario 1: Five-Target Count-Adaptive Encirclement ($N = 40, M = 5$)
Multi-target encirclement benchmark under non-uniform quota allocation and cluttered obstacle fields.

<p align="center">
  <img src="animations/ease_encircle_five_target_seed21.gif" alt="Scenario 1: Five-Target Count-Adaptive Encirclement (N=40, M=5)" width="80%"/>
</p>

> *(a) **Non-Uniform Quotas** ($M=5$): Self-organizing distribution satisfying target threat proportions. (b) **Dynamic Color Blending**: Triangle glyph colors continuously represent simplex commitment weights $\mathbf{a}_i$. (c) **Deadlock-Free Bypass**: Latched tangential curl routes vehicles around obstacle clusters without collinear stalls. (d) **Core Protection**: Zero target-core penetration ($d_{\min}^{\text{tar}} = 0.641\,\text{m} > 2r_{\text{body}}$).*

---

### Scenario 2: Large-Scale Ultra-Dense Encirclement ($N = 80, M = 5$)
Extreme swarm density stress test evaluating high-flux obstacle navigation, collision avoidance, and multi-ring convergence.

<p align="center">
  <img src="animations/ease_encircle_n80_seed21.gif" alt="Scenario 2: Large-Scale Ultra-Dense Encirclement (N=80, M=5)" width="80%"/>
</p>

> *(a) **High-Density Swarm** ($N=80$): High flux coordination through narrow obstacle corridors. (b) **Radial-Priority Entry**: Density-gated spiral merge guides outer vehicles into inner rings, eliminating outer circling traps. (c) **Scale-Invariant Closure**: Sustained high quota satisfaction ($Q \approx 0.749$) with zero permanent stalls and zero collisions across all 80 agents.*

---

## 🎬 Multi-Scale Trajectory Rollouts (Benchmark Scenarios)

The table below provides a side-by-side visual comparison and mechanical characterization of champion controllers discovered by EASE across the benchmark encirclement scenarios:

| Benchmark Task | Scenario Configuration | Rollout Demonstration | Emergent Physical Mechanism & Closed-Loop Performance |
| :--- | :---: | :---: | :--- |
| **Task 1: Five-Target Adaptive Encirclement**<br>*(Unequal Threat Quotas)* | $N=40$ Quadrotors<br>$M=5$ Moving Targets<br>Cluttered Obstacles<br>Held-out Seed 21 | <img src="animations/ease_encircle_five_target_seed21.gif" width="300"/><br><code>ease_encircle_five_target_seed21.gif</code> | **Smooth Simplex Commitment & Zero Thrashing**:<br>Continuous logit dynamics seamlessly split the swarm into assigned quotas ($n^* = [8, 12, 6, 14, \dots]$) without discrete switching latency. Radial-priority guidance and latched obstacle circulation safely steer quadrotors into balanced standoff orbits ($Q \approx 0.923$, zero stalls, target clearance $\ge 0.641\,\text{m}$). |
| **Task 2: Large-Scale Dense Encirclement**<br>*(High-Density Stress Test)* | $N=80$ Quadrotors<br>$M=5$ Moving Targets<br>Narrow Corridors<br>Held-out Seed 21 | <img src="animations/ease_encircle_n80_seed21.gif" width="300"/><br><code>ease_encircle_n80_seed21.gif</code> | **High-Density Deadlock-Free Ring Entry**:<br>Density-gated spiral merging and finite-time tangential bypass prevent outer-ring limit cycles and collinear force cancellation, successfully marshaling 80 quadrotors into stable, collision-free multi-target encirclement rings ($Q \approx 0.749$, $d_{\min} = 0.270\,\text{m} > 2r_{\text{body}}$, zero permanent stalls). |

---

## 📋 Method Architecture & Core Mechanisms

```text
               +-------------------------------------------------------+
               |          EASE Closed-Loop Control Architecture        |
               +-------------------------------------------------------+
                                           |
      +------------------------------------+-----------------------------------+
      |                                    |                                   |
      v                                    v                                   v
+------------------------+   +---------------------------+   +---------------------------------+
| Continuous Simplex     |   | Count-Adaptive Guidance   |   | Safety & Deadlock Bypass        |
| Commitment Dynamics    |   | Potential Fields          |   | Acceleration Filtering          |
+------------------------+   +---------------------------+   +---------------------------------+
| • State a_i in Delta   |   | • Quota-scaled radius r*  |   | • Latched obstacle circulation  |
| • Logit self-excitation|   | • Tangential/radial blend |   | • Density-gated spiral entry    |
| • Cross-agent entropy  |   | • Continuous velocity mix |   | • Protected target-core barrier |
+------------------------+   +---------------------------+   +---------------------------------+
      |                                    |                                   |
      +------------------------------------+-----------------------------------+
                                           |
                                           v
               +-------------------------------------------------------+
               |  Offline Similitude Envelope Calibration via CMA-ES   |
               |  (24-Dim Dimensionless Parameter Optimization)        |
               +-------------------------------------------------------+
```

### 1. Continuous Simplex Commitment Dynamics
Rather than assigning each vehicle $i$ to a single target $j \in \{1,\dots,M\}$, vehicle $i$ maintains a continuous commitment probability vector $\mathbf{a}_i = (a_{i1}, \dots, a_{iM})^\top \in \Delta^{M-1}$ governed by self-exciting logit dynamics:
$$\tau_a \dot{s}_{ij} = -s_{ij} + \kappa a_{ij} + U_j(t) - \beta \sum_{k \in \mathcal{N}_i} a_{kj}, \quad a_{ij} = \frac{\exp(s_{ij})}{\sum_{m=1}^M \exp(s_{im})}$$
This continuous coupling guarantees that velocity commands $\mathbf{v}_i^{\text{des}} = \sum_{j=1}^M a_{ij} \mathbf{v}_{ij}$ change smoothly across operational regimes, entirely avoiding chattering and decision thrashing.

### 2. Count-Adaptive Guidance & Protected Target Standoff
For multi-target encirclement, the nominal standoff ring radius scales automatically with subgroup size:
$$r^*_j = \max\left(r_{\text{star}}, \frac{d_{\text{sep}}}{2\sin(\pi / n_j^*)}\right)$$
This geometric adaptation guarantees uniform angular spacing along the perimeter. To prevent transient overshoot through target centers during rapid convergence, a protected core barrier enforces $d_{ij} \ge \max(4r_{\text{body}}, 2r_{\text{body}} + V_{\max}\Delta t)$ through safe acceleration projection.

### 3. Non-Degenerate Bypass & Deadlock-Free Ring Entry
- **Latched Circulation**: Adds an orthogonal curl component ($\mathbf{n}^\perp$) to obstacle and foreign-target repulsion fields, breaking collinear equilibria where attractive and repulsive forces balance. The circulation side is latched upon entry to prevent high-frequency sign flips.
- **Density-Gated Merging**: Employs radial-priority guidance when local density is low, only activating a bounded tangential merge component when radial progress is temporarily blocked by inner-ring agents, preventing outer limit-cycle orbits.

### 4. 24-Dimensional Similitude Envelope via Active CMA-ES
Kinematics, sensing bounds, and field geometries are mapped to a 24-dimensional dimensionless vector $\bm{\Pi} \in \mathbb{R}^{24}$ invariant under physical similitude scaling. An offline Active CMA-ES calibrates this envelope under randomized multi-scenario evaluations, generating policies that transfer directly across swarm scales without re-tuning.

---

## 🔬 Experimental Reproducibility & Benchmark Evidence

The closed-loop framework is verified across multiple benchmark configurations with matched evaluation parameters:

| Metric / Attribute | Five-Target Encirclement ($N=40, M=5$) | Dense Swarm Encirclement ($N=80, M=5$) |
| :--- | :---: | :---: |
| **Swarm Size ($N$)** | 40 Quadrotors | 80 Quadrotors |
| **Target Count ($M$)** | 5 Maneuvering Targets | 5 Maneuvering Targets |
| **Target Quota Distribution** | $n^* = [8, 12, 6, 14, \dots]$ | $n^* = [12, 18, 12, 14, 24]$ |
| **Quota Satisfaction ($Q$)** | **$0.923$** | **$0.749$** |
| **Minimum Vehicle Clearance ($d_{\min}$)** | $0.488\,\text{m}$ ($> 2r_{\text{body}}$) | $0.270\,\text{m}$ ($> 2r_{\text{body}}$) |
| **Target Core Clearance ($d_{\min}^{\text{tar}}$)** | $0.641\,\text{m}$ (Safe Standoff) | $0.458\,\text{m}$ (Safe Standoff) |
| **Permanent Deadlock / Stall Count** | **0** | **0** |
| **Terminal Outer-Ring Offsets** | **0** | **0** |

---

## 📂 Repository Organization

```text
├── animations/                              # High-resolution trajectory rollouts
│   ├── ease_encircle_five_target_seed21.gif # Five-target encirclement demonstration
│   ├── ease_encircle_n80_seed21.gif         # Large-scale N=80 encirclement demonstration
│   └── README.md                            # Animation specs, resolutions, and frame metadata
├── .gitignore                               # Strict ignore rules excluding local manuscripts and raw code
├── LICENSE                                  # MIT License
├── README.md                                # Project documentation and showcase page
└── upload_to_github.ps1                     # One-click deployment script
```

---

## 📢 Availability Note

> **Notice**: The complete algorithmic source code implementation (`code/`), parameter calibration pipelines, and the full manuscript (`paper/`) are currently under peer review. They will be fully open-sourced in this repository upon official publication.

---

## 📜 Citation

If you find this work, visual benchmarks, or control framework useful in your research, please cite:

```bibtex
@article{wang2026ease,
  title={EASE: Continuous simplex commitment for multi-target allocation and motion control},
  author={Wang, Chen and collaborators},
  journal={Robotics and Autonomous Systems},
  year={2026},
  note={Under Review}
}
```

---

## 📄 License

This repository and its visual media assets are licensed under the [MIT License](LICENSE).
