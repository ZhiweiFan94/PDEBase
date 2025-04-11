NLSE simulations with and without third-order-dispersion under 400 different inputs. It contains typical behaviors like soliton, breather, splitting-merging effect and Cherenkov radiations.

To download the dataset: Fan, Z. (2025). NLSE_W/WO_TOD_400samples [Data set]. Zenodo. https://doi.org/10.5281/zenodo.15164573


To use the data, copy and run the code below:

```python
import h5py
import numpy as np

# 打开 HDF5 文件（只读模式）
filename = "one_soliton_TOD_dataset.h5"
with h5py.File(filename, "r") as f:
    # 查看文件中有哪些数据集
    print("Datasets in file:", list(f.keys()))
    
    # 读取各个数据集
    x = f["x"][:]      # 空间网格，形状 (Nx,)
    t = f["t"][:]      # 时间序列，形状 (Nt,)
    u0 = f["u0"][:]    # 初始条件，形状 (num_samples, Nx)，复数数组
    sol = f["sol"][:]  # 全时域解，形状 (num_samples, Nt, Nx)，复数数组
    params = f["params"][:]  # 随机参数，形状 (num_samples, 8)，复数数组

# 用 x、t、u0、sol、params 进行后续处理或绘图
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

![Example](NLSE/cases_11.png)
