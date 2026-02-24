# Bounding Spectral Features by Physical Reality - A Multi-Layered UAV Anti-Spoofing Framework
 
> **Disclaimer**  
> This repository contains only publicly shareable materials because the associated paper is currently under submission.  
> Therefore, we provide:
> - Public / synthetic data only  
> - Outputs and demonstrations  
> - Input data (mathematical-based generated)

Authors: 

Le Thanh Binh - Computer Engineering - K23 HCMUT

Pham Minh Nhat - Computer Engineering - K23 HCMUT

Our respitory (will be made public after our paper got accepted): https://github.com/Mouse2204/MicroDoppler

---

## 1. Overview

This project implements a **multi-layered radar anti-spoofing framework** designed to distinguish:

- Genuine airborne targets (real drones, helicopters)  
- Deceptive targets (fake drones, spectral camouflage)

The system is motivated by a critical limitation of many modern detection methods:

> High-accuracy classifiers can still be fooled by carefully synthesized micro-Doppler signatures.

Instead of depending purely on pattern recognition, this framework evaluates whether an observed signal is **consistent with physical rotor dynamics**.

---

## 2. Problem Motivation

Traditional UAV detection techniques often rely on:

- Radar Cross Section (RCS)
- Acoustic signatures
- Machine learning classification

However:

- Small drones, birds, and spoofed targets can exhibit overlapping features  
- Deep learning models may accept signals that look correct but are **physically impossible**

Recent advances in **micro-Doppler deception** show that attackers can generate signals that mimic drone-like spectra.

This raises an important question:

> Can we verify not just “how a signal looks”, but “whether it obeys real-world physics”?

---

## 3. Core Principle

Real rotor systems obey strict constraints:

- Harmonic structure from periodic blade motion  
- Smooth temporal evolution due to inertia  
- Coherent geometric patterns in the spectrogram  
- Phase consistency across harmonics  

Spoofed signals may imitate parts of this behavior, but usually fail to satisfy **all constraints simultaneously**.

The framework therefore treats detection as a **physical consistency verification problem** rather than a purely statistical classification task.

---

## 4. Pipeline Architecture

The proposed system consists of five sequential stages:

1. **Multi-Order STFRFT Analysis**  
2. **CFAR Detection & Time–Frequency Mode Decomposition**  
3. **Hodge–Helmholtz Decomposition (HTS)**  
4. **Physics-Informed Spline Optimization**  
5. **Phase Coherence Verification**

Each stage validates a different physical or structural property of the signal.

---

## 5. Stage Descriptions

### Stage 1 – Multi-Order STFRFT

Rotor-induced micro-Doppler signatures are highly non-stationary and resemble **chirp-like components**.

Limitations of STFT:
- Fixed resolution
- Energy spreading
- Poor concentration for rapidly varying signals

Solution:
- STFRFT rotates the time–frequency plane
- Aligns with chirp trajectories
- Produces sharper, high-contrast spectral ridges

Why multi-order?
- Real rotor systems contain multiple components
- A single fractional order may not optimally align all structures
- Multi-order analysis prevents loss of information

Result:
- Improved detectability
- Enhanced robustness to masking and noise

---

### Stage 2 – CFAR Detection & Mode Extraction

After STFRFT, the spectrogram is normalized using **CFAR (Constant False Alarm Rate)**.

Purpose:
- Adaptive thresholding based on local noise estimates
- Stable false alarm behavior across varying SNR
- Suppression of background clutter

Following detection:
- Time–Frequency Mode Decomposition (TFMD) extracts dominant ridges
- Enables estimation of rotor parameters (e.g., periodicity, RPM)

Result:
- Clean structural representation
- Reduction of noise-induced artifacts

---

### Stage 3 – Hodge–Helmholtz Decomposition (HTS)

Instead of treating the spectrogram as a simple image, it is interpreted as a **2D field**.

Hodge–Helmholtz Decomposition separates:

- Gradient-like components (irregular variations)
- Rotational/curl components (cyclic structures)
- Harmonic residuals

Physical interpretation:

- Genuine rotor motion → strong rotational topology
- Spoofed overlays → increased gradient irregularities

**Hodge Trust Score (HTS):**

- Measures dominance of rotational energy
- High HTS → coherent rotor-like topology
- Low HTS → structural inconsistency

Result:
- Geometric validation of rotor dynamics

---

### Stage 4 – Physics-Informed Spline Optimization

Extracted frequency trajectories must obey **mechanical inertia constraints**.

Real rotor behavior:
- Smooth velocity
- Bounded acceleration
- No abrupt discontinuities

Spline optimization:
- Penalizes excessive curvature
- Suppresses non-physical jumps
- Enforces dynamically feasible motion

Result:
- Rejects trajectories inconsistent with real-world rotor mechanics

---

### Stage 5 – Phase Coherence Verification

Rotor harmonics originate from a **single physical rotation source**.

Requirement:
- Harmonics must remain phase-locked

Spoofed mixtures:
- Combine independent sources
- Break harmonic phase relationships

Phase coherence analysis:
- Evaluates stability of harmonic phase differences
- Detects hidden inconsistencies invisible in magnitude-only spectra

Result:
- Physics-based authentication layer

---

## 6. Why This Multi-Layer Approach Works

Each stage validates an independent constraint:

| Stage | Constraint Type |
|------|----------------|
| STFRFT | Chirp / spectral alignment |
| CFAR + TFMD | Statistical significance / structure |
| HHD (HTS) | Geometric rotational topology |
| Spline | Dynamic / inertia consistency |
| Phase | Harmonic coherence |

For a spoofed signal to succeed, it must simultaneously satisfy:

- Spectral plausibility  
- Geometric consistency  
- Dynamic feasibility  
- Phase coherence  

In practice, this requires reproducing **true rotor physics**, not just spectral appearance.

---

## 7. Dataset

This repository includes:

- Physics-based synthetic radar echoes  
- Controlled SNR conditions  
- Publicly shareable simulation data  

Target categories:

- Real Drone  
- Helicopter  
- Fake Drone (composite spoofing)

No proprietary or restricted datasets are used.

---

## 8. Experimental Performance (Summary)

Observed results:

- Near-zero false positives on genuine targets  
- ~99% rejection of fake drones  
- Overall accuracy ≈ 99.7%

Key rejection indicators for deceptive signals:

- Reduced Hodge Trust Score  
- Degraded phase coherence  
- Dynamically inconsistent trajectories  

Additionally, the pipeline provides **interpretable diagnostics**, identifying likely deception mechanisms.

---

## 9. Contributions

This work introduces:

- A physics-constrained UAV anti-spoofing framework  
- Multi-order STFRFT for adaptive chirp concentration  
- Geometric validation using Hodge–Helmholtz Decomposition  
- Dynamics enforcement via spline optimization  
- Harmonic authentication through phase coherence  

The framework emphasizes **physical interpretability** over black-box decision making.

---

## 10. Limitations & Future Work

Planned extensions include:

- Adaptive threshold calibration  
- Validation with real radar hardware  
- Robustness to advanced DRFM deception  
- Multi-target and cluttered environments  

---

## 11. Citation

If referencing this work, please cite the associated paper  
(currently under submission).

