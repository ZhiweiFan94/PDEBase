NLSE simulations with and without third-order-dispersion under 400 different inputs. It contains typical behaviors like soliton, breather, splitting-merging effect and Cherenkov radiations.

To download the dataset: Fan, Z. (2025). NLSE_W/WO_TOD_400samples [Data set]. Zenodo. https://doi.org/10.5281/zenodo.15164573


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
