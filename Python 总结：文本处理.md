
**Python 总结: 文本处理**
--------------------------------------------------------------------------------
[返回目录](outline.md)

--------------------------------------------------------------------------------
tips:

--------------------------------------------------------------------------------

<!-- @import "[TOC]" {cmd="toc" depthFrom=1 depthTo=6 orderedList=false} -->

<!-- code_chunk_output -->

- [1. 内建字符串处理](#1-内建字符串处理)
  - [1.1. 转义符: `\`](#11-转义符)
  - [1.2. f-string](#12-f-string)
  - [1.3. str 类提供的方法](#13-str-类提供的方法)
- [2. 正则表达式 (标准库 re)](#2-正则表达式-标准库-re)
  - [2.1. 支持的正则表达式](#21-支持的正则表达式)
  - [2.2. 使用方法1: 函数](#22-使用方法1-函数)
  - [2.3. 使用方法2: 面向对象](#23-使用方法2-面向对象)
    - [2.3.1. pattern对象](#231-pattern对象)
    - [2.3.2. match对象](#232-match对象)

<!-- /code_chunk_output -->

--------------------------------------------------------------------------------
# 1. 内建字符串处理

## 1.1. 转义符: `\`
转义字符  | 描述
:-------: | --------------------------------
`\`(行尾) | 续行符
`\\`      | 反斜杠符号
`\'`      | 单引号
`\"`      | 双引号
`\a`      | 响铃
`\b`      | 退格(Backspace)
`\e`      | 转义
`\000`    | 空
`\n`      | 换行
`\v`      | 纵向制表符
`\t`      | 横向制表符
`\r`      | 回车
`\f`      | 换页
`\oyy`    | 八进制数, yy代表的字符, 例如: \o12代表换行
`\xyy`    | 十六进制数, yy代表的字符, 例如: \x0a代表换行
`\other`  | 其它的字符以普通格式输出

## 1.2. f-string
* 使用前缀`f|F`, 格式: `f"xxx {变量} xxx {变量[=][:格式描述符]} ..."`
* `{}` 表示被替换字段, 可以是变量、表达式、lambda函数、函数
* 变量后加`=`, 会输出 `"变量=变量的值"` 字符串, 否则输出 `"变量的值"` 字符串
* `{{xxx}}`表示 `"{xxx}"`
* 灵活交替使用`'`, `"`, `'''`, `"""`
* 支持多行
* 格式描述符:
    分类     | 格式描述符 | 说明
    :------: | :--------: | ---------------------------------------------
    对齐     | "<"        | 左对齐
    ^        | ">"        | 右对齐
    ^        | "^"        | 居中
    符号     | "+"        | 负数前加负号 (-), 正数前加正号 (+)
    ^        | "-"        | 负数前加负号 (-), 正数前不加符号 (默认)
    ^        | " "(空格)  | 负数前加负号 (-), 正数前加一个空格
    进制     | "#"        | 数字前加 0b, 0o, 0x
    宽度     | <宽度>     | 指定宽度
    ^        | 0+<宽度>   | 指定宽度, 并以0补全, 不可用于复数
    ^        | <宽度>.<精度>+后缀 | 不可用于整数, <br/>后缀可以为`f|F`,`e|E`, `g|G`,`%`,`s`, <br/>其中`s`表示仅使用前<精度>个字符
    千分位   | ","        | 使用逗号作为千位分隔符
    ^        | "_"        | 使用下划线作为千位分隔符
    格式类型 | s          | 普通字符串
    ^        | c          | 字符格式, 按unicode编码将整数转换为对应字符
    ^        | b          | 二进制整数
    ^        | o          | 八进制整数
    ^        | d          | 十进制整数
    ^        | x/X        | 十六进制整数 (小写\|大写)
    ^        | f          | 定点数, 默认精度是6
    ^        | F          | 与 f 等价, 但将 nan 和 inf 换成 NAN 和 INF
    ^        | e/E        | 科学计数
    ^        | g/G        | 通用格式, 小数用 f\|F, 大数用 e\|E
    ^        | %          | 百分比, 自动计算百分比, 并加 `%` 后缀
* 示例
    ``` python {.line-numbers}
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

## 1.3. str 类提供的方法
分类   | 方法                                       | 说明
:----: | :----------------------------------------- | :---------------------
转换   | encode(encoding='utf-8', errors='strict')  | 转为 bytes
格式化 | format(*args, **kwargs)                    | 格式化
^      | format_map(mapping)                        | ^
大小写 | upper()                                    | 大写
^      | capitalize()                               | 首字母大写
^      | title()                                    | 标题格式文本
^      | lower()                                    | 小写 (非ASCII无效)
^      | casefold()                                 | 小写
^      | swapcase()                                 | 交换大小写
对齐   | ljust / rjust(width[, fillchar])           | 左/右对齐
^      | center(width[, fillchar])                  | 居中
填充   | zfill(width)                               | 左侧填充0
剪裁   | strip(bytes=None)                          | 两侧裁剪
^      | lstrip / rstrip(bytes=None)                | 左/右侧裁剪
^      | removeprefix / removesuffix(前缀或后缀)    | 删除前缀或后缀
查找   | count(sub[, start[, end]])                 | 统计个数
^      | find / rfind(sub[, start[, end]])          | 从左/右侧开始查找
^      | index / rindex(sub[, start[, end]])        | 从左/右侧开始索引, 和 find() 类似, 只是败会报ValueError异常
替换   | replace(old, new, count=-1)                | 替换
^      | translate(table,delete=b'')                | 查表替换
^      | maketrans(x, y=None, z=None)               | 制作转换表
^      | expandtabs(tabsize=8)                      | tab 转 空白
合并   | join(iterable_of_bytes)                    | 合并
拆分   | partition / rpartition(sep)                | 从左/右侧开始按 sep 分成3段
^      | split / rsplit(sep=None, maxsplit=-1)      | 从左/右侧开始按 sep 分割成n段 (不包含sep)
^      | splitlines(keepends=False)                 | 按行分割
信息   | isalnum()                                  | 是否为字母或数字, Unicode的字/数也为True
^      | isalpha()                                  | 是否为字母, Unicode的字也为True
^      | isascii()                                  | 是否为 ASCII 字符, Unicode的字为 False
^      | isupper()                                  | 是否为大写
^      | islower()                                  | 是否为小写
^      | istitle()                                  | 是否为标题格式字符
^      | isidentifier()                             | 是否为标识符
^      | isdigit()                                  | 是否为数字^1^
^      | isnumeric()                                | 是否为数字^2^
^      | isdecimal()                                | 是否为分数^3^
^      | isspace()                                  | 是否为空白
^      | isprintable()                              | 是否为可打印字符
^      | startswith(prefix[, start[, end]])         | 是否以xx开始
^      | endswith(suffix[, start[, end]])           | 是否以xx结尾

^1^ **digit** 包括 Unicode数字, byte数字 (单字节), 全角数字 (双字节), 罗马数字, 但不包括汉数字
^2^ **numeric** 包括 Unicode数字, 全角数字 (双字节), 罗马数字, 汉字数字, 但不包括 byte数字 (字节)
^3^ **decimal** 包括 Unicode数字, 全角数字 (双字节), 但不包括罗马数字, 汉字数字, byte数字 (字节)

--------------------------------------------------------------------------------
# 2. 正则表达式 (标准库 re)
> 对于大字符串, 建议使用 Pattern 对象进行处理, 因为可以选择处理位置

## 2.1. 支持的正则表达式
表达式                | 说明
:-------------------- | :------------------------------------------------------------
`.`                   | 任意字符, 默认不包括`\n`, 如果开启`DOTALL`标志, 包括`\n`
'`^`                  | 行首
`$`                   | 行尾
`*`                   | 重复0次或多次
`+`                   | 重复1次或多次
`?`                   | 重复0次或1次
`*?, +?, ??`          | 贪婪模式
`{m}`                 | 重复m次
`{m,n}`               | 重复m~n次
`{m,n}?`              | 重复m~n次, 贪婪模式
`\`                   | 转义符
`[]`                  | 字符集
`|`                   | 或
`(...)`               | 匹配并捕获到自动命名的组里
`(?...)`              | 匹配并捕获到自动命名的组里, 扩展语法, `?`后的第一个字符表示进一步语法
`(?aiLmsux)`          | 匹配空字符串, </br>'a' ~ re.A (ASCII-only matching), </br>'i' ~ re.I (ignore case), </br>'L' ~ re.L (locale dependent), </br>'m' ~ re.M (multi-line), </br>'s' ~ re.S (dot matches all), </br>'u' ~ re.U (Unicode matching) </br>'x' ~ re.X (verbose)
`(?:...)`             | 匹配但不捕获
`(?aiLmsux-imsx:...)` | 匹配但不捕获的扩展语法
`(?P<name>...)`       | 匹配并捕获到指定名称的组里
`(?P=name)`           | 执行正向预测先行搜索的子表达式
`(?#...)`             | 注释
`(?=...)`             | 匹配`...`前面的位置
`(?!...)`             | 匹配后面不是`...`的位置
`(?<=...)`            | 匹配`...`后面的位置
`(?<!...)`            | 匹配前面不是`...`的位置, ==Python 仅支持定宽匹配==
`(?(id/name)yes-pattern|no-pattern)` | ..
`\number`             | 数字
`\A` / `\Z`           | 字符串开始 / 结尾
`\b` / `\B`           | 字符串边界 / 非字符串边界
`\d` / `\D`           | 数字 / 非数字, 等效于`[0-9]`/`[^0-9]`
`\s` / `\S`           | 空白 / 非空白, 等效于 `[ \t\n\r\f\v]`/`[^ \t\n\r\f\v]`
`\w` / `\W`           | 字符 / 非字符, 等效于`[a-zA-Z0-9_]`/`[^a-zA-Z0-9_]`
`\u` / `\U`           | unicode字符 / 非unicode字符

## 2.2. 使用方法1: 函数
分类        | 方法                                                  | 说明
:---------: | :---------------------------------------------------- | :-----------
pattern 对象| re.**compile**(pattern, flags=0)                      | 创建 pattern 对象
查找        | re.**search**(pattern, string, flags=0)               | 返回第一个成功的匹配
^           | re.**findall**(pattern, string, flags=0)              | 返回一个列表
^           | re.**finditer**(pattern, string, flags=0)             | 返回迭代器
匹配        | re.**match**(pattern, string, flags=0)                | 从字符串起始位开始匹配, 如果起始位置匹配不成功, 返回 None
^           | re.**fullmatch**(pattern, string, flags=0)            | 完全匹配
拆分        | re.**split**(pattern, string, maxsplit=0, flags=0)    | 拆分
替换        | re.**sub**(pattern, repl, string, count=0, flags=0)   | 替换
^           | re.**subn**(pattern, repl, string, count=0, flags=0)  | 替换 n 个
控制        | re.**escape**(pattern)                                | 跳过
^           | re.**purge**()                                        | 清 re 缓存

* 其中, flag包括
    flags           | 说明
    :-------------- | :---
    re.A/ASCII      | 仅启用ASCII模式
    re.DEBUG        | 调试信息
    re.I/IGNORECASE | 忽略大小写
    re.L/LOCALE     | 对当期地区忽略大小写
    re.M/MULTILINE  | 支持多行
    re.S/DOTALL     | `.`包括新行
    re.X/VERBOSE    | 忽略空白和注释

## 2.3. 使用方法2: 面向对象

### 2.3.1. pattern对象
* 由`re.compile(...)`函数创建
* 属性: `flags`, `groups`, `groupindex`, `pattern`

* 方法:
    分类    | 方法                                          | 说明
    :-----: | :-------------------------------------------- | :-----------
    查找    | .search(string[, pos[, endpos]])              | 返回第一个成功的匹配
    ^       | .findall(string[, pos[, endpos]])             | 返回一个列表
    ^       | .finditer(string[, pos[, endpos]])            | 返回迭代器
    匹配    | .match(string[, pos[, endpos]])               | 从字符串起始位开始匹配, 如果起始位置匹配不成功, 返回 None
    ^       | .fullmatch(string[, pos[, endpos]])           | 完全匹配
    拆分    | .split(pattern, string, maxsplit=0, flags=0)  | 拆分
    替换    | .sub(repl, string, count=0)                   | 替换
    ^       | .subn(repl, string, count=0)                  | 替换 n 个

### 2.3.2. match对象
* `.match(...)`, `.saerch(...)`等函数或方法的返回值
* 属性: `pos`, `endpos`, `lastindex`, `lastgroup`, `re`, `regs`, `string`
* 方法:
    方法                        | 说明
    :-------------------------- | :--------
    .expand(template)           | ··
    .\_\_getitem__(g)           | 获取匹配的第n个分组, 如 `<match 对象>[2]`
    .group([group1, ...])       | 获取匹配的字符串 (包括正则的 [捕获组, 一般字符], 不包括非捕获项)
    .groups(default=None)       | 返回所有正则表达式中的子分组
    .groupdict(default=None)    | 获取匹配的分组 (字典形式)
    .start([group])             | 匹配字符串的开始索引
    .end([group])               | 匹配字符串的结束索引
    .span([group])              | (m.start(group), m.end(group))

--------------------------------------------------------------------------------

