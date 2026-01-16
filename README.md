# F/A-18 Low–Angle-of-Attack Flight Dynamics Simulation (Simulink)

## Overview

This repository contains a **six-degrees-of-freedom (6-DOF) nonlinear flight dynamics simulation** of the **F/A-18 aircraft**, implemented in **MATLAB/Simulink**.  
The model is specifically developed for **low angle-of-attack (low-AoA) flight regimes**, where the aircraft aerodynamics can be reasonably approximated using polynomial and linear aerodynamic derivatives.

The primary objective of this project is to provide a **control-oriented and analysis-friendly simulation framework** suitable for:
- Aircraft trimming
- Linearization
- Stability and control analysis
- Flight control system (FCS) development
- Academic and educational studies in flight dynamics

---

## Modeling Scope and Assumptions

### Flight Regime
- Valid for **low angle of attack**
- No deep-stall or post-stall aerodynamics
- No high-AoA vortex-dominated effects

### Aerodynamic Modeling
- Aerodynamic coefficients are modeled using **polynomial fits and linear coupling terms**
- Aerodynamic data is sourced from:

> **Sinha, N. K., & Ananthkrishnan, N.**  
> *Advanced Flight Dynamics with Elements of Flight Control*

This ensures the model remains **physically interpretable and mathematically tractable**, making it suitable for trimming and linearization in Simulink.

---

## Aircraft Physical Parameters

The following parameters correspond to the F/A-18 configuration used in the simulation:

| Quantity | Symbol | Value | Units |
|--------|--------|-------|-------|
| Aircraft mass | m | 15118.35 | kg |
| Wing span | b | 11.405 | m |
| Mean aerodynamic chord | c | 3.511 | m |
| Wing planform area | S | 37.16 | m² |
| Roll moment of inertia | Ixx | 31181.88 | kg·m² |
| Pitch moment of inertia | Iyy | 205113.07 | kg·m² |
| Yaw moment of inertia | Izz | 230400.22 | kg·m² |
| Maximum engine thrust | Tmax | 96000 | N |

### Inertia Tensor Assumptions

The product of inertia \( I_{xz} \) is not provided in the reference text.
For the low-angle-of-attack, symmetric F/A-18 configuration considered in this
simulation, the aircraft is assumed to be mass-symmetric about the body
\( x\text{-}z \) plane. Therefore,

Ixz = 0

This assumption is standard in control-oriented flight dynamics models and is
consistent with the formulations in Sinha & Ananthkrishnan.

---

## Forces and Moments Representation

The simulation computes **external forces and moments** acting on the aircraft from:

### Aerodynamics
- Lift coefficient (CL)
- Drag coefficient (CD)
- Side-force coefficient (CY)
- Rolling moment coefficient (Cl)
- Pitching moment coefficient (Cm)
- Yawing moment coefficient (Cn)

These coefficients are functions of:
- Angle of attack (alpha)
- Sideslip angle (beta)
- Control surface deflections (aileron, elevator, rudder)

### Propulsion
- Thrust modeled using a **generic, control-oriented thrust model**
- Suitable for trim and flight-control studies
- Engine spool dynamics and afterburner effects are neglected

---

## Coordinate Frames and Equations of Motion

- Body-fixed reference frame
- North–East–Down (NED) inertial frame
- Standard **Newton–Euler rigid-body equations of motion**
- Euler angles used for attitude representation

The model structure allows direct integration with:
- State-space representations
- Linearized plant models
- Control law architectures (PID, LQR, etc.)

---

## Intended Applications

This simulation framework is intended for:

- Aircraft trimming and equilibrium analysis
- Linearization and small-disturbance modeling
- Flight control system design
- Academic teaching and learning
- Research-oriented flight dynamics experimentation

---

## Limitations

This model does **not** include:
- High-angle-of-attack aerodynamics
- Post-stall or departure dynamics
- Flexible body effects
- Engine spool dynamics
- Inlet distortion or afterburner modeling

As such, it should **not** be used for:
- High-fidelity performance prediction
- High-AoA maneuvering or departure studies
- Real-time pilot-in-the-loop certification simulations

---

## Software Requirements

- MATLAB (R2021a or later recommended)
- Simulink
- Simulink Control Design (for trimming and linearization)

---

## References

1. Sinha, N. K., & Ananthkrishnan, N.  
   **Advanced Flight Dynamics with Elements of Flight Control**  
   CRC Press

2. Stevens, B. L., Lewis, F. L., & Johnson, E. N.  
   **Aircraft Control and Simulation**  
   Wiley

---

## Author & Motivation

This project is developed as part of an **advanced flight dynamics and control study**, with emphasis on:
- Physical intuition
- Mathematical clarity
- Control-oriented modeling

The goal is not maximum fidelity, but **maximum insight**.
