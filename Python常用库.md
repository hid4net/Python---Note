
0.1. **Python常用库**
--------------------------------------------------------------------------------
返回 [Python基础](Python%20笔记%EF%BC%9APython%20基础.md)

--------------------------------------------------------------------------------
# 1. 包管理 `pip`
## 1.1. 设置镜像:
```shell
# 临时
pip install -i https://pypi.tuna.tsinghua.edu.cn/simple 模块名
# 默认
pip config set global.index-url https://mirrors.aliyun.com/pypi/simple/
```
## 1.2. 常用命令
```shell
pip -h
pip list
pip list -o
pip install 库名
pip install -U 库名
```

--------------------------------------------------------------------------------
# 2. 常用库
分类       | 库
:--------- | :--------------------------------------
代码格式化 | black
数据科学   | 分析: numpy, pandas^1^, scipy, sympy
^          | 作图: matplotlib, plotly^2^
^          | 存储: h5py, openpyxl
开发       | ipython, jupyterlab, line_profiler^3^
GUI        | PySimpleGUI
电子学     | pyserial, crcmod
虚拟环境   | virtualenv, virtualenvwrapper
生成 exe   | PyInstaller^4^

* 注意:
    * ^1^ pandas 读写 HDF5 文件需要安装 `pytables` 库; 读写 excel 文件需要`xlrd, openpyxl`库
    * ^2^ plotly导出静态图片需要安装 `kaleido` 库
    * ^3^ 如果没有C编译器, 建议从 [Unofficial](https://www.lfd.uci.edu/~gohlke/pythonlibs/) 渠道安装
    * ^4^ 建议在虚拟环境中使用, 以减小程序包大小

安装命令
``` bash
pip install -U black
pip install -U ipython jupyterlab
pip install -U numpy pandas
pip install -U plotly kaleido
# pip install -U matplotlib
# pip install -U h5py tables
pip install -U PySimpleGUI
pip install -U pyserial crcmod
# pip install -U xlrd openpyxl
# pip install -U numba
pip install -U scipy sympy
pip install -U virtualenv virtualenvwrapper-win
pip install -U PyInstaller
pip install opencv-python
```

--------------------------------------------------------------------------------
# 3. IPython

## 3.1. 基本操作
* `?` 帮助,  如 `函数名/库名?`
* `??` 查看源代码 (好像不行)
* tab 键补全, 也可用来搜索所有的属性和方法, 也可用于导入module
* 通配符配合tab可以实现搜索

## 3.2. 快捷键
* `ctrl + k` 从光标处剪切到行尾
* `ctrl + u` 从光标处剪切到行首
* `ctrl + y` 粘贴之前剪切的文本
* `ctrl + r` 对历史命令进行方向搜索
* `ctrl + l` 清屏

## 3.3. magic命令
* 基础
    `%<命令>` line magic, 针对一行
    `%%<命令>`  cell magic, 针对一个cell
    `%magic/%lsmagic/%quickref`   列举magic命令
* 常用magic
    分类    | magic                  | 说明
    :-----: | :--------------------: | :--------------------------------------------------
    ipython | %paste                 | 粘贴并运行 (在粘贴之前对目标内容进行格式化)
    ^       | %cpaste                | 粘贴 (在粘贴之前对目标内容进行格式化, 输入 -- 结束)
    ^       | %hist / %history       | 历史
    ^       | %who / %who_ls / %whos | 显示所有变量
    运行    | %run                   | 执行外部程序
    性能    | %time / %%time         | 计时
    ^       | %timeit / %%timeit     | 计时
    ^       | %prun/ %%prun          | 按行统计运行时间
    ^       | %lprun                 | 按行统计运行时间, 使用 %load_ext line_profiler
    ^       | %memit                 | 统计内存
    ^       | %mprun                 | 按行统计运行内存
    shell   | %cd                    | 切换目录
    ^       | %ls                    | ls
    ^       | %ddir / %ldir          | dir
    ^       | %pwd                   | 当前工作目录
    ^       | %mkdir                 | 创建目录
    ^       | %rmdir                 | 创建目录
    ^       | %cls                   | 清屏
    ^       | %env                   | 环境变量
    ^       | %set_env               | 环境变量

--------------------------------------------------------------------------------
# 4. jupyter-lab
* 配合 vscode 使用
