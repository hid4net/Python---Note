
**Python 总结: 数据科学 - 数据存储**
--------------------------------------------------------------------------------
[返回目录](outline.md)

--------------------------------------------------------------------------------
tips:
* HDF5 存储数据非常快
* ==HDF5 用于存数据, 而非处理数据, 尽量不要直接操作数据==
* ==pandas 和 numpy 存储 HDF5 各有优势==
    * pandas 处理结构体数组比 numpy 更好, 会将相同类型的数据放在一起
    * numpy 存储的数据易读
* 保存为 excel 或 csv 时, 浮点数的精度会降低

--------------------------------------------------------------------------------

<!-- @import "[TOC]" {cmd="toc" depthFrom=1 depthTo=3 orderedList=false} -->

<!-- code_chunk_output -->

- [1. CSV](#1-csv)
  - [1.1. with Pandas](#11-with-pandas)
  - [1.2. with Numpy](#12-with-numpy)
- [2. Excel](#2-excel)
  - [2.1. with Pandas](#21-with-pandas)
- [3. HDF5](#3-hdf5)
  - [3.1. HDF5 数据结构](#31-hdf5-数据结构)
  - [3.2. with Pandas](#32-with-pandas)
    - [3.2.1. 基本操作](#321-基本操作)
    - [3.2.2. HDFStore 对象](#322-hdfstore-对象)
  - [3.3. h5py (interface with numpy)](#33-h5py-interface-with-numpy)
    - [3.3.1. 基本操作](#331-基本操作)
    - [3.3.2. 文件对象](#332-文件对象)
    - [3.3.3. group对象](#333-group对象)
    - [3.3.4. dataset对象](#334-dataset对象)
  - [3.4. pytables](#34-pytables)

<!-- /code_chunk_output -->

--------------------------------------------------------------------------------
# 1. CSV

## 1.1. with Pandas
> 参见 [官方文档](https://pandas.pydata.org/docs/user_guide/io.html#csv-text-files), [API](https://pandas.pydata.org/docs/reference/io.html#flat-file)
``` python
# 读取
df = pd.read_csv(..)
df = pd.read_fwf(..)
# 写入
s.to_csv(..)
df.to_csv(..)
```

## 1.2. with Numpy
> 参见 [官方文档](https://numpy.org/doc/stable/reference/routines.io.html#text-files)
``` python
# 读取
arr = pd.loadtxt(..)
arr = pd.genfromtxt(..)
# 写入
arr.savetxt(..)
```

--------------------------------------------------------------------------------
# 2. Excel

## 2.1. with Pandas
> 参见 [官方文档](https://pandas.pydata.org/docs/user_guide/io.html#excel-files), [API](https://pandas.pydata.org/docs/reference/io.html#excel)
``` python
# 读取
df = pd.read_excel(..)
# 批量读取
with pd.ExcelFile('path_to_file.xls') as xls:
    df1 = pd.read_excel(xls, 'Sheet1')
    df2 = pd.read_excel(xls, 'Sheet2')
# 或
data = pd.read_excel('path_to_file.xls', ['Sheet1', 'Sheet2'])
# 写入
df.to_excel('path_to_file.xlsx', sheet_name='Sheet1')
# 批量写入
with pd.ExcelWriter('path_to_file.xlsx') as writer:
    df1.to_excel(writer, sheet_name='Sheet1')
    df2.to_excel(writer, sheet_name='Sheet2')
```

--------------------------------------------------------------------------------
# 3. HDF5

## 3.1. HDF5 数据结构
HDF 是用于存储和分发科学数据的一种自我描述、多对象文件格式。HDF 是由美国国家超级计算应用中心 (NCSA) 创建的, 以满足不同群体的科学家在不同工程项目领域之需要

![HDF5数据结构](/assets/HDF5数据结构.jpg)

* HDF5包括若干 Group, 可嵌套, 以文件结构格式访问, 如'/Grp1/DatSet1'
* 每个组包含一个或多个 Dateset, 主要包含数据和相应的属性, 如下图
    ![HDF5_datasets](/assets/HDF5_datasets.jpg)


## 3.2. with Pandas
> 参见 [官方文档](https://pandas.pydata.org/docs/user_guide/io.html#hdf5-pytables), [API](https://pandas.pydata.org/docs/reference/io.html#hdfstore-pytables-hdf5)

### 3.2.1. 基本操作
``` python
# 读取
df = pd.read_hdf(..)
# 批量读取
with pd.HDFStore(..) as h5:
    df1 = h5.get(..)
    df2 = h5['df2名称']
    df3 = h5.select(..)
# 写入
df.to_hdf(..)
# 批量写入
with pd.HDFStore(..) as h5:
    h5.put(..)
    h5['df2名称'] = df2
    h5.append(..)
```

* 读取时可用 `where` 参数选择数据
    * The following are valid expressions:
        * 'index >= date'
        * "columns = ['A', 'D']"
        * "columns in ['A', 'D']"
        * 'columns = A'
        * 'columns == A'
        * "~(columns = ['A', 'B'])"
        * 'index > df.index[3] & string = "bar"'
        * '(index > df.index[3] & index <= df.index[6]) | string = "bar"'
        * "ts >= Timestamp('2012-02-01')"
        * "major_axis>=20130101"
    * The indexers are on the left-hand side of the sub-expression:
        * columns, major_axis, ts

    * The right-hand side of the sub-expression (after a comparison operator) can be:
        * functions that will be evaluated, e.g. Timestamp('2012-02-01')
        * strings, e.g. "bar"
        * date-like, e.g. 20130101, or "20130101"
        * lists, e.g. "['A', 'B']"
        * variables that are defined in the local names space, e.g. date

### 3.2.2. HDFStore 对象
* 固定格式 vs Table 格式
    * 固定格式读写更快, 但不能 append, 不能 queryable
* 信息: `pd.HDFStore.info, pd.HDFStore.keys, pd.HDFStore.groups, pd.HDFStore.walk`

## 3.3. h5py (interface with numpy)
详见[官方文档](http://docs.h5py.org/en/stable/)

### 3.3.1. 基本操作
```python
import h5py
# 打开文件, 并读取
f = h5py.File('mytestfile.hdf5', 'r')
arr = f['dset'][:]
f.close()
# 打开文件, 创建数据集, 并写入
f = h5py.File("mytestfile.hdf5", "w")
dset = f.create_dataset("dset", (100,), dtype='i')
dset[:] = np.arange(100)
f.close()
# h5py 支持容器管理器, 例如
with h5py.File("mytestfile.hdf5", "w") as f:
    dset = f.create_dataset("dset", (100,), dtype='i') # 写入
    dset[...] = np.arange(100) # 写入
    arr = f["dset"][:] # 读取
```

### 3.3.2. 文件对象
`h5py.File()`
* 打开/创建
`File(name, mode=None, driver=None, libver=None, userblock_size=None, swmr=False, **kwds) -> object(hdf5的root) -> HDF5 File Object`
    mode    | 说明
    --------|-------------------------------------------------
    r       | Readonly, file must exist
    r+      | Read/write, file must exist
    w       | Create file, truncate if exists
    w- or x | Create file, fail if exists
    a       | Read/write if exists, create otherwise (default)

* 属性:
    常用属性 | 说明
    ---------|-------------------
    attrs    | 字典方式访问, 可用list()查看
    driver   | 文件驱动器, 'windows'
    file     | 文件
    filename | 文件名
    id       | ID
    mode     | 文件打开方式
    name     | 名称, '/'
    parent   | 上一级, 根节点'/'

* 常用方法:
    分类     | 方法                                         | 说明
    ---------|----------------------------------------------|------------------------
    文件操作 | flush()                                      | 冲刷
    ^        | close()                                      | 关闭文件
    数据操作 | clear()                                      | 清空数据
    ^        | copy(..)                                     | 复制对象或组
    ^        | create_group(name, ...)                      | 创建组
    ^        | create_dataset(name, ...)                    | 创建数据集
    ^        | create_dataset_like(name, other, **kwupdate) | 创建数据集, 和目标对象相似
    ^        | create_virtual_dataset(name, layout, ...)    | 创建数据集 (虚拟)
    ^        | get(name, ...)                               | 访问数据
    ^        | items()                                      | 所有成员
    ^        | keys()                                       | 所有key
    ^        | move(source, dest)                           | 移动或重命名
    ^        | pop(k[,d]) -> v                              | 删除key, 并返回值
    ^        | popitem() -> (k, v)                          | 删除, 并返回一对儿 (key, value)
    ^        | update([E, ]**F) -> None                     | 更新

### 3.3.3. group对象
* 列举: `.name`, `.keys()`
* 创建: `object.create_group(name, track_order=False)`
    * name可以是路径
    * 可以在group的基础上继续创建subgroup
* 可以使用dict方式访问group, 可以使用迭代器访问 keys(), values(), items()
* 常用属性:
* 常用方法: `create_group/create_dataset/keys/values(..)`

### 3.3.4. dataset对象
* 属性
    分类     | 属性                                 | 说明
    ---------|--------------------------------------|--------------------------
    基本     | attrs, file, id, name, parent        | -
    数据信息 | chunks                               | (Tuple), 建议10 KiB ~ 1 MiB
    ^        | dims                                 | 维度
    ^        | dtype                                | 数据类型, 和numpy相同
    ^        | maxshape                             | 最大形状
    ^        | ndim                                 | 维度
    ^        | shape                                | 形状
    ^        | size                                 | 内存尺寸
    ^        | value                                | 值
    ^        | fillvalue                            | 填充值
    数据操作 | flush                                | 冲刷, SWMR (单写多读) 属性的一部分
    ^        | refresh                              | 刷新
    压缩     | compression/compression_opts/shuffle | -

* 创建: `create_dataset(name, shape=None, dtype=None, data=None, **kwds) -> 数据`
* 读写数据
    * 通过索引操作: 与numpy类似, 可以用`...`代替一个维
        * 如:  dset1[1] = 123, dset[:5] = aa, bb = dset[...]
    * 与Numpy array互操作
        * 读: `read_direct(dest, source_sel=None, dest_sel=None)`
        * 写: `write_direct(source, source_sel=None, dest_sel=None)`
* 改变数据类型: `astype(dtype)`
* 改变尺寸:  `resize(size, axis=None)`
* 获取数据长度
    * `.shape`
    * `len()`
    * 有些文件中, 属性可能包含长度信息

## 3.4. pytables
详见[官方文档](http://www.pytables.org/usersguide/index.html#)

<!-- ### 3.4.1. 基本操作
```python
import tables
h5file = open_file(..)  # 获取文件对象
grp = h5file.create_group(..)    # 创建组
tbl = h5file.create_table(..)  # 创建数据格式
tbl[0] = ...  # 写入数据
tbl.append(..) # 追加数据

tbl_rd = h5file.root.dataset
a = tbl_rd[1]
b = tbl_rd.col('col1')[3]
```

### 3.4.2. 文件对象
* 获取文件对象: 全局函数`tables.open_file(..)`
* 文件对象: `class tables.File(..)`, [官方文档](http://www.pytables.org/usersguide/libref/file_class.html)) :
    * 属性: `title`, `filters`, `open_count`
    * 主要方法:
        * `File.close()`, `File.flush()`, `File.get_filesize()`
        * `File.create_group(..)`
        * `File.create_table/create_array/create_carray/create_earray/create_vlarray(..)`

### 3.4.3. 数据结构: Table
* 创建Table对象: `File.create_table(..)`
* 获得Table对象: `文件对象.group路径.Table名称`
* 类: `class tables.Table(..)`, 相见[官方文档](http://www.pytables.org/usersguide/libref/structured_storage.html)
    * 属性:
        * `attrs`, `autoindex`, `byteorder`, `chunkshape`, `coldescrs`, `coldflts`, `coldtypes`, `colindexed`, `colindexes`, `colinstances`, `colnames`, `colpathnames`, `cols`, `coltypes`, `description`, `dtype`, `extdim`, `filters`, `flavor`, `indexed`, `indexedcolpathnames`, `maindim`, `name`, `ndim`, `nrows`, `nrowsinbuf`, `object_id`, `row`, `rowsize`, `shape`, `size_in_memory`, `size_on_disk`, `title`, `track_times`
    * 主要方法:
        * 读取: `[]`,`.col(name)`, `.read/read_coordinates/read_sorted(..)`
        * 迭代读取: `.iterrows/itersequence/itersorted(..)`
        * 写入: `[]`, `.append(rows)`, `.modify_rows/modify_column/modify_columns/modify_coordinates(..)`, `.remove_row/remove_rows(..)`
        * 查询: `.get_where_list/read_where/where/append_where/will_query_use_indexing(..)`
        * 其他: `.reindex/reindex_dirty(..)`,`...`
* 子类: `Description`, `Row`, `Cols`, `Column`

### 3.4.4. 数据结构: Array, CArray, EArray, VLArray
* 创建Array对象: `File.create_array(..)`
* 获得Array对象: `文件对象.group路径.Array名称`
* 类: `tables.Array(..)`, 相见[官方文档](http://www.pytables.org/usersguide/libref/homogenous_storage.html)
    * 属性: `atom`, `attrs`, `byteorder`, `chunkshape`, `dtype`, `extdim`, `filters`, `flavor`, `listarr`, `name`, `ndim`, `nrows`, `nrowsinbuf`, `object_id`, `rowsize`, `shape`, `size_in_memory`, `size_on_disk`,  `title`, `track_times`
    * 主要方法:
        * 读取: `[]`,`.read(..)`
        * 迭代读取: `.iterrows(..)`
        * 写入: `[]`, `.remove(..)`
        * 其他: `...` -->

