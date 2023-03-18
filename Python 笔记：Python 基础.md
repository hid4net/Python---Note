
<h1 style="text-align:center">Python 基础</h1>

--------------------------------------------------------------------------------
[返回 Outline](outline.md)

<!-- @import "[TOC]" {cmd="toc" depthFrom=1 depthTo=3 orderedList=false} -->

<!-- code_chunk_output -->

- [1. 准备](#1-准备)
- [2. 基础语法](#2-基础语法)
  - [2.1. 一切皆对象](#21-一切皆对象)
  - [2.2. 关键词](#22-关键词)
    - [2.2.1. 所有关键词](#221-所有关键词)
    - [2.2.2. 关键词分类](#222-关键词分类)
  - [2.3. 标识符](#23-标识符)
  - [2.4. 语句结构](#24-语句结构)
  - [2.5. 数据类型](#25-数据类型)
    - [2.5.1. 概述](#251-概述)
    - [2.5.2. Number](#252-number)
    - [2.5.3. String](#253-string)
    - [2.5.4. List](#254-list)
    - [2.5.5. Tuple](#255-tuple)
    - [2.5.6. Set](#256-set)
    - [2.5.7. Dictionary](#257-dictionary)
  - [2.6. 变量](#26-变量)
  - [2.7. 运算符](#27-运算符)
    - [2.7.1. 基本运算符](#271-基本运算符)
    - [2.7.2. 特殊运算符](#272-特殊运算符)
    - [2.7.3. 运算符优先级](#273-运算符优先级)
  - [2.8. 程序控制](#28-程序控制)
    - [2.8.1. 条件控制](#281-条件控制)
    - [2.8.2. 循环控制](#282-循环控制)
  - [2.9. 函数与作用域](#29-函数与作用域)
    - [2.9.1. 函数声明与调用](#291-函数声明与调用)
    - [2.9.2. 函数属性](#292-函数属性)
    - [2.9.3. 闭包](#293-闭包)
    - [2.9.4. 匿名函数 lambda](#294-匿名函数-lambda)
    - [2.9.5. 内建函数](#295-内建函数)
    - [2.9.6. 偏函数](#296-偏函数)
    - [2.9.7. 作用域](#297-作用域)
  - [2.10. 模块和包](#210-模块和包)
  - [2.11. 面向对象](#211-面向对象)
    - [2.11.1. 类声明](#2111-类声明)
    - [2.11.2. 属性](#2112-属性)
    - [2.11.3. 方法](#2113-方法)
    - [2.11.4. 对象](#2114-对象)
    - [2.11.5. 继承与派生](#2115-继承与派生)
    - [2.11.6. 元类](#2116-元类)
  - [2.12. 错误和异常](#212-错误和异常)
    - [2.12.1. 异常处理](#2121-异常处理)
    - [2.12.2. 产生异常](#2122-产生异常)
    - [2.12.3. 断言](#2123-断言)
    - [2.12.4. 内建异常](#2124-内建异常)
    - [2.12.5. 自定义异常](#2125-自定义异常)
  - [2.13. 输入/输出](#213-输入输出)
- [3. 高级语法](#3-高级语法)
  - [3.1. 迭代器 (iterator)](#31-迭代器-iterator)
  - [3.2. 生成器 (generator)](#32-生成器-generator)
    - [3.2.1. 生成器](#321-生成器)
    - [3.2.2. 创建生成器](#322-创建生成器)
    - [3.2.3. yield from](#323-yield-from)
  - [3.3. 装饰器 (Decorator)](#33-装饰器-decorator)
    - [3.3.1. 基础](#331-基础)
    - [3.3.2. 进阶](#332-进阶)
  - [3.4. 上下文管理器 (contextor)](#34-上下文管理器-contextor)
- [4. 标准库简介](#4-标准库简介)
  - [4.1. 内建库 \_\_builtins__](#41-内建库-__builtins__)
  - [4.2. 标准库](#42-标准库)

<!-- /code_chunk_output -->

--------------------------------------------------------------------------------
# 1. 准备
> [Python官方网址](https://www.python.org/)
> [官方文档(en)](https://docs.python.org/3/)
> [官方文档 (中文版)](https://docs.python.org/zh-cn/3/)

* **基本命令**:
    ``` shell
    python -V
    python -h
    help(库或函数)
    ```
* **编码**: Python 3 源文件使用 UTF-8
* **解释器**: 在 CPython/IPython 等解释器中, 最后两次的值分别存在 `_` 和 `__` 中

--------------------------------------------------------------------------------
# 2. 基础语法

## 2.1. 一切皆对象
==数据、操作符、函数、类、......, 所有都是**对象**==

## 2.2. 关键词

### 2.2.1. 所有关键词
```python {.line-numbers}
False, None, True,
and, as, assert, async, await,
break,
class, continue,
def, del,
elif, else, except,
finally, for, from,
global,
if, import, in, is,
lambda,
nonlocal, not,
or,
pass,
raise, return,
try,
while, with,
yield
```
可以使用以下代码查询关键词
```python {.line-numbers}
import keyword
print(keyword.kwlist)
```

### 2.2.2. 关键词分类
|     类别     | 关键词                                                                        |
| :----------: | :---------------------------------------------------------------------------- |
|   内建常量   | `True`, `False`, `None`                                                       |
|      库      | `from`, `import`                                                              |
|   数据相关   | `class`, `global`, `nonlocal`, `del`                                          |
|    运算符    | `and`, `or`, `not`, `is`, `in`                                                |
|   程序控制   | `if...elif...else`, `for...else`, `while...else`, `break`, `continue`, `pass` |
|     函数     | `def`, `return`, `lambda`                                                     |
|   异常处理   | `try...except...as...finally`, `raise`                                        |
|     迭代     | `yield`                                                                       |
|     协程     | `async`, `await`                                                              |
| 上下文管理器 | `with...as`                                                                   |
|     其他     | `assert`                                                                      |

## 2.3. 标识符
* 必须以非数字的 Unicode 字符或下划线开头, 由 Unicode 字符 (包含数字和下划线) 组成
    * 标识符可以是中文
* 不能是关键词
* 区分大小写

## 2.4. 语句结构
* 代码块
    * 使用**缩进**区分代码块, 而非 C/C++ 语言中的 `{}`
    * 缩进的空格数可以是任意的, 但是同一个代码块的语句**必须包含相同的缩进空格数**
* 一条语句在多行
    * 显式: 行尾使用反斜杠 `\`
    * 隐式: `[]`, `{}` 或 `()` 中的多行语句, 不需要使用反斜杠 `\`

    ```Python {.line-numbers}
    a = item_one + \
        item_two + \
        item_three
    b = ['item_one', 'item_two', 'item_three',
         'item_four', 'item_five']
    ```
* 一行中可以包含多条语句
    * 除最后一句外, 每条语句尾部必须使用分号 `;`
* 注释
    * 单行注释: 以 `#` 开头
    * 多行注释: 用三个单引号 `'''` 或者三个双引号 `"""` 将注释括起来

## 2.5. 数据类型

### 2.5.1. 概述
* 6个**基本数据类型**:
    * [number](#252-number)
        * [int](#2521-int)
        * [bool](#2522-bool)
        * [float](#2523-float)
        * [complex](#2524-complex)
    * [string](#253-String)
    * [list](#254-List)
    * [tuple](#255-Tuple)
    * [set](#256-Set)
    * [dictionary](#257-Dictionary)

    其中:
    * `int`, `float`, `complex`, `str`, `tuple` 是不可变类型 (immutable)
    * `list`, `set`, `dict` 是可变类型 (mutable)
* 其他内置数据类型: `bytes`, `bytearray`, `range`, ...
    > `range` 类的构造函数: `range(start=0, stop[, step=1])`
* 数据类型按属性还可分为:
    * **数字类型**: `int`, `float`, `complex`
    * **序列类型**: `list`, `tuple`, `str`, `bytes`, `bytearray`, ...
        * **容器序列**: `list`, `tuple`, ...
        * **扁平序列**: `str`, `bytes`, `bytearray`, ...
    * **集合类型**: `set`, `frozenset`, ...
    * **映射类型**: `dict`, `OrderedDict`, ...
    * **可迭代类型**: 序列、集合、映射、...
    * **生成器类型**: ...
    * ...
* 数据类型的抽象基类
    * `collections.abc`库中包含了各种数据类型的抽象基类
    * `numbers`库包含各种数字类型的抽象基类
* 查看数据类型
    * `type(object)`
    * `isinstance(obj, class_or_tuple, /)`

### 2.5.2. Number
* Number 基类的属性和方法
    * 基本属性: `real`, `imag`
    * 基本方法: `conjugate()`

#### 2.5.2.1. int
* Python 3 只有一种整数类型: **int**, 无论整数是多少位
* `0b`/`0B` 表示 2 进制数字, `0o`/`0O` 表示 8 进制数字, `0x`/`0X` 表示 16 进制数字
* 可使用内置函数 `bin/oct/hex(i)` 查看 2, 8, 16 进制的表示方式
* 数字可以使用 `_` 进行分割, 如 `1.2_34, 10_000`

> int 类的属性和方法
> * 构造函数 or 强制类型转换
>   * **int(x,base=10)**, 其中 x 必须是 string, bytes, bytearray
> * 主要方法
>   * **bit_length()**: int 的位数
>   * **bit_count()**: 二进制表示中11的个数
>   * **to_bytes(length, byteorder, *, signed=False)**: int 转 bytes, 也是类方法
>   * **from_bytes(bytes, byteorder, *, signed=False)**: bytes 转 int, 也是类方法

#### 2.5.2.2. bool
* 内建: `True`, `False`
* 0/0.0/0j, 空的 string/list/tuple/set/dictionary, `None` 等都被当作 `False`; 其他被当作 `True`
* 运算时 `True` eq 1, `False` eq 0, 如 True + 1.1 => 2.1, False + 1.1 => 1.1

> bool 类的属性和方法
> * 构造函数 or 强制类型转换
>   * **bool(x)**, 其中 x 必须是 string, bytes, bytearray
> * 主要方法: 继承自 int, 与 int 相同

#### 2.5.2.3. float
* 普通表示法 ddd`.`ddd, 如: 1.23
* 科学计数法 ddd`.`ddd`e|E[+|-]`ddd, 如: 4.5E-6
* 数字可以使用 `_` 进行分割, 如 `1.2_34_5`

> float 类的属性和方法
> * 构造函数 or 强制类型转换
>   * **float(x=0)**, 其中 x 必须是数字或字符
> * 主要方法:
>   * **is_integer()**: 是否为整数, 如 2.0 是整数, 2.1 不是整数
>   * **as_integer_ratio()**: 转换为分数 (分子, 分母)
>   * **hex()**: 转为 hex 字符串
>   * **.formhex(string)**: hex 字符串转为 float, 也是类方法

#### 2.5.2.4. complex
* 虚部用 `j|J` 表示, 而非 `i`, 如 1 + 2j, 1.1 + 2.2J

> complex 类的属性和方法
> * 构造函数 or 强制类型转换
>   * **complex(real=0, imag=0) -> real + imag*j**
> * 主要方法:
>   * **conjugate()**: 共轭

### 2.5.3. String
* **语法**
    * 单行: `[前缀] <单引号或双引号> <字符串> <单引号或双引号>`
        > 单行字符串放在多行表示:
        > ``` python
        > 字符串 = (
        >   [前缀]"第 1 段"
        >   [前缀]"第 2 段"
        >   [前缀]"..."
        > )
        > ```
    * 多行: `[前缀] <三个单引号或双引号> <多行字符串> <三个单引号或双引号>`
        ```python {.line-numbers}
        # 单行字符串
        >>> a = 'string1'; b = "string2"
        >>> a,b
        ('string1', 'string2')
        # 多行字符串
        >>> a = '''line 1
        ... line 2
        ... line 3'''
        >>> a
        'line 1\nline 2\nline 3'
        ```
* **用法**
    * 字符串不能改变
    * 引号可以是单引号 `'` 或双引号 `"`, 支持混用 (最外层引号用来表示 string, 内层都表示引号本身)
    * Python3中, string 中的字符都使用 Unicode(default: utf-8) 编码
    * Python 没有单独的字符类型, 一个字符就是长度为 1 的字符串
    * 同一行的多个字符串之间如果仅有空白, 则多个字符串会拼接
    * 可以用内建函数 `chr(i)` 将整数转为 unicode 字符, 用 `ord(c)` 将 unicode 字符转为整数
    * **前缀**:
        * `r|R` 表示 RAW 格式字符串, 如
            ```python {.line-numbers}
            >>> a = 'a\tb'; b = r"a\tb"
            >>> a,b
            ('a\tb', 'a\\tb')
            >>> print(a); print(b)
            a   b
            a\tb
            ```
        * `b|B` 表示 Bytes 类型
        * `r` 和 `b` 可以组合
        * `f|F` 表示格式化字符串, 建议用来代替 `%-string` 和 `str.format`
    * **转义符**: `\`
        | 转义字符  | 描述                                         |
        | :-------: | -------------------------------------------- |
        | `\`(行尾) | 续行符                                       |
        |   `\\`    | 反斜杠符号                                   |
        |   `\'`    | 单引号                                       |
        |   `\"`    | 双引号                                       |
        |   `\a`    | 响铃                                         |
        |   `\b`    | 退格(Backspace)                              |
        |   `\e`    | 转义                                         |
        |  `\000`   | 空                                           |
        |   `\n`    | 换行                                         |
        |   `\v`    | 纵向制表符                                   |
        |   `\t`    | 横向制表符                                   |
        |   `\r`    | 回车                                         |
        |   `\f`    | 换页                                         |
        |  `\oyy`   | 八进制数, yy代表的字符, 例如: \o12代表换行   |
        |  `\xyy`   | 十六进制数, yy代表的字符, 例如: \x0a代表换行 |
        | `\other`  | 其它的字符以普通格式输出                     |
    * **inedx(索引)**: `字符串 [索引]`, 从左往右以 0 开始, 从右往左以 -1 开始
        * 索引也可以是表达式, 如
            ```python
            ind = 1
            'hello'[ind+2]  # 'l'
            ```
    * **slice(切片)**: `字符串 [头下标 = 0 : 尾下标 = len(字符串) : 间隔 = 1]`
        * 截取时, 不包含尾下标指向的字符, 即实际范围是`[头下标, 尾下标)`, 如下图所示
            ``` markdown
            从后面索引:   -6  -5  -4  -3  -2  -1
            从前面索引:    0   1   2   3   4   5
                        +---+---+---+---+---+---+
                        | a | b | c | d | e | f |
                        +---+---+---+---+---+---+
            从前面截取:  :   1   2   3   4   5   :
            从后面截取:  :  -5  -4  -3  -2  -1   :
            ```
            * 如 string [1:3] 表示 string[1] ~ string[2];
            * 如 string [3:-1] 表示 string[3] ~ string [-2]
        * 默认间隔为 1, 可以改为其他值, 例如 2 表示间隔一个; -1 表示倒序
        * 示例:
            | 坐标范围 | 含义                            | 举例                      |
            | :------: | ------------------------------- | ------------------------- |
            |   [1]    | 从左到右, 第 1 个字符           | '123456'[1] => '2`        |
            |  [1:4]   | 从左到右, 第 1 ~ 3 个字符       | '123456'[1:4] => '234'    |
            |  [3:-1]  | 从左到右, 第 3 ~ 倒数第二个字符 | '123456'[3:-1] => '45'    |
            |   [2:]   | 从左到右, 第 2 ~ 结尾           | '123456'[2:] => '3456'    |
            |   [:5]   | 从左到右, 前 5 个               | '123456'[:5] => '12345'   |
            | [1:5:2]  | 从左到右, 第 1, 3 个            | '123456'[1:5:2] => '24'   |
            |  [::2]   | 从左到右, 第 0, 2, 4 个         | '123456'[::2] => '135'    |
            |  [::-1]  | 从右到左, 所有字符              | '123456'[::-1] => '54321' |
    * **运算**:
        * `string_1 + string_2`: 将 string_1 和 string_2 拼接到一起
        * `string * N`: 将 string 复制 N 份
    * **格式化**
        * **f-string** (推荐使用, 比 `str.format` 和 `%-string` 的可读性强, 速度更快)
            * 前缀`f|F`, 格式: `f"... {变量或表达式或函数[=][:格式描述符]} ..."`
            * `{}` 表示被替换字段, 可以是变量、表达式、lambda 函数、函数
            * 变量后加 `=` 会输出 `"变量=变量的值"` 字符串, 否则输出 `"变量的值"` 字符串
            * `{{xxx}}`会输出 `"{xxx}"`
            * 灵活交替使用`'`, `"`, `'''`, `"""`
            * 支持多行
            * 格式描述符: `[[填充字符]对齐][符号][#][0][宽度][分组][.精度][类型]`, 其中:

                | 分类  | 格式描述符 | 说明                                                         |
                | :---: | :--------: | ------------------------------------------------------------ |
                | 对齐  |     <      | 左对齐                                                       |
                |   ^   |     `>     | 右对齐                                                       |
                |   ^   |     `^     | 居中                                                         |
                |   ^   |     =      | 在符号和数字中间添加 0                                       |
                | 符号  |     +      | 正负数均加符号                                               |
                |   ^   |     -      | 负数前加负号 (-), 正数前不加符号 (默认)                      |
                |   ^   |   (空格)   | 负数前加负号 (-), 正数前加一个空格                           |
                | 进制  |     #      | 数字前加 `0b`, `0o`, `0x`                                    |
                | 宽度  |   <宽度>   | 指定宽度                                                     |
                |   ^   |  0<宽度>   | 指定宽度, 并添加前导零, 不可用于复数                         |
                | 分组  |     ,      | 使用逗号作为千位分隔符                                       |
                |   ^   |     _      | 十进制时: 千位分隔符, <br/>其他进制: 每 4 个数字加一个下划线 |
                | 精度  |   <精度>   | 仅用于浮点数, 对应的类型应为 `f/F` 或 `g/G`                  |
                | 类型  |     s      | 普通字符串                                                   |
                |   ^   |     c      | 字符格式, 按unicode编码将整数转换为对应字符                  |
                |   ^   |     b      | 二进制整数                                                   |
                |   ^   |     o      | 八进制整数                                                   |
                |   ^   |     d      | 十进制整数                                                   |
                |   ^   |    x/X     | 十六进制整数 (小写/大写)                                     |
                |   ^   |     f      | 定点数, 默认精度是6                                          |
                |   ^   |     F      | 与 f 等价, 但将 nan 和 inf 换成 NAN 和 INF                   |
                |   ^   |    e/E     | 科学计数                                                     |
                |   ^   |    g/G     | 通用格式, 小数用 `f/F`, 大数用 `e/E`                         |
                |   ^   |     %      | 百分比, 自动计算百分比, 并加 `%` 后缀                        |
            * 示例
                ```Python {.line-numbers}
                # 常规
                ystr= 'year'
                ynum= 2018
                f'{ystr.upper()}: {ynum}'   # 'YEAR: 2018'
                # 多行
                message = (f"Hi {name}. "
                        f"You are a {profession}. "
                        f"You were in {affiliation}.")
                # 字典
                f"The comedian is {comedian['name']}, aged {comedian['age']}."
                ```
        * **\<str对象\>.format** **(格式化字符串, 参数列表)** (次推荐)
            * 格式化字符串: `'xxx{[参数序号或key[:格式描述符]]}...'`
            * `{}` 及其中的字符表示对参数的格式化
            * 参数序号表示参数的位置, key 表示参数的名称, 序号和 key可 以混合使用
            * `'!a'` (使用 ascii()), `'!s'` (使用 str()) 和 `'!r'` (使用 repr()) 可以用于在格式化某个值之前对其进行转化
            * 可使用 `{参数序号或key[字典key][:格式字符串]}` 的方式对字典参数进行格式化
            * 也可以使用 `{字典key[:格式字符串]}` 的方式对不定长的字典形式的参数进行格式化
        * **%-string** (不推荐)
            * 格式: `格式字符串 % 参数`, 其中参数是 Tuple 类型

> str 类的属性和方法
> * 构造函数 or 强制类型转换
>   * **str(object='') -> str**
>   * **str(bytes_or_buffer[, encoding[, errors]]) -> str**
>   * **str() -> 空 str ("")**
> * 主要方法
>   分类   | 方法                                       | 说明
>   :----: | :----------------------------------------- | :---------------------
>   转换   | encode(encoding='utf-8', errors='strict')  | 转为字符串
>   格式化 | format(*args, **kwargs)                    | 格式化
>   ^      | format_map(mapping)                        | ^
>   大小写 | upper()                                    | 大写
>   ^      | capitalize()                               | 首字母大写
>   ^      | title()                                    | 标题格式文本
>   ^      | lower()                                    | 小写 (非ASCII无效)
>   ^      | casefold()                                 | 小写
>   ^      | swapcase()                                 | 交换大小写
>   对齐   | ljust / rjust(width[, fillchar])           | 左/右对齐
>   ^      | center(width[, fillchar])                  | 居中
>   填充   | zfill(width)                               | 左侧填充0
>   剪裁   | strip(bytes=None)                          | 两侧裁剪
>   ^      | lstrip / rstrip(bytes=None)                | 左/右侧裁剪
>   ^      | removeprefix / removesuffix(前缀或后缀)    | 删除前缀或后缀
>   查找   | count(sub[, start[, end]])                 | 统计个数
>   ^      | find / rfind(sub[, start[, end]])          | 从左/右侧开始查找
>   ^      | index / rindex(sub[, start[, end]])        | 从左/右侧开始索引, 和 find() 类似, 只是失败会报ValueError异常
>   替换   | replace(old, new, count=-1)                | 替换
>   ^      | translate(table,delete=b'')                | 查表替换
>   ^      | maketrans(x, y=None, z=None)               | 制作转换表
>   ^      | expandtabs(tabsize=8)                      | tab 转 空白
>   合并   | join(iterable_of_bytes)                    | 合并
>   拆分   | partition / rpartition(sep)                | 从左/右侧开始按 sep 分成3段
>   ^      | split / rsplit(sep=None, maxsplit=-1)      | 从左/右侧开始按 sep 分割成n段 (不包含sep)
>   ^      | splitlines(keepends=False)                 | 按行分割
>   信息   | isalnum()                                  | 是否为字母或数字, Unicode的字/数也为True
>   ^      | isalpha()                                  | 是否为字母, Unicode的字也为True
>   ^      | isascii()                                  | 是否为 ASCII 字符, Unicode的字为 False
>   ^      | isupper()                                  | 是否为大写
>   ^      | islower()                                  | 是否为小写
>   ^      | istitle()                                  | 是否为标题格式字符
>   ^      | isidentifier()                             | 是否为标识符
>   ^      | isdigit()                                  | 是否为数字^1^
>   ^      | isnumeric()                                | 是否为数字^2^
>   ^      | isdecimal()                                | 是否为分数^3^
>   ^      | isspace()                                  | 是否为空白
>   ^      | isprintable()                              | 是否为可打印字符
>   ^      | startswith(prefix[, start[, end]])         | 是否以xx开始
>   ^      | endswith(suffix[, start[, end]])           | 是否以xx结尾
>
>   ^1^ **digit** 包括 Unicode数字, byte数字 (单字节) , 全角数字 (双字节) , 罗马数字, 但不包括汉字数字
>   ^2^ **numeric** 包括 Unicode数字, 全角数字 (双字节) , 罗马数字, 汉字数字, 但不包括 byte数字 (单字节)
>   ^3^ **decimal** 包括 Unicode数字, 全角数字 (双字节) , 但不包括罗马数字, 汉字数字, byte数字 (单字节)

### 2.5.4. List
类似 C 语言的数组, 但效率较低
* **语法**
    ``` python
    [数据1, 数据2, 数据3, ... ]
    ```

    如:
    ```Python {.line-numbers}
    list = [ 'abcd', 786 , 2.23, 'runoob', 70.2 ]
    ```
* **用法**
    * 空 list 可用 `[]` 或 `list()` 表示
    * 支持嵌套, 数据可以是任何类型, 包括 **list**
    * 索引和切片规则与 **string** 相同
    * **运算**:  `+` (拼接) 和 `*`(复制)
    * **修改元素**: 索引并修改, `列表[索引] = 新值`
    * **删除元素**: 索引并删除, `del 列表[索引]`或`del 列表[左下标: 右下标]`
    * **删除整个列表**: `del 列表`
    * **复制**:
        * 如果直接复制, 多个变量会指向同一个列表, 修改任意一个, 其他都会跟着改变
        * 使用 `列表2 = 列表1.copy()` 或 `列表2 = 列表1[:]`会创建新的列表
    * **列表推导式**: `[表达式 for 变量 in 序列或迭代]` 或 `[表达式 for 变量 in 序列或迭代 if 条件]`
        * 可用于进行快速生成元组或对数据进行筛选
        * 示例
            ```Python {.line-numbers}
            [x**2 for x in range(5)]                                   # [0, 1, 4, 9, 16, 25]
            [x**2 for x in range(10) if x >= 5]                        # [25, 36, 49, 64, 81]
            [x*y for x in [1,2,3] for y in [1,2,3] ]                   # [1, 2, 3, 2, 4, 6, 3, 6, 9]
            [x*y for x in [1,2,3] if x > 1 for y in [1,2,3] if y > 2 ] # [6, 9]
            [(x, x**2) for x in range(3)]                              # [(0, 0), (1, 1), (2, 4)]
            [x.to_bytes(1,'big') for x in range(3)]                    # [b'\x00', b'\x01', b'\x02']
            [[row[i] for row in matrix] for i in range(4)]
            ```

> list 类的属性和方法
> * 构造函数 or 强制类型转换
>   * **list(iterable=())**
> * 主要方法
>   分类 | 方法                               | 说明
>   :--: | :--------------------------------- | :--
>   修改 | append(object)                     | 追加
>   ^    | extend(iterable)                   | 扩展
>   ^    | insert(index, object)              | 插入
>   ^    | pop(index=-1)                      | 删除
>   ^    | clear()                            | 清空全部
>   ^    | remove(value)                      | 删除第一个出现的 value
>   ^    | reverse()                          | 翻转
>   ^    | sort(key=None, reverse=False)      | 排序
>   查找 | count(value)                       | 统计个数
>   ^    | index(value, start=0, stop=2^63-1) | 查找
>   副本 | copy()                             | 创建副本

### 2.5.5. Tuple
与列表类似, 但其中元素不可改变
* **语法**
    ``` python
    (数据1, 数据2, 数据3, ... )
    ```

     如:
    ```Python {.line-numbers}
    tpl = ( 'abcd', 786 , 2.23, 'runoob', 70.2  )
    ```
* **用法**
    * 空 Tuple 可用 `()` 或 `tuple()` 表示
    * 单个元素的 Tuple 必须在唯一的元素加逗号 `,`, 否则会被当做 number, 如
        ```Python {.line-numbers}
        >>> a = (1.23); b = (3.21,) # a = 1.23, b = (3.21,)
        >>> type(a); type(b)
        <class 'float'>
        <class 'tuple'>
        ```
    * 支持嵌套, 元素可以任何类型, 包括 tuple
    * 索引和截取规则与 **string** 和 **list** 相同
    * **运算**:  `+` (拼接) 和 `*`(复制)
    * 列表中的元素**不**可变
        * 但仅针对一个维度, 其中的元素如果是可变的, 则该元素可以改变, 如
        ```Python {.line-numbers}
        >>> a = (1,[3,2])
        >>> a[1][0] = 1
        >>> a
        (1, [1, 2])
        >>> a[1].append(3)
        >>> a
        (1, [1, 2, 3])
        >>> del a[1][2]
        >>> a
        (1, [1, 2])
        >>> del a[1]
        Traceback (most recent call last):
        File "<stdin>", line 1, in <module>
        TypeError: 'tuple' object doesn't support item deletion
        ```
    * 不能用`del`删除元素, 只能删除整个 tuple
    * 元组拆包
        ```Python {.line-numbers}
        a, b = (1, 2)           # a = 1, b = 2
        a, b, *rest = range(5)  # a = 0, b = 1, rest = [2, 3, 4]
        ```
    * **元组推导式**: `tuple(表达式 for 变量 in 序列或迭代)` 或 `tuple(表达式 for 变量 in 序列或迭代 if 条件)`
        * 可用于进行快速生成集合或对数据进行筛选
        * 示例
            ```Python {.line-numbers}
            tuple(x for x in range(3))  # (0, 1, 2)
            ```
        * ==注意==: 如果直接使用`(表达式 for 变量 in 序列或迭代)` 或 `(表达式 for 变量 in 序列或迭代 if 条件)`, 将返回生成器推导式
    * 通过名称对 Tuple 进行索引
        * 对序号进行预定义, 如
            ```Python {.line-numbers}
            NAME, SCORE = 0, 1
            t1 = ("Xiaoming", 99)
            t1[NAME]    # "Xiaoming"
            t1[SCORE]   # 99
            ```
        * 使用内建库 `collections.namedtuple()`
            ```python {.line-numbers}
            Point = collections.namedtuple('Point', ['x', 'y'])
            p = Point(11, y=22)
            p.x, p.y    # 11, 22
            ```

> tuple 类的属性和方法
> * 构造函数 or 强制类型转换
>   * **tuple(iterable=())**
> * 主要方法
>   分类 | 方法                               | 说明
>   :--: | :--------------------------------- | :---
>   查找 | count(value)                       | 统计个数
>   ^    | index(value, start=0, stop=2^63-1) | 查找

### 2.5.6. Set
类似数学中的集合, 基本功能是进行成员关系测试和删除重复元素, 顺序是随机的
* **语法**
    ``` python
    {数据1, 数据2, 数据3, ... }
    ```

    如
    ```python {.line-numbers}
    >>> student = {'Rose', 'Mary', 'Jim', 'Tom', 'Jack', 'Mary'}
    # student 是 {'Jack', 'Jim', 'Mary', 'Rose', 'Tom'}, 元素 'Mary' 仅出现一次
    ```
* **用法**
    * 创建一个空集合必须用 `set()` 而不是 `{ }`, 因为 `{ }` 是创建一个空字典
    * **运算**:
        |   分类   | 运算                | 说明              |
        | :------: | ------------------- | ----------------- |
        | 集合运算 | a & b               | 交集 ∩            |
        |    ^     | a \| b              | 并集 ∪            |
        |    ^     | a ^ b               | (a ∪ b) - (a ∩ b) |
        |    ^     | a - b               | a - (a ∩ b)       |
        |   判断   | **in** / **not in** | 是否 $\in$        |
        |    ^     | a <= b              | 是否 $\sube$      |
        |    ^     | a < b               | 是否 $\sub$       |
        |    ^     | a > b               | 是否 $\supset$    |
        |    ^     | a >= b              | 是否 $\supe$      |
    * `set("abc")` 和 `set({"abc"})`是不同的, 前者是 {"a", "b", "c"}, 后者是 {"abc"}
    * **集合推导式**: `{表达式 for 变量 in 序列或迭代}` 或 `{表达式 for 变量 in 序列或迭代 if 条件}`
        * 可用于进行快速生成集合或对数据进行筛选
        * 示例
            ```Python {.line-numbers}
            {x for x in range(1,6) if x % 3 == 1} # {1, 4}
            ```
> set 类的属性和方法
> * 构造函数 or 强制类型转换
>   * **set(iterable) -> new set object**
> * 主要方法
>   分类 | 方法                               | 说明
>   :--: | :--------------------------------- | :-------------------------------
>   修改 | add(object_x)                      | 添加一个元素
>   ^    | pop()                              | 随机删除一个元素, 并返回此值, 如果空产生 KeyError 异常
>   ^    | discard(object_x)                  | 删除一个元素
>   ^    | remove(object_x)                   | 和.discard()类似, 只是失败产生 KeyError 异常
>   ^    | clear()                            | 清空全部
>   运算 | difference(set_b)                  | a - b
>   ^    | difference_update(set_b)           | a -= b
>   ^    | intersection(set_b)                | (a & b)
>   ^    | intersection_update(set_b)         | a &= b
>   ^    | union(set_b)                       | a \| b
>   ^    | update(set_b)                      | a \|= b
>   ^    | symmetric_difference(set_b)        | a ^ b
>   ^    | symmetric_difference_update(set_b) | a ^= b
>   判断 | isdisjoint(set_b)                  | 是否无交集
>   ^    | issubset(set_b)                    | 是否包含于, a < b, a <= b
>   ^    | issuperset(set_b)                  | 是否包含, a > b, a >= b
>   副本 | copy(set_b)                        | 副本
>
> frozenset: 特殊的`set`, 不能更改元素, 因此不具有`add`, `pop`, `diacard`, `remove`, `clear`, `xxx_update`等方法

### 2.5.7. Dictionary
一个无序的 `键(key) : 值(value)` 集合
* **语法**
    * 创建方法 1: `{ 键1:值1, 键2:值2, 键3:值3, ... }`, 如
        ```python {.line-numbers}
        >>> {'Alice': '2341', 'Beth': '9102', 'Cecil': '3258'}
        ```
    * 创建方法 2: 动态创建, 如
        ```python {.line-numbers}
        >>> dict = {}
        >>> dict['one'] = 1
        >>> dict[2] = "2"
        >>> dict
        {'one': 1, 2: '2'}
        ```
    * 创建方法 3: `dict([(键1, 值1), (键2, 值2), ...])`, 如
        ```python {.line-numbers}
        >>> dict([('name', 'Tom'), ('age', 33)])
        {'name': 'Tom', 'age': 33}
        ```
    * 创建方法 4: `dict(键1 = 值1, 键2 = 值2, ...)`, 如
        ```python {.line-numbers}
        >>> dict(name = 'Tom', age = 33)
        {'name': 'Tom', 'age': 33}
        ```
    * 访问某项: `字典[键]`
* **用法**
    * 键 (key) 必须使用不可变类型, 如: 数字, string, tuple
    * 在同一个字典中, key 必须是唯一的
    * 支持嵌套
    * **添加**: 直接增加新的 `键:值`, `字典[新键] = 新值`
    * **更改**: 按 key 索引并修改, `字典[键] = 新值`
    * **删除一个元素**: 按 key 索引并删除, `del 字典[键]`
    * **删除整个dict**: `del 字典`
    * **字典更新和合并**: `|` 和 `|=`
        * 类似于集合的操作
    * **字典推导式**: `{键:值-表达式 for 键,/值 in 序列或迭代)` 或 `{键:值-表达式 for 键,/值 in 序列或迭代 if 条件}`
        * 可用于进行快速生成元组或对数据进行筛选
        * 示例
            ```Python {.line-numbers}
            word = 'letters'
            letter_counts = {letter: word.count(letter) for letter in set(word)}
            # letter_counts = {'t': 2, 'l': 1, 'e': 2, 'r': 1, 's': 1}
            ```

> set 类的属性和方法
> * 构造函数 or 强制类型转换
>   * **dict(iterable)** 或 **dict(\*\*kwargs)**
> * 主要方法
>    分类 | 方法                            | 说明
>    :--: | :------------------------------ | :------------------
>    修改 | fromkeys(iterable, value=None)  | 创建, 也是类方法
>    ^    | update([E, ]**F)                | 更新
>    ^    | setdefault(key, default=None)   | 插入元素
>    ^    | pop(k[,d])                      | 根据key删除 key:value, 返回被value
>    ^    | popitem()                       | 删除末尾 key:value
>    ^    | clear()                         | 删除所有
>    属性 | get(key, default=None)          | 根据 key 返回 value
>    ^    | items()                         | 列出所有 key:value
>    ^    | keys()                          | 列出所有 key
>    ^    | values()                        | 列举所有 value
>    副本 | copy()                          | 副本

## 2.6. 变量
* **声明与赋值**:
    * 直接声明并赋值, 无需规定数据类型, 如
        ```Python {.line-numbers}
        a = 1
        b = "string"
        c = [1,2,3,4]
        d = <类名称>[(初始值)]
        ```
    * tuple 方式声明, 如
        ```Python {.line-numbers}
        a, b, c = 1, 'two', 3.0
        a, b, *rest = 1, 2, 3, 4 # rest = [3,4]
        a, *b, c = 1,2,3,4       # b = [2,3]
        ```
    * 链式声明, 如
        ```Python {.line-numbers}
        a = b = 1
        ```
* **删除**: `del 变量1[,变量2[,变量3[....,变量N]]]`
* **数据类型**: `变量:数据类型 [= 值]` 或 `变量:数据类型1|数据类型2 [= 值]`
    * 注释变量类型, 明确指出变量类型, python 本身不强制检查, 可使用第三方工具进行检查
* **海象赋值表达式**: `变量 := 值`
    * 在某些时候让代码更整洁, 如
        ```python
        if (n := len(a)) > 10:
            print(f"{n=}")
        # 原来的写法
        n = len(a)
        if n > 10:
            print(f"{n=}")
        ```

## 2.7. 运算符

### 2.7.1. 基本运算符
* 算术运算符 (均支持 `运算=`)
    | 运算符 |       含义       | 实例                    |
    | :----: | :--------------: | :---------------------- |
    |  `+`   |        加        | 1 + 3 => 4              |
    |  `-`   |        减        | 5.3 - 2.1 => 3.1        |
    |  `*`   |        乘        | (2+3j) * (3-2j) => 2+7j |
    |  `/`   |        除        | 7 / 2 => 3.5            |
    |  `@`   |      矩阵乘      | ...                     |
    |  `**`  |       乘方       | 2 ** 4 => 16            |
    |  `//`  | 整数除, 得到整数 | 5 // 2 => 2             |
    |  `%`   |       取余       | 5 % 2 => 1              |
* 赋值运算符
    |    表达方式     | 含义                       | 实例            |
    | :-------------: | -------------------------- | --------------- |
    |       `=`       | "引用"一个值               | a = 3           |
    |       连=       | 多个变量"引用"同一个值     | a = b = c = 1   |
    |      组合=      | 多个元素分别"引用"对应的值 | a, b = 3, 'txt' |
    | `+=`, `-=`, ... | 先运算, 后赋值             | a += 1          |
* 比较运算符
    |  运算符  |    描述    | 实例              |
    | :------: | :--------: | :---------------- |
    |   `==`   |   相等 ?   | (1 == 2) => False |
    |   `!=`   |   不等 ?   | (1 != 2) => True  |
    | &shy;`>` |   大于 ?   | (1 > 2) => False  |
    |   `<`    |   小于 ?   | (1 < 2) => True   |
    |   `>=`   | 大于等于 ? | (1 >= 2) => False |
    |   `<=`   | 小于等于 ? | (1 <= 1) => True  |

    * Python 支持连续比较, 如
        ```Python {.line-numbers}
        if 1 < a <= 3: pass
        # 等效于
        if a > 1 and a <= 3: pass
        ```
* 位运算符 (均支持 `运算=`)
    |       运算符        |   描述   | 实例                           |
    | :-----------------: | :------: | ------------------------------ |
    |         `&`         |  按位与  | 0b1100 & 0b0101 => 0b0100      |
    | <code>&#124;</code> |  按位或  | 0b1100 &#124; 0b0101 => 0b1101 |
    |         `~`         | 按位取反 | ~0b1100 => 0b0011              |
    |      &shy;`^`       | 按位异或 | 0b1100 ^ 0b0101 => 0b1001      |
    |        `<<`         |   左移   | 0xff << 2 => 0x3fc             |
    |        `>>`         |   右移   | 0xff >> 2 => 0x3f              |
* 逻辑运算符
    | 运算符 |  描述  | 实例                    |
    | :----: | :----: | :---------------------- |
    | `and`  | 逻辑与 | True and False => False |
    |  `or`  | 逻辑或 | True or False => True   |
    | `not`  | 逻辑非 | not True = False        |

### 2.7.2. 特殊运算符
* 成员运算符
    |  运算符  | 描述               | 实例                      |
    | :------: | ------------------ | ------------------------- |
    |   `in`   | 元素是否在序列中   | 'a' in 'abc' => True      |
    | `not in` | 元素是否不在序列中 | 'a' not in 'abc' => False |
* 身份运算符
    |  运算符  | 描述                             | 实例                               |
    | :------: | -------------------------------- | ---------------------------------- |
    |   `is`   | 判断两个标识符是否引用自一个对象 | x is y, 等效于 id(x) == id(y)      |
    | `is not` | 判断两个标识符是否引用自不同对象 | x is not y , 等效于 id(a) != id(b) |

    **注意**: is 用于判断两个变量引用对象是否为同一个,  == 用于判断引用变量的值是否相等
* 三元操作
    * Python 没有三元运算符, 可用 `if...else` 实现三元操作
        `val = 真值 if 条件成立 else 假值`

        如:
        ```Python {.line-numbers}
        a = 1 if True else 0    # a = 1
        a = 1 if False else 0   # a = 0
        ```

### 2.7.3. 运算符优先级
|                  运算符                  | 描述                     |
| :--------------------------------------: | ------------------------ |
|                   `**`                   | 乘方 (最高优先级)        |
|               `~` `+` `-`                | 按位取反, 取正数, 取负数 |
|             `*` `/` `%` `//`             | 乘, 除, 取余, 整数除     |
|                 `+` `-`                  | 加, 减                   |
|                `>>` `<<`                 | 右移, 左移               |
|                   `&`                    | 按位与                   |
|         `^` <code>&#124;</code>          | 按位异或, 按位或         |
|            `<=` `<` `>` `>=`             | 比较运算符               |
|                `==` `!=`                 | 相等 ?, 不等 ?           |
| `=` `%=` `/=` `//=` `-=` `+=` `*=` `**=` | 赋值运算符               |
|              `is` `is not`               | 身份运算符               |
|              `in` `not in`               | 成员运算符               |
|             `and` `or` `not`             | 逻辑运算符               |

## 2.8. 程序控制

### 2.8.1. 条件控制
* `if ... elif ... else`
    ```python {.line-numbers}
    if 条件1:
        ...
    elif 条件2:
        ...
    else:
        ...
    ```
    * 支持嵌套
* Python 在 3.10 引入 `match – case` 语句
    ```python {.line-numbers}
    match 变量:
        case 值_1:
            ...
        case 值_2 | 值_3 | 值_4: # 多个值
            ...
        case 值_5 if ...: # 添加 if 语句
            ...
        case 值_6 as 值_6_别名: # 允许别名
            ...
        case _: # 类似 C 语言中的 default
            ...
    ```
    * `case` 可以添加 `if` 语句
    * `case` 可以添加 `as` 别名
    * `case` 的值可以是
        * 一个或多个简单的字面量
        * 不展开的数据类型 (如 tuple)
            ```Python
            match point:
                case (0, 0):
                    print("Origin")
                case (0, y):
                    print(f"Y={y}")
                case (x, 0):
                    print(f"X={x}")
                case (x, y):
                    print(f"X={x}, Y={y}")
                case _:
                    raise ValueError("Not a point")
            ```
        * 对象
            ```Python
            from dataclasses import dataclass

            @dataclass
            class Point:
                x: int
                y: int

            def whereis(point):
                match point:
                    case Point(0, 0):
                        print("Origin")
                    case Point(0, y):
                        print(f"Y={y}")
                    case Point(x, 0):
                        print(f"X={x}")
                    case Point():
                        print("Somewhere else")
                    case _:
                        print("Not a point")
            ```
        * 列表
            ```Python
            match points:
                case []:
                    print("No points")
                case [Point(0, 0)]:
                    print("The origin")
                case [Point(x, y)]:
                    print(f"Single point {x}, {y}")
                case [Point(0, y1), Point(0, y2)]:
                    print(f"Two on the Y axis at {y1}, {y2}")
                case _:
                    print("Something else")
            ```

### 2.8.2. 循环控制
* **while**
    ```python {.line-numbers}
    # 语法1:
    while 判断条件:
        ...
    else: # 【可选】判断条件不满足时运行, 如果从 break 中断则不运行
        ...
    # 语法2 (简单, 单行) :
    while 判断条件: ...
    ```
* **for**
    ```python {.line-numbers}
    # 语法1:
    for 变量 in 序列:
        ...
    else:
        ...
    # 语法2 (简单, 单行) :
    for 变量 in 序列: ...
    ```

* 注意
    * 对于 `for` 循环, 常用 `range(start=0, stop, step = 1)` 生成序列
    * 循环控制:
        * 关键词 `pass`: 什么都不做
        * 关键词 `break`: 跳出循环
        * 关键词 `continue`: 立即进入下次循环
    * 当条件不满足时, `else` 运行, 运行后代码块结束
        * 但是如果从 `break` 中断, `else` 不运行

## 2.9. 函数与作用域

### 2.9.1. 函数声明与调用
* 函数声明:
    ```Python {.line-numbers}
    def 函数名(参数列表):
        函数说明
        函数体
        [return 返回值]
    ```
* 函数调用:
    ```Python {.line-numbers}
    [返回值 = ]函数名(参数列表)
    ```
    * 支持递归调用

其中
* **函数说明**: 单行或多行字符串, 可以用 `函数名.__doc__` 访问
* **参数列表**:
    * **必需参数**: 调用时, 类型、数量、顺序必须和声明时的一样, 如
        * 声明: `def func(p1,p2): ...`
        * 调用: `func("abc", 100)`
    * **关键字参数**: 函数调用使用关键字参数来确定传入的参数值, 允许顺序不一致, 但数量需一致, 如
        * 声明: `def func(p1,p2): ...`
        * 调用: `func(p2=100, p1="abc")`
    * **默认参数**: 声明时, 默认参数必须在最后; 调用时, 如果没有传递参数, 则会使用默认参数, 如
        * 声明: `def func(p1,p2=100): ...`
        * 调用: `func("abc")`
    * **不定长参数**: 能处理比声明时更多的参数, 这些参数叫做不定长参数, 声明时不会命名, 会收集多个参数, 直到关键词参数为止。基本语法:
        ```Python {.line-numbers}
        # Tuple 形式
        def 函数名([正式参数,] *[可变参数_tuple]):
            函数说明
            函数体
        # dictionary 形式
        def 函数名([正式参数,] **可变参数_dict):
            函数说明
            函数体
        ```
        * tuple类型不定长参数: 将会以tuple形式传入, 如
            * 声明: `def func(p1, *p2): ...`
            * 调用: `func(12, 'abc', (1,2), [3,4,5])`
            * 函数内部: p1=12, p2=('abc', (1, 2), [3, 4, 5])
        * tuple类型不定长参数也可以不写参数名, 但其后的参数必须以关键词参数方式调用, 如
            * 声明: `def func(p1, *, p2): ...`
            * 调用: `func(12, p2=set("abcd"))`
            * 函数内部: p1=12, p2={'a', 'c', 'd', 'b'}
        * dict类型不定长参数: 将会以dict形式传入, 调用时必须以关键词形式输入如
            * 声明: `def func(p1, **p2): ...`
            * 调用: `func(12, dp1='abc', dp2={'one': 1, 'two': 2})`
            * 函数内部: p1=12, p2={'dp1': 'abc', 'dp2': {'one': 1, 'two': 2}}
    * **仅限位置形参**: 参数列表中`/`之前的形参必须是位置限定的, 不能用关键词传参
        ```python
        # a 和 b 为仅限位置形参
        # c 或 d 可以是位置形参或关键字形参
        # e 或 f 要求为关键字形参
        def f(a, b, /, c, d, *, e, f):
            print(a, b, c, d, e, f)
        ```
**参数传递**:
* 不可变类型(immutable): 类似 C/C++ 的值传递, 传递的只是参数对象的值, 没有影响参数本身
* 可变类型(mutable): 类似 C/C++ 的引用传递, 传递的是参数对象本身, 修改后函数外部的参数对象也受影响
* 分配参数: 可以用tuple和dictionary传递定长参数, 如
    ```Python {.line-numbers}
    >>> def myFunc(a, b):
    ...    print('a = ', a, ', b = ', b)
    >>> params1 = 1, 2.3
    >>> params2 = {'b':'6-7', 'a':4+5j}
    >>> myFunc(*params1)
    a = 1 , b = 2.3
    >>> myFunc(**params2)
    a = (4+5j) , b = 6-7
    ```

### 2.9.2. 函数属性
函数也是对象, 也具有属性, 主要的属性包括:

|       属性       | 说明               | 读写权限 |
| :--------------: | ------------------ | -------- |
|    \_\_doc__     | 类或函数文档       | 读写     |
|    \_\_name__    | 函数名称           | 读写     |
|    \_\_code__    | 代码对象           | 读写     |
|   \_\_module__   | 所在的module       | 读写     |
|  \_\_closure__   | 闭包               | 只读     |
|  \_\_globals__   | module中的全局变量 | 只读     |
|    \_\_dict__    | 类或函数的属性     | 读写     |
|  \_\_defaults__  | 函数默认参数的值   | 读写     |
| \_\_kwdefaults__ | 字典参数的默认值   | 读写     |

### 2.9.3. 闭包
位于函数内部的函数, 好处是不必暴露变量到更高的作用域, 如:
```Python {.line-numbers}
def f(...):
    ...
    def g(...): # 闭包
        ...
    ...
```

### 2.9.4. 匿名函数 lambda
* 语法: `函数名 = lambda [参数1 [,参数2,.....参数n]]: 一句代码`
* 调用: `函数名(参数)`
* 注意:
    * `lambda` 的主体是一个表达式, 而不是一个代码块, 仅仅能在 `lambda` 表达式中封装有限的逻辑
    * `lambda` 函数拥有自己的命名空间, 且不能访问自己参数列表之外或全局命名空间里的参数
    * 虽然 `lambda` 函数看起来只能写一行, 却不等同于 C/C++ 的内联函数, 后者的目的是调用小函数时不占用栈内存从而增加运行效率

### 2.9.5. 内建函数
> 注: 其中加粗的为类构造函数

|   分类   |                  内建函数                   | 说明                                                                                                                                                      |
| :------: | :-----------------------------------------: | --------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 数据类型 |              **type**(object)               | 获取数据类型                                                                                                                                              |
|    ^     |           type(name, bases, dict)           | 创建新类型                                                                                                                                                |
| 类型转换 |    **int / bool / float / complex**(..)     | 转为目标类型                                                                                                                                              |
|    ^     |                 **str**(..)                 | ^                                                                                                                                                         |
|    ^     |                **tuple**(..)                | ^                                                                                                                                                         |
|    ^     |                **list**(..)                 | ^                                                                                                                                                         |
|    ^     |           **set / frozenset**(..)           | ^                                                                                                                                                         |
|    ^     |                **dict**(..)                 | ^                                                                                                                                                         |
|    ^     |   **bytes / bytearray / memoryview**(..)    | ^                                                                                                                                                         |
| 数据信息 |               **id**(object)                | 获取标识                                                                                                                                                  |
|    ^     |                 **len**(s)                  | 获取序列的长度                                                                                                                                            |
|   数学   |                 **abs**(x)                  | 求绝对值                                                                                                                                                  |
|    ^     |        **round**(number[, ndigits])         | 求近似值, 四舍六入五成双                                                                                                                                  |
|    ^     |             **pow**(x, y[, z])              | 乘方                                                                                                                                                      |
|    ^     |              **divmod**(a, b)               | =(a // b, a % b)                                                                                                                                          |
|    ^     |             **max / min**(...)              | 求最大值 / 最小值                                                                                                                                         |
|    ^     |         **sum**(iterable[, start])          | 求和                                                                                                                                                      |
|    ^     |        **sorted**(iterable, *, ...)         | 排序                                                                                                                                                      |
|    ^     |                hash(object)                 | 求哈希值                                                                                                                                                  |
|   逻辑   |              **all**(iterable)              | 所有为真, 返回真                                                                                                                                          |
|    ^     |              **any**(iterable)              | 任一为真, 返回真                                                                                                                                          |
| 字符处理 |                 format(...)                 | 格式化, 建议使用 f-string                                                                                                                                 |
|    ^     |                repr(object)                 | 将对象转化为供解释器读取的形式                                                                                                                            |
|    ^     |                ascii(object)                | 返回一个只用 ASCII 表达的 string                                                                                                                          |
|    ^     |                 **chr**(i)                  | 整数转 unicode                                                                                                                                            |
|    ^     |                 **ord**(c)                  | unicode 转整数                                                                                                                                            |
|    ^     |           **bin / oct / hex**(x)            | 转为 2/8/16 进制字符串                                                                                                                                    |
|   迭代   |        **iter**(object[, sentinel])         | 获取迭代对象                                                                                                                                              |
|    ^     |        **next**(iterator[, default])        | 访问迭代器下一个元素                                                                                                                                      |
|    ^     |          **aiter**(async_iterable)          | 获取异步迭代对象                                                                                                                                          |
|    ^     |    **anext**(async_iterator[, default])     | 访问异步迭代器下一个元素                                                                                                                                  |
|    ^     |     **range**(start=0, stop[, step=1])      | 整数序列                                                                                                                                                  |
|    ^     |      **enumerate**(iterable, start=0)       | 迭代器, 元素为 (start + i, iterable[i])  (其中i从0开始累加)                                                                                               |
|    ^     |        **zip**(iter1 [,iter2 [...]])        | 迭代器, 元素为 (iter1[i], iter2[i], ...)                                                                                                                  |
|    ^     |         **map**(func, \*iterables)          | 迭代器, 对每个元素执行 func(*iterables)                                                                                                                   |
|    ^     |       **filter**(function, iterable)        | 迭代器, 仅返回 function(iterable) 或 iterable 为真的对象, 等效于 `(item for item in iterable if function(item))` 或 `(item for item in iterable if item)` |
|    ^     |           **reversed**(sequence)            | 迭代器, 反转序列                                                                                                                                          |
|   索引   |     **slice**(start=0, stop[, step=1])      | 用于增强索引                                                                                                                                              |
|  OOP 类  |                 **object**                  | 基类                                                                                                                                                      |
|    ^     |              **@classmethod**               | 将函数转为类方法                                                                                                                                          |
|    ^     |              **@staticmethod**              | 将函数转为静态方法                                                                                                                                        |
|    ^     |              **property**(...)              | 类属性, 实现`对象.属性`的各种操作                                                                                                                         |
|    ^     |      getattr(object, name[, default])       | 等效于`对象.属性`                                                                                                                                         |
|    ^     |        setattr(object, name, value)         | 等效于`对象.属性 = 值`                                                                                                                                    |
|    ^     |            delattr(object, name)            | 等效于`del 对象.属性`                                                                                                                                     |
|    ^     |            hasattr(object, name)            | 对象是否有指定的属性                                                                                                                                      |
|    ^     |               **super**(...)                | 返回基类                                                                                                                                                  |
|    ^     |      **isinstance**(object, classinfo)      | 是否为class的例化                                                                                                                                         |
|    ^     |        issubclass(class, classinfo)         | 是否为子类                                                                                                                                                |
| 输入输出 | **print**(*objects, sep=' ', end='\n', ...) | 标准输出, sep: 间隔字符, end: 结尾字符                                                                                                                    |
|    ^     |             **input**([prompt])             | 标准输入                                                                                                                                                  |
|    ^     |             **open**(file, ...)             | 打开文件, 详见[文件操作](Python%20笔记: 文件操作.md)                                                                                                      |
| Runtime  |             help(*args, **kwds)             | 帮助                                                                                                                                                      |
|    ^     |              **dir**([object])              | 列出目录                                                                                                                                                  |
|    ^     |               vars([object])                | 列出变量                                                                                                                                                  |
|    ^     |                  globals()                  | 列出所有全局变量                                                                                                                                          |
|    ^     |                  locals()                   | 列举局部变量                                                                                                                                              |
|    ^     |              callable(object)               | 是否可调用                                                                                                                                                |
|    ^     |                compile(...)                 | 编译                                                                                                                                                      |
|    ^     |          **eval**(expression, ...)          | 按python语法运行表达式 (字符串)                                                                                                                           |
|    ^     |      exec(object[, globals[, locals]])      | 动态运行python代码                                                                                                                                        |
|    ^     |        **breakpoint**(*args, **kws)         | 设置断点                                                                                                                                                  |

### 2.9.6. 偏函数
* 使用 `functools.partial(函数, *args, **keywords)`
    * 将原函数当做第一个参数传入, 原函数的各个参数依次作为partial()函数后续的参数, 除非使用关键字参数
    * 示例
        ```Python {.line-numbers}
        from functools import partial
        basetwo = partial(int, base=2)
        basetwo('10010')    # 等效于 int('10010', base=2)
        ```
### 2.9.7. 作用域
* Python 的作用域一共有 4 种
    * L (Local): 局部作用域
    * E (Enclosing): 闭包函数外的函数中
    * G (Global): 全局作用域
    * B (Built-in): 内建作用域
    ```Python {.line-numbers}
    x = int(2.9)        # int 属于内建作用域
    g_count = 0         # 全局作用域
    def outer():
        o_count = 1     # 闭包函数外的函数中
        def inner():
            i_count = 2 # 局部作用域
    ```
* 以 `L –> E –> G –> B` 的规则查找, 即: 在局部找不到, 才会去局部外的局部找 (例如闭包), 再找不到就会去全局找, 再者去内建中找
* 只有 module, class 以及函数 (def, lambda) 才会引入新的作用域, 其它的代码块 (如 if/elif/else/、try/except、for/while等) 不会引入新的作用域, 也即这些语句内定义的变量, 外部也可以访问
* 全局变量
    * 定义在函数外的变量
    * 可在整个程序范围内访问
    * 在函数内可用关键词 `global` 将变量改为全局变量
* 局部变量:
    * 定义在函数内部的变量
    * 只能在其被声明的函数内部访问
    * 在函数内可用关键词 `nolocal` 将变量改为外层的作用域
* `global` 和 `nolocal` 的实例
    ```Python {.line-numbers}
    g_cnt = 0

    def func_l1():
        global g_cnt
        g_cnt += 1
        l1_cnt = 1
        print("\tfunc_l1::g_cnt = %d, L1_cnt = %d" % (g_cnt, l1_cnt))
        def func_l2():
            nonlocal l1_cnt
            # g_cnt += 1    # 无法修改 g_cnt
            l1_cnt += 1
            print("\tfunc_l2::g_cnt = %d, L1_cnt = %d" %
                (g_cnt, l1_cnt))  # 可以访问 g_cnt
        func_l2()

    for i in range(3):
        print('第%d次调用' % (i+1))
        func_l1()
    ```

## 2.10. 模块和包
**包**: 多个模块
**模块**: 单个文件
* **语法**
    ```Python {.line-numbers}
    import <包|模块> [as 别名]                       # 导入整个包/模块, 使用模块的命名空间
    from <包|模块> import <模块|变量|函数> [as 别名] # 导入某个模块/变量/函数到当前命名空间
    from <包|模块> import <模块...|变量...|函数...>  # 导入多个模块/变量/函数到当前命名空间
    from <包|模块> import *                          # 导入全部模块/变量/函数到当前命名空间
    ```
* 注意:
    * 一个模块只会被导入一次, 不管执行了多少次 `import`
    * 尽量避免导入包的全部内容
    * 模块属性
        |    属性    | 含义                                                                   |
        | :--------: | ---------------------------------------------------------------------- |
        | \_\_doc__  | 说明                                                                   |
        | \_\_file__ | 完整路径                                                               |
        | \_\_name__ | 模块的名称, 当其值是 `__main__` 时, 表明该模块自身在运行, 否则是被引入 |
    * 包:
        * 文件结构
        ```Python {.line-numbers}
        /包
            __init__.py
            / dir1
                __init__.py
                module11.py
                module12.py
            / dir2
                __init__.py
                module21.py
                module22.py
        ```
        * 目录中只有包含 \_\_init__.py 才会被认作是一个包
        * 如果包定义文件 \_\_init__.py 存在一个叫做 \_\_all__ 的列表变量, 那么在使用 `from package import *` 的时候就把这个列表中的所有名字作为包内容导入

## 2.11. 面向对象

### 2.11.1. 类声明
```Python {.line-numbers}
class 类名([基类1, 基类2, ...]):
    """ 说明文档 """
    公有属性 = 值   # 类属性
    _保护属性 = 值  # 类属性
    __私有属性 = 值 # 类属性
    ...
    def __init__(self, 参数1, 参数2, ...):  # 构造函数, python特殊方法
        super.__init__(...)
        局部变量 = 值
        self.公有属性 = 值      # 实例属性
        self._保护属性 = 值     # 实例属性
        self.__私有属性 = 值    # 实例属性
        ...
    def 公有方法(self, 参数1, 参数2, ...):
        ...
    def _保护方法(self, 参数1, 参数2, ...):
        ...
    def __私有方法(self, 参数1, 参数2, ...):
        ...
    def __特殊方法__(self, 参数1, 参数2, ...):
        ...
    @classmethod    # 使用装饰器
    def 类方法(cls, 参数1, 参数2, ...): # 使用 cls, 而非 self
        ...
    @staticmethod   # 使用装饰器
    def 静态方法(参数1, 参数2, ...):    # 既不用 cls, 也不用 self
        ...
    def __del__(self, 参数1, 参数2, ...):  # 析构函数, python特殊方法
        ...
    ...
```

### 2.11.2. 属性
* 通用属性
    |       属性        | 说明               | 读写权限 |
    | :---------------: | ------------------ | -------- |
    |     \_\_doc__     | 类或函数文档       | 读写     |
    |    \_\_name__     | 函数名称           | 读写     |
    |  \_\_qualname__   | 函数认证的名称     | 读写     |
    |   \_\_module__    | 所在的module       | 读写     |
    |  \_\_defaults__   | 函数默认参数的值   | 读写     |
    |    \_\_code__     | 代码对象           | 读写     |
    |   \_\_globals__   | module中的全局变量 | 只读     |
    |    \_\_dict__     | 类或函数的属性     | 读写     |
    |   \_\_closure__   | 闭包               | 只读     |
    | \_\_annotations__ | ???                | 读写     |
    | \_\_kwdefaults__  | 字典参数的默认值   | 读写     |

* 类属性与实例属性
    * 通过`类名.类属性名`访问
    * 注意: 如果使用`对象.类属性名`访问, 对象会创建一个与`类属性名`同名的`实例属性`
    * 如果类属性和实例属性同名, 对象会使用`实例属性`
    * 访问对象的私有属性: `对象._类名__私有属性`

### 2.11.3. 方法
* 按访问权限区分
    * 公有方法: 本身、子类、对象都可以访问, 派生类可以继承
    * 保护方法: `_` 开头, 只能允许其本身与子类进行访问
    * 私有方法: `__`开头, 不能被外部访问, 只能内部使用
* 按作用域区分
    * 实例方法/对象方法
        * 参数中必须包含 `self`, `self` 是一个特殊的对象, 与 C++ 的 this 类似
    * 类方法 `@classmethod`
        ```Python {.line-numbers}
        class A:
            @classmethod        # 使用装饰器
            def func(cls, ...): # 使用 cls, 而非 self
                ...
        A.func(...) # 使用 "类名称.类方法" 的方式
        ```
    * 静态方法 `@staticmethod`
        ```Python {.line-numbers}
        class A:
            @staticmethod   # 使用装饰器
            def func(...):  # 既不用 cls, 也不用 self
                ...
        A.func(...) # 使用 "类名称.静态方法" 的方式
        ```
* 内建特殊方法/魔法函数, 实现特殊的功能:
    1. 跟运算符无关的特殊方法
        |      方法      | 作用                                                                                                     |
        | :------------: | -------------------------------------------------------------------------------------------------------- |
        | 实例创建和销毁 | \_\_new__, \_\_init__, \_\_del__                                                                         |
        | 字符串表示形式 | \_\_repr__, \_\_str__, \_\_bytes__, \_\_format__                                                         |
        |    属性管理    | \_\_getattr__, \_\_getattribute__, \_\_setattr__, \_\_delattr__, \_\_dir__                               |
        |   属性描述符   | \_\_get__, \_\_set__, \_\_delete__, \_\_set_name__                                                       |
        |   类管理相关   | \_\_class__, \_\_class_getitem__, \_\_init_subclass__, \_\_prepare__, \_\_slots__                        |
        | 实例和子类检查 | \_\_instancecheck__, \_\_subclasscheck__                                                                 |
        |   集合与序列   | \_\_len__, \_\_length_hint__, \_\_getitem__, \_\_setitem__, \_\_delitem__, \_\_contains__, \_\_missing__ |
        |    迭代枚举    | \_\_iter__, \_\_reversed__, \_\_next__                                                                   |
        |   上下文管理   | \_\_enter__, \_\_exit__                                                                                  |
        |      异步      | \_\_await__, \_\_aiter__, \_\_anext__, \_\_aenter__, \_\_aexit__                                         |
        |   可调用模拟   | \_\_call__                                                                                               |
    2. 跟运算相关的特殊方法
        |       类 别        | 方法名                                                                                                                       | 对应的运算符                                |
        | :----------------: | ---------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------- |
        |     一元运算符     | \_\_neg__, \_\_pos__, \_\_abs__                                                                                              | -, +, abs()                                 |
        |     比较运算符     | \_\_lt__, \_\_le__, \_\_eq__, \_\_ne__, \_\_gt__, \_\_ge__                                                                   | <, <=, ==, !=, >, >=                        |
        |     算术运算符     | \_\_add__, \_\_sub__, \_\_mul__, \_\_matmul__ \_\_truediv__, \_\_floordiv__, \_\_mod__, \_\_divmod__, \_\_pow__, \_\_round__ | +, -, *, @, /, //, %, divmod(), **, round() |
        |   反向算术运算符   | \_\_radd__, \_\_rsub__, \_\_rmul__, \_\_rmatmul__, \_\_rtruediv__, \_\_rfloordiv__, \_\_rmod__, \_\_rdivmod__, \_\_rpow__    | +, -, *, @, /, //, %, rdivmod(), **         |
        | 增量赋值算术运算符 | \_\_iadd__, \_\_isub__, \_\_imul__, \_\_imatmul__, \_\_itruediv__, \_\_ifloordiv__, \_\_imod__, \_\_ipow__                   | +=, -=, *=, @=, /=, //=, %=, **=            |
        |      位运算符      | \_\_invert__, \_\_lshift__, \_\_rshift__, \_\_and__, \_\_or__, \_\_xor__                                                     | ~, <<, >>, &, \|, ^                         |
        |    反向位运算符    | \_\_rlshift__, \_\_rrshift__, \_\_rand__, \_\_ror__, \_\_rxor__                                                              | <<, >>, &, \|, ^                            |
        |  增量赋值位运算符  | \_\_ilshift__, \_\_irshift__, \_\_iand__, \_\_ior__, \_\_ixor__                                                              | <<=,>>=, &=, \|=, ^=                        |
        |        近似        | \_\_round__, \_\_trunc__, \_\_floor__, \_\_ceil__                                                                            | 近似                                        |
        |      数值转换      | \_\_hash__, \_\_bool__, \_\_int__, \_\_float__, \_\_complex__                                                                |
* 属性管理方法
    * 方法1
        使用 `property(fget=None, fset=None, fdel=None, doc=None)` 指定 `getter`, `setter`, `deleter` 等方法
    * 方法2
        * `@property`, 用于指示 `getter` 方法
        * `@变量.setter`, 用于指示 `setter` 方法
        * `@变量.deleter`, 用于指示 `deleter` 方法

### 2.11.4. 对象
* 创建: `对象 = 类(参数)`
* 使用: `对象.公有变量` 或 `对象.方法(..)`

### 2.11.5. 继承与派生
* 语法
    ```Python {.line-numbers}
    class 派生类(基类1, 基类2, ...):
        ...
    ```
* 注意:
    * Python3 使用 C3 算法搜索基类, 可以通过 `__mro__` 属性查看
    * 基类如果在别的模块中, 可以使用`模块.类`的方式引用
    * 基类中的方法可以在子类中重写, 会覆盖基类方法
    * 常用 `super()` 访问基类的方法或变量, 尤其是基类的 `__init__` 方法
        * 注意多重继承时, `super()` 是按照 `__mro__` 顺序调用的
            ```Python {.line-numbers}
            class A:
                def __init__(self):
                    print("A")
            class B(A):
                def __init__(self):
                    print("B")
                    super().__init__()
            class C(A):
                def __init__(self):
                    print("C")
                    super().__init__()
            class D(B, C):
                def __init__(self):
                    print("D")
                    super().__init__()

            d = D()
            ```
            >运行结果
            > D
            > B
            > C
            > A
* **抽象基类**
    * 作用: 强制子类必须实现某种方法
    * 特点:
        * 派生类必须实现其中的方法
        * 无法实例化

### 2.11.6. 元类
* 创建类的类

## 2.12. 错误和异常
Python 是动态语言, 大概率出现错误和异常, 需用户处理:
* 错误: 语法错误
* 异常: 语法正确, 但函数运行错误

异常类继承自 `Exception` 类, 可以直接继承, 或者间接继承, 可以自定义异常

### 2.12.1. 异常处理
```Python {.line-numbers}
try:
    ...
except 异常 [as 异常别名]:  # 待处理的异常
# 或
except (异常1, 异常2, ...):
    ...
except:     # 可选, 所有其他异常
    ...
else:       # 可选, 未发生异常时
    ...
finally:    # 可选, 无论如何都会执行
    ...
```

### 2.12.2. 产生异常
```Python {.line-numbers}
raise 异常(异常信息)
```
* 捕获异常后可以不处理, 而是将其抛出, 如
    ```Python {.line-numbers}
    try:
        raise NameError('HiThere')
    except NameError:
        print('An exception flew by!')
        raise
    ```

### 2.12.3. 断言
* 语法: `assert 表达式 [, 参数]`
* 用法: 如果表达式不满足, `raise` 一个 `AssertionError`

### 2.12.4. 内建异常
```Python {.line-numbers}
BaseException
 +-- SystemExit
 +-- KeyboardInterrupt
 +-- GeneratorExit
 +-- Exception
      +-- StopIteration
      +-- StopAsyncIteration
      +-- ArithmeticError
      |    +-- FloatingPointError
      |    +-- OverflowError
      |    +-- ZeroDivisionError
      +-- AssertionError
      +-- AttributeError
      +-- BufferError
      +-- EOFError
      +-- ImportError
      |    +-- ModuleNotFoundError
      +-- LookupError
      |    +-- IndexError
      |    +-- KeyError
      +-- MemoryError
      +-- NameError
      |    +-- UnboundLocalError
      +-- OSError
      |    +-- BlockingIOError
      |    +-- ChildProcessError
      |    +-- ConnectionError
      |    |    +-- BrokenPipeError
      |    |    +-- ConnectionAbortedError
      |    |    +-- ConnectionRefusedError
      |    |    +-- ConnectionResetError
      |    +-- FileExistsError
      |    +-- FileNotFoundError
      |    +-- InterruptedError
      |    +-- IsADirectoryError
      |    +-- NotADirectoryError
      |    +-- PermissionError
      |    +-- ProcessLookupError
      |    +-- TimeoutError
      +-- ReferenceError
      +-- RuntimeError
      |    +-- NotImplementedError
      |    +-- RecursionError
      +-- SyntaxError
      |    +-- IndentationError
      |         +-- TabError
      +-- SystemError
      +-- TypeError
      +-- ValueError
      |    +-- UnicodeError
      |         +-- UnicodeDecodeError
      |         +-- UnicodeEncodeError
      |         +-- UnicodeTranslateError
      +-- Warning
           +-- DeprecationWarning
           +-- PendingDeprecationWarning
           +-- RuntimeWarning
           +-- SyntaxWarning
           +-- UserWarning
           +-- FutureWarning
           +-- ImportWarning
           +-- UnicodeWarning
           +-- BytesWarning
           +-- ResourceWarning
```

### 2.12.5. 自定义异常
* 可以继承自异常基类 `Exception`, 也可以继承自某个特定的类, 如 `ValueError`
* 示例
    ```Python {.line-numbers}
    class MyException(Exception):
        "数据太大了"
        def __init__(self, val):
            super().__init__()
            self.val = val
        def __str__(self):
            return f"数据太大了: {self.val}"

    try:
        raise MyException(12)
    except MyException as e:
        print(e)    # "数据太大了: 12"
    ```

## 2.13. 输入/输出
* 输入:
    * 标准输入: 内置函数 `input(prompt=None)`
    * 从文件输入: 详见[文件操作](Python%20笔记%EF%BC%9A文件操作.md)
    * pickle:
        * 以读取的形式打开: `x = pickle.load(file)`
* 输出:
    * 标准输出: 终端 `print(...)`
    * 文件输出: 详见[文件操作](Python%20笔记%EF%BC%9A文件操作.md)
    * pickle: 实现了基本的数据序列和反序列化, 通过pickle模块的序列化操作我们能够将程序中运行的对象信息保存到文件中去, 永久存储, 通过 pickle 模块的反序列化操作, 我们能够从文件中创建上一次程序保存的对象
        * 基本接口: `pickle.dump(obj, file, [,protocol])`

--------------------------------------------------------------------------------
# 3. 高级语法

## 3.1. 迭代器 (iterator)
* 创建: 使用内建函数 `iter(对象)`, 返回一个迭代器对象
* 遍历:
    * 使用内建函数 `next(迭代器)` 引用下一个
        * 第一次使用时, 返回迭代器第一个元素
        * 每使用一次, 迭代器向后移动一个
        * 迭代结束后再次使用会产生`StopIteration`异常
    * 使用 `for x in <可迭代对象>: `
* `iter()`和`next()`的实现:
    * 创建`class`时实现方法: `__iter__(self)`, `__next__(self)`
* 技巧:
    * 用内建函数 `zip` 同时迭代多个对象(以最短的为准), 如
        ```Python {.line-numbers}
        for index in zip(myiter1, myiter2):
            # do som thing
        # or
        for index1, index2 in zip(myiter1, myiter2):
            # do som thing
        ```
    * 用内建函数 `enumerate` 可将可迭代对象组成索引序列
        ```Python {.line-numbers}
        for index, dat in enumerate(myiter):
            if(index > 100):
                # do some thing
        ```
    * 用内建函数`reversed`可反向迭代
    * 标准库 `itertools` 提供更多迭代功能, 包括: 周期循环、重复、串联、截断、压缩、挑选、分组、排列、组合等
        * 无限迭代
            |       Iterator       | Results                                          | Example                               |
            | :------------------: | :----------------------------------------------- | :------------------------------------ |
            | count(start, [step]) | start, start+step, start+2*step, ...             | count(10) --> 10 11 12 13 14 ...      |
            |       cycle(p)       | p0, p1, ... plast, p0, p1, ...                   | cycle('ABCD') --> A B C D A B C D ... |
            |  repeat(elem [,n])   | elem, elem, elem, ... endlessly or up to n times | repeat(10, 3) --> 10 10 10            |
        * 在最短的序列结束
            |              Iterator               | Results                                         | Example                                                  |
            | :---------------------------------: | :---------------------------------------------- | :------------------------------------------------------- |
            |        accumulate(p[, func])        | p0, p0+p1, p0+p1+p2                             | accumulate([1,2,3,4,5]) --> 1 3 6 10 15                  |
            |          chain(p, q, ...)           | p0, p1, ... plast, q0, q1, ...                  | chain('ABC', 'DEF') --> A B C D E F                      |
            |  chain.from_iterable([p, q, ...])   | p0, p1, ... plast, q0, q1, ...                  | chain.from_iterable(['ABC', 'DEF']) --> A B C D E F      |
            |      compress(data, selectors)      | (d[0] if s[0]), (d[1] if s[1]), ...             | compress('ABCDEF', [1,0,1,0,1,1]) --> A C E F            |
            |        dropwhile(pred, seq)         | seq[n], seq[n+1], starting when pred fails      | dropwhile(lambda x: x<5, [1,4,6,4,1]) --> 6 4 1          |
            |       filterfalse(pred, seq)        | elements of seq where pred(elem) is False       | filterfalse(lambda x: x%2, range(10)) --> 0 2 4 6 8      |
            |    groupby(iterable[, keyfunc])     | sub-iterators grouped by value of keyfunc(v)    | -                                                        |
            | islice(seq, [start,] stop [, step]) | elements from seq[start:stop:step]              | islice('ABCDEFG', 2, None) --> C D E F G                 |
            |          starmap(fun, seq)          | fun(*seq[0]), fun(*seq[1]), ...                 | starmap(pow, [(2,5), (3,2), (10,3)]) --> 32 9 1000       |
            |        takewhile(pred, seq)         | seq[0], seq[1], until pred fails                | takewhile(lambda x: x<5, [1,4,6,4,1]) --> 1 4            |
            |            tee(it, n=2)             | (it1, it2 , ... itn) splits one iterator into n | -                                                        |
            |       zip_longest(p, q, ...)        | (p[0], q[0]), (p[1], q[1]), ...                 | zip_longest('ABCD', 'xy', fillvalue='-') --> Ax By C- D- |
        * 组合迭代
            |              Iterator               | Results                                  | Example                                                                       |
            | :---------------------------------: | :--------------------------------------- | :---------------------------------------------------------------------------- |
            |    product(p, q, ... [repeat=1])    | cartesian product, 等效于嵌套的 for 循环 | product('ABCD', repeat=2) --> AA AB AC AD BA BB BC BD CA CB CC CD DA DB DC DD |
            |        permutations(p[, r])         | r-length tuples, 排列                    | permutations('ABCD', 2) --> AB AC AD BA BC BD CA CB CD DA DB DC               |
            |         combinations(p, r)          | r-length tuples, 组合 (不包含重复元素)   | combinations('ABCD', 2) --> AB AC AD BC BD CD                                 |
            | combinations_with_replacement(p, r) | r-length tuples, 组合 (包含重复元素)     | combinations_with_replacement('ABCD', 2) --> AA AB AC AD BB BC BD CC CD DD    |
    * 第三方库 `more-itertools`
        * `pip install more-itertools`

## 3.2. 生成器 (generator)

### 3.2.1. 生成器
* 可用于迭代或 for 循环
* 每次调用时, 函数运行到 `yield` 时停止, 并返回 `yield` 的值, 在下一次执行时从当前位置继续运行
* 可以有多个 `yield`
* 可通过 `next(生成器对象)/生成器对象.send(..)` 调用
* 对象方法:
    * `.send(参数)`: 传入数据并返回下一个`yield`的值, 或抛出`StopIteration`
        * 如果生成器没有开始运行, 只能`.send(None)`
    * `.throw(typ[,val[,tb]])`: 抛出异常并返回下一个`yield`的值, 或抛出`StopIteration`
    * `.close(arg)`: 抛出`GeneratorExit`异常
* 可用 `list(生成器对象)` 获取对应的列表
* 计算生成器对象的长度
    ```Python {.line-numbers}
    len(list(生成器对象))
    sum(1 for _ in 生成器对象)
    len([_ for _ in 生成器对象])
    ```
### 3.2.2. 创建生成器
* 方法1: 使用生成器表达式 (列表推导式的 `[] `换成 `()`)
    ```Python {.line-numbers}
    gen = (x for x in range(1,6)) # <generator object <genexpr> at ...>
    next(gen) # 返回 1
    ```
* 方法2: 使用 `yield 变量` 的函数
    ```Python {.line-numbers}
    # 示例1
    def fib(n_max):
        n, a, b = 0, 0, 1
        while n < n_max:
            yield b         # 1: 返回值; 2: 暂停, 等待下一次调用;
            a, b = b, a+b
            n += 1

    for _ in fib(10):
        print(_, end=" ")
    # 输出: 1 1 2 3 5 8 13 21 34 55
    ```

    ```Python {.line-numbers}
    # 示例2
    def gen_func():
        print(f"in generator")
        yield 1              # 1: 返回值; 2: 暂停, 等待下一次调用;
        param = yield "abc"  # 1: 返回值; 2: 暂停, 等待下一次调用; 3: 接收参数
        print(param)
        yield [1,2,3]        # 1: 返回值; 2: 暂停, 等待下一次调用;
        return "Done"

    if __name__ == "__main__":
        gen = gen_func()
        print(gen.send(None))
        # print(next(gen))
        ''' 输出
        in generator
        1
        '''
        print(next(gen))
        # 输出: abc
        print(gen.send({'name':'Alex'}))
        ''' 输出
        {'name': 'Alex'}
        [1, 2, 3]
        '''
        print(next(gen))
        ''' 弹出异常
        StopIteration: Done
        '''
    ```

### 3.2.3. yield from
* 语法:
    ```Python {.line-numbers}
    yield from 可迭代对象
    # 等效于
    for it in 可迭代对象:
        yield it
    ```
* 会在调用方和子生成器之间建立一个**双向通道**
    ```Python {.line-numbers}
    gen = (x for x in range(1,6))

    def f1(it):
        yield from it

    for i in f1(gen):
        print(i, end=", ")
    #输出: 1, 2, 3, 4, 5,
    ```

## 3.3. 装饰器 (Decorator)
* 扩展函数功能
* 语法糖: 在函数或类前使用 `@<装饰器>` 语句

### 3.3.1. 基础
* 简单的装饰器
    ```Python {.line-numbers}
    import logging

    def use_logging(func):
        def wrapper():
            logging.warning(f"{func.__name__} is running")
            return func()
        return wrapper

    # 使用方式1: 装饰器调用
    def foo1():
        print('i am foo1')
    foo = use_logging(foo1)
    # 使用方式2: `@`语法糖
    @use_logging
    def foo2():
        print("i am foo2")
    # 调用
    foo()
    # 运行后输出:
    # WARNING:root:foo1 is running
    # i am foo1
    foo2()  # 等效于 use_logging(foo2)
    # 运行后输出:
    # WARNING:root:foo2 is running
    # i am foo2
    ```
    ```Python {.line-numbers}
    import logging

    def use_logging(level):
        def decorator(func):
            def wrapper():
                if level == "warning":
                    logging.warning(f"{func.__name__} is running")
                elif level == "info":
                    logging.info(f"{func.__name__} is running")
                return func()
            return wrapper
        return decorator

    @use_logging(level="warning")
    def foo():
        print(f"i am foo")

    foo()  # 等效于 (use_logging(level="warning")(foo))()
    # 运行后输出:
    # WARNING:root:foo is running
    # i am foo
    ```
* 带参数的装饰器
    ```Python {.line-numbers}
    import logging

    def use_logging(func):
        def wrapper(*args, **kwargs):
            logging.warning(f"{func.__name__} is running")
            return func(*args)
        return wrapper

    @use_logging
    def foo(name):
        print(f"i am {name}")

    foo("foo")   # 等效于 (use_logging(foo))("foo")
    # 运行后输出:
    # WARNING:root:foo is running
    # i am foo
    ```
* 类装饰器, 主要依靠类的 `__call__` 方法
    ```Python {.line-numbers}
    class Foo(object):
        def __init__(self, func):
            self._func = func

        def __call__(self):
            print ('class decorator runing')
            self._func()
            print ('class decorator ending')

    @Foo
    def bar(): print ('bar')

    bar()
    # 运行后输出:
    # class decorator runing
    # bar
    # class decorator ending
    ```

### 3.3.2. 进阶
* `functools.wraps`
    * 使用装饰器极大地复用了代码, 但是他有一个缺点: 原函数的元信息不见了, 如函数的docstring、\_\_name__、参数列表;
    * 使用`functools.wraps`(本身也是一个装饰器), 把原函数的元信息拷贝到装饰器里面的 func 函数中
    *   ```Python {.line-numbers}
        from functools import wraps

        def logged(func):
            @wraps(func)
            def with_logging(*args, **kwargs):
                print(f"func.__name__: {func.__name__}")
                print(f"func.__doc__: {func.__doc__}")
                return func(*args, **kwargs)
            return with_logging

        @logged
        def f(x):
            """函数说明"""
            return x + x * x

        print(f(10))
        """ 输出
        func.__name__: f
        func.__doc__: 函数说明
        110
        """
        ```
* 装饰器顺序: 一个函数可以同时定义多个装饰器, 执行顺序是从里到外
    ```Python {.line-numbers}
    @a
    @b
    @c
    def f(s): print(s)
    # 等效于
    f = (a(b(c(f))))(s)
    ```

## 3.4. 上下文管理器 (contextor)
* 语法
    ```Python {.line-numbers}
    with 管理器类:
    # 或
    with 管理器类 as 管理器对象:
        with_body
    with 管理器类1 as 管理器对象1, 管理器类2 as 管理器对象2:
        with_body
    with 管理器类1 as 管理器对象1, \
         管理器类2 as 管理器对象2:
        with_body
    # python 3.10 可以用圆括号包裹
    with ( 管理器类1 as 管理器对象1,
           管理器类2 as 管理器对象2
    ):
        with_body
    ```
* 实现上下文管理器: 在创建类时, 实现 `__enter__`(返回值作为 `as` 的变量) 和 `__exit__` 方法
* 执行原理
    1. 获取上下文管理器
    1. 调用 `__enter()__` 方法, 返回上下文管理器对象
    1. 执行子代码块 `with_body`
    1. 调用 `__exit()__` 方法,
        * 如果 `with_body` 的退出是由异常引发的, 那么该异常的 type, value 和 traceback 会作为参数传给 `__exit()__`, 否则传三个 None
    1. 如果 `with_body` 的退出由异常引发, 并且 `__exit()__` 的返回值为 False, 那么这个异常将被重新引发一次, 如果 `__exit()__` 的返回值为 True, 那么这个异常就被无视掉, 继续执行后面的代码

--------------------------------------------------------------------------------
# 4. 标准库简介

## 4.1. 内建库 \_\_builtins__
内建函数、常量、类、异常等位于 `__builtins__` 库

* 内建函数, 详见 [2.11.7. 内建函数](#2117-内建函数)
* 内建常量
    |      常量       | 含义                     |
    | :-------------: | ------------------------ |
    |  True / False   | 真/假                    |
    |      None       | 空                       |
    | NotImplemented  | 未实现                   |
    |    Ellipsis     | 省略号                   |
    |  \_\_debug\_\_  | Python是否以`-O`属性开始 |
    | quit(code=None) | 退出                     |
    | exit(code=None) | 退出                     |
    |    copyright    | 版权信息                 |
    |     credits     | 致谢                     |
    |     license     | 授权                     |
* 内建类: 包括: int, bool, float, complex, str, list, tuple, set, frozenset, dictionary, bytes, bytearray, memoryview, range, ...等
* 内建异常, 参见[2.14.4. 内建异常](#2144-内建异常)

## 4.2. 标准库
* 文本处理
    |    模块     | 说明                                 |
    | :---------: | ------------------------------------ |
    | ==string==  | 通用字符串操作                       |
    |   ==re==    | 正则表达式                           |
    |   difflib   | Helpers for computing deltas         |
    |  textwrap   | Text wrapping and filling            |
    | unicodedata | Unicode数据库                        |
    | stringprep  | Internet String Preparation          |
    |  readline   | GNU readline interface               |
    | rlcompleter | Completion function for GNU readline |

* 二进制操作
    |    模块    | 说明                                  |
    | :--------: | ------------------------------------- |
    | ==struct== | Interpret bytes as packed binary data |
    |   codecs   | Codec registry and base classes       |

* 数据类型
    |        模块         | 说明                                                |
    | :-----------------: | --------------------------------------------------- |
    |    ==datetime==     | Basic date and time types                           |
    |      zoneinfo       | IANA time zone support                              |
    |      calendar       | General calendar-related functions                  |
    |   ==collections==   | Container datatypes                                 |
    | ==collections.abc== | Abstract Base Classes for Containers                |
    |        heapq        | Heap queue algorithm                                |
    |       bisect        | Array bisection algorithm                           |
    |        array        | Efficient arrays of numeric values                  |
    |       weakref       | Weak references                                     |
    |        types        | Dynamic type creation and names for built-in types  |
    |        copy         | Shallow and deep copy operations                    |
    |       pprint        | Data pretty printer                                 |
    |       reprlib       | Alternate repr() implementation                     |
    |        enum         | Support for enumerations                            |
    |      graphlib       | Functionality to operate with graph-like structures |

* 数字和数学
    |      模块      | 说明                                              |
    | :------------: | ------------------------------------------------- |
    |  ==numbers==   | Numeric abstract base classes                     |
    |    ==math==    | 数学函数                                          |
    |     cmath      | 复数的数学函数                                    |
    |  ==decimal==   | Decimal fixed point and floating point arithmetic |
    | ==fractions==  | Rational numbers                                  |
    |   ==random==   | Generate pseudo-random numbers                    |
    | ==statistics== | Mathematical statistics functions                 |

* 函数编程
    |     模块      | 说明                                                      |
    | :-----------: | --------------------------------------------------------- |
    | ==itertools== | Functions creating iterators for efficient looping        |
    | ==functools== | Higher-order functions and operations on callable objects |
    |   operator    | Standard operators as functions                           |

* 文件和目录操作
    |    模块     | 说明                                           |
    | :---------: | ---------------------------------------------- |
    | ==pathlib== | Object-oriented filesystem paths               |
    | ==os.path== | Common pathname manipulations                  |
    |  fileinput  | Iterate over lines from multiple input streams |
    |    stat     | Interpreting stat() results                    |
    |   filecmp   | File and Directory Comparisons                 |
    |  tempfile   | Generate temporary files and directories       |
    |    glob     | Unix style pathname pattern expansion          |
    |   fnmatch   | Unix filename pattern matching                 |
    |  linecache  | Random access to text lines                    |
    |   shutil    | High-level file operations                     |

* 数据存储
    |  模块   | 说明                                      |
    | :-----: | ----------------------------------------- |
    | pickle  | Python object serialization               |
    | copyreg | Register pickle support functions         |
    | shelve  | Python object persistence                 |
    | marshal | Internal Python object serialization      |
    |   dbm   | Interfaces to Unix  "databases"           |
    | sqlite3 | DB-API 2.0 interface for SQLite databases |

* 数据压缩
    |  模块   | 说明                                 |
    | :-----: | ------------------------------------ |
    |  zlib   | Compression compatible with gzip     |
    |  gzip   | Support for gzip files               |
    |   bz2   | Support for bzip2 compression        |
    |  lzma   | Compression using the LZMA algorithm |
    | zipfile | Work with ZIP archives               |
    | tarfile | Read and write tar archive files     |

* 文件格式
    |       模块       | 说明                                     |
    | :--------------: | ---------------------------------------- |
    |     ==csv==      | CSV File Reading and Writing             |
    | ==configparser== | Configuration file parser                |
    |      netrc       | netrc file processing                    |
    |     plistlib     | Generate and parse Mac OS X .plist files |

* 加密
    |  模块   | 说明                                                |
    | :-----: | --------------------------------------------------- |
    | hashlib | Secure hashes and message digests                   |
    |  hmac   | Keyed-Hashing for Message Authentication            |
    | secrets | Generate secure random numbers for managing secrets |

* 操作系统
    |         模块         | 说明                                                        |
    | :------------------: | ----------------------------------------------------------- |
    |        ==os==        | Miscellaneous operating system interfaces                   |
    |          io          | Core tools for working with streams                         |
    |       ==time==       | Time access and conversions                                 |
    |       argparse       | Parser for command-line options, arguments and sub-commands |
    |        getopt        | C-style parser for command line options                     |
    |     ==logging==      | Logging facility for Python                                 |
    |  ==logging.config==  | Logging configuration                                       |
    | ==logging.handlers== | Logging handlers                                            |
    |       getpass        | Portable password input                                     |
    |        curses        | Terminal handling for character-cell displays               |
    |    curses.textpad    | Text input widget for curses programs                       |
    |     curses.ascii     | Utilities for ASCII characters                              |
    |     curses.panel     | A panel stack extension for curses                          |
    |     ==platform==     | Access to underlying platform’s identifying data            |
    |        errno         | Standard errno system symbols                               |
    |      ==ctypes==      | A foreign function library for Python                       |

* 并行运行
    |             模块              | 说明                                                      |
    | :---------------------------: | --------------------------------------------------------- |
    |         ==threading==         | Thread-based parallelism                                  |
    |      ==multiprocessing==      | Process-based parallelism                                 |
    | multiprocessing.shared_memory | Provides shared memory for direct access across processes |
    |    ==concurrent.futures==     | Launching parallel tasks                                  |
    |        ==subprocess==         | Subprocess management                                     |
    |             sched             | Event scheduler                                           |
    |           ==queue==           | A synchronized queue class                                |
    |          contextvars          | Context Variables                                         |
    |            _thread            | Low-level threading API                                   |

* 进程间通信和网络
    |    模块     | 说明                                 |
    | :---------: | ------------------------------------ |
    | ==asyncio== | Asynchronous I/O                     |
    | ==socket==  | 底层网络接口                         |
    |     ssl     | TLS/SSL wrapper for socket objects   |
    |   select    | Waiting for I/O completion           |
    |  selectors  | High-level I/O multiplexing          |
    |   signal    | Set handlers for asynchronous events |
    |    mmap     | Memory-mapped file support           |

* 网络数据处理
    |   模块    | 说明                                          |
    | :-------: | --------------------------------------------- |
    |   email   | An email and MIME handling package            |
    | ==json==  | JSON encoder and decoder                      |
    |  mailcap  | Mailcap file handling                         |
    |  mailbox  | Manipulate mailboxes in various formats       |
    | mimetypes | Map filenames to MIME types                   |
    |  base64   | Base16, Base32, Base64, Base85 Data Encodings |
    |  binhex   | Encode and decode binhex4 files               |
    | binascii  | Convert between binary and ASCII              |
    |  quopri   | Encode and decode MIME quoted-printable data  |

* 结构化文件处理
    |         模块          | 说明                                   |
    | :-------------------: | -------------------------------------- |
    |         html          | HyperText Markup Language support      |
    |      html.parser      | Simple HTML and XHTML parser           |
    |     html.entities     | Definitions of HTML general entities   |
    | xml.etree.ElementTree | The ElementTree XML API                |
    |        xml.dom        | The Document Object Model API          |
    |    xml.dom.minidom    | Minimal DOM implementation             |
    |    xml.dom.pulldom    | Support for building partial DOM trees |
    |        xml.sax        | Support for SAX2 parsers               |
    |    xml.sax.handler    | Base classes for SAX handlers          |
    |   xml.sax.saxutils    | SAX Utilities                          |
    |   xml.sax.xmlreader   | Interface for XML parsers              |
    |   xml.parsers.expat   | Fast XML parsing using Expat           |

* 网络协议
    |        模块        | 说明                                        |
    | :----------------: | ------------------------------------------- |
    |     webbrowser     | Convenient Web-browser controller           |
    |      wsgiref       | WSGI Utilities and Reference Implementation |
    |       urllib       | URL handling modules                        |
    |   urllib.request   | Extensible library for opening URLs         |
    |  urllib.response   | Response classes used by urllib             |
    |    urllib.parse    | Parse URLs into components                  |
    |    urllib.error    | Exception classes raised by urllib.request  |
    | urllib.robotparser | Parser for robots.txt                       |
    |        http        | HTTP modules                                |
    |    http.client     | HTTP protocol client                        |
    |       ftplib       | FTP protocol client                         |
    |       poplib       | POP3 protocol client                        |
    |      imaplib       | IMAP4 protocol client                       |
    |      smtplib       | SMTP protocol client                        |
    |        uuid        | UUID objects according to RFC 4122          |
    |    socketserver    | A framework for network servers             |
    |    http.server     | HTTP servers                                |
    |    http.cookies    | HTTP state management                       |
    |   http.cookiejar   | Cookie handling for HTTP clients            |
    |       xmlrpc       | XMLRPC server and client modules            |
    |   xmlrpc.client    | XML-RPC client access                       |
    |   xmlrpc.server    | Basic XML-RPC servers                       |
    |     ipaddress      | IPv4/IPv6 manipulation library              |

* 多媒体
    |   模块   | 说明                              |
    | :------: | --------------------------------- |
    |   wave   | Read and write WAV files          |
    | colorsys | Conversions between color systems |

* 国际化
    |  模块   | 说明                                       |
    | :-----: | ------------------------------------------ |
    | gettext | Multilingual internationalization services |
    | locale  | Internationalization services              |

* 程序框架
    |  模块  | 说明                                           |
    | :----: | ---------------------------------------------- |
    | turtle | Turtle graphics                                |
    |  cmd   | Support for line-oriented command interpreters |
    | shlex  | Simple lexical analysis                        |

* GUI
    |         模块         | 说明                       |
    | :------------------: | -------------------------- |
    |     ==tkinter==      | Python interface to Tcl/Tk |
    |     tkinter.ttk      | Tk themed widgets          |
    |     tkinter.tix      | Extension widgets for Tk   |
    | tkinter.scrolledtext | Scrolled Text Widget       |

* 开发工具
    |            模块            | 说明                                           |
    | :------------------------: | ---------------------------------------------- |
    |           typing           | Support for type hints                         |
    |           pydoc            | Documentation generator and online help system |
    |          doctest           | Test interactive Python examples               |
    |          unittest          | Unit testing framework                         |
    |       unittest.mock        | mock object library                            |
    |       unittest.mock        | getting started                                |
    |            2to3            | Automated Python 2 to 3 code translation       |
    |            test            | Regression tests package for Python            |
    |        test.support        | Utilities for the Python test suite            |
    | test.support.script_helper | Utilities for the Python execution tests       |

* 调试和性能
    |     模块     | 说明                                          |
    | :----------: | --------------------------------------------- |
    |     bdb      | Debugger framework                            |
    | faulthandler | Dump the Python traceback                     |
    |     pdb      | The Python Debugger                           |
    | ==cProfile== | The Python Profilers                          |
    | ==profile==  | ^                                             |
    |  ==timeit==  | Measure execution time of small code snippets |
    |    trace     | Trace or track Python statement execution     |
    | tracemalloc  | Trace memory allocations                      |

* 软件打包和分发
    |   模块    | 说明                                   |
    | :-------: | -------------------------------------- |
    | distutils | Building and installing Python modules |
    | ensurepip | Bootstrapping the pip installer        |
    |   venv    | Creation of virtual environments       |
    |  zipapp   | Manage executable python zip archives  |

* Python Runtime支持
    |       模块       | 说明                                                 |
    | :--------------: | ---------------------------------------------------- |
    |     ==sys==      | System-specific parameters and functions             |
    |    sysconfig     | Provide access to Python’s configuration information |
    |     builtins     | Built-in objects                                     |
    | ==\_\_main\_\_== | Top-level script environment                         |
    |     warnings     | Warning control                                      |
    |   dataclasses    | Data Classes                                         |
    |    contextlib    | Utilities for with-statement contexts                |
    |       abc        | Abstract Base Classes                                |
    |      atexit      | Exit handlers                                        |
    |    traceback     | Print or retrieve a stack traceback                  |
    |  \_\_future\_\_  | Future statement definitions                         |
    |      ==gc==      | Garbage Collector interface                          |
    |   ==inspect==    | Inspect live objects                                 |
    |       site       | Site-specific configuration hook                     |

* 定制Python解释器
    |  模块  | 说明                     |
    | :----: | ------------------------ |
    |  code  | Interpreter base classes |
    | codeop | Compile Python code      |

* 导入模块
    |     模块     | 说明                                  |
    | :----------: | ------------------------------------- |
    |  zipimport   | Import modules from Zip archives      |
    |   pkgutil    | Package extension utility             |
    | modulefinder | Find modules used by a script         |
    |    runpy     | Locating and executing Python modules |
    |  importlib   | The implementation of import          |

* Python语言支持
    |    模块     | 说明                                   |
    | :---------: | -------------------------------------- |
    |     ast     | Abstract Syntax Trees                  |
    |  symtable   | Access to the compiler’s symbol tables |
    |    token    | Constants used with Python parse trees |
    | ==keyword== | Testing for Python keywords            |
    |  tokenize   | Tokenizer for Python source            |
    |  tabnanny   | Detection of ambiguous indentation     |
    |   pyclbr    | Python class browser support           |
    | py_compile  | Compile Python source files            |
    | compileall  | Byte-compile Python libraries          |
    |   ==dis==   | Disassembler for Python bytecode       |
    | pickletools | Tools for pickle developers            |

* 微软特有服务
    |   模块   | 说明                                     |
    | :------: | ---------------------------------------- |
    |  msvcrt  | Useful routines from the MS VC++ runtime |
    |  winreg  | Windows registry access                  |
    | winsound | Sound-playing interface for Windows      |

* Unix特有服务
    |   模块   | 说明                               |
    | :------: | ---------------------------------- |
    |  posix   | The most common POSIX system calls |
    |   pwd    | The password database              |
    |   grp    | The group database                 |
    | termios  | POSIX style tty control            |
    |   tty    | Terminal control functions         |
    |   pty    | Pseudo-terminal utilities          |
    |  fcntl   | The fcntl and ioctl system calls   |
    | resource | Resource usage information         |
    |  syslog  | Unix syslog library routines       |
