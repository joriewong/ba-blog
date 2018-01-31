---
  layout: default
  title: Using BizCharts
---

# {{ page.title }}

## Init

![image_1bvlrbbm01pcv105012ipcge1gk1m.png-23.1kB][1]

[demo][2]

### 创建容器

在页面的 body 部分创建一个节点，指定一个 id
```
<div id="mountNode"></div>
```

### 使用组件生成图表

- 引入图表需要的组件
- 用组件组装成需要的图表
- 把图表渲染到 mountNode 节点上

```
import React from 'react';
import ReactDOM from 'react-dom';
import { Chart, Geom, Axis, Tooltip, Legend, Coord } from 'bizcharts';

// 数据源
const data = [
  { genre: 'Sports', sold: 275, income: 2300 },
  { genre: 'Strategy', sold: 115, income: 667 },
  { genre: 'Action', sold: 120, income: 982 },
  { genre: 'Shooter', sold: 350, income: 5271 },
  { genre: 'Other', sold: 150, income: 3710 }
];

// 定义度量
const cols = {
  sold: { alias: '销售量' },
  genre: { alias: '游戏种类' }
};

// 渲染图表
ReactDOM.render((
  <Chart width={600} height={400} source={data} scale={cols}>
      <Axis name="genre" />
      <Axis name="sold" />
      <Legend position="top" dy={-20} />
      <Tooltip />
      <Geom type="interval" position="genre*sold" color="genre" />
    </Chart>
), document.getElementById('mountNode'));
```

## Composition

### component

- 实体组件：在图表上有对应的图形、文本显示。
- 抽象组件：没有显示，是一种概念抽象组件。

#### Chart `实体组件`

图表组件。所有的其他组件都必须由`<Chart>`包裹。

![image_1bvlsoud35mg1ijtv3a1aa118h81g.png-70.9kB][3]

**forceFit[Boolean]**

设置图表的宽度是否自适应，设置为 true，则图表 chart 会继承父元素的宽度，用户设置的 width 则不生效。 默认值: false。

**height[Number]**(必填)

指定图表的高度，默认单位为'px'。

**data[Array/DataSet]**

图表数据源，是一个包含 JSON 对象的数组或者 DataView 对象。 

**scale[Object]**

> (fieldName: string, scaleConfig: object) | (scaleConfig: object) 图表数据源相关的比例尺信息，scaleConfig 可配置属性如下。

```
scale={
  {
    fieldName:'sales',
    //scaleConfig
    {
      type: 'identity' | 'linear' | 'cat' | 'time' | 'timeCat' | 'log' | 'pow', // 指定数据类型
      alias: string, // 数据字段的别名
      formatter: function, // 格式化文本内容
      range: array, // 输出数据的范围，默认[0, 1]，格式为 [min, max]，min 和 max 均为 0 至 1 范围的数据。
      tickCount: number, // 设置坐标轴上刻度点的个数
      ticks: array, // 用于指定坐标轴上刻度点的文本信息，当用户设置了 ticks 就会按照 ticks 的个数和文本来显示
      sync: boolean // 当 chart 存在不同数据源的 view 时，用于统一相同数据属性的值域范围
    }
  }
}
```

**placeholder[String]**

图表source为空时显示的内容。 默认值: <div style={{ position: 'relative', top: '48%', textAlign: 'center' }}>暂无数据</div> ;会在图表区域的中间显示 "暂无数据" 。

**更多属性、方法参考[Chart API doc][4]。**

#### Coord `抽象组件`

坐标系组件。用来描述`<Chart> <View>`组件的坐标系，比如笛卡尔坐标系、极坐标系。

抽象出的2维定位系统，描述数据如何映射到平面。BizCharts包含两种类型坐标系：极坐标系（polar、theta、helix）和笛卡尔坐标系。

- `<Coord>`坐标系组件只作为`<Chart>`或`<View>`的child，同时组件下不能嵌套其他图表组件。
- Coord的定义在一个Chart中是唯一的，但`<View>`中可以有独立坐标系存在。
- 默认采用笛卡尔坐标系，**直角坐标系（rect）**。
- 通过`type`属性设置为极坐标

![image_1bvlucc301ei5nu9kct6eg3ej1t.png-6.9kB][5]

**type[String]**

- rect：直角坐标系；仅支持2维的x、y。
- polar：极坐标系；2维的角度和半径。
- theta：一种特殊的极坐标系，半径固定，将数据映射到角度，常用于饼图的绘制。
- helix：螺旋坐标系，基于阿基米德螺旋线。

