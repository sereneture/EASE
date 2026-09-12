# EASE: Swarm Trajectory Animations & Multi-Target Rollout Suite

This directory contains high-resolution animated demonstrations and evaluation rollouts for **EASE: Continuous Simplex Commitment for Multi-Target Allocation and Motion Control**.

All rollouts are generated directly from closed-loop simulations of planar acceleration-bounded swarm dynamics under continuous simplex commitment, count-adaptive standoff rings, and deadlock-free circulation guidance.

---

## 📂 Directory Structure & File Manifest

```text
animations/
├── ease_encircle_five_target_seed21.gif   # Five-target count-adaptive encirclement (N=40, M=5)
├── ease_encircle_n80_seed21.gif           # Large-scale ultra-dense encirclement (N=80, M=5)
└── README.md                              # This file
```

---

## 🎬 Detailed Specifications

### 1. Five-Target Count-Adaptive Encirclement (`ease_encircle_five_target_seed21.gif`)
- **Resolution**: $560 \times 560$ px
- **Frame Count & Timing**: 274 frames, 12 fps, ~21.9 s (including terminal hold)
- **File Size**: ~4.75 MB
- **Configuration**: $N=40$ quadrotors, $M=5$ maneuvering targets with non-uniform quota weights ($n^* = [8, 12, 6, 14, \dots]$), multiple circular obstacle fields.
- **Key Observation**:
  - Continuous logit allocation dynamics smoothly separate the swarm without discrete switching chattering.
  - Heading triangles dynamically interpolate colors matching vehicle commitment weights $\mathbf{a}_i$.
  - Protected target-core constraints prevent transient target penetration while guiding quadrotors into balanced standoff rings.

### 2. Large-Scale Ultra-Dense Encirclement (`ease_encircle_n80_seed21.gif`)
- **Resolution**: $560 \times 560$ px
- **Frame Count & Timing**: 337 frames, 12 fps, ~27.0 s (including terminal hold)
- **File Size**: ~6.73 MB
- **Configuration**: $N=80$ quadrotors, $M=5$ maneuvering targets, dense obstacle clusters, high traffic flux.
- **Key Observation**:
  - Evaluates extreme inter-agent coordination under high density and tight geometric bounds.
  - Density-gated spiral entry and radial-priority ring capture eliminate outer limit-cycle circling traps.
  - Latched obstacle circulation curl prevents collinear force cancellation, achieving stable multi-target encirclement with zero permanent stalls and strict collision-free separation.

---

## ⚙️ Reproducibility Note

Both rollout animations are deterministic evaluations on hold-out scenario seed 21 using the original frozen 24-dimensional Active CMA-ES calibrated genome (`cmaes_4target.mat`). No evolutionary re-optimization or scenario-specific hyperparameter tuning was conducted.
