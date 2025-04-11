## Dataset

NLSE simulations with and without third-order-dispersion under 400 different inputs. It contains typical behaviors like soliton, breather, splitting-merging effect and Cherenkov radiations.

To download the dataset: Fan, Z. (2025). NLSE_W/WO_TOD_400samples [Data set]. Zenodo. https://doi.org/10.5281/zenodo.15164573

The governing equation describes typical soliton solutions with third-order dispersion(TOD).


## Extended Nonlinear Schrödinger Equation with Third-Order Dispersion

In our work, we consider an extended form of the nonlinear Schrödinger equation (NLSE) that includes a third-order dispersion (TOD) term to capture effects such as Cherenkov radiation. The equation is written as:

$$
i\psi_t + \psi_{xx} + i\beta\psi_{xxx} + g|\psi|^2\psi = 0,
$$

where:
- $$\psi(x,t)$$ is the complex wave function;
- $$\psi_t = \frac{\partial \psi}{\partial t}$$, $$\psi_{xx} = \frac{\partial^2 \psi}{\partial x^2}$$, and $$\psi_{xxx} = \frac{\partial^3 \psi}{\partial x^3}$$;
- $$g$$ is the nonlinearity coefficient (typically $$g = 1$$ );
- $$\beta$$ is the TOD coefficient. For the standard NLSE, we set \( \beta = 0 \); to include TOD effects (e.g., Cherenkov radiation), we use a nonzero value (e.g., $$\beta = 0.1$$).

## Soliton Solution and Initial Condition

A fundamental soliton solution of the standard NLSE (with $$\beta = 0$$) is given by

$$
\psi(x,t) = \eta\mathrm{sech}[\eta(x-2\xi t)]
\exp({i[\xi x - (\xi^2-\eta^2)t]}).
$$

where $$\eta$$ controls the amplitude and width, and $$\xi$$  represents the velocity. In the stationary case ($$\xi = 0$$), the solution simplifies to

$$
\psi(x) = \frac{A}{\cosh(W x)},
$$

where we identify $$A$$ with the amplitude and $$W$$ as the inverse width (ideally,  $$W \approx A$$).

In our data generation, we sample $$A$$ and $$W$$ from predetermined ranges (see below) such that the initial condition better reflects a recognizable soliton structure.



To use the data, copy and run the code below:

```python
import h5py
import numpy as np

# Open HDF5 file
filename = "one_soliton_TOD_dataset.h5"
with h5py.File(filename, "r") as f:
    # check the dataset
    print("Datasets in file:", list(f.keys()))
    
    # 读取各个数据集
    x = f["x"][:]      # spatial grid, size (Nx,)
    t = f["t"][:]      # temporal grid，size (Nt,)
    u0 = f["u0"][:]    # initial condition，size (num_samples, Nx)，complex numbers
    sol = f["sol"][:]  # solution，size (num_samples, Nt, Nx)，complex numbers
    params = f["params"][:]  # paras，size (num_samples, 8)，complex numbers

# check x、t、u0、sol、params variables
print("x shape:", x.shape)
print("t shape:", t.shape)
print("u0 shape:", u0.shape)
print("sol shape:", sol.shape)
print("params shape:", params.shape)
```

If you want to check the plot for the single case, use the code below:

```python
import matplotlib.pyplot as plt
import numpy as np

# case 100 is selected
plt.figure(figsize=(10, 6))
plt.imshow(np.abs(sol[100]), 
           extent=(x.min(), x.max(), t.min(), t.max()),
           aspect='auto', 
           cmap='viridis')
plt.title('Initial Condition of First Sample')
plt.xlabel('x')
plt.ylabel('|ψ(x)|')
plt.colorbar(label='|ψ(x)|')
plt.grid()
plt.show()
```
Below displays a set of typical examples for NLSE dynamics:
![NLSE/cases_11.png](https://github.com/ZhiweiFan94/PDEBase/blob/main/NLSE/cases_11.png)