**scale[Array]**

放大、缩小，默认按照坐标系中心放大、缩小。 Array:数据长度必须为2，第一个值代表 x 方向缩放比例，第二个值代表 y 方向缩放比例。

```
<Coord scale={[0.7, 1.2]} />
```

![scale.gif-47.8kB][6]


**reflect**['x'|'y']


镜像, 沿 x 方向镜像或者沿 y 轴方向映射。

![reflect.png-8.5kB][7]


**更多属性、方法参考[Coord API doc][8]**


#### Axis `实体组件`


坐标轴组件。通常包含两个坐标轴，在笛卡尔坐标系下，分别为x轴和y轴，在极坐标系下，则分别由角度和半径2个维度构成。每个坐标轴由坐标轴线（line）、刻度线（tickLine）、刻度文本（label）、标题（title）以及网格线（grid）组成。

![image_1bvlvhu9r18i51k6ofv2u4h11f166.png-40.6kB][9]

- `<Axis>`坐标轴组件只可以作为`<Chart>`或`<View>`的child，同时`<Axis>`组件下不能嵌套其他图表组件。
- BizCharts中将Axis抽离为一个单独的组件，不使用则默认不显示坐标轴及相关信息。
- 使用Axis组件时，必须指定当前坐标轴对应数据源中的字段名

```
// 制定坐标轴对应数据源中的字段名
<Chart width={600} height={400} source={data}>
  <Axis name="sold" />
  <Geom type="interval" position="genre*sold" color="genre" />
</Chart>
```

- 一旦使用`<Axis>`组件，那么所有的坐标轴都会显示，如若需要隐藏某一个坐标轴及相关信息，务必将visible参数并置为false

```
// 只显示其中一条坐标轴
<Chart width={600} height={400} source={data}>
  <Axis name="sold" />
  <Axis name="genre" visible={false} />
  <Geom type="interval" position="genre*sold" color="genre" />
</Chart>
```

**更多属性、方法参考[Axis API doc][10]**。

#### Geom `实体组件`

几何标记组件。点、线、面这些几何图形。

![image_1bvm0jccgcul1em81i1t6ucev6j.png-79kB][11]

BizCharts 中并没有特定的图表类型（柱状图、散点图、折线图等）的概念，用户可以单独绘制某一种类型的图表，如饼图，也可以绘制混合图表，比如折线图和柱状图的组合。

- point：点图、折线图中的点
- path：路径图、地图上的路径
- line：折线图、曲线图、阶梯线图、雷达图
- area：区域图（面积图）、层叠区域图、区间区域图、雷达图
- interval：柱状图、直方图、南丁格尔玫瑰图、饼图、条形环图（玉缺图）、漏斗图
- polygon：色块图（像素图）、热力图、地图
- schema：k线图、箱型图
- edge：树图、流程图、关系图
- heatmap：热力图

**type[String]**

几何标记类型。还提供了组合类型。

- pointStack：层叠点图
- pointJitter：扰动点图
- pointDodge：分组点图
- intervalStack：层叠柱状图
- intervalDodge：分组柱状图
- intervalSymmetric：对称柱状图
- areaStack：层叠区域图
- schemaDodge：分组箱型图

**position[String]**

位置属性的映射，属性用`*`连接符。

```
//以下面的语句为例，在 position 属性上，映射了两个属性： cut 和 price，分别表示将 cut 数据值映射至 x 轴坐标点，price 数据值映射至 y 轴坐标点。
<Geom
  position="cut*price"
/>
```

![image_1bvm1i395l6o15uqebh1fik5ij9.png-22.4kB][12]

**color**['field'|['field', colors]|['field', 'color1-color2-colorN']]

- field：对应数据字段名
- colors：数据值映射到指定的颜色值
- color1-color2-colorN：映射连续数据，实现颜色渐变

**shape、size**

类似color属性的配置。

**更多属性、方法参考[Geom API doc][13]**。

```
//代码示例
<Geom color={['price', '#ff0000-#00ff00']}/>
```

#### Legend `实体组件`

图例组件。只可以作为`<Chart />`组件的Child。

![image_1c4llsfnkumipdh1026ngeoad9.png-30.1kB][14]

- shape 属性，会根据不同的 shape 类型生成图例；
- color 属性, 会赋予不同的图例项不同的颜色来区分图形；
- size 属性, 在图例上显示图形的大小。

**position** 'top'|'left'|'right'|'bottom'

图例显示位置。默认值:'right'。

**itemFormatter Function**

用于格式化图例每项的文本显示。

