# MATLAB TIP

## 限制矩阵内的值
```matlab
m(m > max) = max;
m(m < min) = min;
% 将矩阵的值限制在(min,max)内。
```
## 3D 绘图
首先用`meshgrid(x,y)`方法将x，y转换为矩阵。使用函数计算`zz`的值。
```matlab
[xx,yy] = meshgrid(x,y);
zz = func(xx,yy);
sulf(xx,yy,zz) % 绘制3D网格
% 明暗类型

shading interp % 平滑
shading faceted % 网格
shading flat % 无边框网格
colorbar  % 增加颜色条
```

## 错误停止
如果运行出现错误，matlab会自动停止，并保存相关变量
```matlab
dbstop if error
```
## 数学运算

### 取整
- `fix()` : 向零取整。(截尾取整)
- `floor()` : 向无穷小取整。(高斯取整)
- `ceil()` : 向无穷大取整。
- `round()` ： 四舍五入取整。
### 取模与取余
matlab中的取模`mod()`与取余`rem()`是不一样的。
- 取模`mod()`，使用的是`floor()`函数，向无穷小舍入。 且符号与除数相同。
- 取余`rem()`，使用的是`fix()`函数，向零方向舍入。 且符号与被除数相同。

举个栗子：
```matlab
>> mod(-1, 3) = 2; % -1/3 = -0.333, 向无穷小，商为 -1.
%% 所以 mod(-1, 3) = -1 - 3*-1 = 2
>> rem(-1, 3) = -1; % -1/3 = -0.333, 向零，商为0.
>> mod(1, -3) = -2;
>> rem(1, -3) = -1;
```

## 函数作为参数传递

如果想将函数作为参数传递可以使用`@`符号。

举个栗子：
```matlab
function [y] = funcA(a,b)
    y = a + b; 
end

function [y] = funcB(f)
    y = f(3, 2);
end

y = funcB(@funcA);
%% y = 5
```
在使用函数作为参数时，还可以设置传递函数的默认参数。
举个栗子：
```matlab
function [y] = funcC(f)
    y = f(1);
end
f = @(p1)funcA(p1,3);
y = funcC(f);
%% y = 1 + 3