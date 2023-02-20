
**Python 总结: 日期与时间**
--------------------------------------------------------------------------------
[返回目录](outline.md)

--------------------------------------------------------------------------------
tips:
1. 处理日期时间时, 尽量使用 datetime 库 (虽然time也可以处理日期时间)

--------------------------------------------------------------------------------

<!-- @import "[TOC]" {cmd="toc" depthFrom=1 depthTo=6 orderedList=false} -->

<!-- code_chunk_output -->

- [1. 基本示例](#1-基本示例)
- [2. 日期和时间 (标准库: datetime)](#2-日期和时间-标准库-datetime)
  - [2.1. datetime 类](#21-datetime-类)
  - [2.2. timedelta 类](#22-timedelta-类)
- [3. 运行时间 (标准库: time)](#3-运行时间-标准库-time)

<!-- /code_chunk_output -->

--------------------------------------------------------------------------------
# 1. 基本示例
``` python
# 获取日期
from datetime import datetime, timedelta
print(datetime.now().strftime("%Y-%m-%d %H:%M:%S"))
# 获取运行时间
import time
StratTime = time.time()
time.sleep(1) # 或者 do someting
print(f"运行时间: {time.time() - StratTime}")

```

# 2. 日期和时间 (标准库: datetime)
* 包含6个类 `date`, `time`, `datetime`, `timedelta`, `tzinfo`, `timezone`
* 注意导入方式
    ``` python
    # 方式1
    from datetime import datetime, timedelta
    now = datetime.now()
    # 方式2
    import datetime
    now = datetime.datetime.now()
    ```

## 2.1. datetime 类
是 date 类和 time 类的组合

* 属性: `year`, `month`, `day`,`hour`, `minute`, `second`, `microsecond`, `tzinfo`, `fold`, `max`, `min`, `resolution`

* 方法:
    分类   | 方法                         | 说明
    :----: | :--------------------------- | :-----------------------
    获取   | now()                        | 当前日期时间, datetime
    ^      | today()                      | ^
    ^      | time()                       | ^
    ^      | timestamp()                  | 当前时间, 从元年开始的秒数
    格式化 | strftime()                   | datetime -> string
    ^      | strptime()                   | string -> datetime
    string | ctime(...)                   | 普通格式
    ^      | isoformat(...)               | ISO格式
    创建   | datetime(year, moth, day, *) | 按年月日时分秒创建
    ^      | date(year, moth, day)        | 按年月日创建
    其他   | 包含时区, 其他格式等

* 时间格式
    格式 | 说明
    :--: | :---------------------------------------
    %Y   | 年, 四位数
    %y   | 年, 两位数
    %m   | 月, 两位, 01, 02, …, 12
    %b   | 月, 缩写, Jan, Feb, …, Dec
    %B   | 月, 全称, January, February, …, December
    %d   | 日, 两位, 01, 02, …, 31
    %w   | 周几,  0, 1, …, 6
    %a   | 周几, 缩写, Sun, Mon, …, Sat
    %A   | 周几, 全称, Sunday, Monday, …, Saturday
    %H   | 时, 24小时制, 两位, 00, 01, …, 23
    %I   | 时, 12小时制, 两位, 01, 02, …, 12
    %p   | AM, PM
    %M   | 分, 两位, 00, 01, …, 59
    %S   | 秒, 两位, 00, 01, …, 59
    %f   | 毫秒, 000000, 000001, …, 999999
    %z   | 时区, ±HHMM[SS[.ffffff]], (empty), +0000, -0400, +1030, +063415, -030712.345216
    %Z   | 时区, 名称, (empty), UTC, EST, CST
    %j   | 一年中的第几天, 三位数, 001, 002, …, 366
    %U   | 周序号, 00, 01, …, 53
    %W   | 周序号, 00, 01, …, 53
    %c   | 全部时间
    %x   | 全部时间
    %X   | 全部时间
    %%   | 百分号

## 2.2. timedelta 类
timedelta对象 = datetime对象 - datetime对象
* 常用属性: `days`,
* 方法: total_seconds()　相差多少秒

--------------------------------------------------------------------------------
# 3. 运行时间 (标准库: time)
* 时间信息包括: 时区、年、月、日、时、分、秒、周几、一年中的第几天、元年开始的秒数、夏令时等信息, 对应`time.struct_time`中的 `tm_zone`, `tm_year`, `tm_mon`, `tm_mday`, `tm_hour`, `tm_min`, `tm_sec`, `tm_wday`, `tm_yday`, `tm_gmtoff`, `tm_isdst`

* 函数
    分类       | 方法                                    | 说明
    :--------: | :-------------------------------------- | :-----------------
    获取时间   | time() -> floating point number         | 从元年开始的秒数
    ^          | time_ns() -> int                        | 从元年开始的 ns 数
    处理器时间 | perf_counter() -> float                 | 秒数
    ^          | perf_counter_ns() -> int                | ns 数
    ^          | monotonic() -> float                    | 其他
    ^          | monotonic_ns() -> int                   | ^
    ^          | process_time() -> float                 | ^
    ^          | process_time_ns() -> int                | ^
    ^          | thread_time() -> float                  | ^
    ^          | thread_time_ns() -> int                 | ^
    ^          | get_clock_info(name: str) -> dict       | 时间格式信息
    延时       | sleep(seconds)                          | 延时
    string     | asctime([tuple]) -> string              | 从元祖
    ^          | ctime(seconds) -> string                | 从秒数
    tuple      | gmtime([seconds]) -> tuple              | UTC
    ^          | localtime([seconds]) -> tuple           | 本地时间
    ^          | mktime(tuple) -> floating point number  | 创建时间
    格式化     | strftime(format[, tuple]) -> string     | tuple -> string
    ^          | strptime(string, format) -> struct_time | string -> tuple

--------------------------------------------------------------------------------

