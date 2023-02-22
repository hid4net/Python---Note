
<h1 style="text-align:center">数据科学 - 符号数学</h1>

--------------------------------------------------------------------------------
[返回目录](outline.md)

tips:

--------------------------------------------------------------------------------

<!-- @import "[TOC]" {cmd="toc" depthFrom=1 depthTo=3 orderedList=false} -->

<!-- code_chunk_output -->

- [1. 基本信息](#-1-基本信息-)
- [2. Sympy](#-2-sympy-)
  - [2.1. 基础](#-21-基础-)
    - [2.1.1. 基本常量](#-211-基本常量-)
    - [2.1.2. 符号, 数字, 函数的定义](#-212-符号-数字-函数的定义-)
    - [2.1.3. 运算符](#-213-运算符-)
    - [2.1.4. 符号/表达式的属性和方法](#-214-符号表达式的属性和方法-)
    - [2.1.5. 打印输出](#-215-打印输出-)
  - [2.2. 内置函数](#-22-内置函数-)
  - [2.3. 表达式基本操作](#-23-表达式基本操作-)
  - [2.4. 画图](#-24-画图-)
  - [2.5. 求解方程](#-25-求解方程-)
  - [2.6. 极限](#-26-极限-)
  - [2.7. 微积分](#-27-微积分-)
  - [2.8. 级数](#-28-级数-)
  - [2.9. 常微分方程](#-29-常微分方程-)
  - [2.10. 偏微分方程](#-210-偏微分方程-)
  - [2.11. 矩阵](#-211-矩阵-)
  - [2.12. 集合](#-212-集合-)
  - [2.13. 逻辑](#-213-逻辑-)

<!-- /code_chunk_output -->

--------------------------------------------------------------------------------
# 1. 基本信息

* Sympy

--------------------------------------------------------------------------------
# 2. Sympy
详见[官方文档](https://www.sympy.org/nl/index.html)

## 2.1. 基础

### 2.1.1. 基本常量

``` python
sympy.E             # 自然常数 e
sympy.pi            # 圆周率 𝜋
sympy.I             # 虚数 i
sympy.oo            # 无穷大
sympy.nan           # 无意义
sympy.Complexes     # 复数
sympy.Reals         # 实数
sympy.Integers      # 整数
sympy.Rationals     # 分数
sympy.Naturals0     # 自然数
sympy.Naturals      # 正整数
sympy.EmptySet      # 空集 ∅
sympy.UniversalSet  # 全集 𝕌
sympy.EmptySequence # 空序列
sympy.GoldenRatio   # 黄金分割比
```

### 2.1.2. 符号, 数字, 函数的定义
* 符号 symbols, 详见 [sympy.core.symbol](https://docs.sympy.org/1.5.1/modules/core.html#module-sympy.core.symbol)
``` python
x = sympy.symbols('x')       # 指定一个符号
x,y,z = sympy.symbols('x y z')  # 指定多个符号
x,y,z = sympy.symbols(['x', 'y', 'z'])  # 指定多个符号
x1,x2,y1,y2 = sympy.symbols('x1:3 y1:3')  # 指定多个符号
x50,x51 = sympy.symbols('x5(:2)')  # 指定多个符号
x = sympy.symbols('x', integer=True, positive =True)  # 指定多个符号
f, g = symbols('f g', cls=Function)
```

* 数字 numbers, 详见 [sympy.core.numbers](https://docs.sympy.org/1.5.1/modules/core.html#module-sympy.core.numbers)
``` python
a = sympy.Float(2.3)    # 2.3
b = sympy.Rational(3,5) # 3/5
c = sympy.Integer(3)    # 3
```

* 函数 function, 详见 [sympy.core.function](https://docs.sympy.org/1.5.1/modules/core.html#module-sympy.core.function)
``` python
f = sympy.Function('F')     # 函数
g = sympy.Function('F')(x)  # 函数
f = sympy.Lambda(x, x**2)   # 函数
```

### 2.1.3. 运算符
运算符              | 说明
:-----------------: | :----------------
`+` `-` `*` `/` `=` | 常规运算符
`==`                | 两个表达式是否一样, 而不是是否相等
`sqrt`              | 不是函数, 而是运算符

### 2.1.4. 符号/表达式的属性和方法
类别     | 名称         | 说明
:------: | :----------- | :----------------
常用属性 | args         | 参数
^        | assumptions0 | 类型属性
常用方法 | evalf        | 以指定精度输出
^        | lambdify     | 与evalf类似, 以函数形式输出
^        | as_其他格式  | 转为其他格式
^        | atoms        | 返回元素
^        | is_类型      | 是否为某种类型
^        | compare      | 比较
^        | doit         | 求值
^        | dummy_eq     | ==
^        | equals       | ==
^        | has          | 是否包含某个变量
^        | subs         | 赋值 (具体值或表达式)

### 2.1.5. 打印输出
``` python
# 更好看的输出, 在jupyter中尤其有用
from sympy import init_printing
init_printing()
```
``` python
srepr(x**2) # "Pow(Symbol('x'), Integer(2))"
```

``` python
print(latex(expr)) # 将表达式转为 Latex 代码
```

## 2.2. 内置函数

类别       | 函数
:----------| :-------------
复数       | re, im, sign, Abs, arg, conjugate, polar_lift, periodic_argument, principal_branch
三角函数   | sin, cos, tan, cot, sec, csc, sinc
反三角函数 | asin, acos, atan, acot, asec, acsc, atan2
双曲函数   | sinh, cosh, tanh, coth, sech, csch
反双曲函数 | asinh, acosh, atanh, acoth, asech, acsch
近似函数   | ceiling, floor, RoundFunction, frac
指数函数   | exp, LambertW, log, ln, exp_polar
分段函数   | ExprCondPair, Piecewise
其他       | Min, Max, root, sqrt, cbrt, real_root
组合       | bell, bernoulli, binomial, catalan, euler, factorial, subfactorial, factorial2 / double factorial, FallingFactorial, fibonacci, tribonacci, harmonic, lucas, genocchi, partition, MultiFactorial, RisingFactorial, stirling,
枚举       | nC, nP, nT

* 特殊函数
    * DiracDelta
    * Heaviside
    * Singularity Function
    * Gamma, Beta and related Functions
    * Error Functions and Fresnel Integrals
    * Exponential, Logarithmic and Trigonometric Integrals
    * Bessel Type Functions
    * Airy Functions
    * B-Splines
    * Riemann Zeta and Related Functions
    * Hypergeometric Functions
    * Elliptic integrals
    * Mathieu Functions
    * Orthogonal Polynomials
    * Spherical Harmonics
    * Tensor Functions



## 2.3. 表达式基本操作
函数               | 说明
:----------------- | :-------------
expand             | 展开
expand_trig        | 三角函数展开
expand_power_exp   | 幂函数展开
expand_power_base  | 幂函数展开
expand_log         | 指数函数展开
simplify           | 化简
trigsimp           | 三角函数化简
powsimp            | 幂函数化简
factor             | 提取因数
collect            | 合并同类项
logcombine         | 合并 log
coeff              | 提取系数
cancel             | 去除公因子
together           | 去除公因子 (不消除公因子)
apart              | 部分展开
powdenest          | 用多次幂表示
Eq                 | 创建等式
Ne, Lt, Le, Gt, Ge | 创建不等式

## 2.4. 画图
使用matplotlib作为后端
* `sympy.plot()`
* `sympy.plot_parametric()`
* `sympy.plot3d()`
* `sympy.plot3d_parametric_line()`
* `sympy.plot3d_parametric_surface()`

## 2.5. 求解方程
``` python
sympy.solveset(sympy.Eq(x**3,1), x, domain=sympy.S.Reals)       # {1}
sympy.solveset(sympy.Eq(x**3,1), x, domain=sympy.S.Complexes)   # {1, -1/2 - sqrt(3)*I/2, -1/2 + sqrt(3)*I/2}
sympy.solveset(sympy.Eq(x**3 - 1,0), x, domain=sympy.S.Reals)   # {1}
sympy.solveset(sympy.Eq(x**3 - 1,0), x, domain=sympy.S.Complexes)# {1, -1/2 - sqrt(3)*I/2, -1/2 + sqrt(3)*I/2}
sympy.solveset(sympy.exp(x),x)                                  # EmptySet()
sympy.solveset(sympy.exp(x)-1,x,domain=sympy.S.Reals)           # {0}
sympy.solveset(sympy.exp(x)-1,x,domain=sympy.S.Complexes)       # ImageSet(Lambda(_n, 2*_n*I*pi), Integers)
```

``` python
sympy.solve([x+y-10, x-y-2], [x,y]) # {x: 6, y: 4}
```

## 2.6. 极限
``` python
sympy.limit(f,x,2)
sympy.limit(f,x,sympy.oo)
```

## 2.7. 微积分
* 微分
``` python
f = 1/x
sympy.diff(f,x)     # 1阶导数, -1/x**2
sympy.diff(f,x,2)   # 2阶导数, 2/x**3
sympy.diff(f,x,x)   # 2阶导数, 2/x**3
sympy.diff(f,x,4)   # 4阶导数, 24/x**5
```
* 偏微分
    * 示例1: $\dfrac{\partial ^7}{\partial x \partial y^2 \partial z^4} \mathrm{e}^{xyz}$
        ``` python
        diff(exp(x*y*z), x, y, y, z, z, z, z)
        diff(expr, x, y, 2, z, 4)
        diff(expr, x, y, y, z, 4)
        ```
    * 示例2: $\dfrac{\partial ^n}{\partial x^n} (ax+b)^m$
        ``` python
        m, n, a, b = symbols('m n a b')
        expr = (a*x + b)**m
        expr.diff((x, n))
        ```
* 积分
``` python
f = 1/x
sympy.integrate(f,x)        # 不定积分, log(x)
sympy.integrate(f, (x,1,2)) # 定积分, log(2)
h = sympy.exp(-x**2 - y**2)
sympy.integrate(h, (x,-sympy.oo, sympy.oo), (y, -sympy.oo, sympy.oo))   # 定积分, pi
```
## 2.8. 级数
``` python
expr = exp(sin(x))
expr.series(x, 0, 4)
```
> sin(x) 的前4级级数: $1 + x + \frac{x^{2}}{2} + O\left(x^{4}\right)$
## 2.9. 常微分方程
``` python
f = symbols('f', cls=Function)
diffeq = Eq(f(x).diff(x, x) - 2*f(x).diff(x) + f(x), sin(x))
dsolve(diffeq, f(x))
```
> 微分方程 $f{\left(x \right)} - 2 \dfrac{d}{d x} f{\left(x \right)} + \dfrac{d^{2}}{d x^{2}} f{\left(x \right)} = \sin{\left(x \right)}$ 的解 $f{\left(x \right)} = \left(C_{1} + C_{2} x\right) e^{x} + \dfrac{\cos{\left(x \right)}}{2}$

## 2.10. 偏微分方程

## 2.11. 矩阵

## 2.12. 集合

## 2.13. 逻辑

