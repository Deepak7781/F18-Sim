# Atmospheric Library

## International Standard Atmosphere

The International Standard Atmosphere (ISA) is a standardized model of Earth's atmosphere used in aerospace engineering, aviation, and simulation to predict atmospheric properties (temperature, pressure, and density) as a function of altitude. It provides a consistent reference for aircraft performance calculations, engine design, and flight simulations, assuming a static, non-varying atmosphere without weather disturbances.

Developed by the International Civil Aviation Organization (ICAO) and standardized in documents like the U.S. Standard Atmosphere (1976), the ISA divides the atmosphere into layers based on temperature gradients (lapse rates). The model starts at sea level and extends up to ~32 km (stratosphere), but many simulations (like this one) focus on the troposphere (0–11 km), where most aircraft operate.

The ISA model is fundamental for:
- Aircraft performance calculations
- Flight dynamics and control simulations
- Sensor modeling (barometer, air data systems)
- Propulsion and aerodynamic force estimation

In this model:

- The atmosphere is assumed hydrostatic
- Air behaves as an ideal gas
- Vertical temperature variation follows a piecewise-linear profile

### ISA - Equations

#### Fundamental Assumptions

- Hydrostatic Equilibrium

$$
    \frac{dP}{dh} = -\rho g
$$

- Ideal gas law

$$
    PV = \rho R T
$$

#### Temperature Profile

For any atmospheric layer b

$$
    T(h) = T_b + L_b(h - h_b)
$$

where:
- $T_b$ - Temperature at base of layer
- $L_b$ - temperature lapse rate. (K/m)
- $h_b$ - base altitude of layer

|Layer|Altitude range|Lapse Rate|
|-----|--------------|----------|
|Troposphere|0 - 11 km| -0.0065 K/m|
|Lower startosphere| 11 - 20 km| 0|

#### Pressure Equations

- Gradient Layer ($L_b \neq 0$)

$$
    P(h) = P_b\left(\frac{T(h)}{T_b}\right)^{\frac{-g_0}{L_bR}}
$$

- Isothermal Layer ($L_b = 0$)

$$
    P(h) = P_b e^{\left(-\frac{g(h - h_b)}{RT_b}\right)}
$$

#### Density Equation

Using Ideal Gas Law

$$
    PV = \rho R T
$$

#### Speed of Sound

$$
    a(h) = \sqrt{\gamma RT  }
$$
 ---
### Complete Troposhere ISA (0 - 11 km)

#### Temperature

$$
    T(h) = T_0 + Lh
$$

#### Pressure

$$
    P(h) = P_0\left(\frac{T(h)}{T_0}\right)^{\frac{-g_0}{LR}}
$$

#### Density

$$
    \rho(h) = \rho_0 \left(\frac{T(h)}{T_0}\right)^{\frac{-g0}{LR}-1}
$$

---
### Complete Stratosphere ISA (11 - 20 km)

#### Temperature

$$
    T(h) = T_{11}
$$

#### Pressure

$$
    P(h) = P_{11}e^{-\frac{g(h - 11000)}{RT_{11}}}
$$

#### Density

$$
    \rho(h) = \rho_{11}e^{-\frac{g(h - 11000)}{RT_{11}}}
$$

### Reference Values (ISA Standard)

- $T_0$ = 288.16 K
- $P_0$ = 101325 Pa
- $\rho_0$ = 1.225 $\frac{kg}{m^3}$ 
- $g_0$ = 9.81 $m/s^2$
- R = 287 $J/kg\cdot K$
- $\gamma$ = 1.4

## Calibrated Airspeed



In aircraft flight dynamics and control systems, **airspeed** is not just one quantity.  
Different forms of airspeed are used for different purposes:

- TAS (True Airspeed) – actual speed of aircraft relative to air
- CAS (Calibrated Airspeed) – speed derived from pressure measurements
- EAS (Equivalent Airspeed) – TAS corrected for density effects

---

### Why Do We Need CAS?

#### Key idea:
**Aircraft sensors do not measure velocity directly.**  
They measure **pressure**.

### Real aircraft instruments:
- Pitot tube → **Total pressure** $P_t$
- Static port → **Static pressure** $P_s$

From these pressures, airspeed is inferred.

### Why not directly use TAS?
- TAS depends on **altitude and temperature**
- Flight envelopes, stall speeds, and limits are defined using **CAS**
- CAS remains consistent with **sea-level reference conditions**

**CAS is what pilots and flight control laws trust**

---

### Physical Background

#### Assumptions
- Air behaves as a **perfect gas**
- Flow is **isentropic**
- Specific heat ratio: $\gamma = 1.4

### Step-by-Step Theory

#### Mach Number to Total Pressure

For compressible, isentropic flow:

$$
\boxed{
\frac{P_t}{P_s}
=
\left(1+\frac{\gamma-1}{2}M^2\right)^{\frac{\gamma}{\gamma-1}}
}
$$

Where:
- $M$ = Mach number
- $P_s$ = Static pressure
- $P_t$ = Total pressure

---

#### Impact Pressure

Impact pressure is the pressure sensed by the pitot tube:

$$
\boxed{
q_c = P_t - P_s
}
$$

This is the **key measured quantity** in air-data systems.

---

#### Sea-Level Pressure Reference

CAS is defined using **standard sea-level pressure**:

$$
P_0 = 101325 \ \text{Pa}
$$

This removes altitude dependence.

---

#### Impact Pressure to CAS

Using the inverse compressible flow relation:

$$
\boxed{
V_{CAS}
=
a_0
\sqrt{
\frac{2}{\gamma-1}
\left[
\left(1+\frac{q_c}{P_0}\right)^{\frac{\gamma-1}{\gamma}} - 1
\right]
}
}
$$

Where:
- $a_0$ = Speed of sound at sea level (≈ 340.262 m/s)

## 5. Meaning of CAS (Intuition)

- CAS represents the **sea-level equivalent speed**
- Same CAS $\implies$ same **dynamic pressure**
- Same dynamic pressure ⇒ same **aerodynamic forces**

That is why:
- Stall speeds are given in CAS
- Structural limits use CAS
- Control laws use CAS


### Simulink Block Explanation

#### Input Signals
- **Mach** – from air-relative velocity
- **Pressure (Pa)** – ambient static pressure from ISA model

#### Internal Computation
1. Mach $\rightarrow$ compressibility term
2. Compute total pressure ratio
3. Compute impact pressure $q_c$
4. Normalize using sea-level pressure $P_0$
5. Convert pressure back to velocity (CAS)

### Output
- **CAS (mps)** – Calibrated Airspeed in m/s

---


