# Residual Approximation Complexity in Diffusion Sampling

### Why More Accurate Solvers Can Be Harder to Correct

This repository contains the code and experiments accompanying the paper:

**Residual Approximation Complexity in Diffusion Sampling: Why More Accurate Solvers Can Be Harder to Correct**

by **Evangelos Chatzidimitriou** and **Konstantinos Tserpes**  
School of Electrical and Computer Engineering, National Technical University of Athens (NTUA), Athens, Greece.

## Overview

Numerical and generative samplers are usually compared by the error they leave relative to a high-budget reference. This encourages a natural but generally false intuition: **a more accurate baseline should also be easier to refine**.

We study the residual map

\[
R_{\Phi,B} = \Phi - B
\]

as an approximation problem in its own right and introduce a normalized residual approximation profile together with **Residual Approximation Complexity (RAC)**, the minimum correction complexity required to reach a prescribed relative residual error.

We prove exact scale invariance, an asymptotic principal-residual result for numerical approximations, threshold stability under a margin condition, and arbitrary separations between baseline accuracy and correction complexity.

A controlled 64-dimensional ODE experiment demonstrates the phenomenon under equal function-evaluation budgets: **RK4 is more than three orders of magnitude more accurate than Euler, yet its residual is substantially harder for the same correction model to approximate**. The width-32 residual-correction NMSE is:

- **Euler:** 0.1397 ± 0.0016
- **RK4:** 0.9587 ± 0.0013

The same phenomenon appears in diffusion sampling. On **CIFAR-10**, the accuracy–difficulty separation persists across:

- different training-set sizes,
- multiple corrector architectures,
- a nearly **188× parameter-capacity range**, and
- matched-compute comparisons between **DDIM, DEIS, DPM-Solver++, and UniPC**.

An external replication on **Flowers-102** recovers the inversion at moderate correction capacity while also demonstrating an important limitation: the effect is not universal across capacities.

Finally, we investigate the practical implications for compute allocation. A **50-step DDIM sampler combined with a 78-parameter residual corrector** achieves a slightly lower held-out MSE point estimate relative to a fixed DDIM-1000 reference than baseline-only DDIM-500, while requiring roughly **one tenth of the measured latency**. However, the paired bootstrap confidence interval includes zero, and LPIPS favors DDIM-500.

The practical conclusion is therefore about **reference-map fidelity and compute allocation**, rather than universal perceptual image quality.

The central message of the work is:

> **Residual magnitude is not the same as residual approximation difficulty.**

A more accurate numerical or generative baseline may produce a smaller residual while simultaneously leaving behind an error structure that is more difficult for a restricted correction family to represent.

This motivates treating the **structure of approximation error — not only its magnitude — as a first-class design variable** when constructing hybrid numerical and learned systems.