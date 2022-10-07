# 将地图摄入Carla源代码版本

本节阐述将地图摄入 __Carla源代码版本__ 的过程。如果你正在使用 __CARLA的包(二进制)版本__ 来摄取地图，那么请遵循[这里][package_ingest]的指导内容。

摄入过程涉及将相应的地图文件编译成一个包文件并导入虚幻引擎。然后可以在虚幻引擎编辑器中打开这个包，在生成行人导航前可以定制这个地图包。

[package_ingest]: tuto_M_add_map_package.md

- [__在开始之前__](#before-you-begin)
- [__地图摄入__](#map-ingestion)
- [__下一步__](#next-steps)

---

## 在开始之前

- 确保你使用的是从源代码构建的CARLA版本。如果你使用的是CARLA的打包(二进制)版本，那么请参考[这里][import_map_package]的教程。

- 你应该有至少两个文件，从地图编辑器(如RoadRunner)[生成][rr_generate_map]的`<mapname>.xodr`和`<mapName>.fbx`文件。

- 这些文件的`<mapname>`部分应该相同，以便识别为同个地图。

- 你可以将多个地图摄入到同一个包中。每个地图都应该有一个唯一的名称。

[import_map_package]: tuto_M_add_map_package.md
[rr_generate_map]: tuto_M_generate_map.md

---

## 地图摄入

__1.__ 将需要导入的地图文件放在Carla根目录下的`Import`文件夹。

__2.__ 执行以下命令摄入地图文件：

```sh
make import
```

__注意，有两个可选参数可以设置__:

- 参数`--package=<package_name>`指定包名。默认的包名为`map_package`。两个包不能有相同的名称，因此使用默认值将导致后续摄入错误。__所以强烈建议改变包名__。执行以下命令来使用此标志：

```sh
make import ARGS="--package=<package_name>"
```

- 参数`--no-carla-materials`指定不使用CARLA材质（道路纹理等）。地图将使用RoadRunner的材质。此标志只有在你 __没有提供__[`.json`文件](tuto_M_manual_map_package.md) __才需要__。`.json`文件中的值将覆盖此标志。执行以下命令来使用此标志：

```sh
make import ARGS="--no-carla-materials"
```

在`Unreal/CarlaUE4/Content`中将会创建使用包名命名的文件夹。这个文件夹包含配置文件、overdrive信息、静态资产信息和导航信息。

---

## 下一步

现在你可以在虚幻编辑器中打开你的地图，并使用这个地图进行仿真。你可以在这个步骤中定制地图并且生成行人导航数据。我们建议在所有定制完成之后才生成行人导航，这样就不会有障碍物在行人路径上。

CARLA提供了一些工具和指南来帮助你定制地图：

- [在地图中实现子关卡](tuto_M_custom_layers.md)
- [添加和配置交通灯和交通标志](tuto_M_custom_add_tl.md)
- [使用程序性建筑工具添加建筑](tuto_M_custom_buildings.md)
- [使用道路绘制工具定制道路](tuto_M_custom_road_painter.md)
- [定制天气](tuto_M_custom_weather_landscape.md#weather-customization)
- [使用连续网格定制景观](tuto_M_custom_weather_landscape.md#add-serial-meshes)

完成定制之后，就可以[生成行人导航信息](tuto_M_generate_pedestrian_navigation.md)。

---

如果你对这个过程有任何问题，可以在[论坛](https://github.com/carla-simulator/carla/discussions)中提问。