
<h1 style="text-align:center">调用外部程序或DLL</h1>

--------------------------------------------------------------------------------
[返回 Outline](outline.md)

<!-- @import "[TOC]" {cmd="toc" depthFrom=1 depthTo=6 orderedList=false} -->

<!-- code_chunk_output -->

- [1. 外部程序](#1-外部程序)
  - [1.1. 标准库 os.system(...)](#11-标准库-ossystem)
  - [1.2. 标准库 subprocess.run(...)](#12-标准库-subprocessrun)
- [2. DLL](#2-dll)
  - [2.1. 标准库 ctypes](#21-标准库-ctypes)
    - [2.1.1. 基础](#211-基础)
    - [2.1.2. 数据类型](#212-数据类型)

<!-- /code_chunk_output -->

--------------------------------------------------------------------------------
# 1. 外部程序

## 1.1. 标准库 os.system(...)
* 以前用的比较多的方法, 实际上调用操作系统的 C 函数 `system(...)`, 命令以字符串的形式传入, 在系统子 `shell` 中执行, 和在真实的 `shell` 执行并无二致
* 优点
    * 可以利用 `shell` 的管道和重定向等特性来实现比较复杂的命令
* 缺点
    * 外部进程的输出无法被 `python` 代码捕获
        * `system` 函数只返回一个 `exit status` (不同的系统环境该状态可能不一样), 此外作为命令传入的字符串必须是合格的命令, 否则会出现意想不到的结果
* 示例
    ```Python
    import os
    os.system("ipconfig > result.txt")
    ```

## 1.2. 标准库 subprocess.run(...)
* `run(*popenargs, input=None, capture_output=False, timeout=None, check=False, **kwargs) -> CompletedProcess_对象`
    * 参数
        * `popenargs`: 要运行的命令
        * `input`: 传递给 `stdin`, 内部自动创建 `stdin=PIPE`, 不能和 `stdin` 参数同时使用
        * `capture_output`: 是否捕获 `stdout` 和 `stderr`
            * 若使用, 内部 `Popen` 对象会自动创建 `stdout=PIPE` 和 `stderr=PIPE`
            * 如果希望合并 `stdout` 和 `stderr`, 需请使用 `stdout=PIPE` 和 `stderr= stdout` 而不是 `capture_output`
            * 注意: 如果设置 `capture_output`, 不能和 `stdout` 和 `stderr` 参数共用
        * `timeout`: 若超时, 将杀子进程, 并触发 `TimeoutExpired` 异常, 单位: `s`
        * `check`: 若为 True, 当子进程以非零值退出时, 将触发 `CalledProcessError` 异常
    * 返回值: `CompletedProcess_对象`
        * 常用方法:
            * `check_returncode()`: 如果退出代码是非零值, 触发 `CalledProcessError` 异常
        * 常用属性
            * `args`: 传给 `run` 函数的参数
            * `returncode`: 退出代码
            * `stdout`: 标准输出流
            * `stderr`: 标准错误流
* 示例
    ``` python
    # 如果不需要捕获 stdout
    subprocess.run("ipconfig")
    subprocess.run(['ipconfig', '/all'])
    # 如果需要捕获 stdout
    rslt = subprocess.run("ipconfig", capture_output=True)
    print(rslt.stdout.decode("gb2312"))
    ```
* 内部原理
    1. 使用 `Popen` 创建一个对象
        * `class subprocess.Popen(args, bufsize=-1, executable=None, stdin=None, stdout=None, stderr=None, preexec_fn=None, close_fds=True, shell=False, cwd=None, env=None, universal_newlines=None, startupinfo=None, creationflags=0, restore_signals=True, start_new_session=False, pass_fds=(), *, user=None, group=None, extra_groups=None, encoding=None, errors=None, text=None, umask=-1, pipesize=-1)`
    1. 调用 `Popen_对象.communicate(...)` 方法
    1. 如果正常, 返回 `stdout` 和 `stderr`
    1. 如果异常, 处理异常并返回
    1. 调用 `Popen_对象.poll()` 方法, 返回程序返回代码
    1. 如果正常, 返回 `CompletedProcess_对象`
    1. 如果异常, 返回 `CalledProcessError` 异常

--------------------------------------------------------------------------------
# 2. DLL

## 2.1. 标准库 ctypes

### 2.1.1. 基础
* 基本流程
    1. 加载 DLL, 创建 *dll_对象*
    1. 调用 *dll_对象* 中的函数
* 示例
    ``` python
    from ctypes import *
    # step 1: 加载 dll
    dll = ctypes.windll.LoadLibrary('./test.dll')
    # 或
    dll = ctypes.WinDll('test.dll')
    # step 2: 调用 dll 中的函数
    dll.myFunc()
    ```
* 加载 DLL
    * 方法 1: 使用 `CDLL/WinDLL/OleDLL(name, mode=DEFAULT_MODE, handle=None, use_errno=False, use_last_error=False, winmode=None)` 创建
        * `WinDLL` 和 `OleDLL` 是 `CDLL` 的派生类
    * 方法 2: 使用 `cdll/windll/oledll` 的 `LoadLibrary(name, mode=DEFAULT_MODE, handle=None, use_errno=False, use_last_error=False, winmode=None)` 方法创建
        * 内置的 *dll_对象*
            * `cdll` 内置的 dll: `msvcrt`
            * `windll` 内置的 dll: `kernel32`, `shell32`
        * 区别
            * `cdll`: 加载 dll 中用标准 C 调用标准 `cdecl` 导出的函数
            * `windll`: 加载 dll 中用 `stdcall` 导出的函数
            * `oledll`: 加载 dll 中用 `stdcall` 导出的函数, 并假定函数返回 `Windows HRESULT` 错误代码 (会自动触发 `OSError` 异常)
* 调用函数
    * 普通函数: 格式: `dll_对象.函数名(...)`
    * 乱码的函数: `getattr(dll_对象, 乱码)`
        * 有些 DLL 中, 函数名在 Python 中无效 (字符编码问题)
    * 无名函数: `dll_对象[序号]`
        * 在 Window 中, 有些 DLL 不保留名称, 只有序号
* 访问 DLL 中的变量
    * 使用 `ctypes_类型.in_dll(dll_对象, 变量名称)` 方法

### 2.1.2. 数据类型
* 参数类型
    * 基本类型
        * 支持的类型
            |        ctypes_类型         |                   C 类型                   |       Python type        |
            | :------------------------: | :----------------------------------------: | :----------------------: |
            |          `c_bool`          |                  `_Bool`                   |           bool           |
            |          `c_char`          |                   `char`                   | 1-character bytes object |
            |         `c_wchar`          |                 `wchar_t`                  |    1-character string    |
            |     `c_byte`/`c_ubyte`     |        (`signed`/`unsigned`)`char`         |           int            |
            |    `c_short`/`c_ushort`    |        (`signed`/`unsigned`)`short`        |            ^             |
            |      `c_int`/`c_uint`      |         (`signed`/`unsigned`)`int`         |            ^             |
            |     `c_long`/`c_ulong`     |        (`signed`/`unsigned`)`long`         |            ^             |
            | `c_longlong`/`c_ulonglong` | (`signed`/`unsigned`)`__int64`/`long long` |            ^             |
            |   `c_size_t`/`c_ssize_t`   |            `size_t` / `ssize_t`            |            ^             |
            |         `c_float`          |                  `float`                   |          float           |
            |         `c_double`         |                  `double`                  |            ^             |
            |       `c_longdouble`       |               `long double`                |            ^             |
            |         `c_char_p`         |            `char *` (`\0`结尾)             |  `bytes` 对象或 `None`   |
            |        `c_wchar_p`         |           `wchar_t *` (`\0`结尾)           |   `str` 对象或 `None`    |
            |         `c_void_p`         |                  `void *`                  |     `int` 或 `None`      |
        * `ctypes` 类型的使用方法
            * 创建: `ctypes_类型(值)`, 如 `c_int(42)`
            * 获取: `ctypes_类型.value`
    * 数组
        * `create_string_buffer(init, size=None)`
        * `create_unicode_buffer(init, size=None)`: 支持 unicode
    * 指针/引用
        * `pointer/byref(对象)` 创建指针/引用
            * 效果一样, `pointer` 功能更多, 速度更快
        * 如果参数是 `create_string_buffer(init, size=None)` 创建的对象, 无需转换, 直接使用
    * 结构体或 union
        * 步骤
            1. 创建 `Structure` 或 `Union` 的派生类
                * 数据: `_fields_= [('结构体成员名', ctypes_类型), ('结构体成员名', ctypes_类型), ...]`, 如
                    ```Python
                    class POINT(Structure):
                        _fields_ = [("x", c_int), ("y", c_int)]
                    ```
                * 对齐: `_pack_ = 对齐字节数`, 其中: 对齐字节数需与 C 代码中的 `#pragma pack(对齐字节数)` 一致
                * 大小端: 从 `BigEndianStructure`/`LittleEndianStructure`, `BigEndianUnion`/`LittleEndianUnion` 派生
                * 位域: `_fields_= [('结构体成员名', ctypes_类型, 位域), ('结构体成员名', ctypes_类型, 位域), ...]`
            1. 将派生类的对象直接作为参数
    * 数组
        * 两种方式:
            * 创建数组对象: `数组对象= ctypes_类型 * 个数` 或 `数组对象= Structure/Union_派生类 * 个数`
            * 直接使用参数
    * 类型转换
    * 不完备的参数
    * 回调函数:
        * `CFUNCTYPE()`, 在 windows 系统中使用 `WINFUNCTYPE()`
* 指定参数类型
    * 形式 `dll_对象_函数对象.argtypes = [ctypes_类型列表]`
* 返回值类型
    * 默认返回类型的是 C 语言的 `int`
    * 可以指定返回类型, 步骤
        1. 指定返回值类型: `dll_对象_函数对象.restype = ctypes_类型`
        1. 调用`返回值 = dll_对象.函数(...)`
* 示例
    ```CPP
    // test.c
    #include <string.h>

    __declspec(dllexport) char* myFunc(char* in_str);

    char* myFunc(char* in_str) {
        strcpy(in_str, "I am str_in");
        char* out_str = "I am str_out";
        return out_str;
    }
    // 生成 DLL: gcc -shared -o test.dll test.c
    ```

    ```Python
    import ctypes

    # 导入 dll
    dll = ctypes.cdll.LoadLibrary("./test.dll")
    # 调用函数
    myFunc = dll.myFunc
    myFunc.argtypes = [ctypes.c_char_p] # 指定参数的类型
    myFunc.restype = ctypes.c_char_p    # 指定返回值的类型
    in_str = ctypes.create_string_buffer(b"1234567890") # 初始化参数
    print(f"传入参数: {in_str.value}")
    # >>> 传入参数: b'1234567890'
    out_str = myFunc(in_str)    # 调用函数
    print(f"调用函数后, 传入参数: {in_str.value}")  # 传入参数被改变
    # >>> 调用函数后, 传入参数: b'I am str_in'
    print(f"返回结果: {out_str}")   # 返回值
    # >>> 返回结果: b'I am str_out'
    ```

--------------------------------------------------------------------------------

