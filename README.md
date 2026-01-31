# Electric_field_electrospinning
The project focuses on the characterization of the electric field in the electrospinning process in order to understand its behavior and its influence on the resulting polymeric fiber.
# Characterization of the Electrostatic Field in Electrospinning Systems Using an Adaptive Laplace Equation Solver

## Overview

This project implements a **two–dimensional electrostatic solver** based on the **Laplace equation**, designed to efficiently compute the electric potential and electric field in configurations relevant to **electrohydrodynamic processes**, such as **electrospinning**.

The main goal is to obtain a **physically consistent electric field** using **limited computational resources**, by employing:
- an **adaptive (non-uniform) spatial mesh**, and
- an **iterative Gauss–Seidel solver with Successive Over-Relaxation (SOR)**.

The resulting electric field can be directly used as input for **coupled jet dynamics models**, stability analysis, or reduced-order simulations.

---

## Mathematical Model

In the absence of volumetric charges, the electric potential \( \phi(x,y) \) satisfies the **Laplace equation**:

\[
\nabla^2 \phi = 0 \quad \text{in } \Omega \subset \mathbb{R}^2
\]

where \( \Omega \) represents the domain between an electrode and a collector.

### Boundary Conditions

- **Electrode (top boundary)**:
  \[
  \phi = V
  \]
- **Collector (bottom boundary)**:
  \[
  \phi = 0
  \]
- **Lateral boundaries**:
  \[
  \frac{\partial \phi}{\partial x} = 0
  \]

Once the potential is computed, the electric field is reconstructed as:
\[
\mathbf{E} = -\nabla \phi
\]

---

## Numerical Methodology

### Adaptive Mesh

A **non-uniform grid** is used to concentrate resolution in regions where the electric field gradient is strongest (near the electrode), while keeping a coarser resolution elsewhere.  
This significantly reduces:
- memory usage,
- computational time,

without sacrificing physical accuracy in critical regions.

### Discretization

The Laplace operator is approximated using **finite differences adapted to non-uniform spacing**, ensuring numerical consistency and stability.

### Solver

The resulting linear system is solved using:
- **Gauss–Seidel iteration**
- with **Successive Over-Relaxation (SOR)**

This approach can be interpreted as a descent method for the electrostatic energy functional and guarantees smooth convergence.

---

## Resulting Figures and Their Interpretation

### 1. Electrostatic Potential (2D)

**Figure:** *Electrostatic Potential (Laplace 2D Adaptive)*

- Shows a smooth potential distribution from the electrode (high potential) to the collector (low potential).
- The absence of oscillations confirms the harmonic nature of the solution.
- Curvature in the transverse direction reflects the geometric influence of the domain.

This validates the correct implementation of boundary conditions and discretization.

---

### 2. Axial Electric Field Along the Jet Axis

**Figure:** *Electric Field \( E_y \) along the jet axis*

- Displays the axial component of the electric field evaluated at the domain center.
- The field is strongest near the electrode and decreases monotonically toward the collector.
- This profile directly determines the electrostatic force acting on the jet.

The result is physically consistent with electrohydrodynamic theory.

---

### 3. Magnitude of the Electric Field

**Figure:** *Electric Field Magnitude*

- Highlights regions of high field intensity near the electrode and upper corners.
- Shows a progressive decay of the field through the domain.
- No artificial singularities or numerical artifacts are present.

This confirms the stability and robustness of the solver.

---

## Key Results

- The solver produces **smooth, harmonic potential fields** consistent with electrostatics.
- The electric field is **predominantly axial**, with natural transverse focusing.
- Adaptive meshing allows the simulation to run efficiently on **low-memory systems (≈ 8 GB RAM)**.
- The results are suitable for:
  - jet dynamics modeling,
  - force estimation,
  - reduced-order electrohydrodynamic simulations.

---

## Limitations

- The model assumes **electrostatic conditions** (no space charge).
- The geometry is **two-dimensional**.
- Coupling with fluid dynamics is not included in this solver.

Despite these limitations, the model provides a reliable and efficient baseline for more advanced multiphysics simulations.

---

## Possible Extensions

- Coupling with 1D or 3D jet dynamics models
- Inclusion of space charge effects (Poisson equation)
- Extension to axisymmetric or fully 3D geometries
- Automated mesh adaptation based on error estimators

---

## Author and Context

This project was developed as part of a numerical study on electrostatic field computation for electrohydrodynamic applications, emphasizing **mathematical rigor**, **numerical efficiency**, and **physical consistency**.

---

## License

This project is intended for academic and research use.
