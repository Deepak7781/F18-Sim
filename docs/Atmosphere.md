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
