
**Python 总结: 数据科学 - 可视化**
--------------------------------------------------------------------------------
[返回目录](outline.md)

--------------------------------------------------------------------------------
tips:

--------------------------------------------------------------------------------

<!-- @import "[TOC]" {cmd="toc" depthFrom=1 depthTo=6 orderedList=false} -->

<!-- code_chunk_output -->

- [1. 基本信息](#1-基本信息)
- [2. Plotly](#2-plotly)
    - [2.1. 简介](#21-简介)
    - [2.2. 基本流程](#22-基本流程)
    - [2.3. 详解: 图像](#23-详解-图像)
        - [2.3.1. 图像对象](#231-图像对象)
        - [2.3.2. 创建图像](#232-创建图像)
        - [2.3.3. 创建子图](#233-创建子图)
        - [2.3.4. 显示图像](#234-显示图像)
        - [2.3.5. 保存图片](#235-保存图片)
    - [2.4. 详解: trace](#24-详解-trace)
        - [2.4.1. trace 列表](#241-trace-列表)
        - [2.4.2. 添加轨迹](#242-添加轨迹)
        - [2.4.3. 更新轨迹](#243-更新轨迹)
        - [2.4.4. 轨迹的 marker](#244-轨迹的-marker)
        - [2.4.5. 轨迹的线形](#245-轨迹的线形)
    - [2.5. 详解: Layout](#25-详解-layout)
        - [2.5.1. Layout 属性](#251-layout-属性)
        - [2.5.2. 更新 layout](#252-更新-layout)
        - [2.5.3. 图标题](#253-图标题)
        - [2.5.4. 图注](#254-图注)
        - [2.5.5. 图片尺寸](#255-图片尺寸)
        - [2.5.6. 坐标轴](#256-坐标轴)
        - [2.5.7. Color Axes](#257-color-axes)
        - [2.5.8. 标注](#258-标注)
        - [2.5.9. hover](#259-hover)
        - [2.5.10. shape](#2510-shape)
        - [2.5.11. 图片](#2511-图片)
        - [2.5.12. sliders](#2512-sliders)
        - [2.5.13. updatemenus](#2513-updatemenus)
    - [2.6. 详解: frames](#26-详解-frames)
    - [2.7. Plotly Express](#27-plotly-express)

<!-- /code_chunk_output -->

--------------------------------------------------------------------------------
# 1. 基本信息
* `matplotlib` 最普遍, 最正式, 但 API 复杂
* `plotly` 可产生互动图片, API 简单
    * 导出静态图片需要安装 [Kaleido](https://github.com/plotly/Kaleido) 软件
        ``` shell
        $ pip install -U kaleido
        ```

----------------------------------------------------------------
# 2. Plotly
> [官方文档主页](https://plotly.com/python/), [API 列表](https://plotly.com/python-api-reference/), [属性列表](https://plotly.com/python/reference/)

## 2.1. 简介
* 内部实现过程:
    1. `plotly.py` 创建和更新图像对象 (graph object, GO)
        * 图像对象使用 python dict 保存数据 (`data`, `layout`, `frames`)
    1. `plotly.py` 将 dict 数据转为 json, 然后调用 plotly.js (调用 d3.js) 绘制图像
* 主要有 5 个子模块
    | 子模块                                                                                      | 说明                                 | 常用导入方式                                |
    | ------------------------------------------------------------------------------------------- | ------------------------------------ | ------------------------------------------- |
    | [plotly.express](https://plotly.com/python-api-reference/plotly.express.html)               | 高层接口: 一次性指定 trace 和 layout | `import plotly.express as px`               |
    | [plotly.graph_objects](https://plotly.com/python-api-reference/plotly.graph_objects.html)   | 低层接口: 分别指定 trace 和 layout   | `import plotly.graph_objects as px`         |
    | [plotly.subplots](https://plotly.com/python-api-reference/plotly.subplots.html)             | 子图: 创建子图                       | `from plotly.subplots import make_subplots` |
    | [plotly.figure_factory](https://plotly.com/python-api-reference/plotly.figure_factory.html) | 某些复杂的图                         |
    | [plotly.io](https://plotly.com/python-api-reference/plotly.io.html)                         | 底层显示、渲染器、保存等接口         |

## 2.2. 基本流程
* 一般图片
    1. 创建图像对象: `fig = px.<图像>(...)` 或 `fig = go.Figure(data=..., layout=...)`
    1. 在图像上添加**额外**的 trace: `图像.add_trace(...)`
    1. 更新图像对象的 layout: `图像.update_layout(...)`
    1. 显示图像: `图像.show(...)`
    1. 保存图像: `图像.write_html(...)` 或 `图像.write_image(...)`
* 子图
    1. 创建 "子图" 图像对象: `fig = make_subplots(...)`
    1. 为图像对象添加 trace: `图像.add_trace(...)`
    1. 更新图像对象的 layout: `图像.update_layout(...)`
    1. 显示图像: `图像.show(...)`
    1. 保存图像: `图像.write_html(...)` 或 `图像.write_image(...)`

## 2.3. 详解: 图像

### 2.3.1. 图像对象
* 图像对象的数据包含三个部分, 参见 [官方文档: The Figure Data Structure in Python](https://plotly.com/python/figure-structure/)
    * **data**: 存储 trace 的数据, 包含 `type`, `x`, `y`, ...等属性, 可以是:
        * 单个 trace, 如 `go.Scatter(...), go.Bar(...), ...`,  详见 [trace 列表](#241-trace-列表)
            * 如需添加额外的 trace, 可以使用 `图像.add_trace(...)` 添加
        * trace 列表或元组, 如 `[go.Scatter(...), go.Bar(...)]`, 详见 [trace 列表](#241-trace-列表)
            * 一副图像包含多个 trace
        * 字典列表或元组, 如 `[{"type": "scatter", ...}, {"type": "bar", ...}]`
            * 其中: type 指的是 trace 的类型, 如 `bar, box, heatmap, histogram, ...`
    * **layout**: 存储 [标题](https://plotly.com/python/reference/#layout-title)、[图注](https://plotly.com/python/reference/#layout-showlegend)、[边界](https://plotly.com/python/reference/#layout-margin)、[尺寸](https://plotly.com/python/reference/#layout-autosize)、[字体](https://plotly.com/python/reference/#layout-font)、[颜色](https://plotly.com/python/reference/#layout-paper_bgcolor)、[坐标轴](https://plotly.com/python/reference/#layout-xaxis)、[颜色轴](https://plotly.com/python/reference/#layout-coloraxis)、[标记](https://plotly.com/python/reference/#layout-annotations)、[形状](https://plotly.com/python/reference/#layout-shapes)、[图片](https://plotly.com/python/reference/#layout-images)、[滑块](https://plotly.com/python/reference/#layout-sliders)、[菜单](https://plotly.com/python/reference/#layout-updatemenus) 等数据, 其值可以是
        * 一个 `plotly.graph_objects.Layout` 实例
        * 包含键和值的字典
    * **frames**: 定义动画, 可以是
        * `plotly.graph_objects.Frame` 实例列表或元组
        * 字典列表或元组
    > 示例
    > ``` python
    > import plotly.express as px
    > fig = px.line(x=["a","b","c"], y=[1,3,2], title="sample figure")
    > print(fig)
    > # 输出
    > # Figure({
    > #     'data': [{'hovertemplate': 'x=%{x}<br>y=%{y}<extra></extra>',
    > #               'legendgroup': '',
    > #               'line': {'color': '#636efa', 'dash': 'solid'},
    > #               'marker': {'symbol': 'circle'},
    > #               'mode': 'lines',
    > #               'name': '',
    > #               'orientation': 'v',
    > #               'showlegend': False,
    > #               'type': 'scatter',
    > #               'x': array(['a', 'b', 'c'], dtype=object),
    > #               'xaxis': 'x',
    > #               'y': array([1, 3, 2], dtype=int64),
    > #               'yaxis': 'y'}],
    > #     'layout': {'legend': {'tracegroupgap': 0},
    > #                'template': '...',
    > #                'title': {'text': 'sample figure'},
    > #                'xaxis': {'anchor': 'y', 'domain': [0.0, 1.0], 'title': {'text': 'x'}},
    > #                'yaxis': {'anchor': 'x', 'domain': [0.0, 1.0], 'title': {'text': 'y'}}}
    > # })
    > ```
* 图像的属性
    * 可以用下划线连接快速定位到属性(参见 [官方教程](https://plotly.com/python/creating-and-updating-figures/#magic-underscore-notation)), 例如:
        ``` python
        layout_title_text="Another Graph Object Figure With Magic Underscore Notation"
        # 等效于
        layout=dict(title=dict(text="A Graph Object Figure With Magic Underscore Notation"))
        ```
    * 也可以使用 `.` 方法访问, 如
        ``` python
        fig.layout.title.text = "Using Property Assignment Syntax With A Graph Object Figure"
        ```
* 图像使用归一化位置坐标: 左下角为 (0,0); 右上角为 (1,1)
    > 注意: 这里的坐标不是 trace 的数据点对应的坐标轴的坐标

### 2.3.2. 创建图像
> 参见 [官方教程](https://plotly.com/python/creating-and-updating-figures/)

* 底层方法: 使用底层接口 (`plotly.io`) 接收 python dict 数据,
    - 示例
        ``` python
        import plotly.io as pio
        fig = dict({
            "data": [{"type": "bar",
                        "x": [1, 2, 3],
                        "y": [1, 3, 2]}],
            "layout": {"title": {"text": "A Figure Specified By Python Dictionary"}}
        })
        pio.show(fig)
        ```
* 稍高一层的方法: 使用 `plotly.graph_objects.figure(data=..., layout=..., frames=..., ...)`, 参见  [API](https://plotly.com/python-api-reference/generated/plotly.graph_objects.Figure.html),
    * 其中: `data` 是 trace (详见 [trace 列表](#241-trace-列表)), `layout` 是布局参数, `frames` 是动画相关的参数
    - 示例
        ``` python
        import plotly.graph_objects as go
        fig = go.Figure(
            data=[go.Bar(x=[1, 2, 3], y=[1, 3, 2])],    # trace 列表
            layout=go.Layout(   # layout 对象或字典
                title=go.layout.Title(text="A Figure Specified By A Graph Object")
            )
        )
        fig.show()
        ```
* 更高层的方法: 使用 `plotly.express.图像类(..)`, 详见 [Plotly Express](#26-plotly-express)
    - 示例
        ``` python
        import plotly.express as px
        df = px.data.iris()
        fig = px.scatter(df, x="sepal_width", y="sepal_length", color="species")
        fig.show()
        ```
* 特殊图像 (px 或 go 难以处理的图): 使用 `plotly.figure_factory.图像类(..)`, 参见 [ff 图像列表](https://plotly.com/python-api-reference/plotly.figure_factory.html), [ff 官方教程](https://plotly.com/python/figure-factories/)
    | 图像                       | API                      |
    | :------------------------- | :----------------------- |
    | Dendrograms                | `create_dendrogram`      |
    | Hexagonal Binning Tile Map | `create_hexbin_mapbox`   |
    | Quiver Plots               | `create_quiver`          |
    | Streamline Plots           | `create_streamline`      |
    | Tables                     | `create_table`           |
    | Ternary Contour Plots      | `create_ternary_contour` |
    | Triangulated Surface Plots | `create_trisurf`         |

### 2.3.3. 创建子图
> 参见 [官方教程](https://plotly.com/python/subplots/)
* 创建子图: `plotly.subplots.make_subplots(rows=1, cols=1, shared_xaxes=False, shared_yaxes=False, start_cell='top-left', print_grid=False, horizontal_spacing=None, vertical_spacing=None, subplot_titles=None, column_widths=None, row_heights=None, specs=None, insets=None, column_titles=None, row_titles=None, x_title=None, y_title=None, **kwargs)`, [API](https://plotly.com/python-api-reference/plotly.subplots.html)
    其中
    * 子图标题: `subplot_titles`, `column_titles`, `row_titles` 参数
    * 子图共享坐标: `shared_xaxes`, `shared_yaxes` 参数
    * 子图大小: `column_widths`, `row_heights` 参数, 如: `column_widths=[0.7, 0.3]`
    * 子图间隔: `horizontal_spacing`, `vertical_spacing` 参数
    * 自定义格式: `specs` 参数, 如
        ``` python
        specs=[[{}, {"rowspan": 2}],
               [{}, None],
               [{"rowspan": 2, "colspan": 2}, None],
               [None, None],
               [{}, {}]],
        ```
        ![plotly-marker](/assets/Plotly-specs_examples.png)
        * 使用 `specs` 参数设置子图类型, 参见[官方教程](https://plotly.com/python/graphing-multiple-chart-types/)
            ``` python
            specs=[[{"type": "xy"}, {"type": "polar"}],
                [{"type": "domain"}, {"type": "scene"}]],
            ```
            ![plotly-marker](/assets/Plotly-specs_examples2.png)

### 2.3.4. 显示图像
* plotly 调用 `图像.show(...)` → 调用 `plotly.io.show()` → 调用渲染器绘图
* 图像尺寸, 参见[官方教程](https://plotly.com/python/setting-graph-size/)
    * `图像.show(..., width=..., height=..., ...)`, 参见 [API](https://plotly.com/python-api-reference/generated/plotly.graph_objects.Figure.html#plotly.graph_objects.Figure.show)
        * `width` (int or float, 像素值)
        * `height` (int or float, 像素值)
* 渲染器: 参见[官方教程](https://plotly.com/python/renderers/)
    * 可以通过 `plotly.io.renderers` 查看默认渲染器 和 可用的渲染器, 如:
        ``` python
        import plotly.io as pio
        pio.renderers
        # Renderers configuration
        # -----------------------
        #     Default renderer: 'browser'
        #     Available renderers:
        #         ['plotly_mimetype', 'jupyterlab', 'nteract', 'vscode',
        #         'notebook', 'notebook_connected', 'kaggle', 'azure', 'colab',
        #         'cocalc', 'databricks', 'json', 'png', 'jpeg', 'jpg', 'svg',
        #         'pdf', 'browser', 'firefox', 'chrome', 'chromium', 'iframe',
        #         'iframe_connected', 'sphinx_gallery', 'sphinx_gallery_png']
        ```
    * 可以用 `plotly.io.renderers.default` 查看或设置渲染器
    * 可以利用 `图像.show(renderer=...)` 指定渲染器
    * 可以自定义渲染器
        ``` python
        import plotly.io as pio
        png_renderer = pio.renderers["png"]
        png_renderer.width = 500
        png_renderer.height = 500

        pio.renderers.default = "png"

        import plotly.graph_objects as go
        fig = go.Figure(
            data=[go.Bar(y=[2, 1, 3])],
            layout_title_text="A Figure Displayed with the 'png' Renderer"
        )
        fig.show()
        ```
* 主题和模板, 参见[官方教程](https://plotly.com/python/templates/)
    * 可以通过 `plotly.io.templates` 查看模板信息, 如:
        ``` python
        import plotly.io as pio
        pio.templates
        # Templates configuration
        # -----------------------
        #     Default template: 'plotly'
        #     Available templates:
        #         ['ggplot2', 'seaborn', 'simple_white', 'plotly',
        #         'plotly_white', 'plotly_dark', 'presentation', 'xgridoff',
        #         'ygridoff', 'gridon', 'none']
        ```
    * 可以用 `plotly.io.templates.default` 查看或设置模板
    * 可以在创建 figure 时设置 `template` 参数更改模板, 如:
        ``` python
        fig = px.scatter(..., template="seaborn", ...)
        ```
    * 也可以通过 `update_layout(..)` 更改模板, 如
        ``` python
        fig.update_layout(..., template="seaborn", ...)
        ```
    * 可以自定义模板
* 配置: 参见[官方教程](https://plotly.com/python/configuration-options/)
    * 可以控制图像显示的选项、设置工具条
    * 使用 `.show(config=...)` 配置

### 2.3.5. 保存图片
> 参见[官方文档](https://plotly.com/python/static-image-export/) 和 [底层接口 API](https://plotly.com/python-api-reference/plotly.io.html)
* API
    * `图像.write_image(file, format=None, scale=None, width=None, height=None, validate=True)`, [API](https://plotly.com/python-api-reference/generated/plotly.io.write_image.html)
        * 支持: png, jpeg, WebP, svg, eps, ...
    * `图像.write_html(file, config=None, auto_play=True, include_plotlyjs=True, include_mathjax=False, post_script=None, full_html=True, animation_opts=None, validate=True, default_width='100%', default_height='100%', auto_open=False)`, [API](https://plotly.com/python-api-reference/generated/plotly.io.write_html.html)
* 保存图片的尺寸
    * 参数: `width` (int or float, 像素值)
    * 参数: `height` (int or float, 像素值)

## 2.4. 详解: trace

### 2.4.1. trace 列表
* `plotly.graph_objects.轨迹对象(..)`, 参见 [API 列表](https://plotly.com/python-api-reference/plotly.graph_objects.html)
    * **简单图**: [Scatter](https://plotly.com/python-api-reference/generated/plotly.graph_objects.Scatter.html#plotly.graph_objects.Scatter), `Scattergl`, [Bar](https://plotly.com/python-api-reference/generated/plotly.graph_objects.Bar.html#plotly.graph_objects.Bar), `Pie`, [Heatmap](https://plotly.com/python-api-reference/generated/plotly.graph_objects.Heatmap.html#plotly.graph_objects.Heatmap), `Heatmapgl`, `Image`, `Contour`, `Table`
    * **分布**: `Box`, `Violin`, [Histogram](https://plotly.com/python-api-reference/generated/plotly.graph_objects.Histogram.html#plotly.graph_objects.Histogram), [Histogram2d](https://plotly.com/python-api-reference/generated/plotly.graph_objects.Histogram2d.html#plotly.graph_objects.Histogram2d), `Histogram2dContour`
    * **金融**: `Ohlc`, `Candlestick`, `Waterfall`, `Funnel`, `Funnelarea`, `Indicator`
    * **3D**: [Scatter3d](https://plotly.com/python-api-reference/generated/plotly.graph_objects.Scatter3d.html#plotly.graph_objects.Scatter3d), `Surface`, `Mesh3d`, `Cone`, `Streamtube`, `Volume`, `Isosurface`
    * **地图**: `Scattergeo`, `Choropleth`, `Scattermapbox`, `Choroplethmapbox`, `Densitymapbox`
    * **特殊**: `Scatterpolar`, `Scatterpolargl`, `Barpolar`, `Scatterternary`, `Sunburst`, `Treemap`, `Icicle`, `Sankey`, `Splom`, `Parcats`, `Parcoords`, `Carpet`, `Scattercarpet`, `Contourcarpet`

### 2.4.2. 添加轨迹
* 可以添加到: 现有图像, 空白图像 (使用 `go.Figure()` 或 `make_subplots(...)` 创建)
* `图像.add_trace(trace, row=None, col=None, secondary_y=None)`, [API](https://plotly.com/python-api-reference/generated/plotly.graph_objects.Figure.html#plotly.graph_objects.Figure.add_trace)
* `图像.add_traces(data, rows=None, cols=None, secondary_ys=None)`, [API](https://plotly.com/python-api-reference/generated/plotly.graph_objects.Figure.html#plotly.graph_objects.Figure.add_traces)
* 可直接用 `图像.add_<go图像对象>(..)` 代替 `图像.add_trace(go图像对象...)`, [API 列表](https://plotly.com/python-api-reference/generated/plotly.graph_objects.Figure.html), 例如 `图像.add_bar(..)`
    * 包括: add_annotation, add_bar, add_barpolar, add_box, add_candlestick, add_carpet, add_choropleth, add_choroplethmapbox, add_cone, add_contour, add_contourcarpet, add_densitymapbox, add_funnel, add_funnelarea, add_heatmap, add_heatmapgl, add_histogram, add_histogram2d, add_histogram2dcontour, add_hline, add_hrect, add_icicle, add_image, add_indicator, add_isosurface, add_layout_image, add_mesh3d, add_ohlc, add_parcats, add_parcoords, add_pie, add_pointcloud, add_sankey, add_scatter, add_scatter3d, add_scattercarpet, add_scattergeo, add_scattergl, add_scattersmith, add_scatterternary, add_shape, add_splom, add_streamtube, add_sunburst, add_surface, add_table, add_treemap, add_violin, add_vline, add_volume, add_vrect, add_waterfall

### 2.4.3. 更新轨迹
* `图像.update_traces(patch=None, selector=None, row=None, col=None, secondary_y=None, overwrite=False, **kwargs)`, [API](https://plotly.com/python-api-reference/generated/plotly.graph_objects.Figure.html#plotly.graph_objects.Figure.update_traces)
    * 参数: `overwrite=True` 可以覆盖所有之前的属性
    * 参数: `selector` 可以选择更新那些属性
* 遍历方式更新轨迹: `图像.for_each_trace(..)`, [API](https://plotly.com/python-api-reference/generated/plotly.graph_objects.Figure.html#plotly.graph_objects.Figure.for_each_trace), 如:
    ``` python
    fig.for_each_trace(
        lambda trace: trace.update(marker_symbol="square") if trace.name == "setosa" else (),
    )
    ```

### 2.4.4. 轨迹的 marker
> 参考[官方教程](https://plotly.com/python/marker-style/)
* 设置 trace 时指定 `mode='markers'`, 并设置 `marker={...}`
* [marker 属性](https://plotly.com/python/reference/scatter/#scatter-marker)
    * 样式: `symbol`
        ![plotly-marker](/assets/plotly-marker.png)
    * 外框线: line
    * 尺寸: size, sizemin, sizemode, sizeref,
    * 颜色: cauto, cmax, cmid, cmin, color
    * color bar: `coloraxis`, `colorbar`, `colorscale`, `autocolorscale`, `reversescale`, `showscale`
    * 其他: gradient, maxdisplayed, opacity,
* 更新: `图像.update_traces(marker=dict(...), selector=dict(type='scatter'))`

### 2.4.5. 轨迹的线形
* [line 属性](https://plotly.com/python/reference/scatter/#scatter-line)
    * 线型: [dash](https://plotly.com/python/reference/scatter/#scatter-line-dash), [shape](https://plotly.com/python/reference/scatter/#scatter-line-shape), [width](https://plotly.com/python/reference/scatter/#scatter-line-width)
    * 颜色: color
    * 其他: simplify, smoothing
* 更新: `图像.update_traces(line=dict(...), selector=dict(type='scatter'))`

## 2.5. 详解: Layout

### 2.5.1. Layout 属性
> 参见[属性列表](https://plotly.com/python/reference/#layout)
* Layout 对象是包含各种属性的字典数据
* layout 基本属性
    | 分类        | 属性                                                                                                                                                                                                                                                     |
    | :---------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
    | 标题        | [title](https://plotly.com/python/reference/layout/#layout-title)                                                                                                                                                                                        |
    | 图注        | [legend](https://plotly.com/python/reference/layout/#layout-legend), [showlegend](https://plotly.com/python/reference/layout/#layout-showlegend)                                                                                                         |
    | 尺寸与边界  | [autosize](https://plotly.com/python/reference/#layout-autosize), [width](https://plotly.com/python/reference/#layout-width), [height](https://plotly.com/python/reference/#layout-height), [margin](https://plotly.com/python/reference/#layout-margin) |
    | 字体        | [font](https://plotly.com/python/reference/#layout-font), uniformtext, separators                                                                                                                                                                        |
    | 颜色        | [paper_bgcolor](https://plotly.com/python/reference/#layout-paper_bgcolor), [plot_bgcolor](https://plotly.com/python/reference/#layout-plot_bgcolor),                                                                                                    |
    | 坐标轴相关  | [colorscale](https://plotly.com/python/reference/#layout-colorscale), [colorway](https://plotly.com/python/reference/#layout-colorway), [grid](https://plotly.com/python/reference/layout/#layout-grid), spikedistance                                   |
    | 互动        | hovermode, clickmode, dragmode, selectdirection, hoverdistance, hoverlabel,                                                                                                                                                                              |
    | 形状        | newshape, activeshape                                                                                                                                                                                                                                    |
    | 模板        | [template](https://plotly.com/python/reference/layout/#layout-template)                                                                                                                                                                                  |
    | 条状图      | bargap, bargroupgap, barmode, barnorm                                                                                                                                                                                                                    |
    | 饼图        | extendpiecolors, piecolorway                                                                                                                                                                                                                             |
    | box图       | boxgap, boxgroupgap, boxmode                                                                                                                                                                                                                             |
    | violin图    | violingap, violingroupgap, violinmode                                                                                                                                                                                                                    |
    | 流水账      | waterfallgap, waterfallgroupgap, waterfallmode                                                                                                                                                                                                           |
    | 漏斗图      | funnelgap, funnelgroupgap, funnelmode, extendfunnelareacolors, funnelareacolorway                                                                                                                                                                        |
    | 树状图      | extendtreemapcolors, treemapcolorway                                                                                                                                                                                                                     |
    | sunburst 图 | extendsunburstcolors, sunburstcolorway                                                                                                                                                                                                                   |
    | treemap 图  | extendtreemapcolors, treemapcolorway                                                                                                                                                                                                                     |
    | icicle 图   | extendiciclecolors, iciclecolorway                                                                                                                                                                                                                       |
    | 其他        | autotypenumbers, modebar, transition, datarevision, uirevision, editrevision, selectionrevision, meta, computed, calendar, hidesources, hiddenlabels                                                                                                     |

* layout 中的坐标轴属性
    | 分类   | 属性                                                                                                                                                                                                                                                                                                                                                 |
    | :----- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
    | 坐标轴 | [xaxis](https://plotly.com/python/reference/layout/xaxis/), [yaxis](https://plotly.com/python/reference/layout/yaxis/), ternary, smith, [3D scene](https://plotly.com/python/reference/layout/scene/),  geo, mapbox, [polar](https://plotly.com/python/reference/layout/polar/), [coloraxis](https://plotly.com/python/reference/layout/coloraxis/), |

* layout 中的图层属性
    | 分类     | 属性                                                                           |
    | :------- | ------------------------------------------------------------------------------ |
    | 标注     | [annotations](https://plotly.com/python/reference/layout/annotations/)         |
    | 形状     | [shapes](https://plotly.com/python/reference/layout/shapes/)                   |
    | 图片     | [images](https://plotly.com/python/reference/layout/images/), imagedefaults    |
    | 滑块     | [sliders](https://plotly.com/python/reference/layout/sliders/), sliderdefaults |
    | 更新按钮 | [updatemenus](https://plotly.com/python/reference/layout/updatemenus/)         |

### 2.5.2. 更新 layout
* `图像.update_layout(dict1=None, overwrite=False, **kwargs)`, [API](https://plotly.com/python-api-reference/generated/plotly.graph_objects.Figure.html#plotly.graph_objects.Figure.update_layout)
    * 有多种参数方式, 如
        ``` python
        # 下划线方式
        fig.update_layout(title_text="标题", title_font_size=30)
        # 字典方式
        fig.update_layout(title_text="标题", title_font=dict(size=30))
        fig.update_layout(title=dict(text="标题"), font=dict(size=30))
        # json 方式
        fig.update_layout({"title": {"text": "标题", "font": {"size": 30}}})
        # 函数模式
        fig.update_layout(title=go.layout.Title(text="标题", font=go.layout.title.Font(size=30)))
        ```
    * 设置 `overwrite=True` 属性, 可以覆盖所有全部属性
* 也可以通过属性更改, 如:
    ``` python
    fig = go.Figure(data=go.Bar(x=[1, 2, 3], y=[1, 3, 2]))
    fig.data[0].marker.line.width = 4
    fig.data[0].marker.line.color = "black"
    fig.show()
    ```
* 遍历方式更新
    * for_each_xaxis, for_each_yaxis, for_each_ternary, for_each_smith, for_each_scene, for_each_geo, for_each_mapbox, for_each_polar, for_each_coloraxis
    * for_each_annotation
    * for_each_shape
    * for_each_layout_image

### 2.5.3. 图标题
> 参见 [官方教程](https://plotly.com/python/figure-labels/)
* 参数: [title](https://plotly.com/python/reference/layout/#layout-title)
    * 默认在左上角
    * 主要参数:
        * 文本内容: `text`
        * 字体: `font`(`color`, `family`, `size`),
        * 字间距: `pad`(`t`, `b`, `l`, `r`),
        * 坐标: `x`, `xanchor`, `xref`, `y`, `yanchor`, `yref`

### 2.5.4. 图注
> 参见 [官方教程](https://plotly.com/python/legend/)
* 参数: [showlegend](https://plotly.com/python/reference/layout/#layout-showlegend): 控制是否显示图注
* 参数: [legend](https://plotly.com/python/reference/layout/#layout-legend): 设置图注
    * 主要参数
        * 标题: `title` (`font`, `side`, `text`)
        * 字体: `font`(`color`, `family`, `size`)
        * trace: `tracegroupgap`, `traceorder`
        * 坐标: `x`, `xanchor`, `y`, `yanchor`
        * 排列方向: `orientation`
        * 其他: bgcolor, bordercolor, borderwidth, groupclick, grouptitlefont, itemclick, itemdoubleclick, itemsizing, itemwidth, uirevision, valign
* 使用 `plotly.express` 绘图时, 某些参数 (如 `lables`) 会自动被当作图注
* 使用 `plotly.graph_objects` 添加 trace 时, `name` 会被自动当作图注

### 2.5.5. 图片尺寸
> 参见 [官方教程](https://plotly.com/python/setting-graph-size/)
* 参数: [autosize](https://plotly.com/python/reference/layout/#layout-autosize)
* 参数: [width](https://plotly.com/python/reference/layout/#layout-width)
* 参数: [height](https://plotly.com/python/reference/layout/#layout-height)
* 参数: [margin](https://plotly.com/python/reference/layout/#layout-margin)
    * 主要参数:
        * 边界: `t`, `b`, `l`, `r`
        * 其他: autoexpand, pad
* 参数: automargin
* 使用 `plotly.express` 绘图时, 可直接设置 `width` 和 `height` 等参数

### 2.5.6. 坐标轴
> 参见 [官方教程: axes](https://plotly.com/python/axes/)
* 坐标轴种类
    * [xaxis](https://plotly.com/python/reference/layout/xaxis/), [yaxis](https://plotly.com/python/reference/layout/yaxis/)
    * [ternary](https://plotly.com/python/reference/layout/ternary/), [smith](https://plotly.com/python/reference/layout/smith/), [3D scene](https://plotly.com/python/reference/layout/scene/), [geo](https://plotly.com/python/reference/layout/geo/), [mapbox](https://plotly.com/python/reference/layout/mapbox/), [polar](https://plotly.com/python/reference/layout/polar/), [coloraxis](https://plotly.com/python/reference/layout/coloraxis/)
* 设置方法:
    * 使用 `图像.updata_layout(...)`
    * 直接使用 `图像.update_xaxes(patch=None, selector=None, overwrite=False, row=None, col=None, **kwargs)`, [API](https://plotly.com/python-api-reference/generated/plotly.graph_objects.Figure.html#plotly.graph_objects.Figure.update_xaxes)
    或 `图像.update_yaxes(patch=None, selector=None, overwrite=False, row=None, col=None, secondary_y=None, **kwargs)`, [API](https://plotly.com/python-api-reference/generated/plotly.graph_objects.Figure.html#plotly.graph_objects.Figure.update_yaxes)
* 二维坐标: [xaxis](https://plotly.com/python/reference/layout/xaxis/), [yaxis](https://plotly.com/python/reference/layout/yaxis/) 的主要参数
    * 类型: [type](https://plotly.com/python/reference/layout/xaxis/#layout-xaxis-type) $\in$ {linear, log, date, category, multicategory}
    * 轴标题: [title](https://plotly.com/python/reference/layout/xaxis/#layout-xaxis-title) (`font`, `standoff`, `text`)
    * 范围:
        * [autorange](https://plotly.com/python/reference/layout/xaxis/#layout-xaxis-autorange), [fixedrange](https://plotly.com/python/reference/layout/xaxis/#layout-xaxis-fixedrange)
            * `autorange="reversed"` 可以反转坐标轴
        * [range](https://plotly.com/python/reference/layout/xaxis/#layout-xaxis-range), [rangemode](https://plotly.com/python/reference/layout/xaxis/#layout-xaxis-rangemode)
            * `range=[9, 3]` 也可以反转坐标轴
        * [rangebreaks](https://plotly.com/python/reference/layout/xaxis/#layout-xaxis-rangebreaks) 数组
            * 子参数: bounds, dvalue, enabled, name, pattern, templateitemname, values
        * 其他: rangeselector, rangeslider
    * tick 的相关参数, [官方教程](https://plotly.com/python/tick-formatting/)
        * 如何显示 ticks: [ticks](https://plotly.com/python/reference/layout/xaxis/#layout-xaxis-ticks), [tickson](https://plotly.com/python/reference/layout/xaxis/#layout-xaxis-tickson)
        * tick 数量, 起点, 步进: [nticks](https://plotly.com/python/reference/layout/xaxis/#layout-xaxis-nticks), [tick0](https://plotly.com/python/reference/layout/xaxis/#layout-xaxis-tick0), [dtick](https://plotly.com/python/reference/layout/xaxis/#layout-xaxis-dtick)
        * 模式: [tickmode](https://plotly.com/python/reference/layout/xaxis/#layout-xaxis-tickmode)
            * 如果 tickmode = "auto", tick 依赖 `nticks` 参数
            * 如果 tickmode = "linear", tick 依赖 `tick0` 和 `dtick` 参数
            * 如果 tickmode = "array", tick 依赖 `tickvals` 数组和 `ticktext` 数组, 如
                ``` python
                xaxis = dict(
                    tickmode = 'array',
                    tickvals = [1, 3, 5, 7, 9, 11],
                    ticktext = ['One', 'Three', 'Five', 'Seven', 'Nine', 'Eleven']
                )
                ```
        * tick 标签:
            * `showticklabels`, `showtickprefix`, `showticksuffix`
            * `tickprefix`, `ticksuffix`
            * `ticklabelmode`
            * `ticklabeloverflow`
            * `ticklabelposition`
            * `ticklabelstep`
        * tick 格式: `tickangle`, `tickcolor`, `tickfont`, `tickformat`, `tickformatstops` (`dtickrange`, `enabled`, `name`, `templateitemname`, `value`)
        * 指数显示: [showexponent](https://plotly.com/python/reference/layout/xaxis/#layout-xaxis-showexponent), [exponentformat](https://plotly.com/python/reference/layout/xaxis/#layout-xaxis-exponentformat), [minexponent](https://plotly.com/python/reference/layout/xaxis/#layout-xaxis-minexponent)
        * 其他: `ticklen`, `tickwidth`,
    * 在 tick 之间插入更小的 tick: [minor](https://plotly.com/python/reference/layout/xaxis/#layout-xaxis-minor), 包含以下参数:
        * tick 相关参数: `ticks`, `nticks`, `tick0`, `dtick`, `tickmode`, `tickvals`, `tickcolor`, `ticklen`, `tickwidth`
        * grid 相关参数: `showgrid`, `gridcolor`, `griddash`, `gridwidth`
    * 相关 lines 参数:
        * grid lines: [showgrid](https://plotly.com/python/reference/layout/xaxis/#layout-xaxis-showgrid), [gridcolor](https://plotly.com/python/reference/layout/xaxis/#layout-xaxis-gridcolor), [griddash](https://plotly.com/python/reference/layout/xaxis/#layout-xaxis-griddash), [gridwidth](https://plotly.com/python/reference/layout/xaxis/#layout-xaxis-gridwidth)
        * zero lines: [zeroline](https://plotly.com/python/reference/layout/xaxis/#layout-xaxis-zeroline), [zerolinecolor](https://plotly.com/python/reference/layout/xaxis/#layout-xaxis-zerolinecolor), [zerolinewidth](https://plotly.com/python/reference/layout/xaxis/#layout-xaxis-zerolinewidth)
        * axis lines: [showline](https://plotly.com/python/reference/layout/xaxis/#layout-xaxis-showline), [linecolor](https://plotly.com/python/reference/layout/xaxis/#layout-xaxis-linecolor), [linewidth](https://plotly.com/python/reference/layout/xaxis/#layout-xaxis-linewidth), [mirror](https://plotly.com/python/reference/layout/xaxis/#layout-xaxis-mirror)
    * 缩放: [scaleanchor](https://plotly.com/python/reference/layout/xaxis/#layout-xaxis-scaleanchor), [scaleratio](https://plotly.com/python/reference/layout/xaxis/#layout-xaxis-scaleratio),
    * 其他: ...
* 双/多坐标轴, 参见[官方教程](https://plotly.com/python/multiple-axes/)
    * 方法 1: `图像.add_trace(..., secondary_y=True)`, 将在右侧添加一个 y 轴
    * 方法 2: 设置 trace 时指定 yaxis (如: yaxis="y2"), 然后更新 layout 时设置对应的 y 轴的参数 (如 yaxis2={...}), 如
        ``` python
        import plotly.graph_objects as go

        fig = go.Figure()

        fig.add_trace(go.Scatter(
            x=[1, 2, 3],
            y=[4, 5, 6],
            name="yaxis1 data"
        ))
        fig.add_trace(go.Scatter(
            x=[2, 3, 4],
            y=[40, 50, 60],
            name="yaxis2 data",
            yaxis="y2"
        ))

        fig.update_layout(
            xaxis=dict(domain=[0.3, 0.7]),
            yaxis=dict(
                title="yaxis title",
                titlefont=dict(color="#1f77b4"),
                tickfont=dict(color="#1f77b4")
            ),
            yaxis2=dict(
                title="yaxis2 title",
                titlefont=dict(color="#ff7f0e"),
                tickfont=dict(color="#ff7f0e"),
                anchor="free",
                overlaying="y",
                side="left",
                position=0.15
            ),
        )

        fig.show()
        ```


### 2.5.7. Color Axes
> 参考[官方教程](https://plotly.com/python/colorscales/)
* 显示 color bar
    * 方法 1: `px.图像(..., color=..., ...)` 设置 `color`, `color_discrete_sequence`, `color_discrete_map`, `color_continuous_scale`, `range_color`,  `color_continuous_midpoint` 等参数
    * 方法 2: 部分 `go.图像(...)` 中设置 `marker_color` 参数
    * 方法 3: 部分 `go.图像(...)` 中设置 `coloraxis`, `colorbar`, `colorscale` 等参数
* 更新 color bar
    * 使用 `update_layout(..)` 更改
    * 使用 `update_coloraxes(..)` 更改
    * 使用 `for_each_coloraxis(..)` 更改
* 为子图设置各自的 color bar
    1. 为子图添加 trace 时, 指定每个 trace 的 `coloraxis='coloraxis1'` 或 `coloraxis='coloraxis2'`, ...
    1. 用 `update_layout(..., coloraxis1=..., coloraxis2=..., ...)` 方法更新相应的 coloraxis
<br/>

* plotly 用 [coloraxis](https://plotly.com/python/reference/layout/coloraxis/) 属性管理 colorbar
    * 范围: `cauto`, `cmax`, `cmid`, `cmin`
    * colorscale: [autocolorscale](https://plotly.com/python/reference/layout/coloraxis/#layout-coloraxis-autocolorscale), [colorscale](https://plotly.com/python/reference/#layout-coloraxis-colorscale), [showscale](https://plotly.com/python/reference/#layout-coloraxis-showscale), [reversescale](https://plotly.com/python/reference/#layout-coloraxis-reversescale)
    * [colorbar](https://plotly.com/python/reference/layout/coloraxis/#layout-coloraxis-colorbar)
        * 位置: [x](https://plotly.com/python/reference/layout/coloraxis/#layout-coloraxis-colorbar-x), [xanchor](https://plotly.com/python/reference/layout/coloraxis/#layout-coloraxis-colorbar-xanchor), [xpad](https://plotly.com/python/reference/layout/coloraxis/#layout-coloraxis-colorbar-xpad), [y](https://plotly.com/python/reference/layout/coloraxis/#layout-coloraxis-colorbar-y), [yanchor](https://plotly.com/python/reference/layout/coloraxis/#layout-coloraxis-colorbar-yanchor), [ypad](https://plotly.com/python/reference/layout/coloraxis/#layout-coloraxis-colorbar-ypad)
        * 长度: [len](https://plotly.com/python/reference/layout/coloraxis/#layout-coloraxis-colorbar-len), lenmode,
        * 标题: [title](https://plotly.com/python/reference/layout/coloraxis/#layout-coloraxis-colorbar-title) (`font`, `side`, `text`)
        * tick 的相关参数
            * 如何显示 ticks: [ticks](https://plotly.com/python/reference/layout/coloraxis/#layout-coloraxis-colorbar-ticks)
            * tick 数量, 起点, 步进: [nticks](https://plotly.com/python/reference/layout/coloraxis/#layout-coloraxis-colorbar-nticks), [tick0](https://plotly.com/python/reference/layout/coloraxis/#layout-coloraxis-colorbar-tick0), [dtick](https://plotly.com/python/reference/layout/coloraxis/#layout-coloraxis-colorbar-dtick)
            * 模式: [tickmode](https://plotly.com/python/reference/layout/coloraxis/#layout-coloraxis-colorbar-tickmode)
                * 如果 tickmode = "auto", tick 依赖 `nticks` 参数
                * 如果 tickmode = "linear", tick 依赖 `tick0` 和 `dtick` 参数
            * tick 标签:
                * `showticklabels`, `showtickprefix`, `showticksuffix`
                * `tickprefix`, `ticksuffix`
                * `ticklabeloverflow`
                * `ticklabelposition`
                * `ticklabelstep`
            * tick 格式: `tickangle`, `tickcolor`, `tickfont`, `tickformat`, `tickformatstops` (`dtickrange`, `enabled`, `name`, `templateitemname`, `value`)
            * 显示: `showexponent` `exponentformat`, `minexponent`, `separatethousands`
            * 其他: `ticklen`, `tickwidth`,
        * 样式:
            * bgcolor,
            * bordercolor, borderwidth,
            * thickness, thicknessmode
            * orientation,
            * outlinecolor, outlinewidth,
* 内建的 colorscale
    * [内建连续 colorscales](https://plotly.com/python/builtin-colorscales/)
    * [内建离散 color](https://plotly.com/python/discrete-color/)

### 2.5.8. 标注
> 参见[官方教程](https://plotly.com/python/text-and-annotations/)

* [annotations 属性](https://plotly.com/python/reference/layout/annotations/)
    * 标签: name
    * 文本: align, font, text, textangle
    * 箭头:
        * showarrow,
        * arrowcolor,
        * arrowhead, arrowside, arrowsize, arrowwidth,
        * startarrowhead, startarrowsize
        * ax, axref, ay, ayref, standoff, startstandoff,
    * 坐标:
        * x, xanchor, xclick, xref, xshift,
        * y, yanchor, yclick, yref, yshift
    * 样式:
        * bgcolor
        * bordercolor, borderpad, borderwidth
        * height, width
        * opacity
    * hover: hoverlabel, hovertext,
    * 其他: captureevents, clicktoshow, templateitemname, valign, visible
* 其他属性
    * 某些 trace 支持 `textposition`
    * 某些 trace 支持 `uniformtext`, 设置 `uniformtext_minsize` 属性后, 如果空间不够则不会显示标注
* 添加方法
    * 使用 `图像.add_annotation(...)` 添加, [API](https://plotly.com/python-api-reference/generated/plotly.graph_objects.Figure.html#plotly.graph_objects.Figure.add_annotation)
    * 某些 trace (如 Scatter) 支持 `text` 参数, 可作为标注
* 修改方法:
    * 使用 `图像.update_layout(...)`
    * 使用 `图像.update_annotations(...)`

### 2.5.9. hover
> 参见[官方教程](https://plotly.com/python/hover-text-and-formatting/)

* 所有 trace 默认支持 hover
* 修改 hover 参数:
    * 使用 `图像.update_traces(...)` 修改某些 trace 参数, 如
        * `hover_name`, `hover_data`, `hovertemplate`, `hovertext`, `hoverinfo`
    * 使用 `图像.update_layout(...)` 修改某些 layout 参数, 如:
        * [hovermode](https://plotly.com/python/reference/layout/#layout-hovermode), [hoverdistance](https://plotly.com/python/reference/layout/#layout-hoverdistance), [hoverlabel](https://plotly.com/python/reference/layout/#layout-hoverlabel) (align, bgcolor, bordercolor, font, grouptitlefont, namelength)

### 2.5.10. shape
> 参见[官方教程](https://plotly.com/python/shapes/)

* [shape 属性](https://plotly.com/python/reference/layout/shapes/)
    * 类型:
        * [type](https://plotly.com/python/reference/layout/shapes/#layout-shapes-items-shape-type), 可选列表: "circle" | "rect" | "path" | "line"
        * [path](https://plotly.com/python/reference/layout/shapes/#layout-shapes-items-shape-path)
    * 标签: name, templateitemname
    * 坐标: x0, x1, xanchor, xref, xsizemode, y0, y1, yanchor, yref, ysizemode
    * 样式: fillcolor, fillrule, line (color, dash, width), opacity,
    * 其他: editable, layer, visible

* 添加形状:
    * 使用 `图像.add_shape(...)`, [API](https://plotly.com/python-api-reference/generated/plotly.graph_objects.Figure.html#plotly.graph_objects.Figure.add_shape)
    * 特殊方法, 参见 [官方教程](https://plotly.com/python/horizontal-vertical-shapes/)
        * [.add_hline(...)](https://plotly.com/python-api-reference/generated/plotly.graph_objects.Figure.html), [.add_vline(...)](https://plotly.com/python-api-reference/generated/plotly.graph_objects.Figure.html),
        * [.add_hrect(...)](https://plotly.com/python-api-reference/generated/plotly.graph_objects.Figure.html), [.add_vrect(...)](https://plotly.com/python-api-reference/generated/plotly.graph_objects.Figure.html)
    * 使用 `图像.update_layout(shape=...)`

### 2.5.11. 图片
> 参见[官方教程](https://plotly.com/python/images/)

* [images 属性](https://plotly.com/python/reference/layout/images/)
    * 标签: name, templateitemname
    * 图片源: source
    * 尺寸: sizex, sizey, sizing
    * 坐标: x, xanchor, xref, y, yanchor, yref
    * 样式: opacity,
    * 其他: layer, visible
* 使用 `图像.add_layout_image(...)` 添加, [API](https://plotly.com/python-api-reference/generated/plotly.graph_objects.Figure.html)

### 2.5.12. sliders
* 暂略

### 2.5.13. updatemenus
* 暂略

## 2.6. 详解: frames
> 参见[官方教程](https://plotly.com/python/animations/)


## 2.7. Plotly Express
* 官方教程: 参见[官方教程](https://plotly.com/python/plotly-express/)
    * **Basics**: [scatter](https://plotly.com/python/line-and-scatter/), [line](https://plotly.com/python/line-charts/), `area`, [bar](https://plotly.com/python/bar-charts/), `funnel`, `timeline`
    * **Part-of-Whole**: `pie`, `sunburst`, `treemap`, `icicle`, `funnel_area`
    * **1D Distributions**: [histogram](https://plotly.com/python/histograms/), `box`, `violin`, `strip`, `ecdf`
    * **2D Distributions**: [density_heatmap](https://plotly.com/python/2D-Histogram/), `density_contour`
    * **3-Dimensional**: `scatter_3d`, `line_3d`
    * **Matrix or Image Input**: [imshow](https://plotly.com/python/imshow/)
    * **Multidimensional**: `scatter_matrix`, `parallel_coordinates`, `parallel_categories`
    * **Tile Maps**: `scatter_mapbox`, `line_mapbox`, `choropleth_mapbox`, `density_mapbox`
    * **Outline Maps**: `scatter_geo`, `line_geo`, `choropleth`
    * **Polar Charts**: `scatter_polar`, `line_polar`, `bar_polar`
    * **Ternary Charts**: `scatter_ternary`, `line_ternary`
* [API 列表](https://plotly.com/python-api-reference/plotly.express.html)
    * **Basics**: [scatter](https://plotly.com/python-api-reference/generated/plotly.express.scatter.html#plotly.express.scatter), [line](https://plotly.com/python-api-reference/generated/plotly.express.line.html#plotly.express.line), `area`, [bar](https://plotly.com/python-api-reference/generated/plotly.express.bar.html#plotly.express.bar), `funnel`, `timeline`
    * **Part-of-Whole**: `pie`, `sunburst`, `treemap`, `icicle`, `funnel_area`
    * **1D Distributions**: [histogram](https://plotly.com/python-api-reference/generated/plotly.express.histogram.html#plotly.express.histogram), `box`, `violin`, `strip`, `ecdf`
    * **2D Distributions**: [density_heatmap](https://plotly.com/python-api-reference/generated/plotly.express.density_heatmap.html#plotly.express.density_heatmap), `density_contour`
    * **3-Dimensional**: `scatter_3d`, `line_3d`
    * **Matrix or Image Input**: [imshow](https://plotly.com/python-api-reference/generated/plotly.express.imshow.html#plotly.express.imshow)
        * 如果需要纵坐标自下而上, 需设置参数 `origin='lower'`
    * **Multidimensional**: `scatter_matrix`, `parallel_coordinates`, `parallel_categories`
    * **Tile Maps**: `scatter_mapbox`, `line_mapbox`, `choropleth_mapbox`, `density_mapbox`
    * **Outline Maps**: `scatter_geo`, `line_geo`, `choropleth`
    * **Polar Charts**: `scatter_polar`, `line_polar`, `bar_polar`
    * **Ternary Charts**: `scatter_ternary`, `line_ternary`
* px 参数, 参见[官方教程](https://plotly.com/python/px-arguments/)
* px 样式, 参见[官方教程](https://plotly.com/python/styling-plotly-express/)
* px 表格, 参见[官方教程](https://plotly.com/python/wide-form/)

--------------------------------------------------------------------------------