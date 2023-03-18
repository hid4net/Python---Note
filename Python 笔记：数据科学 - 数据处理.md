
<h1 style="text-align:center">数据科学 - 数据处理</h1>

--------------------------------------------------------------------------------
[返回 Outline](outline.md)

<!-- @import "[TOC]" {cmd="toc" depthFrom=1 depthTo=3 orderedList=false} -->

<!-- code_chunk_output -->

- [1. 标准数学库](#1-标准数学库)
  - [1.1. 内建数学](#11-内建数学)
  - [1.2. 标准库 math: 基本数学](#12-标准库-math-基本数学)
  - [1.4. 标准库 decimal: 小数](#14-标准库-decimal-小数)
  - [1.5. 标准库 fractions: 分数](#15-标准库-fractions-分数)
  - [1.3. 标准库 random: 随机数](#13-标准库-random-随机数)
  - [1.6. 标准库 statistics: 统计](#16-标准库-statistics-统计)
  - [1.7. 标准库 cmath: 复数](#17-标准库-cmath-复数)
- [2. numpy](#2-numpy)
  - [2.1. 基础](#21-基础)
    - [2.1.1. N-dimensional array (ndarray)](#211-n-dimensional-array-ndarray)
    - [2.1.2. 数据类型](#212-数据类型)
    - [2.1.3. 索引](#213-索引)
    - [2.1.4. 迭代](#214-迭代)
    - [2.1.5. 标准子类](#215-标准子类)
    - [2.1.6. 日期时间和间隔](#216-日期时间和间隔)
  - [2.2. array 操作基础](#22-array-操作基础)
    - [2.2.1. 原则: 副本与视图](#221-原则-副本与视图)
    - [2.2.2. 原则: 广播](#222-原则-广播)
    - [2.2.3. 修改 array](#223-修改-array)
    - [2.2.4. ufunc](#224-ufunc)
    - [2.2.5. 函数编程](#225-函数编程)
  - [2.3. 常数](#23-常数)
  - [2.4. Numpy基本函数](#24-numpy基本函数)
    - [2.4.1. Numpy 帮助函数](#241-numpy-帮助函数)
    - [2.4.2. 排序与查找](#242-排序与查找)
    - [2.4.3. 二进制](#243-二进制)
    - [2.4.4. string](#244-string)
  - [2.5. array 数学运算](#25-array-数学运算)
    - [2.5.1. 数学函数](#251-数学函数)
    - [2.5.2. 随机数(numpy.random)](#252-随机数numpyrandom)
    - [2.5.3. 矩阵(numpy.matlib)](#253-矩阵numpymatlib)
    - [2.5.4. 线性代数(numpy.linalg 和 numpy.dual)](#254-线性代数numpylinalg-和-numpydual)
    - [2.5.5. 统计](#255-统计)
    - [2.5.6. 集合](#256-集合)
    - [2.5.7. 逻辑判断](#257-逻辑判断)
    - [2.5.8. FFT](#258-fft)
    - [2.5.9. 窗函数](#259-窗函数)
    - [2.5.10. 多项式](#2510-多项式)
    - [2.5.11. 金融](#2511-金融)
    - [2.5.12. 浮点数错误处理](#2512-浮点数错误处理)
    - [2.5.13. 其他](#2513-其他)
  - [2.6. 输入输出](#26-输入输出)
  - [2.7. C 语言接口](#27-c-语言接口)
- [3. pandas](#3-pandas)
  - [3.1. 数据结构](#31-数据结构)
    - [3.1.1. Series](#311-series)
    - [3.1.2. DataFrame](#312-dataframe)
  - [3.2. 数据的创建](#32-数据的创建)
  - [3.3. 数据类型](#33-数据类型)
    - [3.3.1. 有效的数据类型](#331-有效的数据类型)
    - [3.3.2. 查看数据类型](#332-查看数据类型)
    - [3.3.3. 更改数据类型](#333-更改数据类型)
    - [3.3.4. 其他](#334-其他)
  - [3.4. 索引](#34-索引)
    - [3.4.1. 有效的索引类型](#341-有效的索引类型)
    - [3.4.2. 查看索引](#342-查看索引)
    - [3.4.3. 索引方法](#343-索引方法)
    - [3.4.4. 重设索引](#344-重设索引)
    - [3.4.5. 多级索引](#345-多级索引)
    - [3.4.6. 索引重命名](#346-索引重命名)
  - [3.5. 基本数据操作](#35-基本数据操作)
    - [3.5.1. 原则: 对齐与扩展](#351-原则-对齐与扩展)
    - [3.5.2. 原则: missing data](#352-原则-missing-data)
    - [3.5.3. 数据访问](#353-数据访问)
    - [3.5.4. 迭代](#354-迭代)
    - [3.5.5. 数据信息](#355-数据信息)
    - [3.5.6. 表操作](#356-表操作)
    - [3.5.7. 元素操作](#357-元素操作)
    - [3.5.8. 排序](#358-排序)
    - [3.5.9. 转换](#359-转换)
  - [3.6. 高级数据操作](#36-高级数据操作)
    - [3.6.1. 计算](#361-计算)
    - [3.6.2. 逻辑、关系判断](#362-逻辑-关系判断)
    - [3.6.3. 统计](#363-统计)
    - [3.6.4. 集合](#364-集合)
    - [3.6.5. Split-Apply-Combine (SAC)](#365-split-apply-combine-sac)
    - [3.6.6. 函数映射](#366-函数映射)
    - [3.6.7. 数据透视表](#367-数据透视表)
    - [3.6.8. window](#368-window)
    - [3.6.9. 日期时间](#369-日期时间)
    - [3.6.10. 字符串处理](#3610-字符串处理)
  - [3.7. 可视化](#37-可视化)
  - [3.8. 输入输出](#38-输入输出)
  - [3.9. options](#39-options)
- [4. scipy](#4-scipy)
  - [4.1. optimize](#41-optimize)
    - [4.1.1. 最小二乘法拟合](#411-最小二乘法拟合)
    - [4.1.2. Curve Fitting](#412-curve-fitting)

<!-- /code_chunk_output -->

--------------------------------------------------------------------------------
tips:
* **numpy**: 多维数组, 封装多维同质数据类型
* **pandas**: 类似 excel
* **scipy**: 各种高级数学方法, 如微积分、内插、拟合等
* ==不要随意改动 numpy, pandas数据对象的尺寸, 包括拼接、裁剪、添加、删除等==
* ==不要随意扩大 numpy的维度==
* hdf5存储数据非常快

--------------------------------------------------------------------------------
# 1. 标准数学库

## 1.1. 内建数学
* `pow(x, y[, z])`, `divmod(a, b)`
* `abs(x)`,
* `round(number[, ndigits])`
* `sum(iterable[, start])`
* `max(iterable, *[, key, default]) `, `max(arg1, arg2, *args[, key])`
* `min(iterable, *[, key, default]) `, `min(arg1, arg2, *args[, key])`
* `all(iterable) `,`any(iterable) `

## 1.2. 标准库 math: 基本数学
* 常量
    * `inf`, `nan`
    * `pi`: π = 3.141592...
    * `tau`: τ = 6.283185...
    * `e`: e = 2.718281...
* 数论和表示
    * `fabs(x)`: 绝对值
    * `fsum(iterable)`: 精确的浮点数加法
    * `prod(iterable, *, start=1)`: 连乘
    * `gcd(a, b)`, `lcm(*integers)`: 最大公约数, 最小公倍数
    * `ceil(x)`,`floor(x)`, `trunc(x)`: 取整
    * `fmod(x, y)`, `remainder(x, y)`: 取余
    * `modf(x)`: 分离整数和小数
    * `copysign(x, y)`: 复制正负符合
    * `frexp(x)`, `ldexp(x, i)`: 浮点数表示法
    * `nextafter(x, y)`
    * `ulp(x)`
    * `isclose(a, b, *, rel_tol=1e-09, abs_tol=0.0)`, `isfinite(x)`, `isinf(x)`, `isnan(x)`: 数据判断
* 乘幂、指数、对数
    * `pow(x, y)`, `sqrt(x)`, `isqrt(n)`: 乘方, 开方, 开方并取整
    * `exp(x)`, `expm1(x)`: 指数
    * `log(x[, base])`, `log1p(x)`, `log2(x)`, `log10(x)`: 对数
* 排列组合
    * `perm(n, k=None)`: 排列
    * `comb(n, k)`: 组合
    * `factorial(n)`: 阶乘, 等效于 `prod(range(1, n+1))`
* 三角函数
    * `degrees(x)`, `radians(x)`: 角度, 弧度
    * `sin(x)`, `cos(x)`, `tan(x)`: 三角函数
    * `asin(x)`, `acos(x)`, `atan(x)`,`atan2(y, x)`: 反三角函数
    * `dist(p, q)`: 两点的距离
    * `hypot(x, y)`: 欧几里得范数
* 双曲函数
    * `sinh(x)`, `cosh(x)`, `tanh(x)`: 双曲函数
    * `asinh(x)`, `acosh(x)`, `atanh(x)`: 反双曲函数
* 特殊函数
    * `erf(x)` 误差
    * `erfc(x)` 补码误差
    * `gamma/lgamma(x)`

## 1.4. 标准库 decimal: 小数
* 设置
`getcontext()`
* 精确小数
    * 构造: `Decimal(小数)`
    * 支持普通的运算
    * 方法:
        * `as_integer_ratio() -> (int, int)`
        * `exp()`, `ln()`, `log10()`, `logb()`
        * `sqrt()`
        * `logical_and/logical_or/logical_xor/logical_invert()`
        * `quantize()` 四舍五入
        * is_canonical(), is_finite(), is_infinite(), is_nan(), is_normal(context=None), is_qnan(), is_signed(), is_snan(), is_subnormal(context=None), is_zero()
        * adjusted()
        * as_tuple()
        * canonical()
        * compare(other, context=None), compare_signal(other, context=None), compare_total(other, context=None), compare_total_mag(y),
        * copy_abs(), copy_negate(), copy_sign(other, context=None)
        * fma(other, third, context=None)
        * max(other, context=None)
        * max_mag(other, context=None)
        * min(other, context=None)
        * min_mag(other, context=None)
        * next_minus(context=None)
        * next_plus(context=None)
        * next_toward(other, context=None)
        * normalize(context=None)
        * number_class(context=None)
        * radix()
        * remainder_near(other, context=None)
        * rotate(other, context=None)
        * same_quantum(other, context=None)
        * scaleb(other, context=None)
        * shift(other, context=None)
        * to_eng_string(context=None)
        * to_integral(rounding=None, context=None)
        * to_integral_exact(rounding=None, context=None)
        * to_integral_value(rounding=None, context=None)
        * from_float(f, /) from builtins.type

## 1.5. 标准库 fractions: 分数
* 构造:
    * `Fraction(numerator=0, denominator=1)`
    * `Fraction(other_fraction)`
    * `Fraction(float)`
    * `Fraction(decimal)`
    * `Fraction(string)`
* 支持普通的运算
* 函数 `gcd(a, b)`

## 1.3. 标准库 random: 随机数
* Bookkeeping函数
    * `seed(a=None, version=2)`
    * `getstate()`, `setstate(state)`
* bytes - 随机函数
    * `randbytes(n)`
* 整数 - 随机函数
    * `randrange(start = 0, stop[, step])`
    * `randint(a, b)`
    * `getrandbits(k)`
* 序列 - 随机函数
    * `choice(seq)`
    * `choices(population, weights=None, *, cum_weights=None, k=1)`
    * `shuffle(x[, random])`
    * `sample(population, k)`
* 实数 - 随机分布函数
    * `random()`
    * `uniform(a, b)`
    * `triangular(low, high, mode)`
    * `betavariate(alpha, beta)`
    * `expovariate(lambd)`
    * `gammavariate(alpha, beta)`
    * `gauss(mu, sigma)`
    * `lognormvariate(mu, sigma)`
    * `normalvariate(mu, sigma)`
    * `vonmisesvariate(mu, kappa)`
    * `paretovariate(alpha)`
    * `weibullvariate(alpha, beta)`
* 其他生成器
    * `class random.Random([seed])`
    * `class random.SystemRandom([seed])`

## 1.6. 标准库 statistics: 统计
* 平均
    * `mean/fmean/geometric_mean/harmonic_mean(data)`: 平均值
    * `median/median_low/median_high(data)`: 中位数
    * `median_grouped(data, interval=1)`: 中位数
    * `mode/multimode(data)`: 众数
* 分布
    * `pstdev(data, mu=None)`, 总标准差
    * `pvariance(data, mu=None)`, 总方差
    * `stdev(data, xbar=None)`, 采样标准差
    * `variance(data, xbar=None)`, 采样方差
    * `quantiles(data, *, n=4, method='exclusive')`: 区分度
    * `covariance/correlation(x, y, /)`: 协方差, 相关系数
* 线性回归
    * `linear_regression(x, y, /)`: 线性回归

## 1.7. 标准库 cmath: 复数

--------------------------------------------------------------------------------
# 2. numpy
> 详见 [官方文档](https://numpy.org/doc/stable/index.html) 或 [中文文档](https://www.numpy.org.cn/)

> `import numpy as np`

## 2.1. 基础

### 2.1.1. N-dimensional array (ndarray)
* 多维数组, 封装多维同质数据类型, 底层用 C 语言实现, 运行速度快
* 与标准 Python 序列的区别:
    1. ==固定尺寸, 改变尺寸时创建新的 copy== (不要频繁使用改变尺寸或形状)
    1. array 中的数据类型必须相同, 例外: 元素是 array
    1. 更快

* 大块连续内存 (见 [官方文档](https://numpy.org/doc/stable/reference/arrays.html)) , 结构如下图所示:
    ![numpy ndarray内存结构](/assets/numpy%20ndarray内存结构_official.png)
    ![numpy ndarray内存结构](/assets/numpy%20ndarray内存结构.jpg)

#### 2.1.1.1. 创建
* [np.array(object, dtype=None, *, copy=True, order='K', subok=False, ndmin=0, like=None) -> ndarray](https://numpy.org/doc/stable/reference/generated/numpy.array.html)
    * 参数
        * `object`: array类数据: `list`, 序列, `np.array`, `np.mat`, ...
        * `dtype`: 数据类型, 如果省略, 自动推断数据类型
        * `copy`: `bool`, 是否复制 (尤其是使用 `np.array` 创建时)
        * `order`: `{'K', 'A', 'C', 'F'}`, optional
            | order | no copy   | copy=True                                           |
            | ----- | --------- | --------------------------------------------------- |
            | 'K'   | unchanged | F & C order preserved, otherwise most similar order |
            | 'A'   | unchanged | F order if input is F and not C, otherwise C order  |
            | 'C'   | C order   | C order, C语言顺序 (第一维是行, 第二维是列)         |
            | 'F'   | F order   | F order, Fortran语言顺序 (第一维是列, 第二维是行)   |
        * `ndmin`: 维度
    * 示例:
        ``` python
        np.array([1, 2, 3])         # array([1, 2, 3])
        np.array([1, 2, 3.0])       # array([1., 2., 3.])
        np.array([[1, 2], [3, 4]])  # array([[1, 2],
                                    #        [3, 4]])
        np.array([1, 2, 3], ndmin=2)        # array([[1, 2, 3]])
        np.array([1, 2, 3], dtype=complex)  # array([1.+0.j, 2.+0.j, 3.+0.j])
        x = np.array([(1,2),(3,4)],dtype=[('a','<i4'),('b','<i4')])
        x['a']  # Out[7]: array([1, 3])
        np.array(np.mat('1 2; 3 4')) # array([[1, 2],
                                     #        [3, 4]])
        np.array(np.mat('1 2; 3 4'), subok=True)    # matrix([[1, 2],
                                                    #         [3, 4]])
        ```

* 其他创建方法: 详见 [官方文档](https://numpy.org/doc/stable/reference/routines.array-creation.html)
    * 按 shape 或值创建
        `empty`/`zeros`/`ones`/`full` (..)
        `empty_like`/`zeros_like`/`ones_like`/`full_like` (..)
        `eye`/`identity`(..)
        * 速度:  empty > zeros > ones > full
    * 从已有数据创建
        `array`/`asarray`/`asanyarray`/`ascontiguousarray`/`asmatrix` (..)
        `copy` (..)
        `frombuffer`/`from_dlpack`/`fromfile`/`fromfunction`/`fromiter`/`fromstring` (..)
        `loadtxt` (..)
    * 范围
        `arange`/`linspace`/`logspace`/`geomspace` (..)
        `meshgrid`/`mgrid`/`ogrid` (..)
    * 矩阵
        `diag`/`diagflat` (..)
        `tri`/`tril`/`triu` (..)
        `vander` (..)
    * 矩阵 class
        `mat`/`bmat` (..)
    * 随机数
        `random.xxx(..)`
    * ...

#### 2.1.1.2. 属性
> 详见 [官方文档](https://numpy.org/doc/stable/reference/arrays.ndarray.html#array-attributes)

| 分类     | 属性     | 说明                           |
| :------- | -------- | ------------------------------ |
| 数据类型 | dtype    | numpy数据类型                  |
| ^        | ctypes   | 便于与 ctypes 模块交互         |
| 尺寸     | ndim     | 维度                           |
| ^        | shape    | (行数,列数)                    |
| ^        | size     | 行数×列数                      |
| 内存     | data     | 内存指针                       |
| ^        | itemsize | 每个元素的字节数               |
| ^        | strides  | (每行字节数, 每个元素的字节数) |
| ^        | nbytes   | data的总尺寸                   |
| ^        | flags    | 内存信息                       |
| 迭代     | flat     | 1维迭代器                      |
| 转置     | T        | 转置, 等效于`.transpose()`     |
| 复数     | real     | 实部                           |
| ^        | imag     | 虚部                           |
| 其他     | base     | -                              |

#### 2.1.1.3. 方法
> 详见 [官方文档](https://numpy.org/doc/stable/reference/arrays.ndarray.html#array-methods)

| 分类 | 方法                                       | 说明                                       |
| :--- | ------------------------------------------ | ------------------------------------------ |
| 属性 | .astype(dtype[, order, casting, ...])      | 以另一种数据格式复制 array                 |
| 引用 | .copy([order])                             | 返回一个 copy                              |
| ^    | .view([dtype, type])                       | 返回一个 view                              |
| 形状 | .reshape(shape[, order])                   | 改变 shape, 返回 copy                      |
| ^    | .resize(new_shape[, refcheck])             | 改变 shape, **(in place)**                 |
| ^    | .transpose(*axes)                          | 转置                                       |
| ^    | .swapaxes(axis1, axis2)                    | 交换轴                                     |
| ^    | .flatten([order])                          | 展平, 返回copy                             |
| ^    | .ravel([order])                            | 展平, 返回view                             |
| ^    | .squeeze([axis])                           | 降维, 如 \[\[\[0], [1], [2]]] -> [0, 1, 2] |
| 元素 | .item(*args)                               | 访问元素, 等效于 value = arr[index]        |
| ^    | .itemset(*args)                            | 修改元素, 等效于 arr[index] = value        |
| ^    | .take(indices[, axis, out, mode])          | 索引                                       |
| ^    | .put(indices, values[, mode])              | 索引并赋值                                 |
| ^    | .fill(value)                               | 填充, 等效于 arr[...] = value              |
| ^    | .repeat(repeats[, axis])                   | 重复                                       |
| 选取 | .choose(choices[, out, mode])              | 随机选取                                   |
| ^    | .nonzero()                                 | 非零元素的索引                             |
| ^    | .compress(condition[, axis, out])          | 根据条件筛选                               |
| ^    | .diagonal([offset, axis1, axis2])          | 对角线                                     |
| 数学 | 加减乘除、取余、乘方、移位、比较、逻辑等   | -                                          |
| ^    | .round([decimals, out])                    | round                                      |
| ^    | .dot(b, out=None)                          | 点乘, 可用`@`符号表示                      |
| ^    | .conjugate/conj()                          | 共轭                                       |
| 统计 | .max([axis, out, keepdims])                | 最大值                                     |
| ^    | .argmax([axis, out])                       | 最大值的索引                               |
| ^    | .min([axis, out, keepdims])                | 最小值                                     |
| ^    | .argmin([axis, out])                       | 最小值的索引                               |
| ^    | .mean([axis, dtype, out, keepdims])        | 平均值                                     |
| ^    | .var([axis, dtype, out, ddof, keepdims])   | 方差                                       |
| ^    | .std([axis, dtype, out, ddof, keepdims])   | 标准差                                     |
| ^    | .sum([axis, dtype, out, keepdims])         | 和                                         |
| ^    | .cumsum([axis, dtype, out])                | 累加和                                     |
| ^    | .prod([axis, dtype, out, keepdims])        | 积                                         |
| ^    | .cumprod([axis, dtype, out])               | 累乘                                       |
| ^    | .ptp([axis, out, keepdims])                | 峰峰值                                     |
| ^    | .clip([min, max, out])                     | 两个阈值之间的值                           |
| ^    | .trace([offset, axis1, axis2, dtype, out]) | 对角线的和                                 |
| 逻辑 | .all([axis, out, keepdims])                | 与                                         |
| ^    | .any([axis, out, keepdims])                | 或                                         |
| 排序 | .sort([axis, kind, order])                 | 排序, **in place**                         |
| ^    | .argsort([axis, kind, order])              | 排序后的索引                               |
| ^    | .partition(kth[, axis, kind, order])       | 分组                                       |
| ^    | .argpartition(kth[, axis, kind, order])    | 分组后的索引                               |
| ^    | .searchsorted(v[, side, sorter])           | 查找                                       |
| 转换 | .byteswap([inplace])                       | 交换字节顺序                               |
| ^    | .newbyteorder(new_order='S')               | 返回新的字节顺序                           |
| ^    | .tolist()                                  | 转为 list                                  |
| ^    | .tostring([order])                         | 转为 bytes, 将被淘汰                       |
| ^    | .tobytes([order])                          | 转为 bytes                                 |
| ^    | .tofile(fid[, sep, format])                | 写入文件                                   |
| ^    | .dump(file)                                | 存入 pickle                                |
| ^    | .dumps()                                   | 用 string 表示 array 的 pickle             |
| 内存 | .setflags([write, align, uic])             | 设置标志                                   |
| ^    | .getfield(dtype[, offset])                 | 内存数据                                   |
| ^    | .setfield(val, dtype, offset=0)            | 内存数据                                   |

### 2.1.2. 数据类型

#### 2.1.2.1. 预定义数据类型
| 分类   | 预定义             | 别名                                            | 字符代码 | 说明                                     |
| ------ | ------------------ | ----------------------------------------------- | -------- | ---------------------------------------- |
| 布尔   | bool_              | bool8                                           | ?        | python 的 bool                           |
| 整型   | int_               | python 的 int, 在 x86_64 平台中是 int64         |
| ^      | byte/ubyte         | int8/uint8                                      | b/B      | C 的 singed/unsigned char                |
| ^      | short/ushort       | int16/uint16                                    | h/H      | C 的 singed/unsigned short               |
| ^      | intc/uintc         | int32/uint32                                    | i/I      | C 的 singed/unsigned int                 |
| ^      | int_/uint_         | int64/uint64                                    | l/L      | python 的 int, C 的 singed/unsigned long |
| ^      | ^                  | intp/uintp                                      | -        | C 的 intptr_t                            |
| ^      | longlong/ulonglong | -                                               | q/Q      | C 的 singed/unsigned longlong            |
| 浮点数 | float_             | python 的 float, 在 x86_64 平台中是 float64     |
| ^      | half               | float16                                         | e        | 半精度浮点数                             |
| ^      | single             | float32                                         | f        | 单精度浮点数                             |
| ^      | double             | float_/float64                                  | d        | 双精度浮点数                             |
| ^      | longdouble         | longfloat/float128                              | g        | 四精度浮点数                             |
| 复数   | complex_           | python 的 cfloat, 在 x86_64 平台中是 complex128 |
| ^      | csingle            | singlecomplex/complex64                         | F        | python 的 complex, 双精度复数            |
| ^      | cdouble            | cfloat/complex_/complex128                      | D        | 单精度复数                               |
| ^      | clongdouble        | clongfloat/longcomplex/complex256               | G        | 双精度复数                               |
| 字符串 | bytes_             | string_                                         | S        | bytes                                    |
| ^      | str_               | unicode_                                        | U        | 字符串                                   |
| 时间   | datetime64         | -                                               | M        | 日期时间                                 |
| ^      | timedelta64        | -                                               | m        | 时间差                                   |
| 内存   | void               | -                                               | V        | buffer                                   |
| 对象   | object_            | -                                               | O        | 对象                                     |

#### 2.1.2.2. 自定义数据类型
> 详见 [官方文档](https://numpy.org/doc/stable/reference/arrays.dtypes.html)

* 通过构造函数 `dtype(obj, align=False, copy=False)` 定义特殊的类型, 如结构体类型和数组类型
    * `dtype` 是 numpy 的一个类(`numpy.dtype`)
* 支持的 `obj`
    * 通用 Python 内建类型: `int`, `bool`, `float`, `complex`, `bytes`, `str`, `buffer` 等
    * 别名的字符串: `'int32'`, `'float64'`, `'complex128'` 等, 可用 `numpy.sctypeDict.keys()` 查询
    * 字符串型: 格式为`'[字节顺序][数组] 类型缩写 [长度]'`
        * 字节顺序:
            |  字符  | 含义                             |
            | :----: | -------------------------------- |
            |   <    | little endian                    |
            | &shy;> | big endian                       |
            |   =    | native order                     |
            |   \|   | ignore (no change to byte order) |
        * 数组: 用 tuple 表示, 如 `'3u8'` (等效于`'(3,)u8'`),`'(2,3)f8'`
        * 类型缩写:
            | 缩写  | 对应类型                                |
            | :---: | --------------------------------------- |
            |   ?   | boolean                                 |
            |  b/B  | byte                                    |
            |  i/u  | integer                                 |
            |   f   | floating-point                          |
            |   c   | complex-floating point                  |
            |   M   | datetime                                |
            |   m   | timedelta                               |
            |   O   | (Python) objects                        |
            |  S/a  | zero-terminated bytes (not recommended) |
            |   U   | Unicode string                          |
            |   V   | raw data (void)                         |
        * 长度:
            * 数字: 如`'<i4'`等效于 np.int32, `'|f8'`等效于 np.float64
            * 字符串: 如`U10`表示长度为10的字符串
    * `(flexible_dtype, itemsize)`, 如
        ``` python
        dt = np.dtype((np.void, 10))  # 10-byte wide data block
        dt = np.dtype(('U', 10))      # 10-character unicode string
        ```
    * 数组: 格式 `(fixed_dtype, shape)`, 如
        ``` python
        dt = np.dtype((np.int32, (2,2)))          # 2 x 2 integer sub-array
        dt = np.dtype(('i4, (2,3)f8, f4', (2,3))) # 2 x 3 structured sub-array
        ```
    * 结构体类型
        * string: `'类型1, 类型2, ...'` 等效于 `[('f0', 类型1), ('f1', 类型2), ...]`, 如
            ``` python
            dt = np.dtype("i4, (2,3)f8, f4")  # field named f0 containing a 32-bit integer
                                              # field named f1 containing a 2 x 3 sub-array of 64-bit floating-point numbers
                                              # field named f2 containing a 32-bit floating-point number
            ```
        * list of tuple: `[(field_name, field_dtype, field_shape), ...]`, 如
            ``` python
            dt = np.dtype([('R','u1'), ('G','u1'), ('B','u1'), ('A','u1')])
            ```
        * dict: `{'names': ..., 'formats': ..., 'offsets': ..., 'titles': ..., 'itemsize': ...}`, 如
            ``` python
            dt = np.dtype({'names': ['r','g','b','a'],
                           'formats': [np.uint8, np.uint8, np.uint8, np.uint8]})
            dt = np.dtype({'names': ['r','b'],
                           'formats': ['u1', 'u1'],
                           'offsets': [0, 2],
                           'titles': ['Red pixel', 'Blue pixel']})
            ```
        * dict, `{'field1': ..., 'field2': ..., ...}`, 如
            ``` python
            dt = np.dtype({'col1': ('U10', 0), 'col2': (np.float32, 10), 'col3': (int, 14)})
            ```

#### 2.1.2.3. 修改数据类型
* 使用`ndarray.astype(..) -> copy`方法, 注意该方法产生副本, 而不是直接修改原 array

#### 2.1.2.4. 相关class与函数
详见 [官方文档](https://numpy.org/doc/stable/reference/routines.dtype.html)

#### 2.1.2.5. 结构体 Array
1. 定义结构体类型
1. 创建array
1. 初始化:
    * 用 tuple 赋值
    * 按结构名索引后赋值
1. 访问
    * 以 tuple 访问, 如 arr[1] = \<tuple\>, \<tuple\> = arr[2]
    * 索引之后, 再以`[key]`访问, 如 arr[3]['name']

### 2.1.3. 索引
> 详见 [官方文档](https://numpy.org/doc/stable/reference/arrays.indexing.html)

* 基本索引: `arr[索引]`, 其中索引可以是:
    * 标量(正数, 负数), 如:
        ```python
        arr[0]
        arr[-1]
        ```
    * slice, 如:
        ``` python
        arr[1:7:2]
        arr[-2:10]
        arr[1:]
        arr[:20]
        arr[::2]
        arr[::-1]
        ```
    * list, 如:
        ``` python
        arr[[0,2,4]]
        ```
    * bool 表达式, 如
        ``` python
        arr[arr > 3]
        arr[(arr>5) & (arr <9)]
        ```
* 多维索引
    * `[第一维索引, 第二维索引, ...]`
    * `[第一维索引 (标量) ][第二维索引 (标量) ]...`
    * `[省略号(..), 倒数第二维索引, 最后一维索引]`, 其中`...`表示前边多维的全部采用`:`
* 新维
    * newaxis, 如:
    ``` python {.line-numbers}
    arr = np.array([1,2,3]) # array([1, 2, 3])
    arr[:, np.newaxis]      # array([[1],
                            #        [2],
                            #        [3]])
    ```
* 结构体类型array的索引
    * 正常索引后, 追加`['结构体元素名称']`以定位结构体元素
    * `arr.['结构体元素名称']`则返回该属性的 array 的 view, 等效于`arr[...].['结构体元素名称']`
* 其他取值方法
    * `take/put(..)`
    * `ndarray.flat[展平的索引]`
    * `ndarray.item(..)`, 元素的副本

#### 2.1.3.1. 索引函数
> 详见 [官方文档](https://numpy.org/doc/stable/reference/routines.indexing.html)

* 产生索引
    `r_/c_/s_`
    `nonzero(..)`
    `where(..)`
    `indices(..)`
    `ix_(..)`/`ogrid`
    `ogrid`
    `ravel_multi_index/unravel_index(..)`
    `diag_indices/diag_indices_from(..)`
    `mask_indices(..)`
    `tril_indices/tril_indices_from/triu_indices/triu_indices_from(..)`
* 索引类似操作
    `take/take_along_axis(..)`
    `choose(..)`
    `compress(..)`
    `diag/diagonal(..)`
    `select(..)`
    `lib.stride_tricks.as_strided(..)`
* 插入数据到array
    `place(..)`
    `put/put_along_axis/putmask(..)`
    `fill_diagonal(..)`

### 2.1.4. 迭代
> 详见 [官方文档](https://numpy.org/doc/stable/reference/arrays.nditer.html)

* 普通迭代
* `ndarray.flat`属性迭代: 按展平后顺序索引
* 迭代器: `nditer`
    * 单个array的迭代
        * 按内存顺序迭代, `np.nditer(a) != np.nditer(a.T) `
        * 内存顺序:
            * 'C': C语言内存顺序, 先按行遍历
            * 'F': Frotran语言内存顺序, 先按列遍历
        * `nditer`默认只读, 可使用`nditer(a, op_flags=['readwrite'])`更改
        * 外部循环, `np.nditer(a, flags=['external_loop'])`
        * 跟踪索引
        * buffering
        * 特殊类型数据迭代

    * 广播array的迭代, 如`np.nditer([ndarray1,ndarray2])`
        * Iterator-Allocated Output Arrays
        * Outer Product Iteration
        * Reduction Iteration
* N维枚举: `ndenumerate(arr)`
* 广播迭代: `broadcast`
* 其他迭代方法, 详见 [官方文档](https://numpy.org/doc/stable/reference/arrays.nditer.html)
    `ndindex(..)`
    `nested_iters(..)`
    `lib.Arrayterator(..)`

### 2.1.5. 标准子类
* [矩阵 (matrix)](https://numpy.org/doc/stable/reference/arrays.classes.html#matrix-objects)

* [内存文件 array (memmap)](https://numpy.org/doc/stable/reference/arrays.classes.html#memory-mapped-file-arrays)

* [字符array (numpy.char)](https://numpy.org/doc/stable/reference/arrays.classes.html#character-arrays-numpy-char)

* [记录array (numpy.rec)](https://numpy.org/doc/stable/reference/arrays.classes.html#record-arrays-numpy-rec): 和结构体array类似, 结构体array更快

* [掩码array (numpy.ma)](https://numpy.org/doc/stable/reference/arrays.classes.html#masked-arrays-numpy-ma)
* [标准容器class](https://numpy.org/doc/stable/reference/arrays.classes.html#standard-container-class)

### 2.1.6. 日期时间和间隔
> 详见 [官方文档](https://numpy.org/doc/stable/reference/arrays.datetime.html)

* 时间类型, 包含两个主要的calss
    * datetime64:
        * 表示日期时间
        * `np.datetime64('ISO时间日期字符串')`
    * timedelta64:
        * 表示时间间隔
        * `np.timedelta64(间隔, '日期时间单位')`
* 日期时间单位: Y, M, W, D, h, m, s, ms, us, ns, ps, fs, as
* 工作日函数: `busdaycalendar, is_busday, busday_offset, busday_count(..)`

## 2.2. array 操作基础

### 2.2.1. 原则: 副本与视图
* 副本 (copy, 深复制) , 创建新的内存空间
    * 某些函数运算后自动创建副本
    * 显式调用`ndarray.copy(order='C') -> copy`
* 视图 (view, 浅复制) , 使用原来的内存空间, 通过视图改变元素会影响其他对象
    * 多数函数运算后产生
    * 显式调用`ndarray.view(dtype=None, type=None)`

### 2.2.2. 原则: 广播
* 两个 shape 不一样的 array, 运算前先进性广播, 扩展为相同尺寸, 然后运算
* 从最后一维向前扫描, 如果维度的数值相同或一个为 1, 进行广播
* 如
    ``` python
    # 1
    Image  (3d array): 256 x 256 x 3
    Scale  (1d array):             3
    Result (3d array): 256 x 256 x 3
    # 2
    A      (4d array):  8 x 1 x 6 x 1
    B      (3d array):      7 x 1 x 5
    Result (4d array):  8 x 7 x 6 x 5
    # 3
    A      (2d array):  5 x 4
    B      (1d array):      1
    Result (2d array):  5 x 4
    # 4
    A      (2d array):  5 x 4
    B      (1d array):      4
    Result (2d array):  5 x 4
    # 5
    A      (3d array):  15 x 3 x 5
    B      (3d array):  15 x 1 x 5
    Result (3d array):  15 x 3 x 5
    # 6
    A      (3d array):  15 x 3 x 5
    B      (2d array):       3 x 5
    Result (3d array):  15 x 3 x 5
    # 7
    A      (3d array):  15 x 3 x 5
    B      (2d array):       3 x 1
    Result (3d array):  15 x 3 x 5
    ```
    ``` python
    # 1
    A      (1d array):  3
    B      (1d array):  4 # trailing dimensions do not match
    # 2
    A      (2d array):      2 x 1
    B      (3d array):  8 x 4 x 3 # second from last dimensions mismatched
    ```

### 2.2.3. 修改 array
> 详见 [官方文档](https://numpy.org/doc/stable/reference/routines.array-manipulation.html)

* 复制
    `copyto(..)`
    `shape(..)`
* 改变形状
    `reshape(..)`
    `ndarray.resize(..)`
    `ndarray.flat`
    `ravel(..)`
    `ndarray.flatten(..)`
* 转置与旋转
    `ndarray.T` / `transpose(..)`
    `swapaxes, rollaxis, moveaxis(..)`
* 改变维数
    `atleast_1d, atleast_2d, atleast_3d(..)`
    `broadcast, broadcast_to, broadcast_arrays(..)`
    `expand_dims(..)`
    `squeeze(..)`
* 改变array类型
    `asarray, asanyarray, asmatrix, asfarray, asfortranarray, ascontiguousarray, asarray_chkfinite(..)`
    `asscalar(..)`
    `require(..)`
* 合并
    `concatenate(..)`
    `stack, column_stack, dstack, hstack, vstack(..)`
    `block(..)`
* 拆分
    `split, array_split, dsplit, hsplit, vsplit(..)`
* Tiling
    `tile, repeat(..)`
* 添加或删除元素
    `insert, append(..)`
    > 注意: 每次插入或删除, 都会创建一个新的copy, 效率很低, 建议将多次插入或删除操作作为一个array合并到原array或从原array拆分
    `delete, trim_zeros, unique(..)`
    `resize(..)`
* 重新排列元素
    `flip, fliplr, flipud(..)`
    `reshape(..)`
    `roll(..)`
    `rot90(..)`
* padding
    `pad(..)`

### 2.2.4. ufunc
> 详见 [官方文档](https://numpy.org/doc/stable/reference/ufuncs.html)

* ufunc 是专用于array的函数
* 创建 ufunc: `np.frompyfunc(func, nin, nout)`
* 已有的 ufunc, 包括: 数学函数、三角函数、位运算函数、比较函数、浮点函数等
* ufunc 的高级特性
    * 指定输出: out参数 可以指定结果输出到那个 array, 如
        ``` python
        In [2]: a = np.arange(0,100,10)

        In [3]: y = np.zeros_like(a)

        In [4]: np.subtract(a[1:], a[:-1], out=y[1:])
        Out[4]: array([10, 10, 10, 10, 10, 10, 10, 10, 10])

        In [5]: a,y
        Out[5]:
        (array([ 0, 10, 20, 30, 40, 50, 60, 70, 80, 90]),
        array([ 0, 10, 10, 10, 10, 10, 10, 10, 10, 10]))

        # 可用 np.diff(a, prepend=0) 函数实现上述功能
        In [6]: np.diff(a, prepend=0)
        Out[6]: array([ 0, 10, 10, 10, 10, 10, 10, 10, 10, 10])
        ```
    * 条件执行: where参数
    * 聚合:
        `ufunc.reduce(a[, axis, dtype, out, keepdims])`
        `ufunc.accumulate(array[, axis, dtype, out])`
        `ufunc.reduceat(a, indices[, axis, dtype, out])`
    * 外积:
        `ufunc.outer(A, B, **kwargs)`
    * 结果筛选:
        `ufunc.at(a, indices[, b])`

### 2.2.5. 函数编程
> 详见 [官方文档](https://numpy.org/doc/stable/reference/routines.functional.html)

`apply_along_axis, apply_over_axes(..)`
`vectorize(..)`
`frompyfunc(..)`
`piecewise(..)`

## 2.3. 常数
> 详见 [官方文档](https://numpy.org/doc/stable/reference/constants.html)

`Inf`, `inf`, `Infinity`, `infty`, `PINF`, `NINF`
`NAN`, `NaN`, `nan`
`PZERO`, `NZERO`
`pi`, `e`, `euler_gamma`
`newaxis`

## 2.4. Numpy基本函数

### 2.4.1. Numpy 帮助函数
`np.lookfor(..)`
`np.info(..)`
`np.source(..)`

### 2.4.2. 排序与查找
> 详见 [官方文档](https://numpy.org/doc/stable/reference/routines.sort.html)

* 排序
    `sort, lexsort, msort, sort_complex(..)`
    `ndarray.sort` (==in-place==)
    `argsort(..)`
    `partition, argpartition(..)`
    * 对结构体array的排序: order = 结构名称
* 查找
    `argmax, argmin, nanargmax, nanargmin(..)`
    `where, argwhere(..)`
    `nonzero, flatnonzero(..)`
    `searchsorted(..)`
    `extract(..)`
* 计数
    `count_nonzero(..)`

### 2.4.3. 二进制
> 详见 [官方文档1](https://numpy.org/doc/stable/reference/arrays.ndarray.html#array-conversion)和[2](https://numpy.org/doc/stable/reference/routines.bitwise.html)
* 转换
    * `ndarray.byteswap(..)`
    * `ndarray.newbyteorder(..)`
    * `ndarray.tobytes(..)`
    * `ndarray.getfield(..)`
    * `ndarray.setfield(..)`
* 二进制运算
    `bitwise_and, bitwise_or, bitwise_xor, invert(..)`
    `left_shift, right_shift(..)`
* Bit打包
    `packbits, unpackbits(..)`
* 二进制表示
    `binary_repr(..)`

### 2.4.4. string
> 详见 [官方文档](https://numpy.org/doc/stable/reference/routines.char.html)

类似Python字符串处理 (用于普通元素) , 但这里的函数专用于array,

## 2.5. array 数学运算
可以实现Matlab的常用功能, 参见[与MATLAB的对比](https://numpy.org/doc/stable/user/numpy-for-matlab-users.html)

### 2.5.1. 数学函数
> 详见 [官方文档](https://numpy.org/doc/stable/reference/routines.math.html)
* 数学运算
    `positive, negative(..)`
    `add, subtract, multiply, divide, power, mod(..)` 等效于`+` `-` `*` `/` `**` `%`
    `reciprocal(..)`
    `float_power(..)`
    `true_divide, floor_divide(..)`
    `fmod, mod, modf, remainder, divmod(..)`
* 近似
    `around, round_, rint, fix(..)`
    `floor, ceil, trunc(..)`
* 和、积、微分
    `sum, nansum, cumsum, nancumsum(..)`
    `prod, nanprod, cumprod, nancumprod(..)`
    `diff, ediff1d, gradient(..)`
    `cross(..)`
    `trapz(..)`
* 指数和log
    `exp, expm1, exp2(..)`
    `log, log10, log2, log1p, logaddexp, logaddexp2(..)`
* 三角函数
    `sin, cos, tan(..)`
    `arcsin, arccos, arctan, arctan2(..)`
    `hypot(..)`
    `degrees, radians, unwrap, deg2rad, rad2deg(..)`
* 双曲函数
    `sinh, cosh, tanh(..)`
    `arcsinh, arccosh, arctanh(..)`
* 浮点函数
    `signbit/copysign(..)`
    `frexp/ldexp(..)`
    `nextafter(..)`
    `spacing(..)`
* 有理数
    `lcm, gcd(..)`
* 复数
    `angle(..)`
    `real, imag(..)`
    `conj/conjugate(..)`
* 其他
    `convolve(..)`
    `clip(..)`
    `square, sqrt, cbrt(..)`
    `abs/absolute, fabs, sign(..)`
    `heaviside(..)`
    `maximum, minimum, fmax, fmin(..)`
    `nan_to_num(..)`
    `real_if_close(..)`
    `interp(..)`
* 其他特殊函数
    `i0, dual.i0(..)`
    `sinc(..)`

### 2.5.2. 随机数(numpy.random)
> 详见 [官方文档](https://numpy.org/doc/stable/reference/random/index.html)

* 简单随机数
    `random.Generator.integers(..)`: 代替"randint, random_integers"
    `random.Generator.random(..)`: 代替"rand, random_sample"
    `random.choice(..)`
    `random.bytes(..)`
* 排列
    `random.shuffle(..)`
    `random.permutation(..)`
* 分布
    `random.beta(..)`
    `random.binomial(..)`
    `random.chisquare(..)`
    `random.dirichlet(..)`
    `random.exponential(..)`
    `random.f(..)`
    `random.gamma(..)`
    `random.geometric(..)`
    `random.gumbel(..)`
    `random.hypergeometric(..)`
    `random.laplace(..)`
    `random.logistic(..)`
    `random.lognormal(..)`
    `random.logseries(..)`
    `random.multinomial(..)`
    `random.multivariate_normal(..)`
    `random.negative_binomial(..)`
    `random.noncentral_chisquare(..)`
    `random.noncentral_f(..)`
    `random.normal(..)`
    `random.pareto(..)`
    `random.poisson(..)`
    `random.power(..)`
    `random.rayleigh(..)`
    `random.standard_cauchy(..)`
    `random.standard_exponential(..)`
    `random.standard_gamma(..)`
    `random.standard_normal(..)`
    `random.standard_t(..)`
    `random.triangular(..)`
    `random.uniform(..)`
    `random.vonmises(..)`
    `random.wald(..)`
    `random.weibull(..)`
    `random.zipf(..)`
* 随机产生器
    * `random.BitGenerator`: 产生 32/64随机bits
    * `random.Generator`: 将random.BitGenerator产生的随机bits转为随机数
    * `random.SeedSequence`: 初始化种子

### 2.5.3. 矩阵(numpy.matlib)
> 详见 [官方文档](https://numpy.org/doc/stable/reference/routines.matlib.html)
* 矩阵数据类型
    `mat, asmatrix, bmat(..)`
* matlib中替换的函数
    `empty, zeros, ones(..)`
    `eye, identity(..)`
    `repmat(..)`
    `rand, randn(..)`

### 2.5.4. 线性代数(numpy.linalg 和 numpy.dual)
> 相关子模块: [numpy.linalg](https://numpy.org/doc/stable/reference/routines.linalg.html), [numpy.dual](https://numpy.org/doc/stable/reference/routines.dual.html#linear-algebra)
* 转置
    `.T属性, transpose(..)`
* 矩阵和向量乘法
    `dot, linalg.multi_dot, vdot(..)`
    `tensordot(..)`
    `inner, outer(..)`
    `matmul(..)`
    `einsum, einsum_path(..)`
    `linalg.matrix_power(..)`
    `kron(..)`
* 分解
    `{linalg/dual}.cholesky(..)`
    `linalg.qr(..)`
    `{linalg/dual}.svd(..)`
* 特征值
    `{linalg/dual}.eig, eigh, eigvals, eigvalsh(..)`
* 范
    `{linalg/dual}.norm(..)`
    `linalg.cond(..)`
    `{linalg/dual}.det(..)`
    `linalg.slogdet(..)`
    `linalg.matrix_rank(..)`
    `trace(..)`
* 求解和取反
    `{linalg/dual}.solve`
    `linalg.tensorsolve(..)`
    `{linalg/dual}.lstsq(..)`
    `{linalg/dual}.inv(..)`
    `{linalg/dual}.pinv(..)`
    `linalg.tensorinv(..)`
* 异常
    `linalg.LinAlgError`

### 2.5.5. 统计
> 详见 [官方文档1](https://numpy.org/doc/stable/reference/routines.statistics.html)
* 顺序统计
    `amin, amax, nanmin, nanmax(..)`
    `ptp(..)`
    `percentile, nanpercentile(..)`
    `quantile, nanquantile(..)`
* 平均和方差
    `mean, average, median(..)`
    `nanmean, nanmedian(..)`
    `var, std(..)`
    `nanvar, nanstd(..)`
* 相关性
    `corrcoef(..)`
    `correlate(..)`
    `cov(..)`
* 直方图
    `histogram, histogram2d, histogramdd, histogram_bin_edges(..)`
    `bincount(..)`
    `digitize(..)`
* 计数
    `count_nonzero(..)`

### 2.5.6. 集合
> 详见 [官方文档1](https://numpy.org/doc/stable/reference/routines.set.html)
* `unique(..)`
* `in1d(..)`
* `isin(..)`
* `intersect1d, union1d, setdiff1d, setxor1d(..)`

### 2.5.7. 逻辑判断
> 详见 [官方文档1](https://numpy.org/doc/stable/reference/routines.logic.html)
* 真值测试
    `all, any(..)`
    ==不要使用 python内建的 all 和 any, 结果有误==
* 值判断
    `isfinite, isinf, isposinf, isneginf(..)`
    `isnan, isnat(..)`
* 类型判断
    `iscomplex, iscomplexobj(..)`
    `isreal, isrealobj(..)`
    `isfortran(..)`
    `isscalar(..)`
* 逻辑判断
    `logical_and, logical_or, logical_not, logical_xor(..)`
* 比较
    `allclose, isclose(..)`
    `array_equal, array_equiv(..)`
    `greater, greater_equal(..)`
    `less, less_equal(..)`
    `equal, not_equal(..)`

### 2.5.8. FFT
* 子模块: [numpy.dual](https://numpy.org/doc/stable/reference/routines.dual.html#fft)
    `fft, fft2, fftn(..)`
    `ifft, ifft2, ifftn(..)`
* 子模块: [numpy.fft](https://numpy.org/doc/stable/reference/routines.fft.html)
    `fft, fft2, fftn(..)`
    `ifft, ifft2, ifftn(..)`
    `rfft, rfft2, rfftn(..)`
    `irfft, irfft2, irfftn(..)`
    `hfft, ihfft(..)`
    `fftfreq, rfftfreq(..)`
    `fftshift, ifftshift(..)`

### 2.5.9. 窗函数
> 详见 [官方文档](https://numpy.org/doc/stable/reference/routines.window.html)
* 可变窗
    `bartlett(..)`
    `blackman(..)`
    `hamming(..)`
    `hanning(..)`
    `kaiser(..)`

### 2.5.10. 多项式
> 详见 [官方文档1](https://numpy.org/doc/stable/reference/routines.polynomials.html)

* [Polynomial Package](https://numpy.org/doc/stable/reference/routines.polynomials.package.html)
    * 多项式: `numpy.polynomial.polynomial`
    * Chebyshev: `numpy.polynomial.chebyshev`
    * Legendre: `numpy.polynomial.legendre`
    * Laguerre: `numpy.polynomial.laguerre`
    * Hermite, 物理: `numpy.polynomial.hermite`
    * HermiteE, 概率: `numpy.polynomial.hermite_e`
    * 其他: `numpy.polynomial.polyutils`

* [Poly1d](https://numpy.org/doc/stable/reference/routines.polynomials.poly1d.html)
    * 基本
        `poly1d(c_or_r[, r, variable])`
        `polyval(p, x)`
        `poly(seq_of_zeros)`
        `roots(p)`
    * ==最小二乘多项式拟合==
        `polyfit(x, y, deg[, rcond, full, w, cov])`
    * 微积分
        `polyder(p[, m])`
        `polyint(p[, m, k])`
    * 算数
        `polyadd(a1, a2)`
        `polydiv(u, v)`
        `polymul(a1, a2)`
        `polysub(a1, a2)`
    * 警告
        `RankWarning`

### 2.5.11. 金融
> 详见 [官方文档](https://numpy.org/doc/stable/reference/routines.financial.html)
* 简单的金融函数:
    `fv, pv, npv(..)`
    `pmt, ppmt, ipmt(..)`
    `irr, mirr(..)`
    `nper, rate(..)`

### 2.5.12. 浮点数错误处理
> 详见 [官方文档](https://numpy.org/doc/stable/reference/routines.err.html)

* 错误处理处理
    `seterr, geterr, seterrcall, geterrcall, errstate(..)`
* 内部函数
    `seterrobj, geterrobj(..)`

### 2.5.13. 其他
> 参见[官方文档](https://numpy.org/doc/stable/reference/routines.other.html)
* 性能调整, 内存范围, 阵列, 工具

## 2.6. 输入输出
> 详见 [官方文档](https://numpy.org/doc/stable/reference/routines.io.html)
* NPY, NPZ 文件
    * `np.load(..)`
    * `np.save, savez, savez_compressed(..)`
* 文本文件
    * [np.savetxt(fname, X[, fmt, delimiter, newline, ...])](https://numpy.org/doc/stable/reference/generated/numpy.savetxt.html#numpy.savetxt)
    * [np.loadtxt(fname[, dtype, comments, delimiter, ...])](https://numpy.org/doc/stable/reference/generated/numpy.loadtxt.html#numpy.loadtxt)
    * `np.genfromtxt(fname[, dtype, comments, ...])`
    * `np.fromregex(file, regexp, dtype[, encoding])`
    * `np.fromstring(string[, dtype, count, sep])`
    * `np.ndarray.tofile(fid[, sep, format])`
    * `ndarray.tolist()`
* 二进制文件
    * [fromfile(file, dtype=float, count=- 1, sep='', offset=0, *, like=None)](https://numpy.org/doc/stable/reference/generated/numpy.fromfile.html#numpy.fromfile)
    * [ndarray.tofile(fid, sep='', format='%s')](https://numpy.org/doc/stable/reference/generated/numpy.ndarray.tofile.html#numpy.ndarray.tofile)
* pickle
    * `ndarray.dumps/dump(..)`
* 字符串格式
* 文本格式选项
* 内存映射文件
* 二进制格式
* N进制表示
* 数据源

## 2.7. C 语言接口
> 详见 [官方文档](https://numpy.org/doc/stable/reference/arrays.interface.html)

* 相关模块: [numpy.ctypeslib](https://numpy.org/doc/stable/reference/routines.ctypeslib.html)

--------------------------------------------------------------------------------
# 3. pandas
pandas是一种表格形的数据结构, 详见 [官方文档](http://pandas.pydata.org/pandas-docs/stable/)

## 3.1. 数据结构
* 可以看作增强版的 numpy, 行列的索引都加了标签
* 可以使用 numpy 的大部分函数
* 由于 `numpy.ndarray` 的长度不可变, 而是创建新副本, 因此 Pandas 在操作时, 多数情况下创建新的副本, 而非直接在 object 上改动

### 3.1.1. Series
> 一维结构, 类似 `ndarray`, 也类似 `dict`, 详见 [官方文档](https://pandas.pydata.org/pandas-docs/stable/reference/series.html)

* 构造 [pd.Series(data=None, index=None, dtype=None, name=None, copy=False, fastpath=False)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.Series.html), 其中:
    > **data:** array 类数据、可迭代数据、dict、标量, 详见 [数据类型](#33-数据类型)
    > **index:** 如 ['a', 'b', 'c', ...], 详见 [index](#34-索引)
    > **dtype:** str, numpy.dtype, pandas 的时间等

    示例:
    ``` python
    s = pd.Series([1,2,3,4], index=['r1', 'r2', 'r3', 'r4'])
    # s =
    #   r1    1
    #   r2    2
    #   r3    3
    #   r4    4
    #   Name: test, dtype: int64
    ```

* 主要属性:
    > 参见 [官方文档](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.Series.html)

    | 分类 | 属性                    | 说明                             |
    | ---- | ----------------------- | -------------------------------- |
    | 索引 | index                   | 索引                             |
    | ^    | axes                    | 所有轴的索引, list(index)        |
    | ^    | loc / iloc              | 按标签 / 位置索引                |
    | ^    | at / iat                | 按标签 / 位置索引, 访问单个值    |
    | 结构 | ndim                    | 维数                             |
    | ^    | shape                   | 形状                             |
    | ^    | size                    | 展平后的元素个数                 |
    | 数据 | values                  | 所有值, 以 numpy 的 ndarray 表示 |
    | ^    | array                   | 数据, 以 pandas 的 array 表示    |
    | ^    | dtype / dtypes          | 数据类型                         |
    | ^    | T                       | 转置                             |
    | 内存 | nbytes                  | 内存占用                         |
    | 信息 | name                    | 名称                             |
    | ^    | hasnans                 | 有无 NaN                         |
    | ^    | empty                   | 是否为空                         |
    | ^    | is_monotonic_increasing | 是否单调增                       |
    | ^    | is_monotonic_decreasing | 是否单调减                       |
    | ^    | is_unique               | 值是否唯一                       |

* 方法:
    > 参见 [官方文档](https://pandas.pydata.org/pandas-docs/stable/reference/series.html)

### 3.1.2. DataFrame
class, 二维数据结构, 类似 excel 表格, 详见 [官方文档](https://pandas.pydata.org/pandas-docs/stable/reference/frame.html)

* 构造 [pd.DataFrame(data=None, index=None, columns=None, dtype=None, copy=None)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.html) 其中:
    > **data:** array 类数据、可迭代数据、dict(名称会变为 DataFreame 的列名称)、DataFrame, 详见 [数据类型](#33-数据类型)
    > **index, 行索引标签:**, 如 ['a', 'b', 'c', ...], 详见 [index](#34-索引)
    > **column, 列索引标签:** 详见 [index](#34-索引)
    > **dtype, 数据类型:** str, numpy 数据类型, pandas 的时间等, ==只能写一个类型==, 如果是 None, 自动推导

    示例:
    ``` python
    df = pd.DataFrame(np.array([[1, 2, 3], [4, 5, 6], [7, 8, 9]]),
                      columns=['a', 'b', 'c'])
    # df
    #      a  b  c
    #   0  1  2  3
    #   1  4  5  6
    #   2  7  8  9
    ```

* 主要属性:
    > 参见 [官方文档](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.html)

    | 分类 | 属性       | 说明                        |
    | ---- | ---------- | --------------------------- |
    | 索引 | index      | 行索引                      |
    | ^    | columns    | 列索引                      |
    | ^    | axes       | 所有轴的索引 (列表)         |
    | ^    | loc / iloc | 按标签/位置索引             |
    | ^    | at / iat   | 按标签/位置索引, 访问单个值 |
    | 结构 | ndim       | 维数                        |
    | ^    | shape      | 形状                        |
    | ^    | size       | 展平后的元素个数            |
    | 数据 | values     | 所有值                      |
    | ^    | dtypes     | 数据类型                    |
    | ^    | T          | 转置                        |
    | 信息 | empty      | 是否为空                    |
    | 其他 | style      | 风格                        |

* 方法:
    > 参见 [官方文档](https://pandas.pydata.org/pandas-docs/stable/reference/frame.html)

## 3.2. 数据的创建
* 使用 Series、DataFrame 的构造函数
* 从文件导入, 详见 [官方文档](https://pandas.pydata.org/pandas-docs/stable/user_guide/io.html)
    * 文本文件: **CSV**, **固定宽度的文本**, JSON, HTML, 剪切板
    * 二进制文件: **Excel**, **HDF5**, Feater, Parquet, Msgpack, Stata, SAS, Python Pickle
    * 数据库: SQL, gbq(Google Big Query)

## 3.3. 数据类型
> 参见 [官方文档](https://pandas.pydata.org/pandas-docs/stable/user_guide/basics.html#dtypes)

### 3.3.1. 有效的数据类型
> 参见 [官方文档](https://pandas.pydata.org/pandas-docs/stable/user_guide/basics.html#dtypes)
* 基本类型: numpy 的数据类型, 包括: `float`, `int`, `bool`, `timedelta64[ns]`, `datetime64[ns]`
* 扩展类型:
    |      数据类别       |     数据类型     |   标量    |         阵列         |                                                      字符串别名                                                       |
    | :-----------------: | :--------------: | :-------: | :------------------: | :-------------------------------------------------------------------------------------------------------------------: |
    |  tz-aware datetime  | DatetimeTZDtype  | Timestamp | arrays.DatetimeArray |                                                'datetime64[ns, \<tz>]'                                                |
    |     Categorical     | CategoricalDtype |  (none)   |     Categorical      |                                                      'category'                                                       |
    | period (time spans) |   PeriodDtype    |  Period   |  arrays.PeriodArray  |                                          'period[<freq>]', 'Period[<freq>]'                                           |
    |       sparse        |   SparseDtype    |  (none)   |  arrays.SparseArray  |                                       'Sparse', 'Sparse[int]', 'Sparse[float]'                                        |
    |      intervals      |  IntervalDtype   | Interval  | arrays.IntervalArray | 'interval', 'Interval', 'Interval[<numpy_dtype>]', 'Interval[datetime64[ns, \<tz>]]', 'Interval[timedelta64[<freq>]]' |
    |  nullable integer   | Int64Dtype, ...  |  (none)   | arrays.IntegerArray  |                       'Int8', 'Int16', 'Int32', 'Int64', 'UInt8', 'UInt16', 'UInt32', 'UInt64'                        |
    |       Strings       |   StringDtype    |    str    |  arrays.StringArray  |                                                       'string'                                                        |
    |  Boolean (with NA)  |   BooleanDtype   |   bool    | arrays.BooleanArray  |                                                       'boolean'                                                       |
    * pandas 推荐的字符串类型: `StringDtype`

==注意:==
* 默认使用 `int64`, `float64`
* 由于整数没有 `nan`, 因此在判断时 `int` 可能会被 upcast 为 `float`

### 3.3.2. 查看数据类型
* `<Series/DataFrame对象>.dtypes`
* `<Series对象>.dtype`(等效于`<Series对象>.dtypes`)

### 3.3.3. 更改数据类型
* [astype(dtype, copy=True, errors='raise')](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.astype.html): 可以使用 `dict` 指定每列的类型, 如 `{'col1': np.int8, 'col2':'u4'}`; 返回 copy
* [infer_objects(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.infer_objects.html), [convert_dtypes(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.convert_dtypes.html): 自动推导数据类型, convert_dtypes 可以处理 NA 类型数据
* [to_numeric](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.to_numeric.html)/[to_datetime](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.to_numeric.html)/[to_timedelta](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.to_timedelta.html)(..): 对数据进行转换, 数据类型也随之转换

### 3.3.4. 其他
* 在 DataFrame 中, 可以使 [select_dtypes(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.select_dtypes.html) 进行列筛选

## 3.4. 索引
索引 (axes/index/columns), 其实是 Immutable ndarray, 详见 [官方文档: 索引](https://pandas.pydata.org/pandas-docs/stable/user_guide/indexing.html) 和 [官方文档: 多级索引](https://pandas.pydata.org/pandas-docs/stable/user_guide/advanced.html)

### 3.4.1. 有效的索引类型
* array-like 数据
    * 必须 hashable, 且数据长度相等
    * 可以是 non-unique
* [索引对象](https://pandas.pydata.org/pandas-docs/stable/reference/indexing.html), 操作与 Series 类似, 派生对象包括:
    * Range(==默认索引类型==): [RangeIndex(start=None, stop=None, step=None, dtype=None, copy=False, name=None)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.RangeIndex.html)
    * 数字: [Int64Index](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.Int64Index.html), [UInt64Index](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.UInt64Index.html), [Float64Index](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.Float64Index.html)
    * 类别: [CategoricalIndex](https://pandas.pydata.org/pandas-docs/stable/reference/indexing.html#categoricalindex)
    * 间隔: [IntervalIndex](https://pandas.pydata.org/pandas-docs/stable/reference/indexing.html#intervalindex)
    * 多级索引: [MultiIndex](#345-多级索引)
    * 时间: [DatetimeIndex](https://pandas.pydata.org/pandas-docs/stable/reference/indexing.html#datetimeindex), [TimedeltaIndex](https://pandas.pydata.org/pandas-docs/stable/reference/indexing.html#timedeltaindex), [PeriodIndex](https://pandas.pydata.org/pandas-docs/stable/reference/indexing.html#periodindex)

* 索引对象的[主要属性](https://pandas.pydata.org/pandas-docs/stable/reference/indexing.html#properties)
    | 类别 | 属性                                 | 说明                    |
    | ---- | ------------------------------------ | ----------------------- |
    | 尺寸 | shape                                | 形状                    |
    | ^    | ndim                                 | 维度                    |
    | ^    | size                                 | 尺寸                    |
    | 数据 | values                               | 返回array, 内容是索引值 |
    | ^    | dtype                                | 数据类型                |
    | ^    | inferred_type                        | 推导类型                |
    | ^    | T                                    | 转置                    |
    | 内存 | nbytes                               | 内存占用                |
    | 信息 | name                                 | 名称                    |
    | ^    | names                                | 名称(字典方式访问)      |
    | ^    | is_monotonic/is_monotonic_increasing | 单调性                  |
    | ^    | is_monotonic_decreasing              | 单调减                  |
    | ^    | is_unique                            | 是否唯一                |
    | ^    | has_duplicates                       | 是否重复                |
    | ^    | hasnans                              | 有无NAN                 |
    | ^    | is_all_dates                         | 是否全是日期            |
    | ^    | empty                                | 空                      |

* 索引对象的[主要方法](https://pandas.pydata.org/pandas-docs/stable/reference/indexing.html#modifying-and-computations), 与 pd.Series 类似
    * 维护和计算:
        * 重设: `reindex, rename`
        * 索引: `where, take, putmask`
        * 修改: `insert, repeat, delete, drop, drop_duplicates`
        * 逻辑与判断: `all, any, equals, identical, isin, duplicated, is_, is_boolean, is_categorical, is_floating, is_integer, is_interval, is_mixed, is_numeric, is_object`
        * 统计: `max, min, argmax, argmin, unique, nunique, value_counts`
        * 复制: `copy, view`
        * 编码: `factorize`
    * 多级索引相关:  `set_names`, [droplevel(level=0)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.Index.droplevel.html#pandas.Index.droplevel)
    * 缺失数据: `fillna, dropna, isna, notna`
    * 转换: `astype, item, map, ravel, to_list, to_series, to_frame`
    * 排序: `argsort, searchsorted, sort_values`
    * 合并/集合: `append, join, intersection, union, difference, symmetric_difference`
    * 选择: `asof, asof_locs, get_indexer, get_indexer_for, get_indexer_non_unique, get_level_values, get_loc, get_slice_bound, get_value, slice_indexer, slice_locs`
    * 时间相关: `shift`

### 3.4.2. 查看索引
* 行索引: `<Series/DataFrame对象>.index` 或 `<Series对象>.keys()`
* 列索引: `<Series对象>.name` 或 `<DataFrame对象>.columns/keys()`
* 行列索引: `<Series/DataFrame对象>.axes`: 返回列表, `[行索引, 列索引]`

### 3.4.3. 索引方法
* 基本索引:
    > 参见 [官方文档](https://pandas.pydata.org/pandas-docs/stable/user_guide/indexing.html)
    * `[单标签]`, 如: `s[2], s['A']`
    * `[标签 list/array/Series]`, 如: `s[[2,3,6]], s[['A','C','F']]`
    * `[索引值的切片]`, 切片可以是:
        * `slice`, 如: `s[1:5], s[2:100:2], s[3:], s[:-4], s[:], s[::-1]`
        * `slice` 对象, 如: `s[slice(1,5)], s[slice(2,100,2)], s[slice(3,None)], s[slice(None,-4)], s[slice(None)], s[slice(None,None,-1)]`
        * [IndexSlice](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.IndexSlice.html) 对象, 如:
            ``` python
            idx = pd.IndexSlice
            s[idx[:2]]    # 等效于 s[:2] 或 s[slice(None,2)]
            ```
    * `[bool 值 list/array/Series]`, 如 `s[[True,True,False]]` 或 `s[pd.Series([True,True,False])]`
        > ==注意: bool 值 list/array/Series 的长度必须和被索引的对象相同==
    * `[函数表达式]`, 其中:
        * 函数表达式的返回值必须是: 单索引值、索引值列表、索引值切片、bool值 list 或 Series
        * lambda 函数, 如 `df1.loc[lambda x: x['A'] > 0, :]`
        * bool 表达式包括:
            * 简单表达式, 如: `s[s > 3]`
            * lambda 函数, 如: `s[lambda x: x%2==1]`
            * Series/DataFrame 的关系判断方法, 详见 [逻辑、关系判断](#362-逻辑、关系判断)
                * 大小关系
                * `bool(), isin(..), isna(), notna()` 等方法
        * 多个 bool 表达式可以用 `&, |, ~` 等逻辑运算符合并
            > ==注意: 不是 **and, or, not** 等==
            > ==注意: 多个条件时, 用 [query(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.query.html) 更方便==
    * `.loc[索引]`: 一般和`[索引]`一样, 但用于 DataFrame 时或切片索引时区别很大, ==建议在任何时候都使用`.loc[索引]`==:
        > ==用于 DataFrame 时有区别, 详见 "DataFrame的索引"==
        > ==对于切片, **[切片]** 不包含最后一个元素, 而 **.loc[切片]** 却包含最后一个元素==
    * `.at[索引]`: 索引单个元素
        > 比 `[]` 和 `loc` 快很多
    * 基于位置的索引: `.iloc[索引]` 和 `.iat[索引]`
        > ==注意: 其中索引是基于位置序号的, 不是索引值==
    * 索引函数:
        * 过滤: [where(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.where.html) 和 [mask(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.mask.html)
            * 注意: 返回数据的形状与之前相同, 只是不符合条件的会用`NAN`代替, 可用[.dropna(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.dropna.html)删除不符合要求的, 如`df.where(df['A']>3).dropna()`
        * 随机选择: [sample(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.sample.html)
        * 交叉索引: [xs(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.xs.html), 虽然也可用于单级索引, 但多用于多级索引
        * DataFrame 特有的索引函数: [query(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.query.html)
            * `query` 函数中的布尔表达式中, 下面的符号都是合法的:
                * 行列索引名
                * 字符串
                * `and/not/or/&/|/~/not in/in/==/!=`
                * 四则运算符
                * ...
            * 优势: 多个条件时, 用 `query` 比多个 bool 表达式更方便, 如:
                ``` python
                df.query('(a < b) & (b < c)')
                # 等效于
                df[(df['a'] < df['b']) & (df['b'] < df['c'])]
                ```

* DataFrame的索引
    * 列索引: `df[列索引 (切片除外) ]` 或 `df.loc/iloc[:, 列索引]` 或 `df.列名称`
        > ==注意: **df.loc[列索引 / 列索引切片]** 是错误的, 要用 **df.loc[:, 列索引 / 列索引切片]**==
        > ==注意: 将列名称作为属性访问的方式, 速度较慢, 不推荐使用==
    * 行索引: `df[行索引切片]` 或 `df.loc/iloc[行]` 或 `df.loc/iloc[行,:]`
        > ==注意: 除了切片外, **df[行索引]** 都是错误的==
    * 行列同时索引: `df.loc/iloc[行, 列]`, `df.at/iat[行, 列]`
        > ==注意: **df[行, 列]** 是错误的==
    * 行列同时索引, 但标签和位置混用
        * 位置索引转为标签索引:
            * 使用 `.index[位置索引]` 或 `.columns[位置索引]` 转为标签索引
        * 标签索引转为位置索引
            * 使用 `.index/columns.get_loc(标签)` 转为位置索引
            * 使用 `.index/columns.get_indexer(标签索引)` 计算位置索引
                * 其他方法: `get_indexer_for`, `get_indexer_non_unique`, `slice_indexer`, `slice_locs`
    * 行列组合索引, 要注意行、列单独索引的规则:
        * `df.loc/iloc[行].loc/iloc[列]`,
        * `df.loc/iloc[行 (切片除外) ][列]`,
        * `df.loc/iloc[行 (切片) ][列 (切片除外) ]`,
        * `df[列].loc/iloc[行]`
        > 注意: ==**df.loc/iloc[列][行]** 是错误的==
        > 注意: ==**df.loc/iloc[行切片][列切片]** 是错误的==, 这是因为 **.loc/iloc[行切片]** 先转为DataFrame, 然后再用 **[列切片]** 索引就出现了错误
    * 单元素索引: `df.at/iat[行, 列]`
        * 注意: ==**df.at/iat[行][列]** 是错误的==

### 3.4.4. 重设索引
* 设置某列作为索引: [set_index(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.set_index.html)
    * append 参数可以保证当前索引不变, 并增加一个 level 的索引
* 重置索引: `.index = 新索引` 或 `.columns = 新索引`, [reset_index(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.reset_index.html)
* 更改索引的值: [set_axis(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.set_axis.html), `inplace=True` 时等效于 `.index = 新索引` 或 `.columns = 新索引`,
* 重设索引: [reindex(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.reindex.html), [reindex_like(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.reindex_like.html),
* 交互行列: [swapaxes(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.swapaxes.html), 等效于 `.T`

### 3.4.5. 多级索引
可以当作时array of tuples,
> 参见 [官方文档](https://pandas.pydata.org/pandas-docs/stable/user_guide/advanced.html), [API](https://pandas.pydata.org/pandas-docs/stable/reference/indexing.html#multiindex)
* 创建方法:
    * 使用pd.[MultiIndex](https://pandas.pydata.org/pandas-docs/stable/reference/indexing.html#multiindex) 类创建
        * MultiIndex.[from_arrays(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.MultiIndex.from_arrays.html)
        * MultiIndex.[from_product(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.MultiIndex.from_product.html)
        * MultiIndex.[from_tuples(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.MultiIndex.from_tuples.html)
        * MultiIndex.[from_frame(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.MultiIndex.from_frame.html)
    * 用 list of arrays, array of tuple, 交叉的 set of iterables 等直接创建
    * 指定多个列作为索引
        * [set_index(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.set_index.html)
            * 可以同时指定多列
            * 也可以多次指定单列, 但要加参数`append=True`

* 多级索引方法
    * 列索引:
        * `df[第一级列]`
        * `df[第一级列, 第二级列]` 或 `df[(第一级列, 第二级列)]`
        * `df.loc/iloc[:,(第一级列,第二级列)]`
        * 逐层索引, 每一次按照列索引:
            * `df[第一级列][第二级列]`
            * `df[第一级列].loc[:,第二级列]`
            * `df.loc[:,第一级列][第二级列]`
            * `df.loc[:,第一级列].loc[:,第二级列]`
    * 行索引:
        * `df.loc/iloc[第一级行]`
        * `df.loc/iloc[第一级行, 第二级行]` 或 `df.loc/iloc[(第一级行, 第二级行)]`
        * `df.loc/iloc[(第一级行, 第二级行),:]`
        * 逐层索引, 每一次按照行索引:
            * `df.loc/iloc[第一级行].loc/iloc[第二级行]`
        * 按位置索引
            * `df.iloc[第一级行*第二级行数+第二级行]`
    * 行列同时索引:
        * `df.loc[第一级行, 第一级列]` 或 `df.loc[(第一级行, 第一级列)]`
        * `df.loc[第一级行, (第一级列, 第二级列)]` 或 `df.loc[(第一级行, 第二级行), 第一级列]`
        * `df.loc[(第一级行, 第二级行), (第一级列, 第二级列)]`
        * 逐层索引: 先行后列或先列后行都可以
    * 列表索引
        * `df.loc[行索引列表, 列索引列表]`
            * 其中列表中的元素必须是相同的级别, 不能一个是`(第一级行)`, 另一个是`(第一级行, 第二级行)`
        * 逐层索引: 先行列表后列列表, 或先列列表后行列表都可以
    * 交叉索引函数: [.xs(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.xs.html)
        * `df.xs(某一级, axis=行或列, level=级别)`
        * `df.xs((第一级, 第二级, ...), axis=行或列)`

* 多级索引的切片方法 (==注意: 索引要先排好序才能切片索引==)
    * 行或列整体切片
        * 列切片
            * `df.loc[:, 列1:列2]`,
                * 列1可以只包含前几级, 将自动从最小索引开始
                * 列2可以只包含前几级, 将自动到最大索引结束
        * 行切片
            * `df.loc[行1:行2]` 或 `df.loc[行1:行2, :]`
                * 行1可以只包含前几级, 将自动从最小索引开始
                * 行2可以只包含前几级, 将自动到最大索引结束
        * 行列同时切片
            * `df.loc[行1:行2, 列1:列2]`
            * 逐层索引
    * 行或列的某一级单独切片
        * 可以仅选取某一级进行切片, 不切片的级别如下处理:
            * 如果全选, 用`slice(None)`
            * 如果只选一个, 指定 `标签`
        * 切片只能用`slice(..)`函数 或 [IndexSlice](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.IndexSlice.html) 对象, 不能用`start:stop:interval`形式, 如
            ``` python
            idx = pd.IndexSlice
            df.loc[idx[['A1', 'A3'], :,  ['C1', 'C3']], :]
            # 等效于
            df.loc[(slice('A1', 'A3'), slice(None), ['C1', 'C3']), :]
            ```
        * 具体情况
            * 列分级切片: `df.loc[:, (列1切片, 列2切片)]`
            * 行分级切片: `df.loc[(行1切片, 行2切片),]` 或 `df.loc[(行1切片, 行2切片), :]`
                * ==注意: 必须加逗号==, 可以不加列全选`:`
            * 行列同时分级切片: `df.loc[(行1切片, 行2切片), (列1切片, 列2切片)]`

* 索引层的交换
    * [swaplevel(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.swaplevel.html)
    * [reorder_levels(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.reorder_levels.html)

* 删除某个级别的索引
    * [droplevel(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.droplevel.html)

* 多级索引对象的属性和方法
    * [主要属性](https://pandas.pydata.org/pandas-docs/stable/reference/indexing.html#multiindex-properties): `names, levels, nlevels, levshape, codes`
    * [主要方法](https://pandas.pydata.org/pandas-docs/stable/reference/indexing.html#multiindex-components):
        * 继承自[Index对象的方法](#341-有效的索引类型)
        * 对象维护: [set_levels(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.MultiIndex.set_levels.html), [sortlevel(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.MultiIndex.sortlevel.html), [droplevel(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.MultiIndex.droplevel.html), [swaplevel(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.MultiIndex.swaplevel.html), [reorder_levels(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.MultiIndex.reorder_levels.html), [remove_unused_levels(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.MultiIndex.remove_unused_levels.html), [set_codes(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.MultiIndex.set_codes.html)
        * 访问数据: [get_loc(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.MultiIndex.get_loc.html), [get_locs(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.MultiIndex.get_locs.html), [get_loc_level(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.MultiIndex.get_loc_level.html), [get_indexer(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.MultiIndex.get_indexer.html), [get_level_values(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.MultiIndex.get_level_values.html)
        * 数据转换: [to_flat_index(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.MultiIndex.to_flat_index.html), [to_frame(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.MultiIndex.to_frame.html)
        * 信息: [is_lexsorted(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.MultiIndex.is_lexsorted.html)

### 3.4.6. 索引重命名
* [rename(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.rename.html): 修改列或者行索引标签, 而不是索引对象的名称
* [rename_axis(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.rename_axis.html): 修改索引对象的名称 (或多级索引中某一层的索引名), 而不是索引标签
* [add_prefix(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.add_prefix.html), [add_suffix(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.add_suffix.html): 在索引上添加前缀或后缀

## 3.5. 基本数据操作

### 3.5.1. 原则: 对齐与扩展

* 两个 Series/DataFrame 会按照行、列索引 (而非位置) 对齐进行运算
* 两个 Series/DataFrame 的尺寸不同时, 运算后的 object 的尺寸的扩展为两者中(最大行, 最大列)

### 3.5.2. 原则: missing data
> 参见 [官方文档](https://pandas.pydata.org/pandas-docs/stable/user_guide/missing_data.html)

* `NaN`, `NaT` 是 missing data, 与之运算的结果还是 `NaN`
* 除非运算时加上选项填充、内插、忽略选项
* 也可以丢弃包含missing data的元素
* `NaN` != `NaN`
* `equals`与`==`不同, `equals`将 NaN 当成一样的

### 3.5.3. 数据访问
* 通过索引访问, 详见 [索引](#34-索引)
* 索引相关函数: [where(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.where.html), [mask(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.mask.html), [query(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.query.html), [xs(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.xs.html)
* 片段: [head(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.head.html), [tail(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.tail.html)
* 筛选: [where(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.where.html), [mask(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.mask.html), [query(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.query.html), [filter(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.filter.html), [truncate(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.truncate.html)
* 随机取样: [sample(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.sample.html)
* 其他访问方式:
    * [get(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.get.html)
    * [take(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.take.html)

### 3.5.4. 迭代
* 列迭代: [items(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.items.html)
* 行迭代:
    * [iterrows(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.iterrows.html)
    * [itertuples(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.itertuples.html), 普遍认为效率最高

### 3.5.5. 数据信息
* 基本信息: [info(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.info.html)
* 是否为空: `empty`属性
* 类型判断: [isna()](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.isna.html) / [notna()](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.notna.html)
    * 判断 DataFrame 中是否有 NaN:
        ``` python
        df.isna().values.all()  # 最快
        df.notna().any().all()
        ```
* 数据维度、尺寸、内存占用:
    * `ndim` 属性
    * `shape/size` 属性
    * [memory_usage(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.memory_usage.html)
    * Series 特有:
        * `nbytes` 属性
        * `hasnans` 属性
* 单调性 (Series 特有属性) : `is_monotonic_increasing, is_monotonic_decreasing`

### 3.5.6. 表操作
* 合并, 详见 [官方示例](https://pandas.pydata.org/pandas-docs/stable/user_guide/merging.html)
    * [pd.concat](https://pandas.pydata.org/docs/reference/api/pandas.concat.html)(objs, axis=0, join='outer', ignore_index= False, keys=None, levels=None, names=None, verify_integrity=False, sort=False, copy=True)
        > * **行拼接**: axis=0: index1 + index2, columns 取集合, join='outer': 并集; 'inner': 交集
        >   * 当axis=0时, pd.concat([obj1, obj2])与 obj1.append(obj2) 的效果是相同的, 使用参数 key 可以为每个数据集 (bj1, obj2) 指定块标记
        > * **列拼接**: axis=1: columns1 + columns2, index 取集合, join='outer': 并集; 'inner': 交集
        >   * 当axis=1时, pd.concat([obj1, obj2], axis=1) 与 pd.merge(obj1, obj2, left_index=True, right_index=True, how='outer') 的效果是相同的
    * [pd.merge](https://pandas.pydata.org/docs/reference/api/pandas.merge.html)(left, right, how='inner', on=None, left_on=None, right_on=None, left_index=False, right_index=False, sort=False, suffixes=('_x', '_y'), copy=True, indicator=False, validate=None),
    * [df.merge](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.merge.html)
        > * 主要参数:
        >   * how: 连接方式, 有inner、left、right、outer, 默认为inner
        >   * on: 指定用于连接的 column 名称, 必须同时存在于左、右两个DataFrame中, 默认是以两个DataFrame列名的交集作为连接键, 要实现多键连接, ‘on’参数后传入多键列表即可
        >   * left_on/right_on: 左/右侧DataFrame中用于连接键的列名, 这个参数在左右列名不同但代表的含义相同时非常有用;
        >   * left_index/right_index: 使用左/右侧DataFrame中的行索引作为连接键 ( 但是这种情况下最好用JOIN)
        > * **典型应用场景**:  两张表有相同内容的某一列, 根据主键将两张表进行列拼接整合到一张表中, 合并表的列数等于两个原数据表的列数和减去连接键的数量
        > * df1和df2的 columns 仅有一项重复时, 存在如下三种类型的数据合并:
        >   1. 一对一: 若 df1 和 df2 的重名列中, 各列的值均不重复, 能够自动识别相同的行作为主键, 进行列拼接;
        >       > 备注: 共同列中的元素位置可以不一致, 能够自动选取相同的行进行拼接。另外, merge() 默认会丢弃原来的索引, 重新生成索引
        >   2. 多对一: 若 df1 和 df2 的重名列中, 有一列的值有重复, 通过多对一合并获得的连接表将会保留重复值
        >   3. 多对多: 若 df1 和 df2 的重名列中, 都包含重复值, 那么通过多对多合并获得的连接表将会保留所有重复值
        >       > 备注:  若重名列有 m 行重名, df2 有 n 行重名, 则合并表将有 m×n 行数据
        > * df1 和 df2 的 columns 有两项及以上重复时, 即: 实现多键连接, 仅需在'on'参数后传入多键列表即可
    * [df.join](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.join.html)(other, on=None, how='left', lsuffix='', rsuffix='', sort=False)
        > * **行拼接**:
        >   * 无重复列的两个表 df1 和 df2: 直接使用df1.join(df2)即可, 无需添加任何参数, 合并表的行数取左右表或集合, column 直接相加
        >   * 两个表有重复的列名: 需指定lsuffix, rsuffix参数
        > * **列拼接**, 需借助参数‘on’。常见的基于列索引的列拼接方式有3种:
        >   * 列名不同, 列内容有相同: 需要用到 l.join(r.set_index(key of r), on='key of l')
        >   * 列名和列内容均有相同: 需要用到l.join(r.set_index(key), on='key')
        >   * 列名不同, 列内容也不同: 这种情况是典型的基于行索引进行列拼接, 不能用JOIN的ON参数
    > ==注意: 以上操作后返回的是副本, 不是在原数据上直接操作==
    * [df.combine](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.combine.html), [df.combine_first](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.combine_first.html), [s.combine](https://pandas.pydata.org/docs/reference/api/pandas.Series.combine.html), [s.combine_first](https://pandas.pydata.org/docs/reference/api/pandas.Series.combine_first.html):
        > 用 df2/s2 更新 df1/s1 中的空值, 且 index1 = index1 ∪ index2
* 对齐: [align(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.align.html)
* 插入列: [insert(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.insert.html), [assign(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.assign.html)
* 变形: [stack(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.stack.html), [unstack(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.unstack.html), [explode(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.explode.html), [squeeze(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.squeeze.html)
    * 对于Series: [ravel(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.Series.ravel.html), [repeat(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.Series.repeat.html)

### 3.5.7. 元素操作
* 替换:
    * [replace](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.replace.html), [update](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.update.html)
    * [where(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.where.html), [mask(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.mask.html)
    * [fillna(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.fillna.html)
        * `backfill/bfill(..)`, `ffill/pad(..)`,
    * [df.combine(..)](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.combine.html), [df.combine_first(..)](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.combine_first.html), [s.combine(..)](https://pandas.pydata.org/docs/reference/api/pandas.Series.combine.html), [s.combine_first(..)](https://pandas.pydata.org/docs/reference/api/pandas.Series.combine_first.html):
* 删除
    * [drop(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.drop.html), [dropna(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.dropna.html)
    * [pop(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.pop.html)
    * `del ..`
* 重复元素:
    * 查询: [duplicated(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.duplicated.html)
    * 删除: [drop_duplicates(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.drop_duplicates.html)

### 3.5.8. 排序
* 按索引: [sort_index(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.sort_index.html)
* 按值: [sort_values(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.sort_values.html)
* 对于Series:
    * [argmin(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.Series.argmin.html), [argmax(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.Series.argmax.html), [argsort(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.Series.argsort.html)
    * [searchsorted(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.Series.searchsorted.html)

### 3.5.9. 转换
* 创建副本: [copy(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.copy.html)
    * 对于Series: [view(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.Series.view.html)
* 转为 np.array
    * `values`属性
    * Series 专有: [to_numpy(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.Series.to_numpy.html)
* 到其他类型
    * [to_dict(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.to_dict.html), [to_records(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.to_records.html), [to_string(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.to_string.html)
    * Series 专有: [to_list(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.Series.to_list.html)
* 从其他类型
    * [from_dict(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.from_dict.html), [from_records(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.from_records.html)
* 其他:
    * 对于 Series: [factorize(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.Series.factorize.html)

## 3.6. 高级数据操作

### 3.6.1. 计算
* 基本:
    * `+, -, *, /, %`
    * [add(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.add.html), [sub(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.sub.html), [mul(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.mul.html), [div(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.div.html), [truediv(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.truediv.html), [floordiv(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.floordiv.html), [mod(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.mod.html)
    * [radd(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.radd.html), [rsub(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.rsub.html), [rmul(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.rmul.html), [rdiv(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.rdiv.html), [rtruediv(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.rtruediv.html), [rfloordiv(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.rfloordiv.html), [rmod(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.rmod.html)
    * [pow(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.pow.html), [rpow(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.rpow.html)
    * [sum(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.sum.html), [prod/product(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.prod.html)
    * [cumsum(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.cumsum.html), [cumprod(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.cumprod.html)
* 绝对值: [abs(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.abs.html)
* 近似: [round(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.round.html)
* 差值/微分: [diff(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.diff.html)
* 矩阵: [dot(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.dot.html), [transpose(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.transpose.html), `T`属性
* 内插: [interpolate(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.interpolate.html)
* 运行代码: [eval(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.eval.html)

### 3.6.2. 逻辑、关系判断
* 大小/相等判断:
    * `==, !=, <, <=, >, >=`
    * [eq(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.eq.html),  [ne(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.ne.html),  [lt(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.lt.html),  [le(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.le.html),  [gt(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.gt.html),  [ge(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.ge.html)
    * [equals(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.equals.html)
    > ==注意==
    > `np.nan` != `np.nan`
    > `equals`与`==`不同, 将 `np.nan` 当成一样的
    * [compare(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.compare.html)
    * [s.between(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.Series.between.html)
* 规约判断: [all(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.all.html),  [any(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.any.html)
    * ==不要使用 python 内建的 `all` 和 `any`, 结果有误==
* 布尔判断: [bool(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.bool.html)
* missing data: [isna / isnull(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.isna.html), [notna / notnull(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.notna.html)
* 其他判断: [isin(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.isin.html)

### 3.6.3. 统计
* 基本信息: [describe(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.describe.html)
* 极值:
    * [max(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.max.html), [min(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.min.html), [mean(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.mean.html), [median(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.median.html)
    * [nlargest(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.nlargest.html), [nsmallest(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.nsmallest.html)
    * [idxmax(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.idxmax.html), [idxmin(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.idxmin.html)
    * [cummax(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.cummax.html), [cummin(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.cummin.html)
    * [mode(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.mode.html): 出现次数最多的数
* 偏差:
    * 方差: [var(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.var.html)
    * 标准差: [std(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.std.html)
    * 协方差: [cov(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.cov.html)
    * 其他偏差: [sem(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.sem.html), [skew(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.skew.html)
* 相关系数:
    * 对于DataFrame: [corr(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.corr.html), [corrwith(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.corrwith.html)
    * 对于Series: [autocorr(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.Series.autocorr.html)
* 计数: [count(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.count.html)
    * 对于 Series: [value_counts(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.Series.value_counts.html)
* 剪裁: [clip(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.clip.html)
* 分级:
    * [rank(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.rank.html), [pct_change(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.pct_change.html), [quantile(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.quantile.html)
    * [pd.cut(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.cut.html), [pd.qcut(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.cut.html)
* 峰度: [kurt/kurtosis(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.kurt.html)

### 3.6.4. 集合
* [nunique(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.nunique.html)
* 对于 Series: [unique(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.Series.unique.html)
    > 可以先将 Series 转为 np.array, 然后再用 np 的集合函数

### 3.6.5. Split-Apply-Combine (SAC)
**[SAC](https://pandas.pydata.org/pandas-docs/stable/user_guide/groupby.html)**, 其中:
> 1. split 指基于某一些规则, 将数据拆成若干组,
> 1. apply 是指对每一组独立地使用函数, 在该过程中, 我们实际往往会遇到四类问题:
>       * 整合 (Aggregation) ——即分组计算统计量 (如求均值、求每组元素个数)
>       * 变换 (Transformation) ——即分组对每个单元的数据进行操作 (如元素标准化)
>       * 过滤 (Filtration) ——即按照某些规则筛选出一些组 (如选出组内某一指标小于50的组)
>       * 综合问题——即前面提及的三种问题的混合
> 1. combine指将每一组的结果组合成某一类数据结构

#### 3.6.5.1. Split (groupby)
> 参见 [官方文档](https://pandas.pydata.org/pandas-docs/stable/user_guide/groupby.html#splitting-an-object-into-groups), [API](https://pandas.pydata.org/pandas-docs/stable/reference/groupby.html)
* 分组对象: [DataFrame.groupby(by=None, axis=0, level=None, as_index=True, sort=True, group_keys=True, squeeze=NoDefault.no_default, observed=False, dropna=True)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.groupby.html)
    * 可以按一个或多个列 (或行) 分组
    * 也可以按某级索引分组
    * 也可以同时按行和列 (以及多级索引级别) 分组
        * 可用 [pd.Grouper(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.Grouper.html) 创建分组依据对象, 如
        ``` python
        df.groupby([pd.Grouper(level=1), 'A'])
        ```
    * 也可以是函数, 返回值作为索引, 如
        ``` python
        df.groupby(lambda x: print(x))
        df.groupby(lambda x:'奇数行' if not df.index.get_loc(x)%2==1 else '偶数行').groups
        ```
* 选取分组: [get_group(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.core.groupby.GroupBy.get_group.html), 如
    ``` python
    df.groupby(['A', 'B']).get_group(('bar', 'one'))
    ```
* 选取列: `分组[列索引]`, 如
    ``` python
    df.groupby(['A', 'B']).get_group(('bar', 'one'))
    ```
* 迭代分组:
    ``` python
    for name, group in grouped:
        print(name)
        print(group)
    ```
* 分组对象的主要属性:
    * `groups`: Dict {group name -> group labels}
    * `ngroups`: 有多少组
    * `indices`: Dict {group name -> group indices}.
    * Series特有: `is_monotonic_increasing, is_monotonic_decreasing`
* 分组对象的方法:
    * 信息: [describe(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.core.groupby.DataFrameGroupBy.describe.html), [ngroup(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.core.groupby.GroupBy.ngroup.html), [size()](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.core.groupby.GroupBy.size.html)
    * 选取: [get_group(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.core.groupby.GroupBy.get_group.html), [first(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.core.groupby.GroupBy.first.html), [last(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.core.groupby.GroupBy.last.html), [head(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.core.groupby.GroupBy.head.html), [tail(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.core.groupby.GroupBy.tail.html), [nth(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.core.groupby.GroupBy.nth.html), [filter(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.core.groupby.DataFrameGroupBy.filter.html), [take(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.core.groupby.DataFrameGroupBy.take.html)
    * 计算: [sum(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.core.groupby.GroupBy.sum.html), [ohlc(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.core.groupby.GroupBy.ohlc.html), [prod(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.core.groupby.GroupBy.prod.html), [cumsum(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.core.groupby.GroupBy.cumsum.html), [cumprod(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.core.groupby.GroupBy.cumprod.html), [diff(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.core.groupby.DataFrameGroupBy.diff.html), [corr(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.core.groupby.DataFrameGroupBy.corr.html), [cov(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.core.groupby.DataFrameGroupBy.cov.html)
        * DataFrame特有: [corrwith(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.core.groupby.DataFrameGroupBy.corrwith.html)
    * 填充: [fillna(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.core.groupby.DataFrameGroupBy.fillna.html), [bfill(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.core.groupby.GroupBy.bfill.html), [ffill(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.core.groupby.GroupBy.ffill.html)
    * 统计: [count(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.core.groupby.GroupBy.count.html), [cumcount(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.core.groupby.GroupBy.cumcount.html), [nunique(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.core.groupby.DataFrameGroupBy.nunique.html), [max(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.core.groupby.GroupBy.max.html), [min(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.core.groupby.GroupBy.min.html), [mean(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.core.groupby.GroupBy.mean.html), [median(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.core.groupby.GroupBy.median.html), [cummax(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.core.groupby.GroupBy.cummax.html), [cummin(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.core.groupby.GroupBy.cummin.html), [idxmax(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.core.groupby.DataFrameGroupBy.idxmax.html), [idxmin(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.core.groupby.DataFrameGroupBy.idxmin.html), [rank(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.core.groupby.GroupBy.rank.html), [pct_change(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.core.groupby.GroupBy.pct_change.html), [var(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.core.groupby.GroupBy.var.html), [std(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.core.groupby.GroupBy.std.html), [sem(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.core.groupby.GroupBy.sem.html), [mad(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.core.groupby.DataFrameGroupBy.mad.html), [skew(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.core.groupby.DataFrameGroupBy.skew.html), [quantile(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.core.groupby.DataFrameGroupBy.quantile.html), [resample(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.core.groupby.DataFrameGroupBy.resample.html)
        * Series特有: [nlargest(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.core.groupby.SeriesGroupBy.nlargest.html), [nsmallest(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.core.groupby.SeriesGroupBy.nsmallest.html), [unique()](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.core.groupby.SeriesGroupBy.unique.html), [value_counts(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.core.groupby.SeriesGroupBy.value_counts.html)
    * 逻辑: [all](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.core.groupby.GroupBy.all.html), [any](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.core.groupby.GroupBy.any.html)
    * 函数:
        * 表级: [pipe](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.core.groupby.GroupBy.pipe.html)
        * 行列级: [apply](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.core.groupby.GroupBy.apply.html)
        * 聚合: [agg/aggregate](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.core.groupby.GroupBy.agg.html)
        * 变换: [transform](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.core.groupby.GroupBy.transform.html)
    * 绘图: [hist(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.core.groupby.DataFrameGroupBy.hist.html), [plot(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.core.groupby.DataFrameGroupBy.plot.html)
        * DataFrame特有: [boxplot(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.core.groupby.DataFrameGroupBy.boxplot.html)

#### 3.6.5.2. Apply (聚合: agg, 变换: transform, 过滤: filter, 应用: apply)
* 聚合: [agg/aggregate(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.agg.html)
    > 聚合是把一堆数, 变成一个标量, mean, sum, size, count, std, var, sem, describe, first, last, nth, min, max 都是聚合函数
    * 可以使用现有函数, 也可以使用自定义函数, 示例
        ``` python
        # 使用现有函数
        grp.agg([np.sum, np.mean, np.std])   # 常用函数
        grp.agg(['sum','mean','std'])   # 常用函数
        grp.agg([('rename_sum','sum'),('rename_mean','mean')])  # 利用元组进行重命名
        grp.agg({'Math':['mean','max'],'Height':'var'}) # 指定哪些函数作用哪些列
        # lambda函数
        grp['Math'].agg(lambda x: print(x.head(),'间隔'))   # 使用自定义函数
        grp['Math'].agg(lambda x: x.max()-x.min())  # 使用自定义函数
        # 利用NamedAgg函数进行多个聚合
        def R1(x):
            return x.max()-x.min()
        def R2(x):
            return x.max()-x.median()
        grp['Math'].agg(min_score1=pd.NamedAgg(column='col1', aggfunc=R1),
                        max_score1=pd.NamedAgg(column='col2', aggfunc='max'),
                        range_score2=pd.NamedAgg(column='col3', aggfunc=R2))
        # 带参数的聚合函数
        def f(s,low,high):
            return s.between(low,high).max()
        grp['Math'].agg(f,50,52)
        #
        ```
* 命名聚合: `pd.NamedAgg`, 可用于多个聚合
    > ==注意: 不支持lambda函数, 但是可以使用外置的def函数==
* 变换: [transform(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.transform.html)
    * 返回对象的索引与分组相同, 变换函数必须返回的结果的尺寸必须与分组相同 (或可扩展到相同尺寸) , 一列一列的操作, 不能 inplace 操作
    ``` python
    # transform函数中传入的对象是组内的列, 并且返回值需要与列长完全一致
    grp[['Math','Height']].transform(lambda x:x-x.min())
    # 如果返回了标量值, 那么组内的所有元素会被广播为这个值
    grp[['Math','Height']].transform(lambda x:x.mean())
    ```
* 过滤: [filter(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.filter.html)
    * filter函数是用来筛选某些组的 (务必记住结果是组的全体) , 因此传入的值应当是布尔标量
    * 示例:
        ``` python
        grp[['Math','Physics']].filter(lambda x:(x['Math']>32).all()).head()
        ```
* 应用: [apply(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.apply.html)
    * 示例
    ``` python
    # 返回标量
    df.groupby('School').apply(lambda x:x.max())
    # 返回列表
    df.groupby('School').apply(lambda x:x-x.min())
    # 返回 DataFrame
    df.groupby('School').apply(lambda x: pd.DataFrame(
                                            {'col1':x['Math']-x['Math'].max(),
                                             'col2':x['Math']-x['Math'].min(),
                                             'col3':x['Height']-x['Height'].max(),
                                             'col4':x['Height']-x['Height'].min()}))
    # 用apply同时统计多个指标
    from collections import OrderedDict
    def f(df):
        data = OrderedDict()
        data['M_sum'] = df['Math'].sum()
        data['W_var'] = df['Weight'].var()
        data['H_mean'] = df['Height'].mean()
        return pd.Series(data)
    grp.apply(f)
    ```

#### 3.6.5.3. Combine
> 参见 [官方文档](https://pandas.pydata.org/pandas-docs/stable/user_guide/merging.html)
> 参见 [表操作](#356-表操作)

### 3.6.6. 函数映射
> 参见 [官方文档](https://pandas.pydata.org/pandas-docs/stable/getting_started/basics.html)
* 表级: [pipe(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.pipe.html)
* 行列级: [apply(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.apply.html)
* 元素级:
    * 对于DataFrame: [applymap(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.applymap.html)
    * 对于Series: [map(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.Series.map.html)
* 聚合: [agg/aggregate(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.agg.html)
* 变换: [transform(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.transform.html)

### 3.6.7. 数据透视表
* [pd.pivot(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.pivot.html), [pd.pivot_table(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.pivot_table.html)
* [pivot(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.pivot.html), [pivot_table(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.pivot_table.html)
    > pivot_table速度稍慢
* [pd.crosstab(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.crosstab.html)
* [melt(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.melt.html)

### 3.6.8. window
详见 [官方文档](https://pandas.pydata.org/pandas-docs/stable/user_guide/computation.html#window-functions)
* 滚动: [rolling(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.rolling.html)
* 扩展: [expanding(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.expanding.html)
* 指数加权: [ewm(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.ewm.html)

### 3.6.9. 日期时间
* 通过`.dt`对日期时间Series进行操作
* 时间Series处理
* `at_time, between_time, first, last`

### 3.6.10. 字符串处理
* 通过`.str`属性操作Series

## 3.7. 可视化
* [内置 plot](https://pandas.pydata.org/pandas-docs/stable/user_guide/visualization.html)
    * `plt.plot`
    * `plot.area`
    * `plot.bar`
    * `plot.barh`
    * `plot.box`
    * `plot.density`
    * `plot.hexbin`
    * `plot.hist`
    * `plot.kde`
    * `plot.line`
    * `plot.pie`
    * `plot.scatter`
    * `boxplot`
    * `hist`
* 也可以使用 matplotlib

## 3.8. 输入输出
> 参见 [官方教程](https://pandas.pydata.org/pandas-docs/stable/user_guide/io.html)
* 支持
    * 文本文件: [CSV](https://pandas.pydata.org/pandas-docs/stable/user_guide/io.html#csv-text-files), JSON, HTML, 剪切板, ...
    * 二进制文件: Excel, [HDF5](https://pandas.pydata.org/pandas-docs/stable/user_guide/io.html#io-hdf5), Python Pickle, ...
    * SQL: SQL, gbq(Google Big Query)
* API
    * CSV
        * [pd.read_csv(...)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.read_csv.html#)
            * 支持迭代读取, 参数: `iterator=True` 或 `chunksize=数值`
        * DataFrame 对象方法: [.to_csv(...)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.to_csv.html)
        * Series 对象方法: [.to_csv(...)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.Series.to_csv.html)
    * HDF5
        * [pd.read_hdf(...)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.read_hdf.html)
            * 支持迭代读取, 参数: `iterator=True` 或 `chunksize=数值`
        * DataFrame 对象方法: [.to_hdf(...)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.to_hdf.html)
        * Series 对象方法: [.to_hdf(...)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.Series.to_hdf.html)
        * `pd.HDFStore` 对象
            * 支持容器
            * 构造函数: `pd.HDFStore(path, mode="a", complevel=None, complib=None, fletcher32=False, **kwargs)`
            * 对象方法
                * [.append(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.HDFStore.append.html)
                * [.get(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.HDFStore.get.html)
                * [.groups(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.HDFStore.groups.html)
                * [.info(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.HDFStore.info.html)
                * [.keys(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.HDFStore.keys.html)
                * [.put(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.HDFStore.put.html)
                * [.select(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.HDFStore.select.html)
                * [.walk(..)](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.HDFStore.walk.html)

## 3.9. options
> 详见 [官方文档](https://pandas.pydata.org/pandas-docs/stable/user_guide/options.html)
* 选项包括: 计算 (是否使用 numexpr, bottleneck) , 显示, IO选项 ( excel, hdf5, parquet) , 模式, 绘图等
* 设置方法:
    * 属性: `pd.options.xxx`
    * method: `get_option`/`set_option`/`reset_option`/`describe_option`/`option_context`

----------------------------------------------------------------
# 4. scipy
> 参见 [官方文档](https://docs.scipy.org/doc/scipy/reference/)

| 子模块         | 说明                                                                                 |
| :------------- | ------------------------------------------------------------------------------------ |
| cluster        | [聚类算法](https://docs.scipy.org/doc/scipy/reference/cluster.html)                  |
| constants      | [物理和数学常数](https://docs.scipy.org/doc/scipy/reference/constants.html)          |
| fftpack        | [快速傅里叶变换](https://docs.scipy.org/doc/scipy/reference/fft.html)                |
| integrate      | [积分和常微分方程](https://docs.scipy.org/doc/scipy/reference/integrate.html)        |
| interpolate    | [内插和平滑](https://docs.scipy.org/doc/scipy/reference/interpolate.html)            |
| io             | [输入和输出](https://docs.scipy.org/doc/scipy/reference/io.html)                     |
| linalg         | [线性代数](https://docs.scipy.org/doc/scipy/reference/linalg.html)                   |
| ndimage        | [N维图像处理](https://docs.scipy.org/doc/scipy/reference/ndimage.html)               |
| odr            | [正交距离回归](https://docs.scipy.org/doc/scipy/reference/odr.html)                  |
| ==optimize==   | [优化和寻根](https://docs.scipy.org/doc/scipy/reference/optimize.html)               |
| signal         | [信号处理](https://docs.scipy.org/doc/scipy/reference/signal.html)                   |
| sparse         | [稀疏矩阵](https://docs.scipy.org/doc/scipy/reference/sparse.html)                   |
| sparse.linalg  | [稀疏矩阵的线性代数](https://docs.scipy.org/doc/scipy/reference/sparse.linalg.html)  |
| sparse.csgraph | [稀疏矩阵的图像处理](https://docs.scipy.org/doc/scipy/reference/sparse.csgraph.html) |
| spatial        | [空间数据结构和算法](https://docs.scipy.org/doc/scipy/reference/spatial.html)        |
| special        | [特殊函数](https://docs.scipy.org/doc/scipy/reference/special.html)                  |
| stats          | [统计和分布](https://docs.scipy.org/doc/scipy/reference/stats.html)                  |
| stats.mstats   | [掩码阵列的统计和分布](https://docs.scipy.org/doc/scipy/reference/stats.mstats.html) |

## 4.1. optimize

### 4.1.1. 最小二乘法拟合
``` python
from scipy.optimize import leastsq
```

### 4.1.2. Curve Fitting
* `curve_fit(f, xdata, ydata[, p0, sigma, ...])` 用非线性最小二乘法拟合
    * 实例
    ``` python {.line-numbers}
    import numpy as np
    from scipy.optimize import curve_fit
    import matplotlib.pyplot as plt
    # 创建一个函数模型用来生成数据
    def func(x, a, b, c):
        return a * np.exp(-((x - b) ** 2) / (2 * c ** 2))
    # 生成原始数据
    x = np.linspace(0, 10, 100)
    y = func(x, 1, 5, 2)
    # 对原始数据增加噪声
    yn = y + 0.2 * np.random.normal(size=len(x))
    # 使用curve_fit函数拟合噪声数据
    popt, pcov = curve_fit(func, x, yn)
    # popt返回最拟合给定的函数模型func的参数值
    print(popt)
    plt.plot(x, yn)
    plt.plot(x, func(x, popt[0], popt[1], popt[2]))
    plt.show()
    ```

--------------------------------------------------------------------------------
