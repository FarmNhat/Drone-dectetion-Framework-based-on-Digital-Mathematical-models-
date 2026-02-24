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

This project implements a physics-constrained UAV anti-spoofing framework designed to distinguish:

- Genuine airborne targets (e.g., real drones, helicopters)  
- Deceptive / spoofed targets (fake drones, spectral camouflage)

Unlike purely data-driven classifiers, this approach embeds physical laws of rotor motion directly into the signal processing pipeline.

The key idea:

> Authentic micro-Doppler signatures must obey physical constraints  
> (harmonic structure, geometric consistency, smooth dynamics, phase coherence)

Spoofed signals often fail to satisfy these simultaneously.

---

## Core Concept

Traditional ML-based detection can be fooled by carefully synthesized signals.  
This framework instead verifies whether observed radar signatures are:

- Physically plausible  
- Geometrically consistent  
- Dynamically feasible  
- Phase-coherent  

---

## Pipeline Architecture

The detection system consists of five stages:

1. Multi-Order STFRFT Analysis  
2. CFAR Detection & Time–Frequency Mode Decomposition  
3. Hodge–Helmholtz Decomposition (HTS)  
4. Physics-Informed Spline Optimization  
5. Phase Coherence Verification  

---

## Mathematical Foundations

### 1. Rotor Micro-Doppler Signal Model

A rotating blade induces sinusoidal phase modulation:

\[
s(t) = A(t)\, e^{j\beta \sin(\omega t)} + n(t)
\]

Where:

- \( \omega \): rotor angular velocity  
- \( \beta \): modulation index (depends on blade radius & wavelength)

Using Jacobi–Anger expansion:

\[
e^{j\beta \sin(\omega t)} =
\sum_{k=-\infty}^{\infty} J_k(\beta) e^{jk\omega t}
\]

This reveals the harmonic structure and phase-locking behavior.

Implication:  
A genuine rotor signature is not merely a set of frequencies but a coherent harmonic system.

---

### 2. STFRFT (Short-Time Fractional Fourier Transform)

Rotor signatures resemble local chirps (LFM signals):

\[
x(t) = A e^{j2\pi(f_0 t + \frac{k}{2}t^2)}
\]

STFT limitation → energy spreading.

FRFT interprets transform as rotation in the time–frequency plane:

\[
\alpha = p \frac{\pi}{2}
\]

STFRFT:

\[
\text{STFRFT}_x(t,u) =
\int x(\tau) w(\tau-t) K_\alpha(u,\tau) d\tau
\]

Benefits:

- Better energy concentration  
- Chirp alignment  
- Improved detectability at low SNR  

---

### 3. Multi-Order Analysis

Multiple fractional orders \( \{\alpha_i\} \):

\[
S(t,u,\alpha_i) = |X_{\alpha_i}(t,u)|^2
\]

Advantages:

- Captures diverse chirp rates  
- Avoids order mismatch  

---

### 4. CFAR Detection

Adaptive thresholding:

\[
S(t,u,\alpha_i) > \gamma \hat{N}(t,u,\alpha_i)
\]

Purpose:

- Controls false alarms  
- Suppresses noise/interference  

---

### 5. Hodge–Helmholtz Decomposition (HHD)

Spectrogram → vector field:

\[
V = (\partial_t S, \partial_f S)
\]

Decomposition:

\[
V = \nabla \phi + \nabla^\perp \psi + h
\]

Energy components:

\[
E_{total} = E_{grad} + E_{rot} + E_{harm}
\]

Hodge Trust Score (HTS):

\[
HTS = \frac{E_{rot}}{E_{total}}
\]

Interpretation:

- High HTS → coherent rotational topology  
- Low HTS → irregular / spoofed structure  

---

### 6. Physics-Informed Spline Constraint

Trajectory smoothness:

\[
E_1 = \sum (f[n+1] - f[n])^2
\]

Curvature / acceleration penalty:

\[
E_2 = \sum (f[n+1] - 2f[n] + f[n-1])^2
\]

Physical constraint:

\[
E_{phys} = \sum \left(\frac{|a[n]|}{a_{max}}\right)^2
\]

Optimization:

\[
\min_f (E_{total} + \lambda E_{phys})
\]

Effect:

- Enforces inertia-consistent motion  
- Rejects abrupt non-physical jumps  

---

### 7. Phase Coherence Check

For harmonics \( m, n \):

\[
\Delta_{m,n}(t) =
\frac{\Phi_m(t)}{m} -
\frac{\Phi_n(t)}{n}
\]

Coherence metric:

\[
C_{phase} =
\frac{1}{T} \sum |\Delta_{m,n}(t) - \bar{\Delta}_{m,n}|^2
\]

Meaning:

- Genuine rotor → constant phase relationship  
- Spoofed mixture → incoherence  

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

No proprietary or restricted datasets are included.

---

## Key Results (Summary)

| Metric | Performance |
|--------|-------------|
| False Positive Rate | ~0.00% |
| True Negative Rate | ~99.00% |
| Overall Accuracy | ~99.67% |

Fake drones fail primarily due to:

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

- Threshold adaptation for edge cases  
- Real radar hardware validation  
- Robustness against advanced DRFM deception  
- Multi-target & clutter scenarios  

---

## Citation

If referencing this work, please cite the associated paper  
(currently under submission).

---

## Contact

For academic collaboration or questions, please open an issue.
