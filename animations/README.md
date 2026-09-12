# EASE: Swarm Trajectory Animations & Multi-Target Rollout Suite

This directory contains the complete visual evaluation suite of high-resolution looping animations for **EASE: Continuous Simplex Commitment for Multi-Target Allocation and Motion Control**.

All rollouts are generated directly from closed-loop simulations under planar acceleration-bounded quadrotor dynamics, continuous simplex commitment allocation, count-adaptive standoff geometry, and non-degenerate circulation bypass.

---

## 📂 Directory Structure & Full 18-File Manifest

```text
animations/
│
├── # --- Center-Launch Encirclement Allocation Suite (Paper Fig. 3) ---
├── ease_encircle_eq_m2.gif          # Equal threat, M=2 (N=8,  n*=4:4)
├── ease_encircle_eq_m3.gif          # Equal threat, M=3 (N=12, n*=4:4:4)
├── ease_encircle_eq_m4.gif          # Equal threat, M=4 (N=16, n*=4:4:4:4)
├── ease_encircle_eq_m5.gif          # Equal threat, M=5 (N=20, n*=4:4:4:4:4)
├── ease_encircle_gr_m2.gif          # Graded threat, M=2 (N=12, n*=4:8)
├── ease_encircle_gr_m3.gif          # Graded threat, M=3 (N=24, n*=4:8:12)
├── ease_encircle_gr_m4.gif          # Graded threat, M=4 (N=40, n*=4:8:12:16)
├── ease_encircle_gr_m5.gif          # Graded threat, M=5 (N=60, n*=4:8:12:16:20)
│
├── # --- Expendable Interception Tactical Engagement Suite (Paper Fig. 7) ---
├── ease_impact_s1_s.gif             # Scenario 1, Scale S  (N=9,  M=6)
├── ease_impact_s1_m.gif             # Scenario 1, Scale M  (N=12, M=9)
├── ease_impact_s1_l.gif             # Scenario 1, Scale L  (N=16, M=12)
├── ease_impact_s1_xl.gif            # Scenario 1, Scale XL (N=24, M=16)
├── ease_impact_s2_s.gif             # Scenario 2, Scale S  (N=9,  M=6, complex evasive roles)
├── ease_impact_s2_m.gif             # Scenario 2, Scale M  (N=12, M=9, complex evasive roles)
├── ease_impact_s2_l.gif             # Scenario 2, Scale L  (N=16, M=12, complex evasive roles)
├── ease_impact_s2_xl.gif            # Scenario 2, Scale XL (N=24, M=16, complex evasive roles)
│
├── # --- Macro Benchmark & Extreme Density Stress Demonstrations ---
├── ease_encircle_five_target_seed21.gif  # Five-target adaptive encirclement (N=40, M=5)
├── ease_encircle_n80_seed21.gif          # Large-scale ultra-dense encirclement (N=80, M=5)
│
└── README.md                        # Complete suite documentation & specifications (this file)
```

---

## 📊 Comprehensive 18-Scenario Specification Matrix

