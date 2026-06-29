# Numerical Solution of Radioactive Decay Kinetics Using Scilab

An undergraduate computational physics project (2014) that solves the radioactive‑decay
differential equation numerically in [Scilab](https://www.scilab.org/), validates the
solvers against the exact analytical solution, and recovers the decay constant from the
simulated data. The same ODE‑based reasoning underlies survival analysis, disease
modeling, and pharmacokinetics in modern quantitative health research.

**Live project page:** https://kgahanduke-25.github.io/radioactive-decay-scilab/

## Overview

Radioactive decay is governed by a first‑order linear ODE — the rate of decay is
proportional to the amount of material present:

```
dN/dt = -λN          (governing ODE)
N(t)  = N₀ · e^(-λt)  (analytical solution)
t½    = ln 2 / λ      (half-life)
```

Because a closed‑form solution exists, the equation is an ideal benchmark for studying how
numerical integrators behave: every approximation can be measured against exact truth.

## Methods

Two integrators are implemented and compared against the analytical solution:

- **Euler's method** (first order) — a single slope estimate per step; global error scales
  with the step size `h`.
- **Runge–Kutta (RK4)** (fourth order) — four weighted slope evaluations per step; global
  error scales with `h⁴`, tracking the analytical curve almost exactly at the same step size.

The simulated trajectory is then treated as data, and the decay constant `λ` (and half‑life
`t½`) are recovered via log‑linear regression with `polyfit`, closing the loop from model to
estimate.

## Files

| File | Description |
|------|-------------|
| `index.html` | Self‑contained project page (served via GitHub Pages). |
| `decay_kinetics.sce` | Core Scilab routine (shown on the page). |
| `README.md` | This file. |

> The Scilab source is embedded and documented in `index.html`. To run it, copy the
> `decay_kinetics.sce` block from the page into a `.sce` file.

## Running the code

1. Install [Scilab](https://www.scilab.org/download).
2. Save the routine as `decay_kinetics.sce`.
3. In the Scilab console:

   ```scilab
   exec('decay_kinetics.sce', -1);
   ```

The script computes the analytical solution, the Euler and RK4 trajectories, and the
recovered `lambda_hat` and `t_half`.

## Why it matters

The decay equation's structure — a quantity changing at a rate proportional to itself —
reappears across quantitative health research:

- **Survival analysis:** the exponential survival function `S(t) = e^(-λt)` is identical in
  form, with `λ` becoming a constant hazard rate.
- **Disease modeling:** compartmental (SIR) models are coupled ODE systems solved with the
  very integrators used here.
- **Pharmacokinetics:** first‑order drug clearance is exponential decay by another name.

This early project established the ODE‑based reasoning and parameter‑estimation habits that
carry directly into survival modeling, disease dynamics, and pharmacoepidemiology.

## Author

**Kamalakanta Gahan** — MS in Population Health Sciences (Quantitative Methods), Duke
University. Research applying survival analysis, structural‑determinant indices, and
simulation methods to cancer disparities.

*Physics → Medical Anthropology → Public Health → Population Health Sciences*