**更多属性、方法参考[Legend API doc][15]**。

#### Label `实体组件`

几何标记的辅助文本组件。必须是`<Geom>`的child。

```
<Geom>
  <Label content='sales' .../>
</Geom>
```

**content**[String|Array:[String, Function]]

指定label上显示的文本内容，可以是数据纬度，也可以自定义。

```
<Label
  content="常量字符串"
  //或者
  content="sales*date"
  //或者
  content={["sales*date", (sales, date)=>{
    return `${data}:${sales}`;
  }]}
/>
```
**formatter[Function]**

格式化显示文本信息。

```
<Label
  content='name'
  formatter={(name, item, index)=>{
    // text 为每条记录 x 属性的值
    // item 为映射后的每条数据记录，是一个对象，可以从里面获取你想要的数据信息
    // index 为每条记录的索引
    var point = item.point; // 每个弧度对应的点
    var percent = point['percent'];
    percent = (percent * 100).toFixed(2) + '%';
    return name + ' ' + percent;
  }}
/>
```

**htmlTemplate[Function]**

自定义html文本。

```
<Label
  content='name'
  htmlTemplate={(text, item, index)=>{
    // text 为每条记录 x 属性的值
    // item 为映射后的每条数据记录，是一个对象，可以从里面获取你想要的数据信息
    // index 为每条记录的索引
    var point = item.point; // 每个弧度对应的点
    var percent = point['percent'];
    percent = (percent * 100).toFixed(2) + '%';
    // 自定义 html 模板
    return '<span class="title" style="display: inline-block;width: 50px;">' + text + '</span><br><span style="color:' + point.color + '">' + percent + '</span>';
    }
  });
chart.render();  }}
/>
```

**更多属性、方法参考[Label API doc][16]**。

#### Tooltip `实体组件`

![image_1bvmamgeke7rbtfpmvenf3rd13.png-39.5kB][17]

![image_1bvmalsle1217q7hqbhkbc1punm.png-9.3kB][18]

提示框组件。

- `<Tooltip>`只可以作为`<Chart>`或`<View>`的child，同时`<Tooltip>`组件下不能嵌套其他图表组件。
- BizCharts中将Tooltip抽离为一个单独的组件，不使用Tooltip组件则默认不显示所有提示信息。

```
<Chart width={600} height={400} data={data}>
  <Tooltip />
  <Geom type="bar" position="genre*sold" color="genre" />
</Chart>
```

**crosshairs[Object]**

```
//可配置值
//geom为 'line', 'area', 'path', 'areaStack 时默认会展示垂直辅助线
//geom为 'interval' 默认会展示矩形背景框
{
  //rect: 矩形框,x: 水平辅助线,y: 垂直辅助线,cross: 十字辅助线。
  type: 'rect' || 'x' || 'y' || 'cross',
  style: {
    lineWidth:2,
    stroke:"#ff0000",
  }
}
```
**containerTpl[String]**

tooltip容器模板，必须包含以下class。

```
<div class="g2-tooltip">
  <!-- tooltip 标题 -->
  <div class="g2-tooltip-title" style="margin:10px 0;"></div>
  <!-- tooltip 内容列表容器 -->
  <ul class="g2-tooltip-list"></ul>
</div>
```

**itemTpl[String]**

tooltip每项记录的模板，这个属性可以格式化tooltip的显示内容。

```
<li data-index={index}>
  <!-- 每项记录的 marker -->
  <span style="background-color:{color};width:8px;height:8px;border-radius:50%;display:inline-block;margin-right:8px;"></span>
  {name}: {value}
</li>
```

**格式化tooltip显示内容**

```
<Chart>
  <Geom
    tooltip={['time*sold', (time, sold) => {
      return {
        //自定义 tooltip 上显示的 title 显示内容等。
        name: 'sold',
        title: 'dddd' + time,
        value: sold
      };
    }]}
  />
</Chart>
```

**更多属性、方法参考[Tooltip API doc][19]**。

#### Guide `辅助标记组件`

**子组件**

- Line：辅助线（可带文本），例如表示平均值或者预期分布的直线
- Image：辅助图片，在图表上添加辅助图片
- Text：辅助文本，指定位置添加文本说明
- Region：辅助框，框选一段图区，设置背景、边框
- Html：辅助html，指定位置添加自定义html，显示自定义信息
- Arc：辅助弧线

不同的辅助标记组件所支持的配置属性不一样，主要差异为坐标位置属性差异。

- Text，Html中使用position
- Line，Region，Image，Arc中使用start、end

