## Dataset

Burgers equation simulations with two different viscosity coefficients under 400 different inputs. This dataset contains typical behaviors such as shock formation, smooth transitions, and rarefaction waves. The localized initial conditions yield noticeable nonlinear dynamics that resemble shock-like features.

To download the dataset:  
Fan, Z. (2025). Burgers_RandomShock_400samples [Data set]. Zenodo. https://doi.org/zenodo.XXXXXXXX

The governing equation describes the viscous Burgers equation.

## Viscous Burgers' Equation

In our work, we consider the following viscous Burgers equation:

$$
u_t + u\,u_x = \nu\,u_{xx},
$$

where:
- $$u(x,t)$$ is the scalar field (e.g., velocity);
- $$u_t = \frac{\partial u}{\partial t}$$, $$u_x = \frac{\partial u}{\partial x}$$, and $$u_{xx} = \frac{\partial^2 u}{\partial x^2}$$;
- $$\nu$$ is the viscosity coefficient.

A typical localized initial condition is chosen in the form

$$
u(x,0) = \frac{U}{2}\Bigl[1 - \tanh\bigl(W(x-x_0)\bigr)\Bigr],
$$

where:
- $$U$$ determines the jump height,
- $$W$$ controls the steepness (or width) of the transition, and
- $$x_0$$ is the spatial shift which localizes the shock-like profile.

In our data generation, we sample:
- $$U$$ uniformly from the interval $$[0.8,1.2]$$,
- $$W$$ uniformly from the interval $$[0.8,1.2]$$, and
- $$x_0$$ uniformly from $$[-3,3]$$.
  
Furthermore, we generate two groups of samples:
- **Group 1:** with viscosity $$\nu = 0.01$$ (low viscosity);
- **Group 2:** with viscosity $$\nu = 0.1$$ (high viscosity).

Each group contains 200 samples (20 $$U$$ values × 10 $$W$$ values, with random $$x_0$$), forming a total of 400 samples.

## Using the Data

To use the data, copy and run the code below:

```python
import h5py
import numpy as np

# Open HDF5 file
filename = "burgers_dataset.h5"
with h5py.File(filename, "r") as f:
    # Check the dataset contents
    print("Datasets in file:", list(f.keys()))
    
    # Read each dataset
    x = f["x"][:]         # spatial grid, shape (Nx,)
    t = f["t"][:]         # temporal grid, shape (Nt,)
    u0 = f["u0"][:]       # initial condition, shape (num_samples, Nx), real numbers
    sol = f["sol"][:]     # solution, shape (num_samples, Nt, Nx), real numbers
    params = f["params"][:]  # parameters, shape (num_samples, 4): [U, W, x0, nu]

# Check the shapes of the arrays
print("x shape:", x.shape)
print("t shape:", t.shape)
print("u0 shape:", u0.shape)
print("sol shape:", sol.shape)
print("params shape:", params.shape)
