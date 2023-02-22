
<h1 style="text-align:center">PySimpleGUI</h1>

--------------------------------------------------------------------------------
[返回目录](outline.md)

tips:
* ==多看示例==
* 参见 [官方文档](https://pysimplegui.readthedocs.io/)
--------------------------------------------------------------------------------

<!-- @import "[TOC]" {cmd="toc" depthFrom=1 depthTo=6 orderedList=false} -->

<!-- code_chunk_output -->

- [1. 入门](#-1-入门)
  - [1.1. 入门示例](#-11-入门示例)
  - [1.2. 基本概念](#-12-基本概念)
  - [1.3. 窗口的运行类型](#-13-窗口的运行类型)
- [2. 详解: 窗口 (Window)](#-2-详解-窗口-window)
  - [2.1. class: Window](#-21-class-window)
  - [2.2. 创建窗口](#-22-创建窗口)
  - [2.3. 多线程支持](#-23-多线程支持)
  - [2.4. 其他](#-24-其他)
- [3. 详解: 事件与事件循环](#-3-详解-事件与事件循环)
  - [3.1. 事件](#-31-事件)
    - [3.1.1. 窗口事件](#-311-窗口事件)
    - [3.1.2. 按钮事件](#-312-按钮事件)
    - [3.1.3. Element 事件](#-313-element-事件)
  - [3.2. 事件循环](#-32-事件循环)
    - [3.2.1. 事件处理](#-321-事件处理)
    - [3.2.2. 事件循环与多线程](#-322-事件循环与多线程)
- [4. 详解: 布局与容器](#-4-详解-布局与容器)
  - [4.1. 布局](#-41-布局)
  - [4.2. 布局相关容器或函数](#-42-布局相关容器或函数)
- [5. 详解: Widget](#-5-详解-widget)
  - [5.1. 基本组件](#-51-基本组件)
  - [5.2. 组件操作](#-52-组件操作)
    - [5.2.1. key](#-521-key)
    - [5.2.2. 组件的通用属性和方法](#-522-组件的通用属性和方法)
    - [5.2.3. 组件样式](#-523-组件样式)
  - [5.3. 标题, 菜单, 状态栏](#-53-标题-菜单-状态栏)
    - [5.3.1. 标题](#-531-标题)
    - [5.3.2. 菜单](#-532-菜单)
    - [5.3.3. 状态栏](#-533-状态栏)
  - [5.4. 按钮](#-54-按钮)
  - [5.5. 输入类控件](#-55-输入类控件)
  - [5.6. 显示类控件](#-56-显示类控件)
  - [5.7. 表格/树状](#-57-表格树状)
  - [5.8. 画布](#-58-画布)
  - [5.9. 弹出窗口](#-59-弹出窗口)
  - [5.10. 系统托盘](#-510-系统托盘)
  - [5.11. 其他控件](#-511-其他控件)
  - [5.12. 打印调试信息](#-512-打印调试信息)
- [6. 设置、定制、美化](#-6-设置-定制-美化)
  - [6.1. 通用方法](#-61-通用方法)
  - [6.2. 主题、颜色、字体](#-62-主题-颜色-字体)
  - [6.3. 图标](#-63-图标)
  - [6.4. 窗口](#-64-窗口)
  - [6.5. 控件尺寸](#-65-控件尺寸)
- [7. 鼠标和键盘](#-7-鼠标和键盘)
  - [7.1. 鼠标](#-71-鼠标)
  - [7.2. 键盘和鼠标的捕获](#-72-键盘和鼠标的捕获)

<!-- /code_chunk_output -->

--------------------------------------------------------------------------------
# 1. 入门
* 参见 [官方文档](https://pysimplegui.readthedocs.io/)
* ==多看示例==

## 1.1. 入门示例
```Python {.line-numbers}
# 导入库
import PySimpleGUI as sg
# 设置主题 (可选, 美化)
sg.theme('DarkAmber')
# 各种组件 (用于窗口布局)
layout = [  [sg.Text('Some text on Row 1')],
            [sg.Text('Enter something on Row 2'), sg.InputText()],
            [sg.Button('Ok'), sg.Button('Cancel')] ]
# 创建窗口
window = sg.Window('Window Title', layout)
# 事件循环
while True:
    event, values = window.read()   # 返回: 事件标签 (str), 所有输入控件的值
    if event == sg.WIN_CLOSED or event == 'Cancel': # 如果用户关闭窗口或点击取消
        break
    print(f'You entered: {values[0]}')
# 关闭窗口
window.close()
```

## 1.2. 基本概念
* 窗口
* 组件
    * 容器
    * 控件
* 事件
* 事件循环

## 1.3. 窗口的运行类型
* one-shot (non-persistent): 不使用事件循环: 弹出 -> 收集信息 -> 销毁, 典型的是对话框类窗口
    ```Python
    import PySimpleGUI as sg

    layout = [
        [sg.Text("SHA-1 and SHA-256 Hashes for the file")],
        [sg.InputText(), sg.FileBrowse()],
        [sg.Submit(), sg.Cancel()],
    ]
    # 一种写法
    window = sg.Window("SHA-1 & 256 Hash", layout)
    event, values = window.read()   # 不使用事件循环
    window.close()                  # 窗口关闭后, 销毁窗口
    # 另一种写法
    event, values = sg.Window("SHA-1 & 256 Hash", layout).read(close=True)  # 自动销毁窗口
    # 使用数据
    source_filename = values[0]
    ```
* persistent: 启用事件循环, window 持续可见
    ```Python
    import PySimpleGUI as sg

    layout = [
        [sg.Text("Your typed chars appear here:"), sg.Text(size=(12, 1), key="-OUTPUT-")],
        [sg.Input(key="-IN-")],
        [sg.Button("Show"), sg.Button("Exit")],
    ]

    window = sg.Window("Window Title", layout)

    while True:  # 启用事件循环
        event, values = window.read()
        print(event, values)
        if event == sg.WIN_CLOSED or event == "Exit":
            break
        if event == "Show":
            window["-OUTPUT-"].update(values["-IN-"])
    # 窗口关闭后, 销毁窗口
    window.close()
    ```

--------------------------------------------------------------------------------
# 2. 详解: 窗口 (Window)

## 2.1. class: Window
* PySimpleGUI 使用 `Window` 类管理窗口
    * 别名: `FlexForm`
* 创建窗口: `window_对象 = Window(标题, 布局, ...)`
* 关闭窗口:
    * `.close()`, 别名: `Close`, `CloseNonBlocking`, `CloseNonBlockingForm`
    * 也可以设置 `.read(close=True)` 关闭窗口, 常用于 one-shot 型的窗口
* 窗口管理
    * `.finalize()`, 别名: `Finalize`, 固化窗口
        * 如果创建窗口对象后对窗口进行了更改, 需要在 `.read` 之前调用 `.finalize`
    * `.enable()`, 别名: `Enable`
    * `.disable()`, 别名: `Disable`
    * `.make_modal()`
    * `.move(x, y)`, 别名: `Move`
    * `.move_to_center()`
* 布局
    * `.add_row(...)`, 别名: `AddRow`
    * `.add_rows(...)`, 别名: `AddRows`
    * `.layout(rows)`, 别名: `Layout`
    * `.extend_layout(container, rows)`
* 组件管理
    * `.element_list()`
    * `.fill(values_dict)`, 别名: `Fill`
    * `.find_element(key, silent_on_error=False)`, 别名: `Element`, `Find`, `Elem`, `[]`
    * `.find_element_with_focus()`, 别名: `FindElementWithFocus`
    * `.key_dict()`
    * `.widget_to_element(widget)`
* 事件
    * `.read(timeout=None, timeout_key=TIMEOUT_KEY, close=False)`, 别名: `Read`
* 显示
    * `.maximize()`, 别名: `Maximize`
    * `.minimize()`, 别名: `Minimize`
    * `.normal()`, 别名: `Normal`
        <br/>
    * `.bring_to_front()`, 别名: `BringToFront`
    * `.send_to_back()`, 别名: `SendToBack`
    * `.force_focus()`
    * `.hide()`, 别名: `Hide`
    * `.un_hide()`, 别名: `UnHide`
    * `.disappear()`, 别名: `Disappear`
    * `.reappear()`, 别名: `Reappear`
    * `.refresh()`, 别名: `Refresh`
    * `.visibility_changed()`, 别名: `VisibilityChanged`
        <br/>
    * `.set_cursor(cursor)`
    * `.set_icon(icon=None, pngbase64=None)`, 别名: `SetIcon`
    * `.set_title(title)`
    * `.set_transparent_color(color)`, 别名: `SetTransparentColor`
    * `.size(size)`, 别名: `Size`
    * `.set_min_size(size)`
        <br/>
    * `.keep_on_top_set()`
    * `.keep_on_top_clear()`
        <br/>
    * `.set_alpha(alpha)`, 别名: `SetAlpha`
* 窗口信息
    * `.current_location(more_accurate=False)`, 别名: `CurrentLocation`
    * `.current_size_accurate()`
    * `.get_screen_dimensions()`, 别名: `GetScreenDimensions`
    * `.get_screen_size()`
    * `.is_closed()`
    * `.was_closed()`
    * `.mouse_location()`
* 多线程
    * `.perform_long_operation(func, end_key)`, 别名: `start_thread`
    * `.write_event_value(key, value)`
* 快捷键
    * `.bind(bind_string, key, propagate=True)`
* 其他
    * `.grab_any_where_on()`, 别名: `GrabAnyWhereOn`
    * `.grab_any_where_off()`, 别名: `GrabAnyWhereOff`

## 2.2. 创建窗口
* 步骤
    1. 创建窗口对象
    1. 添加布局
    1. 可选: 在调用 `.read` 之前定下来 (`.finalize`)
* 编程
    * 方法 1: 一步到位
        ```Python
        window = sg.Window(标题, 布局, ...)
        ```
    * 方法 2: 三步走
        ```Python
        window = sg.Window(标题)
        window.layout(布局)
        window.finalize()
        # 链式写法
        window = sg.Window(标题).Layout(布局).finalize()
        ```
* 注意
    * 窗口只允许运行在主线程
    * 如果想要调用了组件的 `update` 方法或调用了 `Graph` 组件的绘图原型, 必须先调用窗口对象的 `read` 或 `finalize` 方法

## 2.3. 多线程支持
* 调用长耗时的任务
    * 使用窗口对象的 `.perform_long_operation(func, end_key)` 方法调用, 它会启用一个线程
        * `func` 是函数名
            * 如果函数带参数, 可用 lambda 函数转换, 如 `func=lambda: 带参函数(参数)`
        * `end_key` 是任务结束时的事件名, 会加入到事件循环
        * 返回值: 线程句柄
        * 别名: `start_thread`
* 子线程与窗口互动
    * 子线程调用窗口对象的 `.write_event_value(key, value)` 方法向事件循环写入事件
        * 仅 tkinter 端口支持

## 2.4. 其他
* 长时间运行的窗口
    * 可以使用 `.refresh()` 定时刷新窗口, 防止无响应

# 3. 详解: 事件与事件循环

## 3.1. 事件
* 事件类型
    分类        | 事件
    :---------: | :--------------------
    所有窗口    | 关闭窗口
    ^           | 点击按钮
    Element 事件| 键盘
    ^           | 鼠标滚轮
    ^           | 菜单
    ^           | 控件改变 (slider, spinner, etc)
    ^           | 点击列表控件的某项
    ^           | 输入控件的回车键
    ^           | 超时
    ^           | 文字被选中
    ^           | Combobox 被选中
    ^           | ...

    注意: 不是所有的控件都默认启动了事件, 如需使用, 创建控件时需设置 `enable_events=True`

### 3.1.1. 窗口事件
* 一般情况下, 关闭窗口的事件为 `sg.WIN_CLOSED` (=`None`), 必须处理, 否则程序崩溃
    ``` python
    while True:
        event, values = window.read()
        if event == sg.WIN_CLOSED or event == 'Exit':   # 或
        # if event in (sg.WIN_CLOSED, 'Exit'):
            break
    window.close()
    ```
* 如需在用户试图关闭窗口时进行提示, 可以在创建窗口时设置 `enable_close_attempted_event=True`, 这样关闭窗口时返回 `sg.WINDOW_CLOSE_ATTEMPTED_EVENT` 事件, 如
    ```Python
    import PySimpleGUI as sg

    layout = [
        [sg.Text("Very basic Window")],
        [sg.Text("Click X in titlebar or the Exit button")],
        [sg.Button("Go"), sg.Button("Exit")],
    ]

    window = sg.Window("Window Title", layout, enable_close_attempted_event=True)

    while True:
        event, values = window.read()
        print(event, values)
        if (event == sg.WINDOW_CLOSE_ATTEMPTED_EVENT or event == "Exit") and sg.popup_yes_no(
            "Do you really want to exit?"
        ) == "Yes":
            break

    window.close()
    ```

### 3.1.2. 按钮事件
* 默认情况下, 点击、释放按钮和按钮按下等, 总是产生一个 `event`
* 可以添加按钮改变事件 (创建按钮时设置 `enable_events=True`), These events are triggered when something 'writes' to a button, usually it's because the button is listed as a "target" in another button.

### 3.1.3. Element 事件
* 注意: 不是所有的控件都默认启动了事件, 如需使用, 创建控件时需设置 `enable_events=True`
* 菜单栏选择事件
    * 接收 `MenuBar` 和 `ButtonMenu` 的 `key`, 从返回值字典中读取 `key`
* 右键点击菜单事件
    * 直接接收菜单文本和 `key`
* 键盘、鼠标和滚轮
    * 返回单个字符串或字符串
    * 滚轮事件返回字符串: `MouseWheel:Up`, `MouseWheel:Down`
* 超时/定时
    * 在 `window_对象.read(timeout=None, timeout_key=TIMEOUT_KEY, close=False)` 方法中设置 `timeout` (单位是 ms)
        * 一般不要低于 10 ms
    * 默认事件是 `TIMEOUT_KEY` (= `'__TIMEOUT__'`, 别名: `EVENT_TIMEOUT`/`TIMEOUT_EVENT` )

## 3.2. 事件循环

### 3.2.1. 事件处理
* 一般形式
    ```Python
    while True:
        event, values = window.read()   # 返回: 事件标签 (str), 所有输入控件的值
        if event == sg.WIN_CLOSED or event == 'Cancel': # 如果用户关闭窗口或点击取消
            break
        print(f'You entered: {values[0]}')
    ```
    * 对于多窗口程序, 可使用全局函数 `read_all_windows(timeout = None, timeout_key = "__TIMEOUT__")` 处理所有事件
* `event`
    * 数据类型: `str|int|tuple|object`
    * 一般是
        * 预定义的事件名
        * 组件的 `key`
        * 自定义的事件名
* `values: list/dict`
    * 所有可输入控件的值
    * 数据类型: 如果任一输入控件有 `key`, 则 `values` 是字典
        * 有 `key` 的通过 `key` 访问
        * 其余没有 `key` 的控件, 可以通过 0 开始的数字索引
            * 注意: 已有 `key` 的不再被分配数字, 不能通过数字索引
            * 注意: 数字不是从第一个控件开始, 而是从第一个 ==没有 key== 的控件开始

### 3.2.2. 事件循环与多线程
* 子线程可以通过调用窗口对象的 `.write_event_value(key, value)` 方法向事件循环写入事件
    * 仅 tkinter 端口支持

# 4. 详解: 布局与容器

## 4.1. 布局
* 布局原理
    * 一个窗口包含很多行, 每行可以有多个组件
    * 因此布局用一个嵌套列表 (list of lists) 存储, 每个元素是一个组件
        * 容器是一个特殊的组件, 内含更多布局
    * 示例
        ``` python
        headings = ['HEADER 1', 'HEADER 2', 'HEADER 3','HEADER 4']
        header =  [[sg.Text('  ')] + [sg.Text(h, size=(14,1)) for h in headings]]

        input_rows = [[sg.Input(size=(15,1), pad=(0,0)) for col in range(4)] for row in range(10)]

        layout = header + input_rows

        window = sg.Window('Table Simulation', layout, font='Courier 12')
        ```
        效果如下
        ![table效果](/assets/PySimpleGUI-布局.png)

## 4.2. 布局相关容器或函数
* 容器
    容器或控件      | 别名                  | tkinter 组件          | 描述
    :-------------- | :-------------------- | :-------------------- | :---------------
    `Column`        | `Col`                 | Combination Canvas & Frame  | 嵌入式布局
    `Pane`          | -                     | tk.PanedWindow        | 可滑动的列
    `Frame`         | `Fr`                  | tk.LabelFrame         | 框
    `Tab`           | -                     | tk.Frame              | 页
    `TabGroup`      | -                     | ttk.Notebook          | 页组
    `HorizontalSeparator`| `HSep`/`HSeparator`  | ttk.Separator     | 横线
    `VerticalSeparator`  | `VSeparator`/`VSep`  | ttk.Separator     | 竖线, 用于分隔 `Column`, 和 `Column` 等高
* 函数
    布局函数    | 说明
    :---------- | :---
    `Sizer`     | 用于占位 (特殊的 `Column`)
    `pin`       | 固定位置 (特殊的 `Column`)
    `vtop`      | 顶端居中对齐 (特殊的 `Column`)
    `vbottom`   | 底部居中对齐 (特殊的 `Column`)
    `vcenter`   | 中心居中对齐 (特殊的 `Column`)

# 5. 详解: Widget

## 5.1. 基本组件
组件            | 别名                  | tkinter 组件          | 描述
:-------------- | :-------------------- | :-------------------- | :---------------
`Text`          | `T`/`Txt`             | tk.Label              | 一行或多行文本
`Input`         | `I`/`In`/`InputText`  | tk.Entry              | 单行输入文本框
`Combo`         | `DD`/`Drop`/`DropDown`/`InputCombo`| ttk.Combobox | 下拉列表
`OptionMenu`    | `InputOptionMenu`     | tk.OptionMenu         | 下拉列表
`Multiline`     | `ML`/`MLine`          | tk.Text or tk.scrolledtext.ScrolledText  | 用于输入或输出的多行文本
`Radio`         | `R`/`Rad`             | tk.Radiobutton        | 单选
`Checkbox`      | `CB`/`CBox`/`Check`   | tk.Checkbutton        | 复选框
`Spin`          | `Sp`                  | tk.Spinbox            | 旋钮
`Button`        | `B`/`Btn`             | tk.Button or ttk.Button  | 按钮
`Image`         | `Im`                  | tk.Label              | 图片 (PNG or GIF)
`Canvas`        | -                     | tk.Canvas             | 画布, 建议选用 `Graph`
`Graph`         | `G`                   | tk.Canvas             | 画布
`Slider`        | `Sl`                  | tk.Scale              | 滑动条
`Listbox`       | `LB`/`LBox`           | tk.Listbox            | 列表框
`Menu`          | `MenuBar`/`Menubar`   | tk.Menu               | 菜单
`MenubarCustom` | -                     | Combined Elements     | 自定义菜单
`ButtonMenu`    | `BM`/`BMenu`          | tk.Menubutton         | 菜单按钮
`Titlebar`      | -                     | Combined Elements     | 自定义颜色的标题栏
`ProgressBar`   | `PBar`/`Prog`/`Progress` | ttk.Progressbar    | -
`Table`         | -                     | ttk.Treeview          | 表
`Tree`          | -                     | ttk.Treeview          | 树
`StatusBar`     | `SBar`                | tk.Label              | 状态栏
`Sizegrip`      | `SGrip`               | ttk.Sizegrip          | 窗口右下角用于调节尺寸的
`Push`          | `P`/`Stretch`         | PySimpleGUI Elements  | 横线推挤组件
`VPush`         | `VP`/`VStretch`       | PySimpleGUI Elements  | 纵向推挤组件

## 5.2. 组件操作

### 5.2.1. key
* `key` 是组件的基本属性, 创建组件对象时指定, 用于定位组件, 可用于
    * 事件标签
    * 用字典方式访问窗口对象 `.read()` 的返回值
    * 更新组件时, 定位组件
* 默认 `key`
    * 如果没有指定 `key`, 某些组件会生成默认 `key`, 如按钮的默认 `key` 是按钮的文本
* `WRITE_ONLY_KEY` 调节
    * 对于一些组件, 返回值特别长, 如果进将其作为输出, 则不需要返回值, 可以在指定 `key` 时添加 `WRITE_ONLY_KEY`, 如
        ```Python
        sg.Multiline(size=(40,8), key='-MLINE-' + sg.WRITE_ONLY_KEY)
        ```
* 查找组件
    * 使用窗口对象的 `.find_element(key, silent_on_error=False)` 方法, 别名: `Find`, `Element`, `Elem`, `[]`, 如
        ```Python
        # 以下写法等效
        window.find_element(key)
        window.Find(key)
        window.Element(key)
        window.Elem(key)
        window[key]
        ```

### 5.2.2. 组件的通用属性和方法
* 属性
    属性            | 说明
    :-------------: | :---
    `key`           | 组件的 key, 类似 ID
    `tooltip`       | 悬浮提示
    `size`          | (width, height), 单位一般为字符, 某些组件是像素
    `font`          | 指定字体, 格式: (family, size, styles)
    `colors`        | 预定义颜色名称或 #RRGGBB 字符串
    `pad`           | 元素周围的隔离带宽度, 单位: 像素
    `enable_events` | 组件特定的事件
    `visible`       | 是否可见
* 方法
    * 组件内容更新: `.update(new_value)`, 可进一步简化为 `组件对象(new_value)`, 如
        ```Python
        # 以下写法等效
        window.find_element(key).update(new_value)  # 可简化为
        window[key].update(new_value)   # 可简化为
        window[key](new_value)
        ```
    * `.bind(bind_string, key_modifier, propagate=True)` 和 `.unbind(bind_string)`
    * `.set_size(size=(None, None))` 和 `.get_size()`
    * `.set_tooltip(tooltip_text)`
    * ...

### 5.2.3. 组件样式
* 控件尺寸的默认单位是字符, 默认尺寸是 (45,1)
    * 部分控件的尺寸的单位是像素, 如 `Progress Meters` 和 `Sliders`

## 5.3. 标题, 菜单, 状态栏

### 5.3.1. 标题
* 控件: `Titlebar`
    * 可以自定义标题栏的颜色

### 5.3.2. 菜单
* 控件
    * `Menu`, 别名 `MenuBar`/`Menubar`
        * 使用 `AddMenuItem(...)` 添加
    * `ButtonMenu`, 别名 `BMenu`/`BM`
    * `OptionMenu`, 别名 `InputOptionMenu`
    * `MenubarCustom`

### 5.3.3. 状态栏
* 控件
    * `StatusBar`, 别名 `SBar`

## 5.4. 按钮
* 控件
    * `Button`, 别名 `Btn`/`B`
* `Button` 的变种
    * `ReadButton` = `RButton` = `ReadFormButton`
    * `RealtimeButton`
    * `DummyButton`
    * 关闭窗口: `CloseButton`=`CButton`
    * 通用: `OK` = `Ok`, `Submit`, `Cancel`, `Yes`, `No`, `Exit`, `Quit`, `Help`, `Save`, `SaveAs`, `Open`
    * 选择: `FileBrowse`, `FilesBrowse`, `FolderBrowse`, `FileSaveAs`, `CalendarButton`, `ColorChooserButton`
        * 可以指定 target, 如 `Input` 控件
    * `SimpleButton`
    * `Debug`
* 为按钮指定图片
    * 图片格式: PNG, GIF
    * 步骤:
        1. 选定图片
        2. 转换为 base64 string
        3. 创建按钮时指定 `image_data` 参数
        4. 可选: 指定 `buton_color` 使得按钮背景与窗口背景一致

## 5.5. 输入类控件
* 控件
    * `InputText`=`Input`=`In`=`I`
        * `do_not_clear` 参数: 如果为 `False`, 每次 `window.read()` 后, 都会清除文本
    * `Checkbox`=`Check`=`CBox`=`CB`
    * `Radio`=`Rad`=`R`
    * `Listbox`=`LBox`=`LB`
    * `Combo`=`InputCombo`=`DropDown`=`Drop`=`DD`
    * `Slider`=`Sl`
    * `Spin`=`Sp`

## 5.6. 显示类控件
* 文本
    * `Text`=`Txt`=`T`
    * `Multiline`=`MLine`=`ML`
* 图片
    * `Image`, 别名 `Im`
* 进度条
    * 控件
        * `ProgressBar`=`PBar`=`Progress`=`Prog`
        * `QuickMeter`
    * Functions
        * `OneLineProgressMeter`/`one_line_progress_meter`
        * `OneLineProgressMeterCancel`/`one_line_progress_meter_cancel`

## 5.7. 表格/树状
* `Table`
* `Tree`
    * `TreeData`

## 5.8. 画布
* `Canvas`
* `Graph`, 别名 `G`

## 5.9. 弹出窗口
* `Popup`/`popup`
* `Popup` 的变种
    * `PopupNoFrame`/`popup_no_frame` = `PopupNoBorder`/`popup_no_border` = `PopupAnnoying`/`popup_annoying` = `PopupNoTitlebar`/`popup_no_titlebar`
    * `PopupAnimated`/`popup_animated`
    * `PopupAutoClose`/`popup_auto_close` = `PopupTimed`/`popup_timed`
    * `PopupCancel`/`popup_cancel`
    * `PopupError`/`popup_error`
    * `PopupGetFile`/`popup_get_file`
    * `PopupGetFolder`/`popup_get_folder`
    * `PopupGetText`/`popup_get_text`
    * `PopupNoButtons`/`popup_no_buttons`
    * `PopupNoWait`/`popup_no_wait` = `PopupNonBlocking`/`popup_non_blocking`
    * `PopupOK`/`popup_ok`
    * `PopupOKCancel`/`popup_ok_cancel`
    * `PopupQuick`/`popup_quick`
    * `PopupQuickMessage`/`popup_quick_message`
    * `PopupScrolled`/`popup_scrolled`
    * `PopupYesNo`/`popup_yes_no`

## 5.10. 系统托盘
* `SystemTray`

## 5.11. 其他控件
* `Sizegrip`=`SGrip`
* `Push`=`P`=`Stretch`
* `VPush`=`VP`=`VStretch`

## 5.12. 打印调试信息
* `EasyPrint`/`easy_print` = `Print` = `eprint` = `sgprint`
* `EasyPrintClose`/`easy_print_close` = `sgprint_close` = `PrintClose`

--------------------------------------------------------------------------------
# 6. 设置、定制、美化

## 6.1. 通用方法
* `sg.set_options(...)`, 别名: `SetOptions`

## 6.2. 主题、颜色、字体
* 主题
    * 主题列表
        ![PySimgleGUI_theme_previewer](/assets/PySimgleGUI-theme_previewer.png)
        * 可通过以下两个函数查询:
            * `theme_list() -> list[str]`: 所有主题的名称
                * 等效于: `list_of_look_and_feel_values()` (别名: `ListOfLookAndFeelValues`)
            * `theme_previewer(...)`: 通过窗口显示主题预览
                * 别名: `preview_all_look_and_feel_themes`
        * 系统默认为 `DarkBlue3`
    * 可通过以下函数设置主题
        * `theme(new_theme=None)`
        * `theme_xxx(...)`
    * 如需使用系统默认的主题, 调用 `theme("gray gray gray")`
* 颜色
    * 通过函数 `GetComplimentaryHex/get_complimentary_hex` 得到Hex颜色string
    * 通过函数 `RGB/rgb` 根据 Red, Green, Blue 设置颜色
* 字体
    * 预定义字体
    * 自定义字体:
        * 两种方式:
            * Tuple - (family, size, styles)
            * String - "Family Size Styles"
        * 其中 styles 为以下选项
            * "italic"
            * "roman"
            * "bold"
            * "normal"
            * "underline"
            * "overstrike"
    * 窗口的默认字体: 创建窗口对象时设置 `font` 参数

## 6.3. 图标
* `SetGlobalIcon`/`set_global_icon`
* 为按钮指定图片
    * 图片格式: PNG, GIF
    * 步骤:
        1. 选定图片
        2. 转换为base64 string
        3. 创建Button 时指定image_data参数
        4. 指定buton_color使得按钮背景与窗口背景一致

## 6.4. 窗口
美化项      | 方法
:---------- | :--------
取消标题栏  | 创建窗口时设置 `no_titlebar` 参数
窗口尺寸    | 创建窗口时设置 `size` 参数
^           | 修改窗口对象的属性: `.size()` (别名: `Size`)
窗口透明    | 创建窗口时设置 `alpha_channel` 参数
^           | 修改窗口对象的属性: `.alpha_channel` (别名: `AlphaChannel`)
^           | 使用窗口对象的方法: `.set_alpha()`
总是在顶层  | 创建窗口时设置 `keep_on_top` 参数
^           | 使用窗口对象的方法: `.keep_on_top_set()` 或 `.keep_on_top_clear()`
抓取窗口    | 创建窗口时设置 `grab_anywhere` 参数
^           | 使用窗口对象的方法: `.grab_any_where_on()` 或 `.grab_any_where_off()`
* 注意:
    * 如果取消标题栏, 一定要创建一个 "退出" 按钮

## 6.5. 控件尺寸
* 三种方法:
    * 全局: 使用 `SetOptions` 全局函数
    * Window 级别: 修改 `default_element_size` 参数
    * Element 级别: 每个控件有 `size` 参数

--------------------------------------------------------------------------------
# 7. 鼠标和键盘

## 7.1. 鼠标
* 鼠标样式
    * 窗口对象的 `.set_cursor(cursor)` 方法设置

## 7.2. 键盘和鼠标的捕获
* 编程步骤
    1. 创建窗口对象时, 设置 `return_keyboard_events=True`
    1. 事件循环中处理 `event`
* 示例
    ```Python
    import PySimpleGUI as sg

    # Recipe for getting keys, one at a time as they are released
    # If want to use the space bar, then be sure and disable the "default focus"

    text_elem = sg.Text(size=(18, 1))

    layout = [[sg.Text("Press a key or scroll mouse")],
              [text_elem],
              [sg.Button("OK")]]

    window = sg.Window("Keyboard Test", layout,  return_keyboard_events=True, use_default_focus=False)

    # ---===--- Loop taking in user input --- #
    while True:
        event, value = window.read()

        if event == "OK" or event == sg.WIN_CLOSED:
            print(event, "exiting")
            break
        text_elem.update(event)
    ```