**更多属性、方法参考[Guide API doc][20]**。

#### Facet `抽象组件`

分面组件。将一份数据按照某个维度分隔成若干子集，然后创建一个图表的矩阵，将每一个数据子集绘制到图形矩形的窗格中，所有子图采用相同的图表类型。

- 按照指定的维度划分数据集
- 对图表进行排版

![image_1bvmf2bad15ck7gs1g9e1p3p1fch9.png-209.9kB][21]

`<Facet>` 系组件只可以作为 `<Chart>` 组件的child，同时 `<Facet>` 组件下只能嵌套一个返回组件的匿名函数。

```
<Facet type='tree' fields={['cut', 'clarity']}>
        //该匿名函数会转为 `eachView:function`
        {(view, facet)=>{
          view.point()
          .position('carat*price')
          .color('cut')
          .shape('circle')
          .opacity(0.3)
          .size(3); 
        }}
</Facet>
```

**type**['rect'|'list'|'circle'|'tree'|'mirror']

- rect：默认类型，指定2个维度作为行列，形成图表的矩阵
- list：指定一个维度，可以指定一行有几列，超出自动换行
- circle：指定一个维度，沿着圆分布
- tree：指定多个维度，每个维度作为树的一级，展开多层图表
- mirror：指定一个维度，形成镜像图表
- matrix：指定两个维度，形成矩阵分面图表

**fields**[String|Array]

设定数据划分的维度，是数据的字段名，包含多个维度时使用数组传入。

更多属性、方法参考[Facet API doc][22]

#### View `抽象组件`

视图组件。由 Chart 实例生成和管理，拥有自己独立的数据源、坐标系和图层，用于异构数据的可视化以及图表组合。一个 Chart 由一个或者多个视图 View 组成，因此 view 上的属性基本同 chart 基本相同。

- 在同一个容器中出现两个或者更多不同坐标系的图表时，可以采用View组件来实现。
- 同一个容器中的两个图表需要采用不同的数据源时。

**id[String]**

视图的 id 标识，用于唯一标定视图，如果用户不指定，G2 会默认提供一套 id 生成机制（‘view’ + views.length，如 view0, view1, …, viewN)。

更多属性、方法参考[View API doc][23]

### position

![image_1bvlrggu61asdn4krma1s231sth13.png-556.3kB][24]

## Data

图表数据支持两种数据格式：

- JSON数组
- DataView对象

### DataSet

DataSet的目标是为数据可视化场景提供状态驱动（state driven）的、丰富而强大的数据处理能力。

- DataSet（数据集）：一组数据集合
- DataView（数据视图）：单个数据视图，目前有普通二维数据（类似一张数据库表）、树形数据、图数据和地理信息数据几种类型
- state（状态量）：数据集内部流转的控制数据状态的变量
- Transform（变换）：数据变换函数，数据视图做数据处理时使用，包括图布局、数据补全、数据过滤
- Connector（连接器）：数据接入函数，用于把某种数据源（譬如csv）载入到某个数据视图上

### 数据处理

数据处理分为两个大的步骤：数据连接（Connector）和数据转换（Transform）。

![image_1bvtj3rq5jhvobpi01dm4f2p9.png-141.5kB][25]

#### 数据连接（Connector）

数据连接负责导入和归一化数据（例如CSV、GeoJSON）。

#### 数据转换（Transform）

数据转换负责进行各种数据转换操作（例如图布局、数据统计、数据补全等）。

在单个数据视图（DataView）的基础上增加了数据集（DataSet）的概念，通过统一的 DataSet 管理，实现了各个数据视图之间的状态同步和交互。

更多属性、方法参考[DataSet API doc][26]

### 数据流

1. 加载数据
2. 对数据进行分组（默认根据`size`、`shape`、`color`分组）
3. 保存原始数据到属性`_origin`中 
4. 数据数值化（例如分类类型转换为索引值）
5. 归一化操作（数值优化、调整分布范围，均匀分布易于用户理解）
6. 计算绘制图形需要的点
7. 映射至图形属性
8. 渲染绘制

参考[G2 的数据处理流程][27]

## Theme

默认提供两种主题：default、dark。

### 主题切换

使用`setTheme`方法切换主题。

```
 BizCharts.setTheme('dark');
```

### 自定义主题

```
  const seaTheme = {
    animate:false,
    colors:{},
    shapes:{},
  };
  BizCharts.setTheme(seaTheme);
```

[定制参数参考][28]

## Interaction

### 默认交互

- active激活：hover
- select选中：选择、框选