| # | Animation Asset | Mission Type | Swarm Scale | Target Count | Quota Distribution ($n^*$) | Stride / FPS | Duration | Emergent Physical Mechanism |
| :-: | :--- | :--- | :-: | :-: | :---: | :-: | :-: | :--- |
| **1** | `ease_encircle_eq_m2.gif` | Encircle (Center-Launch) | $N=8$ | $M=2$ | $4:4$ | $10$ / $12$ | $16.7\,\text{s}$ | Symmetrical two-lobe bifurcation; zero overshoot on inner rings |
| **2** | `ease_encircle_eq_m3.gif` | Encircle (Center-Launch) | $N=12$ | $M=3$ | $4:4:4$ | $10$ / $12$ | $16.7\,\text{s}$ | Tri-directional flow splitting; uniform chordal spacing |
| **3** | `ease_encircle_eq_m4.gif` | Encircle (Center-Launch) | $N=16$ | $M=4$ | $4:4:4:4$ | $10$ / $12$ | $16.7\,\text{s}$ | Four-quadrant cluster partition; zero assignment thrashing |
| **4** | `ease_encircle_eq_m5.gif` | Encircle (Center-Launch) | $N=20$ | $M=5$ | $4:4:4:4:4$ | $10$ / $12$ | $16.7\,\text{s}$ | Pentagonal uniform capture; balanced angular variance ($\text{CV} < 0.12$) |
| **5** | `ease_encircle_gr_m2.gif` | Encircle (Center-Launch) | $N=12$ | $M=2$ | $4:8$ | $10$ / $12$ | $16.7\,\text{s}$ | Asymmetric flow splitting; proportional ring radius dilation |
| **6** | `ease_encircle_gr_m3.gif` | Encircle (Center-Launch) | $N=24$ | $M=3$ | $4:8:12$ | $10$ / $12$ | $16.7\,\text{s}$ | Graded quota self-organization without discrete auction arbitration |
| **7** | `ease_encircle_gr_m4.gif` | Encircle (Center-Launch) | $N=40$ | $M=4$ | $4:8:12:16$ | $10$ / $12$ | $16.7\,\text{s}$ | Dense multi-scale encirclement; smooth simplex commitment |
| **8** | `ease_encircle_gr_m5.gif` | Encircle (Center-Launch) | $N=60$ | $M=5$ | $4:8:12:16:20$ | $12$ / $12$ | $13.9\,\text{s}$ | Large swarm ladder split; count-adaptive standoff radius |
| **9** | `ease_impact_s1_s.gif` | Interception (Scenario 1) | $N=9$ | $M=6$ | $1:1$ contact | $3$ / $12$ | $7.0\,\text{s}$ | Nominal perimeter defense; rapid non-thrashing interception |
| **10** | `ease_impact_s1_m.gif` | Interception (Scenario 1) | $N=12$ | $M=9$ | $1:1$ contact | $4$ / $12$ | $13.8\,\text{s}$ | Medium-scale coordinated ingress defense; starburst contact points |
| **11** | `ease_impact_s1_l.gif` | Interception (Scenario 1) | $N=16$ | $M=12$ | $1:1$ contact | $5$ / $12$ | $12.0\,\text{s}$ | High-density multi-intruder pursuit; zero trajectory crossing collision |
| **12** | `ease_impact_s1_xl.gif` | Interception (Scenario 1) | $N=24$ | $M=16$ | $1:1$ contact | $6$ / $12$ | $14.5\,\text{s}$ | Fleet-scale interception corridor clearing; minimum expended pursuers |
| **13** | `ease_impact_s2_s.gif` | Interception (Scenario 2) | $N=9$ | $M=6$ | $1:1$ contact | $3$ / $12$ | $14.0\,\text{s}$ | Evasive serpentine intruders; dynamic lead-angle pursuit |
| **14** | `ease_impact_s2_m.gif` | Interception (Scenario 2) | $N=12$ | $M=9$ | $1:1$ contact | $4$ / $12$ | $14.0\,\text{s}$ | Loitering & feint intruder neutralization; obstacle circulation |
| **15** | `ease_impact_s2_l.gif` | Interception (Scenario 2) | $N=16$ | $M=12$ | $1:1$ contact | $5$ / $12$ | $13.5\,\text{s}$ | Cluttered dynamic hazard negotiation; high-rate target interception |
| **16** | `ease_impact_s2_xl.gif` | Interception (Scenario 2) | $N=24$ | $M=16$ | $1:1$ contact | $6$ / $12$ | $15.0\,\text{s}$ | Complex heterogeneous fleet defense; zero permanent vehicle stalls |
| **17** | `ease_encircle_five_target_seed21.gif` | Macro Benchmark | $N=40$ | $M=5$ | $8:12:6:14:\dots$ | $8$ / $12$ | $21.9\,\text{s}$ | Continuous logit commitment; non-uniform quotas; zero core penetration |
| **18** | `ease_encircle_n80_seed21.gif` | Ultra-Dense Stress | $N=80$ | $M=5$ | $12:18:12:14:24$ | $8$ / $12$ | $27.0\,\text{s}$ | Density-gated spiral merge; narrow corridor clearance; collision-free |

---

## 🎨 Scientific Visualization Standards

Every animation asset is rendered in strict accordance with the visual identity established in the manuscript:

1. **Airframe Representation**: Quadrotors are rendered with crisp body circles and four crosshair rotors. Triangle hulls dynamically interpolate color gradients matching instantaneous simplex commitment weights $\mathbf{a}_i \in \Delta^{M-1}$.
2. **Hazard Fields**: Static obstacles are represented as light-grey keep-out regions with crisp '+' center coordinates matching paper Fig. 3 & Fig. 7.
3. **Adaptive Formations**: Target rings dynamically expand and contract to match $r^*(n_j^*)$, ensuring uniform inter-vehicle clearance along the perimeter.
4. **Interception Impacts**: Consumed vehicles leave faded flight trails, while terminal interception points are permanently marked by clean 5-pointed collision starbursts.
5. **Standardized Coordinates**: Pure dimensionless coordinate framing with uniform grid intervals and Times New Roman typography.

---

## ⚙️ Reproducibility Guarantee

- **Encirclement Genome**: Authoritative 24-dimensional Active CMA-ES champion parameter vector (`tools/param_evo/results/cmaes_4target.mat`).
- **Interception Genome**: Evolved competitive interceptor parameter vector (`tools/param_evo/results/ras_impact_evolution.mat`).
- **Evaluation Seed**: Fixed hold-out seed 21 across all scenarios.
- **Output Standard**: $560 \times 560$ px RGB indexed GIF, 128 colors, 12 fps, infinite loop, zero MP4 artifacts.
