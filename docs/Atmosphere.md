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

