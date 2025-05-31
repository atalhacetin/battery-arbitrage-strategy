# Battery Arbitrage Strategy with Mixed Integer Nonlinear Programming

This repository contains a battery trading strategy implemented using integer optimization in GEKKO. The model decides when to charge, hold, or discharge based on electricity price forecasts, while considering battery capacity, cycle limits, and degradation cost.

## Features

- Integer decision variable X[t] in {-1, 0, 1}
- Battery capacity and cycle constraints
- Profit maximization with cycle degradation cost
- Solved using GEKKO with APOPT solver

## Output

- Optimal charge or discharge actions for each time step
- Final profit value
- Printed input price vector

## Parameters

- initial_capacity: Initial energy stored in the battery (MWh)
- max_capacity: Battery storage limit (MWh)
- max_cycle: Maximum full cycles allowed
- cycle_cost: Cost per cycle (Euro)
- prices: Electricity prices for each time step

## Mathematical Formulation

**Variables**
- X_t ∈ {-1, 0, 1}: action at time t (charge, hold, or discharge)
- p_t: electricity price at time t
- E_t: state of charge at time t

**Objective**
Maximize profit over time:

    maximize ∑ (X_t * p_t - 0.5 * cycle_cost * X_t^2)

**Constraints**
- SOC update:
      E_{t+1} = E_t - ΔE * X_t

- SOC limits:
      0 ≤ E_t ≤ max_capacity

- Total cycle energy constraint:
      ∑ (0.5 * X_t^2 * ΔE) ≤ max_cycle * max_capacity

- Decision domain:
      X_t ∈ {-1, 0, 1}

This setup ensures the battery operates within capacity limits, respects a cap on cycling, and trades energy to maximize profit while considering degradation cost.
