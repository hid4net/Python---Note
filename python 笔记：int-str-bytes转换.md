
<h1 style="text-align:center">int-str-bytes 转换</h1>

--------------------------------------------------------------------------------
[返回 Outline](outline.md)

<!-- @import "[TOC]" {cmd="toc" depthFrom=1 depthTo=6 orderedList=false} -->

<!-- code_chunk_output -->

- [1. 概览](#1-概览)
  - [1.1. 基本转换](#11-基本转换)
  - [1.2. 批量转换](#12-批量转换)
  - [1.3. 示例](#13-示例)
- [2. 内建类: bytes, bytearray, memoryview](#2-内建类-bytes-bytearray-memoryview)
  - [2.1. 基本特征](#21-基本特征)
  - [2.2. 创建](#22-创建)
  - [2.3. 转换](#23-转换)
  - [2.4. bytes](#24-bytes)
  - [2.5. bytearray](#25-bytearray)
  - [2.6. memoryview](#26-memoryview)
- [3. 标准库 struct](#3-标准库-struct)
  - [3.1. 基本流程](#31-基本流程)
  - [3.2. 转换格式](#32-转换格式)
  - [3.3. struct类](#33-struct类)
  - [3.4. 函数](#34-函数)

<!-- /code_chunk_output -->

----------------------------------------------------------------
tips:
1. 使用 **[bytes](#23-bytes)**, **[bytearray](#24-bytearray)** 与基本数据类型 (**int**, **bool**, **string**, **tuple**, **list**, **set**) 实现转换
1. 使用 **[标准库 struct](#3-标准库-struct)** 中的函数或Struct类转换

--------------------------------------------------------------------------------
# 1. 概览

## 1.1. 基本转换

| From  |  to   | 方法                    | 注意                          |
| :---: | :---: | ----------------------- | ----------------------------- |
|  int  |  str  | f-string                | -                             |
|   ^   |   ^   | hex()                   | -                             |
|  str  |  int  | int(十进制字符串)       | base 默认为 10                |
|   ^   |   ^   | int(十六进制字符串, 16) | 0x+十六进制字符串             |
|  int  | bytes | *int_对象*.to_bytes(..) | 注意大小端: 'big' or 'little' |
| bytes |  int  | int.from_bytes(..)      | ^                             |
|  str  | bytes | bytes(..)               | 注意编码, 如 'utf-8'          |
|   ^   |   ^   | *str_对象*.encode(..)   | ^                             |
|   ^   |   ^   | bytes.fromhex(hex_str)  | 必须为偶数个十六进制字符      |
| bytes |  str  | str(..)                 | 格式化字符串, 没有转换        |
|   ^   |   ^   | *bytes_对象*.decode(..) | 注意编码, 如 'utf-8'          |
|   ^   |   ^   | *bytes_对象*.hex()      | 必须为偶数个十六进制字符      |

## 1.2. 批量转换
使用 **[标准库 struct](#3-标准库-struct)** 库进行转换:
1. 设置 format 字符串
    * 直接使用转换函数
    * 或用 **struct**(format) 构造一个对象
1. 转换
    * to bytes: **pack**, **pack_into**
    * to 数据: **unpack**, **unpack_from**, **iter_unpack**

## 1.3. 示例
``` python {.line-numbers}
# int -> str
f"{919:2x}" # '397'
hex(919)    # '0x397'
# str -> int
int("919")      # 919
int("919", 10)  # 919
int("919", 16)  # 2329 = 0x919
# int -> bytes
int.to_bytes(919, 4, "big")     # b'\x00\x00\x03\x97'
int.to_bytes(919, 4, "little")  # b'\x97\x03\x00\x00'
# bytes -> int
int.from_bytes(b"\x03\x97", "big")      # 919
int.from_bytes(b"\x97\x03", "little")   # 919
int.from_bytes(b"0919", "big")          # 809054521
int.from_bytes(b"0919", "little")       # 959527216
# str -> bytes
bytes("919", "utf-8")   # b'919'
"919".encode("utf-8")   # b'919'
bytes.fromhex("0919")   # b'\t\x19'  # 必须是偶数个数字
# bytes -> str
str(b"919")         # "b'919'"
str(b"\x03\x97")    # "b'\\x03\\x97'"
b"919".decode()     # '919'
b"\xe6\x88\x91".decode()    # '我'
b"919".hex()        # '393139'
b"\x03\x97".hex()   # '0397'
```

``` python {.line-numbers}
import struct

a = 20
bt = a.to_bytes(4, "big")  # b'\x00\x00\x00\n'

[struct.unpack(i, bt) for i in ("i", "@i", "=i", "<i", ">i", "!i")]
# [(335544320,), (335544320,), (335544320,), (335544320,), (20,), (20,)]
[struct.pack(i, 0x01020304) for i in ("i", "@i", "=i", "<i", ">i", "!i")]
# [b'\x04\x03\x02\x01',
# b'\x04\x03\x02\x01',
# b'\x04\x03\x02\x01',
# b'\x04\x03\x02\x01',
# b'\x01\x02\x03\x04',
# b'\x01\x02\x03\x04']

record = b"WangXH \x07\xc1\x12"
name, birth, age = struct.unpack(">7sHb", record)
name, birth, age  # (b'WangXH ', 1985, 18)

struct.pack("ci", b"*", 0x12131415)  # b'*\x00\x00\x00\x12\x13\x14\x15'
struct.pack("ic", 0x12131415, b"*")  # b'\x12\x13\x14\x15*'
struct.calcsize("ci")  # 8
struct.calcsize("ic")  # 5
```

--------------------------------------------------------------------------------
# 2. 内建类: bytes, bytearray, memoryview

## 2.1. 基本特征
* 都用来处理byte数组
* bytes, memoryview 不能更改
* bytearray 可以改变
* memoryview 在索引时不创建 copy, 效率更高
* bytearray 被 memoryview 索引后不可改;  **del \<memoryview object\>** 后可以修改

## 2.2. 创建
* 直接声明 bytes 类型: `b'字符串'` 或 `rb'字符串'`
* 使用构造函数创建
    * binType = **bytes/bytearray/memoryview** (iterable_of_ints)
    * binType = **bytes/bytearray/memoryview** (iterastring, encoding[, errors]ble_of_ints)
    * binType = **bytes/bytearray/memoryview** (bytes_or_buffer)
    * binType = **bytes/bytearray.fromhex**(hex string)

## 2.3. 转换
* bytes (..)
    * vs int: ...
    * vs str: ...
    * vs tuple, list, set
        * **tuple**/**list**/**set**(bytes对象)
* bytearray (..)
    * int, str 先转为 bytes, 再转为 bytearray
    * bytearray 可直接转为 int, str

* memoryview (..)
    * int, str 先转为 bytes, 再转为 memoryview
    * **\<memoryview object\>.tolist**() -> list

## 2.4. bytes
* 构造函数
    * **bytes**(iterable_of_ints) -> bytes
    * **bytes**(string, encoding[, errors]) -> bytes
    * **bytes**(bytes_or_buffer) -> immutable copy of bytes_or_buffer
    * **bytes**(int) -> 创建指定数量的空 bytes
    * **bytes**() -> 空 bytes
* 主要方法
    | 分类       | 方法                                       | 说明                                             |
    | :--------- | ------------------------------------------ | ------------------------------------------------ |
    | 转换       | decode(encoding='utf-8', errors='strict')  | 转为字符串                                       |
    | ^          | hex() -> string                            | bytes 转 hex 字符                                |
    | ^          | **bytes**.fromhex(string)                  | hex 字符转为 bytes                               |
    | 格式化     | upper() -> copy of B                       | 大写                                             |
    | ^          | capitalize() -> copy of B                  | 首字母大写                                       |
    | ^          | title() -> copy of B                       | 标题格式文本                                     |
    | ^          | lower() -> copy of B                       | 小写                                             |
    | ^          | swapcase() -> copy of B                    | 交换大小写                                       |
    | ^          | ljust(width[, fillchar]) -> copy of B      | 左对齐                                           |
    | ^          | center(width[, fillchar]) -> copy of B     | 居中                                             |
    | ^          | rjust(width[, fillchar]) -> copy of B      | 右对齐                                           |
    | ^          | zfill(width) -> copy of B                  | 左侧填充0                                        |
    | ^          | strip(bytes=None)                          | 两侧裁剪                                         |
    | ^          | lstrip(bytes=None)                         | 左侧裁剪                                         |
    | ^          | rstrip(bytes=None)                         | 右侧裁剪                                         |
    | ^          | expandtabs(tabsize=8) -> copy of B         | 扩展 tab 宽度                                    |
    | 查找       | count(sub[, start[, end]]) -> int          | 统计个数                                         |
    | ^          | find(sub[, start[, end]]) -> int           | 查找                                             |
    | ^          | rfind(sub[, start[, end]]) -> int          | 从右侧开始查找                                   |
    | ^          | index(sub[, start[, end]]) -> int          | 索引, 和 find() 类似, 只是失败会报ValueError异常 |
    | ^          | rindex(sub[, start[, end]]) -> int         | 从右侧开始索引                                   |
    | 替换       | replace(old, new, count=-1)                | 替换                                             |
    | 合并与拆分 | join(iterable_of_bytes)                    | 合并                                             |
    | ^          | partition(sep)                             | 按 sep 分成3段                                   |
    | ^          | rpartition(sep)                            | 从右侧分割                                       |
    | ^          | split(sep=None, maxsplit=-1)               | 按 sep 分割成n段 (不包含sep)                     |
    | ^          | rsplit(sep=None, maxsplit=-1)              | 从右侧分割                                       |
    | ^          | splitlines(keepends=False)                 | 按行分割                                         |
    | 判断       | isalnum() -> bool                          | 是否为字母或数字                                 |
    | ^          | isalpha() -> bool                          | 是否为字母                                       |
    | ^          | isdigit() -> bool                          | 是否为数字                                       |
    | ^          | isascii() -> bool                          | 是否为 ASCII 字符                                |
    | ^          | isupper() -> bool                          | 是否为大写                                       |
    | ^          | islower() -> bool                          | 是否为小写                                       |
    | ^          | istitle() -> bool                          | 是否为标题格式字符                               |
    | ^          | isspace() -> bool                          | 是否为空白                                       |
    | ^          | startswith(prefix[, start[, end]]) -> bool | 是否以xx开始                                     |
    | ^          | endswith(suffix[, start[, end]]) -> bool   | 是否以xx结尾                                     |

## 2.5. bytearray
*构造函数
    * **bytesarray**(iterable_of_ints) -> bytes
    * **bytesarray**(string, encoding[, errors]) -> bytes
    * **bytesarray**(bytes_or_buffer) -> immutable copy of bytes_or_buffer
    * **bytesarray**(int) -> 创建指定数量的空 bytes
    * **bytesarray**() -> 空 bytes
* 主要方法
    | 分类       | 方法                                       | 说明                                             |
    | :--------- | ------------------------------------------ | ------------------------------------------------ |
    | 修改       | append(item)                               | 追加                                             |
    | ^          | extend(iterable_of_ints)                   | 扩展                                             |
    | ^          | insert(index, item)                        | 插入                                             |
    | ^          | pop(index=-1)                              | 删除                                             |
    | ^          | remove(value)                              | 删除第一个出现的                                 |
    | ^          | clear()                                    | 清空                                             |
    | ^          | reverse()                                  | 翻转                                             |
    | 转换       | decode(encoding='utf-8', errors='strict')  | 转为字符串                                       |
    | ^          | hex() -> string                            | bytes 转 hex 字符                                |
    | ^          | **bytearray**.fromhex(string)              | hex 字符转为 bytes                               |
    | 格式化     | upper() -> copy of B                       | 大写                                             |
    | ^          | capitalize() -> copy of B                  | 首字母大写                                       |
    | ^          | title() -> copy of B                       | 标题格式文本                                     |
    | ^          | lower() -> copy of B                       | 小写                                             |
    | ^          | swapcase() -> copy of B                    | 交换大小写                                       |
    | ^          | ljust(width[, fillchar]) -> copy of B      | 左对齐                                           |
    | ^          | center(width[, fillchar]) -> copy of B     | 居中                                             |
    | ^          | rjust(width[, fillchar]) -> copy of B      | 右对齐                                           |
    | ^          | zfill(width) -> copy of B                  | 左侧填充0                                        |
    | ^          | strip(bytes=None)                          | 两侧裁剪                                         |
    | ^          | lstrip(bytes=None)                         | 左侧裁剪                                         |
    | ^          | rstrip(bytes=None)                         | 右侧裁剪                                         |
    | ^          | expandtabs(tabsize=8) -> copy of B         | 扩展 tab 宽度                                    |
    | 查找       | count(sub[, start[, end]]) -> int          | 统计个数                                         |
    | ^          | find(sub[, start[, end]]) -> int           | 查找                                             |
    | ^          | rfind(sub[, start[, end]]) -> int          | 从右侧开始查找                                   |
    | ^          | index(sub[, start[, end]]) -> int          | 索引, 和 find() 类似, 只是失败会报ValueError异常 |
    | ^          | rindex(sub[, start[, end]]) -> int         | 从右侧开始索引                                   |
    | 替换       | replace(old, new, count=-1)                | 替换                                             |
    | 合并与拆分 | join(iterable_of_bytes)                    | 合并                                             |
    | ^          | partition(sep)                             | 按 sep 分成3段                                   |
    | ^          | rpartition(sep)                            | 从右侧分割                                       |
    | ^          | split(sep=None, maxsplit=-1)               | 按 sep 分割成n段 (不包含sep)                     |
    | ^          | rsplit(sep=None, maxsplit=-1)              | 从右侧分割                                       |
    | ^          | splitlines(keepends=False)                 | 按行分割                                         |
    | 判断       | isalnum() -> bool                          | 是否为字母或数字                                 |
    | ^          | isalpha() -> bool                          | 是否为字母                                       |
    | ^          | isdigit() -> bool                          | 是否为数字                                       |
    | ^          | isascii() -> bool                          | 是否为 ASCII 字符                                |
    | ^          | isupper() -> bool                          | 是否为大写                                       |
    | ^          | islower() -> bool                          | 是否为小写                                       |
    | ^          | istitle() -> bool                          | 是否为标题格式字符                               |
    | ^          | isspace() -> bool                          | 是否为空白                                       |
    | ^          | startswith(prefix[, start[, end]]) -> bool | 是否以xx开始                                     |
    | ^          | endswith(suffix[, start[, end]]) -> bool   | 是否以xx结尾                                     |
    | 副本       | copy()                                     | 副本                                             |

## 2.6. memoryview
* 构造函数
    * **memoryview**(bytes-like object) -> new memoryview object
        * bytes-like object: int, str, tuple, list, set, dict 都不行
* 主要方法
    | 分类 | 方法                   | 说明                                       |
    | :--- | ---------------------- | ------------------------------------------ |
    | 转换 | cast(format, *, shape) | Cast a memoryview to a new format or shape |
    | ^    | hex()                  | 转为 hex 字符串                            |
    | ^    | tobytes()              | 转为 bytes                                 |
    | ^    | tolist()               | 转为 list                                  |
    | ^    | release()              | 释放空间                                   |
* 成员变量
    | 变量         | 说明                                                                                                     |
    | :----------- | -------------------------------------------------------------------------------------------------------- |
    | c_contiguous | 内存是否 C contiguous                                                                                    |
    | contiguous   | 内存是否 contiguous                                                                                      |
    | f_contiguous | 内存是否 Fortran contiguous                                                                              |
    | format       | A string containing the format (in struct module style) for each element in the view                     |
    | itemsize     | 每个元素是几个字节                                                                                       |
    | nbytes       | The amount of space in bytes that the array would use in a contiguous representation                     |
    | ndim         | An integer indicating how many dimensions of a multi-dimensional array the memory represents             |
    | obj          | The underlying object of the memoryview                                                                  |
    | readonly     | A bool indicating whether the memory is read only                                                        |
    | shape        | A tuple of ndim integers giving the shape of the memory as an N-dimensional array                        |
    | strides      | A tuple of ndim integers giving the size in bytes to access each element for each dimension of the array |
    | suboffsets   | A tuple of integers used internally for PIL-style arrays                                                 |

--------------------------------------------------------------------------------
# 3. 标准库 struct
按 format 字符串将 bytes 和数据互换

## 3.1. 基本流程
1. 设置 format 字符串
    * 直接在函数中使用
    * 或用 **struct**(format) 构造一个对象
1. 转换
    * 转为 bytes: **pack**, **pack_into**
    * 转为数据: **unpack**, **unpack_from**, **iter_unpack**

## 3.2. 转换格式
* format
    | Format | C Type                     |    Python Type    | Standard size |
    | ------ | -------------------------- | :---------------: | :-----------: |
    | ?      | _Bool                      |       bool        |       1       |
    | b\|B   | (signed \| unsigned) char  |      integer      |       1       |
    | h\|H   | (signed \| unsigned) short |         ^         |       2       |
    | i\|I   | (signed \| unsigned) int   |         ^         |       4       |
    | l\|L   | (signed \| unsigned) int   |         ^         |       4       |
    | q\|Q   | (signed \| unsigned) long  |         ^         |       8       |
    | n\|N   | ssize_t\|size_t            |         ^         |       x       |
    | e      | x (IEEE 754 16为浮点数)    |       float       |       2       |
    | f      | float                      |         ^         |       4       |
    | d      | double                     |         ^         |       8       |
    | c      | char                       | bytes of length 1 |       1       |
    | s      | char[]                     |       bytes       |       x       |
    | p      | char[]                     |         ^         |       x       |
    | P      | void *                     |      integer      |       x       |
    | x      | pad byte                   |     no value      |       x       |
* 注意:
    * `n|N` 仅支持 native size
    * `p` 仅支持 native byte ordering
    * 空格被忽略
* 字节顺序
    | 字符  | Byte order             | Size     | alignment |
    | :---: | ---------------------- | -------- | :-------: |
    |  "@"  | native                 | native   |  native   |
    |  "="  | native                 | standard |   none    |
    |  "<"  | little-endian          | standard |   none    |
    |  ">"  | big-endian             | standard |   none    |
    |  "!"  | network (= big-endian) | standard |   none    |

## 3.3. struct类
* 构造函数
    * **Struct**(format): 创建 format
* 主要方法
    | 分类          | 方法                                   | 说明                          |
    | ------------- | -------------------------------------- | ----------------------------- |
    | bytes -> 数据 | pack(v1, v2, ...)                      | 打包为 bytes                  |
    | ^             | pack_into(buffer, offset, v1, v2, ...) | 打包为 bytes, offset 必须设置 |
    | 数据 -> bytes | unpack(buffer)                         | 转为数据, 返回 tuple 类型     |
    | ^             | unpack_from(buffer, offset=0)(buffer)  | ^                             |
    | ^             | iter_unpack(buffer)                    | 迭代器, 转换                  |

## 3.4. 函数
| 分类          | 方法                                           | 说明                          |
| ------------- | ---------------------------------------------- | ----------------------------- |
| bytes -> 数据 | pack(format, v1, v2, ...)                      | 打包为 bytes                  |
| ^             | pack_into(format, buffer, offset, v1, v2, ...) | 打包为 bytes, offset 必须设置 |
| 数据 -> bytes | unpack(format, buffer)                         | 转为数据, 返回 tuple 类型     |
| ^             | unpack_from(format, buffer, offset=0)(buffer)  | ^                             |
| ^             | iter_unpack(format, buffer)                    | 迭代器, 转换                  |
| 信息          | calcsize(format)                               | 计算字节数                    |

