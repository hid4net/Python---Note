
0.1. **Python 总结: 调试与开发**
--------------------------------------------------------------------------------
[返回目录](outline.md)

--------------------------------------------------------------------------------
tips:

--------------------------------------------------------------------------------

<!-- @import "[TOC]" {cmd="toc" depthFrom=1 depthTo=6 orderedList=false} -->

<!-- code_chunk_output -->

- [1. Runtime 信息](#1-runtime-信息)
  - [1.1. 标准库 sys](#11-标准库-sys)
- [2. 日志 (标准库 logging)](#2-日志-标准库-logging)
  - [2.1. 基本](#21-基本)
  - [2.2. 重要: 解决 logger 重复打印的问题](#22-重要-解决-logger-重复打印的问题)
  - [2.3. 面向对象方法](#23-面向对象方法)
    - [2.3.1. 基本流程](#231-基本流程)
    - [2.3.2. 主要的 class](#232-主要的-class)
    - [2.3.3. class: Logger](#233-class-logger)
    - [2.3.4. class: Filterer](#234-class-filterer)
    - [2.3.5. class: Handler](#235-class-handler)
    - [2.3.6. class: Formatter](#236-class-formatter)
  - [2.4. 函数方法](#24-函数方法)
  - [2.5. 高级技巧](#25-高级技巧)
- [3. 运行时间测量](#3-运行时间测量)
  - [3.1. 标准库 time](#31-标准库-time)
  - [3.2. 标准库 timeit](#32-标准库-timeit)
  - [3.3. 使用解释器](#33-使用解释器)
- [4. Profile](#4-profile)
  - [4.1. 标准库 cProfile, profile](#41-标准库-cprofile-profile)
  - [4.2. 第三方库 line_profiler](#42-第三方库-line_profiler)
- [5. numba](#5-numba)
  - [5.1. wrapper](#51-wrapper)
  - [5.2. @jit](#52-jit)
- [6. cython](#6-cython)
- [7. 反汇编](#7-反汇编)
  - [7.1. 标准库 dis](#71-标准库-dis)
- [8. 运行环境](#8-运行环境)
  - [8.1. Virtualenv](#81-virtualenv)
  - [8.2. Virtualenvwrapper](#82-virtualenvwrapper)
- [9. 生成可执行文件](#9-生成可执行文件)
  - [9.1. PyInstaller](#91-pyinstaller)

<!-- /code_chunk_output -->

--------------------------------------------------------------------------------
# 1. Runtime 信息

## 1.1. 标准库 sys
* `import sys`
* 访问与 Python 解释器紧密相关的变量和函数, 其中一些重要的函数和变量
    函数/变量       | 描述
    :-------------: | :----------------------
    `argv`          | 命令行参数, 包括脚本名
    `exit([arg])`   | 退出当前程序, 可通过可选参数指定返回值或错误消息
    `modules`       | 一个字典, 将模块名映射到加载的模块
    `path`          | 一个列表, 包含要在其中查找模块的目录的名称
    `platform`      | 平台标识符, 如 `win32`
    `stdin`         | 标准输入流
    `stdout`        | 标准输出流
    `stderr`        | 标准错误流
    ...             | ...

--------------------------------------------------------------------------------
# 2. 日志 (标准库 logging)

## 2.1. 基本
* 默认情况下, logging 将日志打印到屏幕, 日志级别为 `WARNING`
* 日志级别大小关系为: `CRITICAL (50)` > `ERROR (40)` > `WARNING (30)` > `INFO (20)` > `DEBUG (10)` > `NOTSET (0)`
* 可以自己定义日志级别
* logger 是线程安全的
* 示例:
    ```Python
    # 同时打印到屏幕和文件
    import logging
    from pathlib import Path
    #-------------------------------------------------------------------------------
    # 获取或创建 Logger
    # ! 官方建议: 不要直接 logger, 而使用模块中的 getLogger 函数 (即便多次调用, 仍返回同一个对象)
    log = logging.getLogger(Path(__file__).stem)    # 如果未命名, 默认为 root logger
    log.setLevel(logging.DEBUG)
    #-------------------------------------------------------------------------------
    log_fmt = logging.Formatter('%(asctime)s %(levelname)s: %(message)s', '%Y-%m-%d %H:%M:%S')
    #-------------------------------------------------------------------------------
    log.handlers.clear()    # 如果多次使用同名的 logger, 会重复, 这样可以防止重复
    #-------------------------------------------------------------------------------
    # 打印到屏幕
    ch = logging.StreamHandler()
    ch.setFormatter(log_fmt)
    # ch.setLevel(logging.DEBUG)  # 可选, 如不设置, 继承 log 的级别
    log.addHandler(ch)
    #-------------------------------------------------------------------------------
    # 打印到文件
    fh = logging.FileHandler(Path(__file__).stem+'.log', 'w', "utf-8")
    fh.setFormatter(log_fmt)
    fh.setLevel(logging.INFO)   # 可选, 如不设置, 继承 log 的级别
    log.addHandler(fh)
    #-------------------------------------------------------------------------------
    log.info(f"正在处理数据...")    # 2019-06-24 16:35:59 INFO: 正在处理数据...
    ```

## 2.2. 重要: 解决 logger 重复打印的问题
* 问题: 多次使用同名的 logger, 会重复打印
* 原因: 实际上 `log = logging.getLogger('mylog')` 在执行时, 没有每次生成一个新的 logger, 而是先检查内存中是否存在一个叫做 mylog 的logger 对象, 存在则取出, 不存在则新建. 每次新建都会增加 handler, 所以会重复
* 解决方案:
    * 方法 1: 及时清理 logger 的 handler: `log.handlers.clear()`
        > 也可以用 `removeHandler` 方法, 但兼容性差
    * 方法 2: 用之前判断是否有已经存在 handler, 如果没有才增加 handler, 如:
        ```Python
        if not log.hasHandlers():
            # 添加 handler
        ```
    * 方法 3: 每次都更改 logger 的名字

## 2.3. 面向对象方法

### 2.3.1. 基本流程
1. 使用模块的全局函数 `getLogger(log_名)` 创建 **Logger** 对象
    * ==官方不建议自己创建 logger 对象==, 而是通过 `logging.getLogger(log_名)` 获取
    * `log_名` 是可选的, 如果不设置, 默认使用 `root`
    * `log_名` 可以是多级的, 如 *'root.child1'*, *'root.child1.child2'*
    * 可以使用代码或函数名称 *\_\_name\_\_*
1. 【建议】根据所需的 log 文件的格式创建 **Formatter** 对象
1. 创建 **Handler** 对象, 并设置其格式和 log 级别
    * 设置格式: `.setFormatter` 方法
    * 设置 log 级别: `.setLevel` 方法
1. 为 **Logger** 对象添加 **Handler** 对象
1. 输出 log 内容: 可使用 **Logger** 对象的方法
    * `.debug(..)`
    * `.info(..)`
    * `.warning(..)`
    * `.error(..)`
    * `.critical(..)`

### 2.3.2. 主要的 class
* **Logger** 是面向对象的日志记录器, 输出日志
* **Logger** 通过加载 **Handler** 指定日志输出到哪, 常用的有三个
    * `StreamHandler`: 输出到屏幕
    * `FileHandler`: 输出到文件
    * `NullHandler`: 空的, 一般用于设计模块代码
* **Logger** 或 **Handler** 通过加载 **Filter** 决定输出哪些信息
* **Handler** 通过加载 **Formatter** 决定输出信息的格式
![关系图](/assets/python%20logging.webp)

### 2.3.3. class: Logger
* 构造: `Logger(name, level=0)`
* 主要方法
    分类        | 方法
    :---------: | ----
    管理 Handler| `addHandler(hdlr)`, `removeHandler(hdlr)`, `hasHandlers()`, ...
    输出        | `debug(msg, ...)` <br/> `info(msg, ...)` <br/> `warning(msg, ...)` <br/> `error(msg, ...)` ≈ `exception(msg, exc_info=True)`^1^ <br/> `critical(msg, ...)`
    ^           | `log(level, msg, ...)`
    ^           | ...
    级别        | `setLevel(level)`, `isEnabledFor(level)`, ...
    其他        | ...
    * 注意:
        ^1^ 基本等效于 `error(msg, ...)`
* 主要属性: `name`, `level`, `handles`, `disabled`, ...

### 2.3.4. class: Filterer
* 构造: `Filterer()`
* 主要方法
    * `addFilter(filter)`
    * `removeFilter(filter)`
    * `filter(record)`
* 主要属性: `filters`

### 2.3.5. class: Handler
* 继承自 `Filterer`
* 构造: `Handler(level=0)`
* 主要方法
    分类        | 方法
    :---------: | ----
    设置        | `setLevel(level)`, `set_name(name)`, `get_name()`
    Formatter   | `setFormatter(fmt)`,
    控制        | `flush()`, `close()`,
    多线程锁    | `createLock()`, `acquire()`, `release()`
    其他        | ...
* 主要属性: `level`, `name`, `formatter`, `lock`
* 子类
    * `StreamHandler`
        * 构造: `StreamHandler(stream=None)`
        * 增加的主要方法: `setStream(stream)`
        * 增加的主要属性: `stream`
    * `FileHandler` (继承自 `StreamHandler`)
        * 构造: `FileHandler(filename, mode='a', encoding=None, delay=False, errors=None)`
        * 增加的主要方法: `setStream(stream)`
        * 增加的主要属性: `stream`, `baseFilename`, `mode`, `encoding`, `delay`, `errors`

### 2.3.6. class: Formatter
* 构造: `Formatter(fmt=None, datefmt=None, style='%', ...)`
    * `fmt`: 常用的选项
        基本格式字符串  | 说明
        :-------------- | :-----------------------
        %(levelno)s     | 打印日志级别的数值
        %(levelname)s   | 打印日志级别的名称
        %(pathname)s    | 打印当前执行程序的路径, 其实就是sys.argv[0]
        %(filename)s    | 打印当前执行程序名
        %(funcName)s    | 打印日志的当前函数
        %(lineno)d      | 打印日志的当前行号
        %(asctime)s     | 打印日志的时间
        %(msecs)d       | 打印日志的时间 - 毫秒部分
        %(thread)d      | 打印线程ID
        %(threadName)s  | 打印线程名称
        %(process)d     | 打印进程ID
        %(processName)s | 打印线程名称
        %(module)s      | 打印模块名称
        %(message)s     | 打印日志信息
    * `datefmt`: 与内建库 `datetime` 的格式一致
* 主要方法: ...
* 主要属性: ...

## 2.4. 函数方法
分类    | 函数                      | 说明
:-----: | :-----------------------: | :---
Logger  | getLogger(..)             | 默认 Logger 是 `<RootLogger root (WARNING)>`
输出    | debug(..)                 | 调试信息 (最低级别) , 级别: 10
^       | info(..)                  | 普通信息, 级别: 20
^       | warning(..)               | 警告信息, 级别: 30
^       | error(..) ≈ exception(..) | 错误信息, 级别: 40
^       | critical(..)              | 严重错误信息 (最高级别) , 级别: 50
^       | log(..)                   | 通用函数
配置    | basicConfig(..)           | logging 系统基本配置, 详见^1^
^       | getLevelName(..)          | 获取级别名称
^       | addLevelName(..)          | 添加级别名称
^       | disable(..)               | 禁用某个级别
^       | shutdown(..)              | 关闭 Logger
其他    | ...

注:
1. basicConfig
    参数     | 说明
    :------: | :---
    filename | 文件名, 如果没有, 默认创建一个 StreamHandler
    filemode | 文件模式
    format   | 格式, 默认格式:  BASIC_FORMAT = '%(levelname)s:%(name)s:%(message)s'
    datefmt  | 时间格式
    style    | 风格
    level    | 级别
    stream   | 输出流
    handlers | 函数

## 2.5. 高级技巧
* 配置方式
    * 显式创建记录器 Logger、处理器 Handler 和格式化器 Formatter, 并进行相关设置
    * 简单方式: 使用 `basicConfig()` 函数直接进行配置
    * 文件方式: 使用 `logging.config.fileConfig()` 函数读取配置文件
    * 字典方式: 使用 `logging.config.dictConfig()` 函数读取配置信息
    * 网络方式: 使用 `logging.config.listen()` 函数进行网络配置
* 其他 handler
    * `logging.handlers.RotatingFileHandler` 当文件达到一定大小之后, 它会自动将当前日志文件改名, 然后创建一个新的同名日志文件继续输出
    * `logging.handlers.TimedRotatingFileHandler`和`RotatingFileHandler`类似, 不过它没有通过判断文件大小来决定何时重新创建日志文件, 而是间隔一定时间就自动创建新的日志文件

--------------------------------------------------------------------------------
# 3. 运行时间测量

## 3.1. 标准库 time
* `time() -> float`: 返回当前时间 (单位: s)
* `time_ns() -> int`: 返回当前时间 (单位: ns)
* 其他函数
    * `monotonic() -> float`: 返回时间, 单位: s, 时间起点不确定, 仅用于计算时间差
    * `perf_counter() -> float`: 返回时间, 单位: s, 时间精度最高
    * `process_time() -> float`: 返回时间, 单位: s, CPU 运行的时间, 不包含睡眠的时间
    * `xxx_ns() -> int`: 返回时间, 单位: ns

## 3.2. 标准库 timeit
* `timeit(stmt="pass", setup="pass", timer=default_timer, number=default_number, globals=None)`: 用 timeit 方法统计
* `repeat(stmt="pass", setup="pass", timer=default_timer, repeat=default_repeat, number=default_number, globals=None)`: 重复 n 次

## 3.3. 使用解释器
* Python: `python -m timeit [-n N] [-r N] [-u U] [-s S] [-h] 表达式`
* iPython终端中:
    * `%time 表达式`
    * `%timeit 表达式`

--------------------------------------------------------------------------------
# 4. Profile

## 4.1. 标准库 cProfile, profile
* `cProfile` 是 C  语言实现的 `profile`, 性能更好, 推荐使用
* 使用方法:
    * 代码: `cProfile/profile.run('表达式', filename=None, sort=-1)`
    * 终端:
        * python: `python -m profile 文件路径`
        * iPytyhon: `%prun 文件路径`
* 可以使用 `pstats.Stats` 进行统计
    1. `python -m cProfile -o 统计文件.stats 文件路径`
    1. `pstats.Stats`

## 4.2. 第三方库 line_profiler
* 步骤
    1. 在代码中用 `@profile` 装饰被测函数
    1. 命令行运行: `kernprof -l -v 文件路径`
    1. 查看结果: `python -m line_profiler 结果.lprof`

--------------------------------------------------------------------------------
# 5. numba
> 参见 [官方文档](http://numba.pydata.org/numba-doc/latest/index.html)

## 5.1. wrapper
`@jit`, `@njit` (等效于 `@jit(nopython=True)`): 加速函数
`@vectorize`, `@guvectorize`: 生成 numpy ufunc
`@stencil`: 生成模板函数
`@jitclass`: 加速 class, 尚有问题
`@cfunc`
`@overload`

## 5.2. @jit
* 会自动适配函数的数据类型
* 也可以规定函数参数和返回值类型, `@jit(返回值类型(参数1类型, 参数2类型, ...))`
    * 数据类型:
        * `void`: None
        * `intp`, `uintp`: 指针
        * `intc`, `uintc`: C语言中的int, unsigned int
        * `int8`, `uint8`, `int16`, `uint16`, `int32`, `uint32`, `int64`, `uint64`
        * `float32`, `float64`
        * `complex64`, `complex128`: 复数, real/imag: `float32`/`float64`
        * 数组, 如`float32`[:], `int8`[:,:]
* 模式:
    * `nopython 模式`: 设置选项 `nopython = True`, 更快的速度, 但可能失败
    * `object 模式`: nopython模式失败后退回该模式
* 选项:
    * `nopython`, `nogil`, `cache`, `parallel`, `fastmath`

--------------------------------------------------------------------------------
# 6. cython




--------------------------------------------------------------------------------
# 7. 反汇编

## 7.1. 标准库 dis
```Python
import dis
dis.dis(函数名)
```

--------------------------------------------------------------------------------
# 8. 运行环境

## 8.1. Virtualenv
> 建议使用 Virtualenvwrapper 进行管理
* 安装
    ```Python
    pip install virtualenv
    ```
* 创建运行环境
    ```Shell
    # 在全局目录或项目目录中
    virtualenv 虚拟环境名称
    #如果不想使用系统的包, 加上–no-site-packeages 参数
    virtualenv --no-site-packages 虚拟环境名称
    ```
* 激活环境
    ```Shell
    cd 虚拟环境名称
    .\Scripts\activate.bat
    ```
* 使用环境
    ```Python
    pip install xxx
    ```
* 退出环境
    ```Shell
    .\Scripts\deactivate.bat
    ```

## 8.2. Virtualenvwrapper
* Virtaulenvwrapper是virtualenv的扩展包, 用于更方便管理虚拟环境, 它可以做:
    - 将所有虚拟环境整合在一个目录下
    - 管理 (新增, 删除, 复制) 虚拟环境
    - 快速切换虚拟环境
* 安装
    ```Shell
    pip install virtualenvwrapper-win
    ```
* 创建虚拟环境
    ```Shell
    mkvirtualenv 虚拟环境名称
    ```
* 激活环境
    ```Shell
    # 列出虚拟环境列表
    workon
    # 切换环境
    workon 虚拟环境名称
    ```
* 退出环境
    ```Shell
    deactivate
    ```
* 删除环境
    ```Shell
    rmvirtualenv 虚拟环境名称
    ```
* 激活虚拟环境 -> 执行命令 -> 退出虚拟环境
    ```bash
    workon 虚拟环境名称 && 要执行的命令 && deactivate
    ```
* 其他有用指令
    ```Shell
    pip freeze # 查看当前安装库版本
    # 创建 requirements.txt 文件，其中包含了当前环境中所有包及各自的版本的简单列表
    pip freeze > requirements.txt
    # 保持部署相同，一键安装所有包
    pip install -r requirements.txt
    lsvirtualenv    # 列举所有的环境
    cdvirtualenv    # 导航到当前激活的虚拟环境的目录中，相当于pushd 目录
    cdsitepackages  # 和上面的类似，直接进入到 site-packages 目录
    lssitepackages  # 显示 site-packages 目录中的内容
    ```

--------------------------------------------------------------------------------
# 9. 生成可执行文件

## 9.1. PyInstaller
* 安装
    ```Shell
    # 建议在所需的虚拟环境中安装
    pip install pyinstaller
    ```
* 生成单个 exe 文件
    ```Shell
    pyinstaller -F xxx.py   # 生成单个文件
    pyinstaller -Fw xxx.py  # 生成单个文件, 且不使用 console
    ```

