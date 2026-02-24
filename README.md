# Bounding Spectral Features by Physical Reality  
### A Multi-Layered UAV Anti-Spoofing Framework

> **Disclaimer**  
> This repository contains only publicly shareable materials.  
> The associated paper is currently under submission.  
> Therefore, we provide:
> - Public / synthetic data only  
> - Non-confidential outputs and demonstrations  
> - No proprietary datasets or reviewer-sensitive content  

---

## Overview

This project presents a **physics-constrained anti-spoofing framework** for radar-based UAV detection.

Goal:

- Accept **genuine airborne targets** (real drones, helicopters)  
- Reject **deceptive targets** (fake drones, spectral camouflage)

Instead of relying purely on machine learning, the system verifies whether a radar micro-Doppler signature is **physically plausible**.

---

## Key Idea

A real rotor system obeys strict physical laws:

- Harmonic structure  
- Smooth motion (bounded acceleration)  
- Geometric consistency in the spectrogram  
- Phase coherence between harmonics  

Spoofed signals may mimic appearance, but typically fail to satisfy **all constraints simultaneously**.

---

## Pipeline Summary

The framework operates in five stages:

1. **Multi-Order STFRFT Analysis**  
   Enhances time–frequency concentration for chirp-like rotor signals.

2. **CFAR Detection & Mode Extraction**  
   Identifies statistically significant spectral components.

3. **Hodge–Helmholtz Decomposition (HTS)**  
   Measures rotational topology consistency.

4. **Physics-Informed Spline Optimization**  
   Enforces smooth, inertia-consistent trajectories.

5. **Phase Coherence Verification**  
   Validates harmonic locking from a common rotor source.

Each stage tests a **different physical property**.

---

## Physical Signal Interpretation

Rotor blades induce periodic phase modulation in radar echoes.

Practical consequence:

- Energy appears at harmonic frequencies  
- Harmonics are phase-locked  
- Spectrogram structure is cyclic and smooth  

A genuine rotor signature is therefore not just "bright lines", but a **coherent dynamical system**.

---

## Why STFRFT Instead of STFT?

Standard STFT suffers from fixed resolution and energy spreading.

STFRFT (Short-Time Fractional Fourier Transform):

- Rotates the time–frequency plane  
- Aligns with chirp-like components  
- Produces sharper energy concentration  

Multi-order analysis further prevents missing components due to order mismatch.

---

## Role of CFAR

CFAR (Constant False Alarm Rate):

- Computes local noise statistics  
- Applies adaptive thresholds  
- Suppresses background noise  

Result: robust peak detection under varying SNR.

---

## Geometric Validation via HHD

The spectrogram is interpreted as a 2D field.

Hodge–Helmholtz Decomposition separates:

- Gradient-like variations  
- Rotational (curl) structures  
- Harmonic residuals  

**Hodge Trust Score (HTS):**

- High HTS → coherent rotational topology  
- Low HTS → irregular / inconsistent structure  

Spoofed overlays often increase gradient noise and reduce rotational dominance.

---

## Physics-Based Trajectory Check

Extracted frequency tracks must resemble **physically feasible motion**.

Constraints applied:

- Smooth velocity  
- Bounded acceleration  
- No abrupt jumps inconsistent with inertia  

Spline optimization penalizes non-physical behavior.

---

## Phase Coherence Principle

For a real rotor:

- Harmonics originate from one rotation source  
- Their phases evolve proportionally  

Spoofed mixtures:

- Combine independent sources  
- Break harmonic phase relationships  

Phase coherence metric quantifies this inconsistency.

---

## Dataset

This repository includes:

- Synthetic radar echoes  
- Physics-based simulation  
- Publicly shareable signals  

Target classes:

- Real Drone  
- Helicopter  
- Fake Drone (composite spoofing)

No proprietary datasets are included.

---

## Experimental Results (Summary)

| Metric | Performance |
|--------|-------------|
| False Positive Rate | ~0.00% |
| True Negative Rate | ~99.00% |
| Overall Accuracy | ~99.67% |

Primary rejection factors for fake drones:

- Reduced HTS  
- Poor phase coherence  
- Dynamically inconsistent trajectories  

---

## Contributions

- Physics-grounded anti-spoofing framework  
- Multi-order STFRFT enhancement  
- Geometric validation via HHD  
- Dynamics enforcement via spline optimization  
- Harmonic authentication via phase coherence  

---

## Limitations & Future Work

- Adaptive threshold refinement  
- Real radar hardware validation  
- Robustness to advanced DRFM deception  
- Multi-target and clutter scenarios  

---

## Citation

If referencing this work, please cite the associated paper  
(currently under submission).

---

## Contact

For academic collaboration or questions, please open an issue.
