
<h1 style="text-align:center">文件操作</h1>

--------------------------------------------------------------------------------
[返回目录](outline.md)

tips:

--------------------------------------------------------------------------------

<!-- @import "[TOC]" {cmd="toc" depthFrom=1 depthTo=6 orderedList=false} -->

<!-- code_chunk_output -->

- [1. 路径](#-1-路径-)
  - [1.1. 路径管理](#-11-路径管理-)
  - [1.2. 目录管理](#-12-目录管理-)
  - [1.3. 文件管理](#-13-文件管理-)
  - [1.4. 信息判断](#-14-信息判断-)
  - [1.5. 应用实例](#-15-应用实例-)
    - [1.5.1. pyinstaller 打包 exe 后的路径问题](#-151-pyinstaller-打包-exe-后的路径问题-)
- [2. 普通文件](#-2-普通文件-)
- [3. json](#-3-json-)
- [4. yaml](#-4-yaml-)
- [5. ini](#-5-ini-)
- [6. csv](#-6-csv-)
  - [6.1. 标准库 csv](#-61-标准库-csv-)
  - [6.2. 第三方库 numpy](#-62-第三方库-numpy-)
  - [6.3. 第三方库 pandas](#-63-第三方库-pandas-)
- [7. excel 文件](#-7-excel-文件-)
  - [7.1. 第三方库 openpyxl](#-71-第三方库-openpyxl-)
  - [7.2. 第三方库 xlrd/xlwt/xlutils](#-72-第三方库-xlrdxlwtxlutils-)
  - [7.3. 第三方库 numpy, pandas](#-73-第三方库-numpy-pandas-)
- [8. 自动生产文档](#-8-自动生产文档-)
  - [8.1. 标记语法](#-81-标记语法-)
  - [8.2. API](#-82-api-)

<!-- /code_chunk_output -->

--------------------------------------------------------------------------------
# 1. 路径
* 相关模块
    ```Python
    from pathlib import Path
    import PySimpleGUI as sg
    import os.path
    ```

## 1.1. 路径管理
* 创建路径
    * 直接使用 `pathlib` 中 `Path` 类的构造函数, 如
        ```Python
        from pathlib import Path
        p = Path('C:\Program Files')
        ```
    * 使用 `pathlib` 中 `Path` 对象的方法 `joinpath(*args)` 或 `/` 拼接路径, 如
        ```Python
        from pathlib import Path
        p = Path.cwd() / "temp.txt"                 # WindowsPath('d:/Temp/temp.txt')
        p = Path.home().joinpath("dir2", "tmp.txt") # WindowsPath('C:/Users/xxx/dir2/tmp.txt')
        ```
* 获取路径
    * 选择路径: PySimpleGUI 中的对话框, 如
        ```Python
        import PySimpleGUI as sg

        filename = sg.popup_get_file()      # 返回 str
        foldername = sg.popup_get_folder()  # 返回 str
        ```
    * 获取特定路径: `pathlib` 中 `Path` 的类方法
        ```Python
        from pathlib import Path
        fpath = Path.cwd()  # 获取当前路径
        fpath = Path.home() # 获取 home 路径
        ```
    * 获取路径列表
        * 使用 pathlib 中 `Path_对象.glob(pattern)` 或 `Path_对象.rglob(pattern)`
            ```Python
            p.glob('*.py')      # 遍历本级目录
            p.glob('*/*.py')    # 遍历子目录
            p.glob('**/*.py')   # 遍历本级目录及子目录
            p.rglob('*.py')     # 等效于 p.glob('**/*.py')
            ```
        * 使用 pathlib 中 `Path_对象.iterdir() -> 生成器`, 注意: 仅遍历本级目录
            * 列举子目录或文件: `list(p.iterdir())`
            * 列举子目录:  `[x for x in p.iterdir() if x.is_dir()]`
            * 列举目录下所有文件:  `[x for x in p.iterdir() if x.is_file()]`
* 路径转换
    * 绝对路径: pathlib `Path_对象.absolute()`, 如
        ```Python
        p = Path(".")       # WindowsPath('.')
        p = p.absolute()    # WindowsPath('d:/Temp')
        ```
    * 相对路径: pathlib 中 `Path_对象.relative_to(*other)`
    * posix 路径: pathlib `Path_对象.as_posix()`
    * uri 路径: pathlib `Path_对象.as_uri()`
* 路径属性
    * 根目录: pathlib 中 Path 对象的属性 `anchor` (如: `d:\\`), `drive` (如: `d:`), `root` (如: `\\`)
    * 上级目录: pathlib 中 Path 对象的属性 `parent`, `parents`, `parts` (`tuple(各级目录 + 文件全名)`)
    * 文件名: pathlib 中 Path 对象的属性 `name`(文件名+后缀), `stem`(文件名), `suffix`(文件后缀), `suffixes`(文件后缀列表)
* 更改路径
    * 替换文件全名: pathlib 中 `Path_对象.with_name(name)`
    * 替换文件名: pathlib 中 `Path_对象.with_stem(stem)`
    * 替换文件后缀: pathlib 中 `Path_对象.with_suffix(suffix)`

## 1.2. 目录管理
* 创建
    * pathlib 中 `Path_对象.mkdir(mode=0o777, parents=False, exist_ok=False)`
    * os 模块中的函数 `makedirs(name, mode=511, exist_ok=False)` 创建多级目录
* 删除
    * pathlib 中 `Path_对象.rmdir()`
    * os 模块中的函数 `removedirs(name)` 递归删除目录

## 1.3. 文件管理
* 创建: pathlib 中 `Path_对象.touch(mode=0o666, exist_ok=True)`
* 删除: pathlib 中 `Path_对象.unlink(missing_ok=False)`
* 打开文件:
    * 内建函数 `open(file, mode='r', buffering=-1, encoding=None, errors=None, newline=None, closefd=True, opener=None)`
    * pathlib 中 `Path_对象.open(mode='r', buffering=-1, encoding=None, errors=None, newline=None)`
* 读写文件:
    * 内建函数
    * pathlib 中 `Path_对象.read_bytes()`
    * pathlib 中 `Path_对象.read_text(encoding=None, errors=None)`
    * pathlib 中 `Path_对象.write_bytes(data)`
    * pathlib 中 `Path_对象.write_text(data, encoding=None, errors=None, newline=None)`
* 复制文件: `shutil` 中的函数 `copy/copy2/copyfile/copytree(..)`
* 移动/重命名:
    * pathlib 中 `Path_对象.rename(target)`, 当文件已存在时，无法创建该文件
    * pathlib 中 `Path_对象.replace(target)`, 强制重命名
* 文件信息:
    * pathlib `Path_对象.stat()`, 提供文件的大小、创建时间等信息
        * 返回 `os.stat_result(st_mode=xxx, st_ino=xxx, st_dev=xxx, st_nlink=x, st_uid=x, st_gid=x, st_size=xxx, st_atime=xxx, st_mtime=xxx, st_ctime=xxx)`
    * pathlib `Path_对象.lstat()`, 与 `stat` 类似, 用于文件链接
* 更改权限:
    * pathlib 中 `Path_对象.chmod(mode, *, follow_symlinks=True)`
    * pathlib 中 `Path_对象.lchmod(mode)`
* 文件链接:
    * pathlib 中 `Path_对象.link_to(target)`
    * pathlib 中 `Path_对象.symlink_to(target, target_is_directory=False)`
    * pathlib 中 `Path_对象.hardlink_to(target)`
    * pathlib 中 `Path_对象.readlink()`
* linux 文件信息
    * 文件所有者: pathlib 中 `Path_对象.owner()`
    * 文件组: pathlib 中 `Path_对象.group()`

## 1.4. 信息判断
* 常用
    * 是否存在: pathlib `Path_对象.exists()`
    * 是否为目录: pathlib `Path_对象.is_dir()`
    * 是否为文件: pathlib `Path_对象.is_file()`
* 其他
    * 是否为绝对路径: pathlib 中 `Path_对象.is_absolute()`
    * 是否为相对路径: pathlib 中 `Path_对象.is_relative_to(*other)`
    * 是否匹配给定类型: pathlib `Path_对象.match(path_pattern)`
    * 是否为特殊路径: pathlib `Path_对象.is_reserved()`
    * 是否为挂载点: pathlib `Path_对象.is_mount()`
    * 是否为链接: pathlib `Path_对象.is_symlink()`
    * 是否为 socket: pathlib `Path_对象.is_socket()`
    * 是否为相同文件: pathlib `Path_对象.samefile(other_path)`

## 1.5. 应用实例

### 1.5.1. pyinstaller 打包 exe 后的路径问题
* 测试代码
    ```Python
    import os
    import sys
    from pathlib import Path

    print(f"{sys.path[0] = }")

    print(f"{sys.argv[0] = }")
    print(f"{os.path.realpath(sys.argv[0]) = }")
    print(f"{Path(sys.argv[0]).absolute() = }")

    print(f"{Path.cwd() = }")
    print(f"{os.getcwd() = }")

    print(f"{__file__ = }")
    print(f"{os.path.abspath(__file__) = }")
    print(f"{os.path.realpath(__file__) = }")
    print(f"{os.path.dirname(os.path.realpath(__file__)) = }")

    print(f"{os.path.dirname(sys.executable) = }")
    ```
* 打包后在 exe 所在目录运行
    ```shell
    sys.path[0] = 'C:\\Users\\用户名\\AppData\\Local\\Temp\\_MEI27122\\base_library.zip'
    sys.argv[0] = 'tmp.exe'
    os.path.realpath(sys.argv[0]) = 'D:\\Work\\VSCode_Ext_Dev\\Prj_hdl\\prj_hyhdl\\src\\documentation\\_temp_debug\\dist\\tmp.exe'
    Path(sys.argv[0]).absolute() = WindowsPath('D:/Work/VSCode_Ext_Dev/Prj_hdl/prj_hyhdl/src/documentation/_temp_debug/dist/tmp.exe')
    Path.cwd() = WindowsPath('D:/Work/VSCode_Ext_Dev/Prj_hdl/prj_hyhdl/src/documentation/_temp_debug/dist')
    os.getcwd() = 'D:\\Work\\VSCode_Ext_Dev\\Prj_hdl\\prj_hyhdl\\src\\documentation\\_temp_debug\\dist'
    __file__ = 'C:\\Users\\用户名\\AppData\\Local\\Temp\\_MEI27122\\tmp.py'
    os.path.abspath(__file__) = 'C:\\Users\\用户名\\AppData\\Local\\Temp\\_MEI27122\\tmp.py'
    os.path.realpath(__file__) = 'C:\\Users\\用户名\\AppData\\Local\\Temp\\_MEI27122\\tmp.py'
    os.path.dirname(os.path.realpath(__file__)) = 'C:\\Users\\用户名\\AppData\\Local\\Temp\\_MEI27122'
    os.path.dirname(sys.executable) = 'D:\\Work\\VSCode_Ext_Dev\\Prj_hdl\\prj_hyhdl\\src\\documentation\\_temp_debug\\dist'
    ```
    * exe 会将必要文件解压到临时文件后, 开始运行
* 在任意路径运行 exe (如 `C:`)
    ```shell
    sys.path[0] = 'C:\\Users\\用户名\\AppData\\Local\\Temp\\_MEI20922\\base_library.zip'
    sys.argv[0] = 'D:\\Work\\VSCode_Ext_Dev\\Prj_hdl\\prj_hyhdl\\src\\documentation\\_temp_debug\\dist\\tmp.exe'
    os.path.realpath(sys.argv[0]) = 'D:\\Work\\VSCode_Ext_Dev\\Prj_hdl\\prj_hyhdl\\src\\documentation\\_temp_debug\\dist\\tmp.exe'
    Path(sys.argv[0]).absolute() = WindowsPath('D:/Work/VSCode_Ext_Dev/Prj_hdl/prj_hyhdl/src/documentation/_temp_debug/dist/tmp.exe')
    Path.cwd() = WindowsPath('C:/')
    os.getcwd() = 'C:\\'
    __file__ = 'C:\\Users\\用户名\\AppData\\Local\\Temp\\_MEI20922\\tmp.py'
    os.path.abspath(__file__) = 'C:\\Users\\用户名\\AppData\\Local\\Temp\\_MEI20922\\tmp.py'
    os.path.realpath(__file__) = 'C:\\Users\\用户名\\AppData\\Local\\Temp\\_MEI20922\\tmp.py'
    os.path.dirname(os.path.realpath(__file__)) = 'C:\\Users\\用户名\\AppData\\Local\\Temp\\_MEI20922'
    os.path.dirname(sys.executable) = 'D:\\Work\\VSCode_Ext_Dev\\Prj_hdl\\prj_hyhdl\\src\\documentation\\_temp_debug\\dist'
    ```

--------------------------------------------------------------------------------
# 2. 普通文件
* 文件是一个 IO 对象, 调用对象的方法读写文件
* 主要方法
    * 打开与关闭
        * 使用内建函数 `open(..) -> IO_对象`, 需要用户调用 `.close()` 关闭文件
            * `open(file, mode='r', buffering=-1, encoding=None, errors=None, newline=None, closefd=True, opener=None)`
                * mode: 可选, 文件打开模式
                    模式                   | 描述
                    :--------------------: | -----------------------------
                    r                      | 只读, 文件指针在文件头, 默认
                    w                      | 只写, 若存在, 删除原内容, 从头编辑; 若不存在, 创建
                    x                      | 若不存在, 创建; 否则, 报错
                    a                      | 若存在, 追加; 若不存在, 创建
                    [r\|w\|x\|a] b         | 二进制模式
                    [r\|w\|x\|a] t         | 文本模式 (默认)
                    [r\|w\|x\|a] [b\|t]\ + | 读写模式, 若不存在, r+报错, w+和a+则创建文件
                * `buffering`: 设置缓冲区大小
                * `encoding`: 一般使用 `utf8`
        * 也可以使用 `ptahlib` 中 `Path` 对象的方法 `open` 打开, 需要用户调用 `close` 关闭文件
        * 使用 `with open(..) as IO_对象:` 打开, 退出 `with` 时自动关闭文件
            * 同时打开多个文件
                ```Python
                with (open(filename1) as fp1,
                    Path.open() as fp2, ...):
                    ...
                ```
    * 读取
        * `read(size=-1)`: 读取指定的字节数, 如果未给定或为负则读取所有
        * `readline(size=-1)`: 读取整行, 包括 `"\n"` 字符
        * `readlines(hint=-1)`: 读取所有行, 返回列表, 若给定 `hint` > 0, 返回总和大约为 `hint` 字节的行, 实际读取值可能比 `hint` 较大, 因为需要填充缓冲区
    * 写入
        * `.write(str)`: 将字符串写入文件, 返回写入字符的长度, 需要自己加入换行
        * `.writelines(sequence)`: 将字符串列表写入文件, 需要自己加入换行
        * `flush()`: 刷新文件缓冲区, 立即写入文件
    * 文件位置
        * `tell()`: 返回文件当前位置
        * `seek(offset,origin)`: 设置文件当前位置,
            * `origin`:
                * =0 表示开头
                * =1 表示当前位置
                * =2 表示文件结尾
    * 信息
        * `readable()`: 文件是否可读
        * `writable()`: 文件是否可可写
        * `isatty()`: 如果文件连接到一个终端设备返回 `True`, 否则返回 `False`
    * 其他
        * `fileno()`: 返回一个整型的文件描述符, 可以用在如 `os` 模块的 `read` 方法等一些底层操作上
        * `truncate(pos=None)`: 从文件的首行首字符开始截断, 截断文件为 size 个字符, 无 size 表示从当前位置截断; 截断之后后面的所有字符被删除, 其中 Widnows 系统下的换行代表2个字符大小
        * `reconfigure(..)`: 重新配置文件流
* 主要属性
    * `closed`: 文件是否已经关闭
    * `name`: 文件名字
    * `mode`: 文件打开模式
    * `encoding`: 文件编码
    * `errors`: 报错级别
    * `buffer`: 文件对象的 buffer 对象
    * `line_buffering`: bool
    * `newlines`: 换行符
    * `write_through`: bool

--------------------------------------------------------------------------------
# 3. json
> 使用标准库 json

* 基本方法
    src         | dst           | function
    :---------: | :-----------: | :----
    json 文件   | 数据          | **json.load**(fp, *, </br> cls=None, object_hook=None, parse_float=None, parse_int=None, parse_constant=None, object_pairs_hook=None, **kw)
    json 字符串 | ^             | **json.loads**(s, *, </br> cls=None, object_hook=None, parse_float=None, parse_int=None, parse_constant=None, object_pairs_hook=None, **kw)
    数据        | json 字符串   | **json.dumps**(obj, *, </br> skipkeys=False, ensure_ascii=True, check_circular=True, allow_nan=True, cls=None, indent=None, separators=None, default=None, sort_keys=False, **kw)
    ^           | json 文件     | **json.dump**(obj, fp, *, </br> skipkeys=False, ensure_ascii=True, check_circular=True, allow_nan=True, cls=None, indent=None, separators=None, default=None, sort_keys=False, **kw)
* 简单示例
    ```Python
    import json
    dat1 = ['foo', {'bar': ('baz', None, 1.0, 2)}]
    # 数据 -> 转为 json 字符串
    json1 = json.dumps(dat1)    # json1 = '["foo", {"bar": ["baz", null, 1.0, 2]}]'
    # 数据 -> 保存为 json 文件
    with open("json_test.json",'w') as fp:
        json.dump(dat1, fp)
    # json字符串 -> 数据
    dat2 = json.loads(json1)    # dat2 = ['foo', {'bar': ['baz', None, 1.0, 2]}]
    # json文件 -> 数据
    with open("json_test.json",'r') as fp:
        dat3 = json.load(fp)    # dat3 = ['foo', {'bar': ['baz', None, 1.0, 2]}]
    ```
* 处理非规则 json ()
    ```Python
    def get_abnormal_json(expr):
        """
        解析非标准JSON的Javascript字符串, 等同于json.loads(JSON str)
        :param expr:非标准JSON的Javascript字符串
        :return:Python字典
        """
        return eval(expr, type('Dummy', (dict,), dict(__getitem__=lambda s, n: n))())
    ```

--------------------------------------------------------------------------------
# 4. yaml
> 需要安装第三方库: `pip install -U pyyaml`

> [官方文档](https://pyyaml.org/wiki/PyYAMLDocumentation)

* 基本应用
    ```Python
    import yaml
    # load: stream 是字符串类型
    data = yaml.load(stream, yaml.Loader)
    data = yaml.loadall(stream, yaml.Loader)    # 返回一个迭代器
    # load: 从文件
    with open(file, "r", ...) as fp:
        data = yaml.load(fp, yaml.Loader)
        data = yaml.loadall(fp, yaml.Loader)    # 返回一个迭代器
    # dump: 到字符串
    output = yaml.dump(data, stream)    # data 中的数据尽量使用标准类型
    # dump: 到文件
    with open(file, "w", ...) as fp:
        output = yaml.dump(data, fp)    # data 中的数据尽量使用标准类型
    ```

--------------------------------------------------------------------------------
# 5. ini
> 使用标准库 configparser

* 基本步骤
    1. 初始化`configparser.ConfigParser`对象
    1. 从文件或其他读取数据: `.read(..)`
    1. 查看数据: `cfg[段名][选项名]`
    1. 添加、修改、删除数据
    1. 将数据写入文件: `.write(..)`
* 示例
    ```Python
    import configparser
    cfg = configparser.ConfigParser()
    # 读取
    cfg.read("ini_test.ini")
    # 查看
    print(f"{cfg['section1']['item1']=}")   # "1"
    print(f"{cfg['section1']['item2']=}")   # "1,2, 3"
    print(cfg.getfloat('section1','item3')) # 3.3
    # 添加、修改、删除等
    cfg.add_section("section1")
    cfg["section1"] = {"item1": "1", "item2": "1,2, 3"}
    cfg["section1"]["item3"] = "3.3"
    # 写入
    with open("ini_test.ini", "w") as cfg_file:
        cfg.write(cfg_file)
    ```
* 读取
    1. 对象方法`.read(filenames, encoding=None)`读取文件
        * 或 `.read_dict/read_file/read_string(..)`读取其他对象
    1. 查看对象
        * 字典模式访问, 返回字符串: `object[段名][选项名]`(等效于 `.get(段名, 选项名)`)
        * 以特定格式访问: `.getboolean/getint/getfloat(段名, 选项名)`
        * 迭代方式访问: `.keys/values/items()`
        * 段相关
            * 列举所有段: `.sections()`
            * 查询: `.has_section(段名)`
            * 属性: `.default_section`
        * 选项相关
            * 列举所有选项: `.options(段名)`
            * 查询: `.has_option(段名, 选项名)`
        * 其他:
            * 方法: `.defaults(..)`
* 写入
    1. 调用对象方法新建或修改值
        * 新建段: `.add_section(段名)`
        * 字典模式新建或修改: `object[段名][选项名] = 值` (等效于`.set(段名, 选项名, 值)`)
        * 删除: `.remove_section(段名)`, `remove_option(段名, 选项名)`
        * 其他: `.update/clear/pop/popitem/setdefault()`
    1. 使用`.write(fileobject, space_around_delimiters=True)`方法写入文件

--------------------------------------------------------------------------------
# 6. csv

## 6.1. 标准库 csv
* 基本步骤
    1. 打开文件
    2. 例化读/写对象 (reader/DictReader, writer/DictWriter)
    3. 迭代方式或字典方式读写内容
* 示例
    ```Python
    import csv
    with open('some.csv', newline='') as f:
        reader = csv.reader(f, delimiter=':', quoting=csv.QUOTE_NONE)
        for row in reader:
            print(row)
    with open('some.csv', 'w', newline='', encoding='utf-8') as f:
        writer = csv.writer(f)
        writer.writerows(someiterable)
    ```
* 读取对象
    * `.reader(csvfile, dialect='excel', ..)`
        * 逐行迭代, 迭代器返回 list of string
        * 属性:
            * `.dialect`, 格式
            * `.line_num`, 当前行数
    * `.DictReader(f, fieldnames=None, restkey=None, restval=None, dialect='excel', ..)`: 读取所有内容并转为 dict
        * 逐行迭代, 迭代器返回 odered dict, 格式`[('表头1', '数据1'), ('表头2', '数据2'), ...]`
* 写入对象
    * `csv.writer(csvfile, dialect='excel', **fmtparams) -> object`
        * 需要写入 list of string
        * 方法:
            * `.writerow(..)`: 写入一行
            * `.writerows(..)`: 写入多行
    * `csv.DictWriter(f, fieldnames, restval='', extrasaction='raise', dialect='excel', *args, **kwds)`
        * 需要写入 dict
        * 方法:
            * `.writeheader(..)`
            * `.writerow(..)`
            * `.writerows(..)`
* dialect 格式
    * `csv.Dialect`类定义了格式, 包括分隔符、转义符、行结束符等, 详见帮助文档
    * 预定义的 dialect
        * `csv.excel` -> 'excel', 即常见的csv格式
        * `csv.excel_tab` -> 'excel-tab'
        * `csv.unix_dialect` -> 'unix'
    * 可以调用`csv.Sniffer`模块中的函数自动判断 dialect
    * csv 提供了一些 `dialect` 相关函数

## 6.2. 第三方库 numpy
相见 numpy 笔记

## 6.3. 第三方库 pandas
详见 pandas 笔记

--------------------------------------------------------------------------------
# 7. excel 文件

## 7.1. 第三方库 openpyxl
简单易用, 功能广泛, 详见[官方文档 (英文) ](https://openpyxl.readthedocs.io/en/stable/)

* 基础
    * 组件: cell, chart, chartsheet, comments, compat, constants, descriptors, drawing, formatting, formula, load_workbook, packaging, pivot, reader, styles, utils, workbook, worksheet, writer, xml
    * 访问顺序: Workbook -> worksheet -> cell
* 基本操作
    1. 创建或读取 excel 文件
        ```Python
        # 创建
        from openpyxl import load_workbook
        wb = Workbook()
        #加载
        from openpyxl import load_workbook
        wb2 = load_workbook('test.xlsx')
        ```
    1. 创建或访问 Worksheet

        * 创建 worksheet
            * 创建 excel 文件后会自动创建一个 Worksheet, `wb.active` -> Worksheet对象
            * <Worksheet对象>.`create_sheet(title=None, index=None)` -> Worksheet对象
            *
        * 访问 Worksheet
            * `wb.active`
            * <Workbook对象>[<sheet名称>]
            *
    1. 访问 cell
        * <Workbook对象>[<单元格名称, 如‘A1’, ‘B2’>]
        * <Workbook对象>[<单元格范围, 如‘A1:D4’>]
        * <Workbook对象>[<单元格列, 如‘C’>]
        * <Workbook对象>[<单元格列范围, 如‘C:F’>]
        * <Workbook对象>[<单元格行, 如‘10’>]
        * <Workbook对象>[<单元格行范围, 如‘2:9’>]
        * <Workbook对象>.`cell(row, column, value)`
        * <Workbook对象>.`iter_rows()`
        * <Workbook对象>.`iter_cols()`
        * <Workbook对象>.`rows`
        * <Workbook对象>.`columns`
        * <Workbook对象>.`values`

    1. 读写
        * 按 cell
            * 读: <cell对象>.`value`
            * 写: <cell对象> = val
        * 按行
            * <Workbook对象>.`append(iterable)`
    1. 保存到文件
        * <Worksheet对象>.`save(filename)`
* 与 Pandas 互操作
    ```Python
    from openpyxl.utils.dataframe import dataframe_to_rows
    wb = Workbook()
    ws = wb.active

    for r in dataframe_to_rows(df, index=True, header=True):
    ws.append(r)
    ```
    ```Python
    df = DataFrame(ws.values)
    # 或
    data = ws.values
    cols = next(data)[1:]
    data = list(data)
    idx = [r[0] for r in data]
    data = (islice(r, 1, None) for r in data)
    df = DataFrame(data, index=idx, columns=cols)
    ```

## 7.2. 第三方库 xlrd/xlwt/xlutils
老牌python包, xlrd可以读取xlsx文件, xlwt不兼容xlsx文件

## 7.3. 第三方库 numpy, pandas

--------------------------------------------------------------------------------
# 8. 自动生产文档
> 基于第三方库 jinja2, 参见 [官方文档](https://jinja.palletsprojects.com/), 或 [中文参考资料](http://docs.jinkan.org/docs/jinja2/templates.html)

## 8.1. 标记语法
* 基本示例
    ``` jinja2
    <title>{% block title %}{% endblock %}</title>
    <ul>
    {% for user in users %}
    <li><a href="{{ user.url }}">{{ user.username }}</a></li>
    {% endfor %}
    </ul>
    ```
* **标记变量**:
    * `{% 变量/语句 %}`: 标记变量, 也可以执行循环或分支判断
    * `{{ 变量 }}`: 标记变量
    * `{{r 变量 }}`: 用于标记富文本, `r`要紧跟着`{`
    * 多级变量: "foo.bar" 或 "foo[bar]"
* **过滤器**:
    * 变量可以通过 `过滤器` 修改, 过滤器与变量用管道符号 (`|`) 分割, 并且也可以用圆括号传递可选参数, 多个过滤器可以链式调用, 前一个过滤器的输出会被作为后一个过滤器的输入
        * 例如 `{{ name|striptags|title }}` 会移除 name 中的所有 HTML 标签, 并改写标题为 title 格式
    * 过滤器接受带圆括号的参数, 如同函数调用
        * 如: `{{ list|join(', ') }}`
    * [内置过滤器清单](http://docs.jinkan.org/docs/jinja2/templates.html#builtin-filters)
* **判断**:
    * 可判断一个变量的类型, 如:
        ``` jinja2
        {% if loop.index is divisibleby 3 %}
        {% if loop.index is divisibleby(3) %}
        ```
    * [内置判断清单](http://docs.jinkan.org/docs/jinja2/templates.html#builtin-tests)
* **注释**:
    * 要把模板中一行的部分注释掉, 默认使用 {# ... #} 注释语法, 如
        ``` jinja2
        {# note: disabled template because we no longer use this
            {% for user in users %}
                ...
            {% endfor %}
        #}
        ```
* **空白控制**:
    * 默认配置中, 模板引擎不会对空白做进一步修改, 每个空白 (空格、制表符、换行符 等等) 都会原封不动返回
    * 如果应用配置了 Jinja 的 trim_blocks, 模板标签后的第一个换行符会被自动移除
    * 也可以手动剥离模板中的空白: 在块的开始或结束放置一个减号 (`-`), 如
        ``` jinja2
        {% for item in seq -%}
            {{ item }}
        {%- endfor %}
        ```
* **for 循环**: 遍历序列中的每项
    * 示例1:
        ``` jinja2
        {% for user in users %}
            {{ user.username|e }}
        {% endfor %}
        ```
    * 示例2:
        ``` jinja2
        {% for key, value in my_dict.iteritems() %}
            {{ key|e }}
            {{ value|e }}
        {% endfor %}
        ```
    * 特殊变量
        变量           | 描述
        ---------------|-----------------------
        loop.index     | 当前循环迭代的次数 (从 1 开始)
        loop.index0    | 当前循环迭代的次数 (从 0 开始)
        loop.revindex  | 到循环结束需要迭代的次数 (从 1 开始)
        loop.revindex0 | 到循环结束需要迭代的次数 (从 0 开始)
        loop.first     | 如果是第一次迭代, 为 True
        loop.last      | 如果是最后一次迭代, 为 True
        loop.length    | 序列中的项目数
        loop.cycle     | 在一串序列间期取值的辅助函数。见下面的解释
* **if 分支判断**:
    * 示例1:
        ``` jinja2
        {% if users %}
            {% for user in users %}
                {{ user.username|e }}
            {% endfor %}
        {% endif %}
        ```
    * 示例2:
        ``` jinja2
        {% if kenny.sick %}
            Kenny is sick.
        {% elif kenny.dead %}
            You killed Kenny!  You bastard!!!
        {% else %}
            Kenny looks okay --- so far
        {% endif %}
        ```
* **运算符**:
    * **算术**: `+`, `-`, `*`, `**`, `/`, `//`, `%`
    * **比较**: `==`, `!=`, `>`, `>=`, `<`, `<=`
    * **逻辑**: `and`, `or`, `not`,` (表达式)`
    * **其它运算符**: `in`, `is`, `|` (应用一个过滤器), `~` (操作数转为字符串)
* 其他:
    * 行语句
    * 模板继承: 基本模板, 子模板, Super 块, 命名块结束标签, 嵌套块和作用域, 模板对象
    * 转义: 手动转义, 自动转义
    * 其他控制结构: 宏, 调用, 过滤器, 赋值, 继承, 块, 包含, 导入
    * 导入上下文行为
    * 表达式: 字面量, 算术, 比较, 逻辑, 其它运算符

## 8.2. API
* 简单示例
    ``` python
    from jinja2 import Environment, FileSystemLoader
    env_对象 = Environment(loader=FileSystemLoader(目录))
    模板对象 = env_对象.get_template(模板文件)
    out = 模板对象.render(替换字典)     # 要一次性全部替代
    ```

