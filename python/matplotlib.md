# Matplotlib

## 3d plot

使用`numpy`的`meshgrid` 将 x 轴和 y 轴映射到平面，再用公式求出 z 轴。

```python
import numpy as np
x = linespece(-5.12,5.12,50)
y = x
(xx,yy) = np.meshgrid(x,y)
zz = function((xx,yy))
```

为`matplotlib`导入3d坐标轴。

```python
import matplotlib.pyplot as plt
from mpl_toolkits.mplot3d import Axes3D

fig = plt.figure() # 建立2D图像
ax = fig.add_subplot(111, projection='3d') # 生成3D坐标轴
# 在 3D 坐标轴上绘图
ax.plot_surface(xx,yy,zz, rstride=1, cstride=1, cmap='rainbow')
"""
rstride : 行跨
cstride : 列跨
cmap    : 颜色图
"""
# 增加底部等高线
ax.contourf(xx,yy,zz, zdir='z', offset=-2, cmap='rainbow')
"""
zdir    : 投影方向
offset  : 投影到哪个值的平面
cmap    : 颜色地图
"""