#### 激活

开启以及关闭shape对于hover的响应效果。

```
<Geom active={false} />
<Geom active={true} />
```

#### 选中

- 不可选中
- 单选
- 多选
- 选中是否可取消选中

```
<Geom select={false} />; // 关闭
<Geom select={true} />; // 打开
<Geom select={[true, {
 mode: 'single' || 'multiple', // 选中模式，单选、多选
 style: { }, // 选中后 shape 的样式
 cancelable: true | false, // 选中之后是否允许取消选中，默认允许取消选中
 animate: true | false // 选中是否执行动画，默认执行动画
}]} />;
```

默认饼图支持选中交互，其他Geom的选中模式默认关闭。

## 参考链接

> [BizCharts](https://github.com/alibaba/BizCharts) 


  [1]: http://static.zybuluo.com/wongjorie/wf3d8rzh0e8jyhb3euaqnp3e/image_1bvlrbbm01pcv105012ipcge1gk1m.png
  [2]: https://alibaba.github.io/BizCharts/demo.html
  [3]: http://static.zybuluo.com/wongjorie/sbkafvgrnagrhaseru3px1p3/image_1bvlsoud35mg1ijtv3a1aa118h81g.png
  [4]: https://github.com/joriewong/BizCharts/blob/master/doc/api/chart.md
  [5]: http://static.zybuluo.com/wongjorie/2qomztlzivfvjwykk1euwm23/image_1bvlucc301ei5nu9kct6eg3ej1t.png
  [6]: http://static.zybuluo.com/wongjorie/7qojx3jua2cmv437wfajslcd/scale.gif
  [7]: http://static.zybuluo.com/wongjorie/9qo8s39md5q3f28k4cwjcb2v/reflect.png
  [8]: https://github.com/joriewong/BizCharts/blob/master/doc/api/coord.md
  [9]: http://static.zybuluo.com/wongjorie/8u1ixd45s2uxl6x2x2a8rk12/image_1bvlvhu9r18i51k6ofv2u4h11f166.png
  [10]: https://github.com/joriewong/BizCharts/blob/master/doc/api/axis.md
  [11]: http://static.zybuluo.com/wongjorie/mkg7b30rx243tpdevbx9tb4k/image_1bvm0jccgcul1em81i1t6ucev6j.png
  [12]: http://static.zybuluo.com/wongjorie/n1bwkjbwdyqf3weaqawndb2z/image_1bvm1i395l6o15uqebh1fik5ij9.png
  [13]: https://github.com/joriewong/BizCharts/blob/master/doc/api/geom.md
  [14]: http://static.zybuluo.com/wongjorie/4t550emon136knwy8yw669jl/image_1c4llsfnkumipdh1026ngeoad9.png
  [15]: https://github.com/joriewong/BizCharts/blob/master/doc/api/legend.md
  [16]: https://github.com/joriewong/BizCharts/blob/master/doc/api/label.md
  [17]: http://static.zybuluo.com/wongjorie/53p8mv995011kv7i3lr4jme8/image_1bvmamgeke7rbtfpmvenf3rd13.png
  [18]: http://static.zybuluo.com/wongjorie/20xwmxex720repb5klm6cn22/image_1bvmalsle1217q7hqbhkbc1punm.png
  [19]: https://github.com/joriewong/BizCharts/blob/master/doc/api/tooltip.md
  [20]: https://github.com/joriewong/BizCharts/blob/master/doc/api/guide.md
  [21]: http://static.zybuluo.com/wongjorie/whbweomi100jhfc7j243b65b/image_1bvmf2bad15ck7gs1g9e1p3p1fch9.png
  [22]: https://github.com/joriewong/BizCharts/blob/master/doc/api/facet.md
  [23]: https://github.com/joriewong/BizCharts/blob/master/doc/api/view.md
  [24]: http://static.zybuluo.com/wongjorie/9p2mdnj6bi81dn6xzjoxtpz4/image_1bvlrggu61asdn4krma1s231sth13.png
  [25]: http://static.zybuluo.com/wongjorie/wlb62wzd42cg8rij1tcveic4/image_1bvtj3rq5jhvobpi01dm4f2p9.png
  [26]: https://github.com/joriewong/BizCharts/blob/master/doc/api/dataset.md
  [27]: https://github.com/joriewong/BizCharts/blob/master/doc/tutorial/dataflow.md
  [28]: https://github.com/joriewong/BizCharts/blob/master/doc/api/theme.md

`{{ page.date | date_to_string }},wongjorie`
