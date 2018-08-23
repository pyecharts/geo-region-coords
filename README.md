# 中国五级行政区域坐标

### 数据来源

数据来自 [china_area_mysql](https://github.com/kakuilan/china_area_mysql)，包括省市县镇村 5 个层级（港澳地区的数据只有 3 级，台湾地区 4 级），数据被处理成 json 和 txt 两种格式类型。

### pyecharts 自定义坐标

在 [pyecharts](https://github.com/pyecharts/pyecharts) 中，Geo/Geolines 图需要定义地区坐标，由于全国地区众多且多重名，pyecharts 无法精确度较高的区域坐标。pyecharts 中提供自定义坐标的方式有 4 种：

1. **（推荐）** 使用 `geo_cities_coords` 参数，字典类型，如 {'阿城': [126.58, 45.32],}

    coords.txt
    ```
    "北京": [116.407526, 39.90403],
    "北京东城": [116.416357, 39.928353],
    "北京东城东华门": [116.406708, 39.914219],
    "北京东城东华门多福巷": [116.412747, 39.923014],
    "北京东城东华门银闸": [116.406708, 39.914219],
    "北京东城东华门东厂": [116.406708, 39.914219],
    "北京东城东华门智德": [116.404642, 39.918634],
    "北京东城东华门南池子": [116.40318, 39.907837],
    "北京东城东华门黄图岗": [116.410022, 39.920854],
    "北京东城东华门灯市口": [116.414391, 39.918751],
    ```

    **在 coords.txt 中查找对应关键字,复制到 `geo_cities_coords` 参数即可**

2.  **（推荐）** 使用 `add_coordinate()` 方法提供一个自定义坐标

    本质上 `geo_cities_coords` 内部就是调用 `add_coordinate()` 方法
    ```
    add_coordinate(self, name: six.text_type, longitude: float, latitude: float): -> None

    example:
        add_coordinate("某地", 100.0, 20.0)
    ```

3. **（推荐 V0.5.9+）** 使用 `add_coordinate_json()` 方法提供一个自定义坐标 JSON 文件
    ```
    add_coordinate_json(self, json_file: six.text_type): -> None
 
    example:
        add_coordinate_json("my_coords.json")

    # my_coords.json
    {
        "某地": [100.0, 20.0],
        ...
    }
    ```

4. **（不推荐，这种操作方式一旦 pyecharts 更新，坐标会失效）** *Hack* pyecharts 源代码，对应文件位于 `Lib/site-packages/pyecharts/datasets/city_coordinates.json` 具体路径根据操作系统和 Python 环境而定。

    coords.json
    ```
    [
        {"北京": [116.407526, 39.90403]},
        {"北京东城": [116.416357, 39.928353]},
        {"北京东城东华门": [116.406708, 39.914219]},
        {"北京东城东华门多福巷": [116.412747, 39.923014]},
        {"北京东城东华门银闸": [116.406708, 39.914219]},
        {"北京东城东华门东厂": [116.406708, 39.914219]},
        {"北京东城东华门智德": [116.404642, 39.918634]},
        {"北京东城东华门南池子": [116.40318, 39.907837]},
        {"北京东城东华门黄图岗": [116.410022, 39.920854]},
        {"北京东城东华门灯市口": [116.414391, 39.918751]},
        ...
    ]
    ```

    **在 coords.json 中查找对应关键字，补充到 city_coordinates.json 文件中即可**


### License

MIT [©chenjiandongx](https://github.com/chenjiandongx)
