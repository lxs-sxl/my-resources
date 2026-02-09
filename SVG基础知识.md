

## 一、SVG 简介

​	SVG 意为可缩放矢量图形（Scalable Vector Graphics）。SVG 是一种用于描述二维图形的 XML 标记语言，与位图图像不同，SVG图像以文本形式存储，并且可以缩放到任意大小而不会失真，因为它们基于数学描述而不是像素。

​	SVG 图形是可伸缩的，无需分辨率依赖，这意味着它们可以在不失真的情况下被放大或缩小。SVG 广泛应用于网页设计、图标制作、数据可视化和其他图形相关的领域。

## 二、SVG基本语法

​	SVG 文档由一个或多个 SVG 元素组成，它们定义了图形的内容和属性。

```
<svg
  width="200"     <!-- 指定SVG画布的宽度 -->
  height="200"    <!-- 指定SVG画布的高度 -->
  xmlns="http://www.w3.org/2000/svg">   <!-- 指定SVG命名空间 -->
  <!-- SVG图形内容 -->
</svg>
```

- `width` 和 `height` 属性定义了SVG画布的宽度和高度。
- `xmlns` 属性指定 SVG 文档的 XML 命名空间。

​	SVG 提供了一系列的图形元素来绘制各种形状的图形，如矩形、圆形、直线、多边形等。

### 2.1 基本图形

#### 2.1.1.矩形（Rectangles）

​	使用 `<rect>` 元素绘制矩形，可以指定矩形的位置、大小、圆角等属性。

```
<rect x="50" y="50" width="100" height="50" rx="10" ry="10" fill="blue" />
```

#### 2.1.2.圆形（Circles）

​	使用 `<circle>` 元素绘制圆形，可以指定圆心坐标和半径。

```
<circle cx="100" cy="100" r="50" fill="red" />
```

#### 2.1.3.椭圆（Ellipses）

​	使用 `<ellipse>` 元素绘制椭圆，可以指定椭圆的中心坐标和长短轴的半径。

```
<ellipse cx="100" cy="100" rx="80" ry="50" fill="green" />
```

#### 2.1.4.直线（Lines）

​	使用 `<line>` 元素绘制直线，需要指定起点和终点坐标。

```
<line x1="50" y1="50" x2="150" y2="150" stroke="black" stroke-width="2" />
```

#### 2.1.5.多边形（Polygons）

​	使用 `<polygon>` 元素绘制多边形，需要指定多个顶点的坐标。

```
<polygon points="100,50 150,150 50,150" fill="orange" />
```

#### 2.1.6.折线（Polylines）

​	使用 `<polyline>` 元素绘制折线，需要指定多个点的坐标。

```
<polyline points="100,50 150,150 50,150" fill="none" stroke="blue" stroke-width="2" />
```

#### 2.1.7.路径（Paths）

​	使用 `<path>` 元素绘制路径，可以通过指定一系列的路径命令来绘制各种形状。

```
<path d="M10 10 L90 10 L90 90 Z" fill="none" stroke="black" stroke-width="2" />
```

### 2.2 渐变和填充

​	使用 `<linearGradient>` 或 `<radialGradient>` 定义渐变。

​	使用 `fill` 和 `stroke` 属性指定填充和描边样式。

### 2.3 文本和字体

​	使用 `<text>` 元素插入文本。

​	使用 `font-family`、`font-size` 等属性控制文本样式。

### 2.4 元素属性

​	SVG元素可以具有各种属性，用于指定图形的位置、大小、颜色等特性。

```
<circle
  cx="100"       <!-- 圆心的x坐标 -->
  cy="100"       <!-- 圆心的y坐标 -->
  r="50"         <!-- 圆的半径 -->
  fill="red"     <!-- 填充颜色 -->
  stroke="black" <!-- 描边颜色 -->
  stroke-width="2" <!-- 描边宽度 -->
/>
```

- `cx` 和 `cy` 属性定义了圆心的x和y坐标。
- `r` 属性定义了圆的半径。
- `fill` 属性定义了填充颜色。
- `stroke` 属性定义了描边颜色。
- `stroke-width` 属性定义了描边宽度。

### 2.5 嵌套和分组

SVG 元素可以嵌套和分组，以便更好地组织和管理图形元素。

```
<g id="group1">   <!-- 定义一个分组 -->
  <!-- 分组内的图形元素 -->
  <rect x="10" y="10" width="50" height="50" />
  <circle cx="100" cy="100" r="30" />
</g>
```

- `<g>` 元素用于创建一个分组。
- `id` 属性用于为分组指定一个唯一的标识符。

### 2.6 示例

```
<svg width="200" height="200" xmlns="http://www.w3.org/2000/svg">
  <circle cx="100" cy="100" r="80" fill="blue" />
</svg>
```

<svg width="200" height="200" xmlns="http://www.w3.org/2000/svg">
  <circle cx="100" cy="100" r="80" fill="blue" />
</svg>

## 三、引入SVG

### 3.1 使用`<img>`标签

​	通过 `<img>` 标签可以将 SVG 图像作为图片嵌入到 HTML 页面中，可以使用 src 属性指定 SVG 文件的路径，也可以设置 width 和 height 属性来指定图片的宽度和高度。

```
<img src="example.svg" alt="SVG Image" width="200" height="200">
```

### 3.2 使用 `<object>` 标签

​	`<object>` 标签用于将外部资源嵌入到HTML页面中，可以使用 `data` 属性指定 SVG 文件的路径，`type` 属性指定资源的 MIME 类型。

​	支持 SVG 的浏览器会直接显示 SVG 图像，不支持的浏览器会显示替代内容。

```
<object data="example.svg" type="image/svg+xml" width="200" height="200">
  Your browser does not support SVG
</object>
```

### 3.3 使用 `<iframe>` 标签

​	`<iframe>`标签用于在 HTML 页面中嵌入另一个HTML文档。可以使用 `src` 属性指定 SVG 文件的路径，并设置 `width` 和 `height` 属性来指定 iframe 的宽度和高度。

```
<iframe src="example.svg" width="200" height="200"></iframe>
```

### 3.4 直接嵌入代码

​	在 HTML 页面中直接嵌入 SVG 代码，SVG 代码可以放置在 `<body>` 标签中或其他合适的位置。这种方式使得 SVG 图像与 HTML 内容混合在一起，可以直接在 HTML 页面中编辑和调整 SVG 图像。

```
<svg xmlns="http://www.w3.org/2000/svg" version="1.1">
   <circle cx="100" cy="50" r="40" stroke="black" stroke-width="2" fill="red" />
</svg>
```

## 四、矩形（Rectangles）

​	SVG中的 `<rect>` 元素用于绘制矩形，是 SVG 中常用的基本形状之一，它允许你绘制矩形，并可以通过设置属性来控制矩形的位置、大小、圆角等样式。

```
<rect
  x="x-coordinate"        <!-- 矩形左上角的 x 坐标 -->
  y="y-coordinate"        <!-- 矩形左上角的 y 坐标 -->
  width="width-value"     <!-- 矩形的宽度 -->
  height="height-value"   <!-- 矩形的高度 -->
  rx="rx-value"           <!-- 矩形的圆角半径（水平方向） -->
  ry="ry-value"           <!-- 矩形的圆角半径（垂直方向） -->
  fill="fill-color"       <!-- 矩形的填充颜色 -->
  stroke="stroke-color"   <!-- 矩形的描边颜色 -->
  stroke-width="width-value" <!-- 矩形的描边宽度 -->
/>
```

- `x` 和 `y` 属性指定了矩形左上角的坐标，即矩形的起始点。
- `width` 和 `height` 属性定义了矩形的宽度和高度。
- `rx` 和 `ry` 属性用于指定矩形的圆角半径。如果只设置 `rx`，则所有角的圆角半径都相同；如果同时设置 `rx` 和 `ry`，则可以分别指定水平和垂直方向的圆角半径。
- `fill` 属性定义了矩形的填充颜色。
- `stroke` 属性定义了矩形的描边颜色。
- `stroke-width` 属性定义了矩形的描边宽度。

```
<svg xmlns="http://www.w3.org/2000/svg" version="1.1">
 
<rect x="50" y="20" rx="20" ry="20" width="150"
height="150"
  style="fill:red;stroke:black;stroke-width:5;opacity:0.5"/>
</svg>
```

<svg xmlns="http://www.w3.org/2000/svg" version="1.1">
<rect x="50" y="20" rx="20" ry="20" width="150"
height="150"
  style="fill:red;stroke:black;stroke-width:5;opacity:0.5"/>
</svg>

## 五、圆形（Circles）

​	SVG 中的 `<circle>` 元素用于绘制圆形，它是SVG中常用的基本形状之一。使用 `<circle>` 元素可以创建圆形的图形，并可以通过设置属性来控制圆形的位置、大小和样式。

```
<circle
  cx="x-coordinate"      <!-- 圆心的 x 坐标 -->
  cy="y-coordinate"      <!-- 圆心的 y 坐标 -->
  r="radius"             <!-- 圆的半径 -->
  fill="fill-color"      <!-- 圆的填充颜色 -->
  stroke="stroke-color"  <!-- 圆的描边颜色 -->
  stroke-width="width"   <!-- 圆的描边宽度 -->
/>
```

- `cx` 和 `cy` 属性定义了圆心的坐标，即圆的中心点的位置。

- `r` 属性定义了圆的半径，以确定圆的大小。

- `fill` 属性定义了圆的填充颜色。

- `stroke` 属性定义了圆的描边颜色。

- `stroke-width` 属性定义了圆的描边宽度。

- ```
  <svg xmlns="http://www.w3.org/2000/svg" version="1.1">
  <circle cx="100" cy="50" r="40" stroke="black" stroke-width="2" fill="red"/></svg>
  ```

  <svg xmlns="http://www.w3.org/2000/svg" version="1.1"><circle cx="100" cy="50" r="40" stroke="black"stroke-width="2" fill="red"/>
  </svg>

## 六、椭圆（Ellipses）

​	SVG 中的 `<ellipse>` 元素用于绘制椭圆形，它是SVG中常用的基本形状之一。使用 `<ellipse>` 元素可以创建椭圆形的图形，并可以通过设置属性来控制椭圆的位置、大小和样式。

```
<ellipse
  cx="x-coordinate"      <!-- 椭圆中心点的 x 坐标 -->
  cy="y-coordinate"      <!-- 椭圆中心点的 y 坐标 -->
  rx="x-radius"          <!-- 椭圆水平轴的半径 -->
  ry="y-radius"          <!-- 椭圆垂直轴的半径 -->
  fill="fill-color"      <!-- 椭圆的填充颜色 -->
  stroke="stroke-color"  <!-- 椭圆的描边颜色 -->
  stroke-width="width"   <!-- 椭圆的描边宽度 -->
/>
```

- `cx` 和 `cy` 属性定义了椭圆的中心点坐标，即椭圆的中心位置。

- `rx` 属性定义了椭圆水平轴（x轴）的半径。

- `ry` 属性定义了椭圆垂直轴（y轴）的半径。

- `fill` 属性定义了椭圆的填充颜色。

- `stroke` 属性定义了椭圆的描边颜色。

- `stroke-width` 属性定义了椭圆的描边宽度。

  

椭圆与圆很相似，不同之处在于椭圆有不同的 x 和 y 半径，而圆的 x 和 y 半径是相同的。

```
<svg xmlns="http://www.w3.org/2000/svg" version="1.1">
  <ellipse cx="300" cy="80" rx="100" ry="50"
  style="fill:yellow;stroke:purple;stroke-width:2"/>
</svg>
```

<svg xmlns="http://www.w3.org/2000/svg" version="1.1">
  <ellipse cx="300" cy="80" rx="100" ry="50"
  style="fill:yellow;stroke:purple;stroke-width:2"/>
</svg>

## 七、直线（Lines）

​	SVG 中的 `<line>` 元素用于绘制直线，它是 SVG 中常用的基本形状之一。使用 `<line>` 元素可以创建两个点之间的直线，并可以通过设置属性来控制直线的位置、长度和样式。

```
<line
  x1="x1-coordinate"     <!-- 起点的 x 坐标 -->
  y1="y1-coordinate"     <!-- 起点的 y 坐标 -->
  x2="x2-coordinate"     <!-- 终点的 x 坐标 -->
  y2="y2-coordinate"     <!-- 终点的 y 坐标 -->
  stroke="stroke-color"  <!-- 直线的颜色 -->
  stroke-width="width"   <!-- 直线的宽度 -->
/>
```

- `x1` 和 `y1` 属性定义了直线的起点x、y坐标。
- `x2` 和 `y2` 属性定义了直线的终点x、y坐标。
- `stroke` 属性定义了直线的颜色。
- `stroke-width` 属性定义了直线的宽度。

```
<svg xmlns="http://www.w3.org/2000/svg" version="1.1">
 
<line x1="0" y1="0" x2="200" y2="200"
 
style="stroke:rgb(255,0,0);stroke-width:2"/>
</svg>
```

<svg xmlns="http://www.w3.org/2000/svg" version="1.1"><line x1="0" y1="0" x2="200" y2="200"style="stroke:rgb(255,0,0);stroke-width:2"/>
</svg>
## 八、多边形（Polygons）

​	SVG 中的 `<polygon>` 元素用于绘制多边形，它是 SVG 中常用的基本形状之一。使用 `<polygon>` 元素可以创建闭合的多边形，并可以通过设置属性来控制多边形的顶点坐标、填充颜色、边框颜色等。

```
<polygon
  points="x1,y1 x2,y2 x3,y3 ..."   <!-- 多边形各个顶点的坐标 -->
  fill="fill-color"                <!-- 多边形的填充颜色 -->
  stroke="stroke-color"            <!-- 多边形的边框颜色 -->
  stroke-width="width"             <!-- 多边形的边框宽度 -->
/>
```

- `points` 属性定义了多边形各个顶点的坐标，多个顶点的坐标以空格或逗号分隔，并且每对坐标使用逗号分隔。
- `fill` 属性定义了多边形的填充颜色。
- `stroke` 属性定义了多边形的边框颜色。
- `stroke-width` 属性定义了多边形的边框宽度。

```
<svg  height="210" width="500">
  <polygon points="200,10 250,190 160,210"
  style="fill:lime;stroke:purple;stroke-width:1"/>
</svg>
```

<svg  height="210" width="500">
  <polygon points="200,10 250,190 160,210"
  style="fill:lime;stroke:purple;stroke-width:1"/>
</svg>

## 九、折线（Polylines）

​	SVG 中的 `<polyline>` 元素用于绘制多段线，它是 SVG 中常用的基本形状之一。与 `<polygon>` 元素不同， `<polyline>` 绘制的线条是未封闭的，即起点和终点不会自动连接。使用 `<polyline>` 元素可以创建多个连接的线段，并可以通过设置属性来控制线段的顶点坐标、填充颜色、边框颜色等。

```
<polyline
  points="x1,y1 x2,y2 x3,y3 ..."   <!-- 多段线各个顶点的坐标 -->
  fill="none"                      <!-- 多段线的填充颜色，使用 "none" 表示不填充 -->
  stroke="stroke-color"            <!-- 多段线的边框颜色 -->
  stroke-width="width"             <!-- 多段线的边框宽度 -->
/>
```

- `points` 属性定义了多段线各个顶点的坐标，多个顶点的坐标以空格或逗号分隔，并且每对坐标使用逗号分隔。
- `fill` 属性用于定义多段线的填充颜色，通常设置为 "none" 表示不填充。
- `stroke` 属性定义了多段线的边框颜色。
- `stroke-width` 属性定义了多段线的边框宽度。

```
<svg xmlns="http://www.w3.org/2000/svg" version="1.1">
  <polyline points="20,20 40,25 60,40 80,120 120,140 200,180"
  style="fill:none;stroke:black;stroke-width:3" />
</svg>
```

<svg xmlns="http://www.w3.org/2000/svg" version="1.1">
  <polyline points="20,20 40,25 60,40 80,120 120,140 200,180"
  style="fill:none;stroke:black;stroke-width:3" />
</svg>

## 十、路径（Paths）

​	SVG 中的 `<path>` 元素用于创建路径，它是 SVG 中最强大和最灵活的基本形状之一。使用 `<path>` 元素可以绘制直线、曲线、弧线等各种复杂的图形，并且可以通过设置路径命令来控制路径的形状和样式。

```
<path
  d="path-data"            <!-- 定义路径的路径数据 -->
  fill="fill-color"        <!-- 路径的填充颜色 -->
  stroke="stroke-color"    <!-- 路径的描边颜色 -->
  stroke-width="width"     <!-- 路径的描边宽度 -->
/>
```

- `d` 属性定义了路径的路径数据，即路径命令序列。路径数据由一系列的路径命令组成，每个路径命令以字母开头，后面跟随一组数字参数。常用的路径命令包括：M（移动到）、L（直线到）、H（水平线到）、V（垂直线到）、C（三次贝塞尔曲线）、S（光滑曲线）、Q（二次贝塞尔曲线）、T（光滑二次贝塞尔曲线）、A（圆弧）、Z（闭合路径）等。
- `fill` 属性定义了路径的填充颜色。
- `stroke` 属性定义了路径的描边颜色。
- `stroke-width` 属性定义了路径的描边宽度。

```
<svg xmlns="http://www.w3.org/2000/svg" version="1.1">
  <path id="lineAB" d="M 100 350 l 150 -300" stroke="red"
  stroke-width="3" fill="none" />
  <path id="lineBC" d="M 250 50 l 150 300" stroke="red"
  stroke-width="3" fill="none" />
  <path d="M 175 200 l 150 0" stroke="green" stroke-width="3"
  fill="none" />
  <path d="M 100 350 q 150 -300 300 0" stroke="blue"
  stroke-width="5" fill="none" />
  <!-- Mark relevant points -->
  <g stroke="black" stroke-width="3" fill="black">
    <circle id="pointA" cx="100" cy="350" r="3" />
    <circle id="pointB" cx="250" cy="50" r="3" />
    <circle id="pointC" cx="400" cy="350" r="3" />
  </g>
  <!-- Label the points -->
  <g font-size="30" font="sans-serif" fill="black" stroke="none"
  text-anchor="middle">
    <text x="100" y="350" dx="-30">A</text>
    <text x="250" y="50" dy="-10">B</text>
    <text x="400" y="350" dx="30">C</text>
  </g>
</svg>
```

<svg xmlns="http://www.w3.org/2000/svg" version="1.1">
  <path id="lineAB" d="M 100 350 l 150 -300" stroke="red"
  stroke-width="3" fill="none" />
  <path id="lineBC" d="M 250 50 l 150 300" stroke="red"
  stroke-width="3" fill="none" />
  <path d="M 175 200 l 150 0" stroke="green" stroke-width="3"
  fill="none" />
  <path d="M 100 350 q 150 -300 300 0" stroke="blue"
  stroke-width="5" fill="none" />
  <!-- Mark relevant points -->
  <g stroke="black" stroke-width="3" fill="black">
    <circle id="pointA" cx="100" cy="350" r="3" />
    <circle id="pointB" cx="250" cy="50" r="3" />
    <circle id="pointC" cx="400" cy="350" r="3" />
  </g>
  <!-- Label the points -->
  <g font-size="30" font="sans-serif" fill="black" stroke="none"
  text-anchor="middle">
    <text x="100" y="350" dx="-30">A</text>
    <text x="250" y="50" dy="-10">B</text>
    <text x="400" y="350" dx="30">C</text>
  </g>
</svg>

## 十一、文本（Text）

​	SVG 中的 `<text>` 元素用于在 SVG 图像中添加文本内容，它允许你在指定的位置显示文本，并可以通过设置属性来控制文本的样式、字体、大小等。

```
<text
  x="x-coordinate"          <!-- 文本左上角的 x 坐标 -->
  y="y-coordinate"          <!-- 文本左上角的 y 坐标 -->
  font-family="font"        <!-- 字体名称 -->
  font-size="size"          <!-- 字体大小 -->
  fill="fill-color"         <!-- 文本颜色 -->
  text-anchor="anchor"      <!-- 文本锚点 -->
>
  Text content              <!-- 文本内容 -->
</text>
```

- `x` 和 `y` 属性定义了文本左上角的坐标，即文本的起始点位置。
- `font-family` 属性定义了文本的字体名称，可以是系统字体或自定义字体。
- `font-size` 属性定义了文本的字体大小，以像素为单位。
- `fill` 属性定义了文本的颜色。
- `text-anchor` 属性定义了文本锚点，即文本相对于指定坐标的对齐方式，常用取值有 "start"（默认，左对齐）、"middle"（居中对齐）和 "end"（右对齐）。

```
<svg width="200" height="200" xmlns="http://www.w3.org/2000/svg">
  <text x="100" y="100" font-family="Arial" font-size="20" fill="blue" text-anchor="middle">Hello, SVG!</text>
</svg>
```

<svg width="200" height="200" xmlns="http://www.w3.org/2000/svg">
  <text x="100" y="100" font-family="Arial" font-size="20" fill="blue" text-anchor="middle">Hello, SVG!</text>
</svg>

## 十二、Stroke 属性

​	SVG 中的 `stroke` 属性用于定义图形元素的描边（边框）颜色，它可以应用于任何具有轮廓的图形元素，如 `<rect>`、`<circle>`、`<path>` 等。

- `stroke` 属性定义了图形元素的描边颜色，可以使用颜色名称、十六进制颜色值、RGB值、RGBA值等来表示颜色。
- 如果不想显示描边，可以将 `stroke` 属性设置为 "none"。

​	SVG 提供了一个范围广泛 stroke 属性。

- stroke
- stroke-width
- stroke-linecap
- stroke-dasharray

```
<svg xmlns="http://www.w3.org/2000/svg" version="1.1">
  <g fill="none">
    <path stroke="red" d="M5 20 l215 0" />
    <path stroke="blue" d="M5 40 l215 0" />
    <path stroke="black" d="M5 60 l215 0" />
  </g>
</svg>
```

<svg xmlns="http://www.w3.org/2000/svg" version="1.1">
  <g fill="none">
    <path stroke="red" d="M5 20 l215 0" />
    <path stroke="blue" d="M5 40 l215 0" />
    <path stroke="black" d="M5 60 l215 0" />
  </g>
</svg>

### 1. stroke-width 属性

```
<svg xmlns="http://www.w3.org/2000/svg" version="1.1">
  <g fill="none" stroke="black">
    <path stroke-width="2" d="M5 20 l215 0" />
    <path stroke-width="4" d="M5 40 l215 0" />
    <path stroke-width="6" d="M5 60 l215 0" />
  </g>
</svg>
```

<svg xmlns="http://www.w3.org/2000/svg" version="1.1">
  <g fill="none" stroke="black">
    <path stroke-width="2" d="M5 20 l215 0" />
    <path stroke-width="4" d="M5 40 l215 0" />
    <path stroke-width="6" d="M5 60 l215 0" />
  </g>
</svg>

### 2. stroke-linecap 属性

```
<svg xmlns="http://www.w3.org/2000/svg" version="1.1">
  <g fill="none" stroke="black" stroke-width="6">
    <path stroke-linecap="butt" d="M5 20 l215 0" />
    <path stroke-linecap="round" d="M5 40 l215 0" />
    <path stroke-linecap="square" d="M5 60 l215 0" />
  </g>
</svg>
```

<svg xmlns="http://www.w3.org/2000/svg" version="1.1">
  <g fill="none" stroke="black" stroke-width="6">
    <path stroke-linecap="butt" d="M5 20 l215 0" />
    <path stroke-linecap="round" d="M5 40 l215 0" />
    <path stroke-linecap="square" d="M5 60 l215 0" />
  </g>
</svg>

### 3. stroke-dasharray 属性

```
<svg xmlns="http://www.w3.org/2000/svg" version="1.1">
  <g fill="none" stroke="black" stroke-width="4">
    <path stroke-dasharray="5,5" d="M5 20 l215 0" />
    <path stroke-dasharray="10,10" d="M5 40 l215 0" />
    <path stroke-dasharray="20,10,5,5,5,10" d="M5 60 l215 0" />
  </g>
</svg>
```

<svg xmlns="http://www.w3.org/2000/svg" version="1.1">
  <g fill="none" stroke="black" stroke-width="4">
    <path stroke-dasharray="5,5" d="M5 20 l215 0" />
    <path stroke-dasharray="10,10" d="M5 40 l215 0" />
    <path stroke-dasharray="20,10,5,5,5,10" d="M5 60 l215 0" />
  </g>
</svg>

- 如果要同时设置描边颜色和宽度，可以使用 `stroke-width` 属性来定义描边的宽度。
- 可以通过 `stroke-opacity` 属性来定义描边的透明度。
- 描边的颜色和宽度可以通过 CSS 样式表进行设置，也可以直接在元素上使用 `style` 属性进行定义。

## 十三、滤镜

### 1. 语法

​	SVG 滤镜是一种强大的图形效果技术，可以用来实现各种视觉效果，例如模糊、阴影、光照等。滤镜可以应用于 SVG 图形元素，例如矩形、圆形、路径等，以及 SVG 文本元素，使它们呈现出不同的外观和效果。

**SVG 滤镜通常使用 `<filter>` 元素定义，并通过 `filter` 属性将其应用于目标元素。**

```
<svg width="200" height="200" xmlns="http://www.w3.org/2000/svg">
  <!-- 定义滤镜 -->
  <filter id="filter_id">
    <!-- 滤镜效果 -->
  </filter>
  
  <!-- 应用滤镜的目标元素 -->
  <rect x="50" y="50" width="100" height="80" filter="url(#filter_id)" />
</svg>
```

<svg width="200" height="200" xmlns="http://www.w3.org/2000/svg">
  <!-- 定义滤镜 -->
  <filter id="filter_id">
    <!-- 滤镜效果 -->
  </filter><!-- 应用滤镜的目标元素 -->
  <rect x="50" y="50" width="100" height="80" filter="url(#filter_id)" />
</svg>
### 2.效果

#### 2.1 模糊（Blur）

​	使图像产生模糊效果，通过 `<feGaussianBlur>` 元素实现。

#### 2.2 阴影（Shadow）

​	为图像添加阴影效果，通过 `<feDropShadow>` 元素实现。

#### 2.3 亮度、对比度调整（Brightness, Contrast）

​	调整图像的亮度和对比度，通过 `<feComponentTransfer>` 元素实现。

#### 2.4 颜色矩阵（Color Matrix）

​	通过颜色矩阵操作修改图像的颜色，通过 `<feColorMatrix>` 元素实现。

#### 2.5 混合模式（Blend Mode）

​	将两个图像混合在一起，通过 `<feBlend>` 元素实现。

<svg width="200" height="200" xmlns="http://www.w3.org/2000/svg">
  <!-- 定义模糊滤镜 -->
  <filter id="blur_filter">
    <feGaussianBlur in="SourceGraphic" stdDeviation="5" />
  </filter><!-- 应用模糊滤镜的矩形 -->
  <rect x="50" y="50" width="100" height="80" fill="red" filter="url(#blur_filter)" />
</svg>
## 十四、模糊效果

​	SVG 中的模糊效果可以通过 `<feGaussianBlur>` 元素实现，该元素使用高斯模糊算法来模糊图像。模糊效果可以用于创建柔和的阴影、景深效果、模糊背景等各种视觉效果。

`<feGaussianBlur>` 元素用于对图像进行高斯模糊处理，它有两个主要参数：

- `stdDeviation`：指定高斯模糊的标准差。标准差越大，模糊程度越高。可以使用一个或两个数字，分别表示水平和垂直方向的标准差。如果只提供一个数字，则水平和垂直方向的标准差相同。
- `in`：指定输入图像，通常为 `SourceGraphic`，表示应用滤镜效果的目标元素本身。

```
<svg xmlns="http://www.w3.org/2000/svg" version="1.1">
  <defs>
    <filter id="f1" x="0" y="0">
      <feGaussianBlur in="SourceGraphic" stdDeviation="15" 
/>
    </filter>
  </defs>
  <rect width="90" height="90" stroke="green" stroke-width="3"
  fill="yellow" filter="url(#f1)" />
</svg>
```

<svg xmlns="http://www.w3.org/2000/svg" version="1.1">
  <defs>
    <filter id="f1" x="0" y="0">
      <feGaussianBlur in="SourceGraphic" stdDeviation="15" 
/>
    </filter>
  </defs>
  <rect width="90" height="90" stroke="green" stroke-width="3"
  fill="yellow" filter="url(#f1)" />
</svg>

## 十五、阴影

​	`<feOffset>` 是 SVG 滤镜中的一个元素，用于在图像上创建一个偏移效果，可以用来创建阴影、轮廓和其他视觉效果。它的作用是将输入图像的每个像素沿着指定的水平和垂直方向移动一定的距离，然后将结果图像作为滤镜效果的输出。

```
<feOffset dx="x-offset" dy="y-offset" />
```

- `dx` 属性定义了阴影在水平方向上的偏移量。
- `dy` 属性定义了阴影在垂直方向上的偏移量。

<svg width="200" height="200" xmlns="http://www.w3.org/2000/svg">
  <!-- 定义偏移滤镜 -->
  <filter id="offset_filter">
    <feOffset dx="5" dy="5" />
  </filter><!-- 应用偏移滤镜的矩形 -->
  <rect x="50" y="50" width="100" height="80" fill="red" filter="url(#offset_filter)" />
</svg>
## 十六、渐变

### 1. 线性渐变

​	SVG 中的 `<linearGradient>` 元素用于创建线性渐变，它可以沿着一条直线从一个颜色过渡到另一个颜色，从而创建平滑的渐变效果。线性渐变可用于填充或描边 SVG 图形元素，使其呈现出丰富的颜色变化。

```
<linearGradient id="gradient_id" x1="x1" y1="y1" x2="x2" y2="y2">
  <stop offset="offset1" stop-color="color1" />
  <stop offset="offset2" stop-color="color2" />
  <!-- 更多的 <stop> 元素 -->
</linearGradient>
```

- `id` 属性定义了线性渐变的唯一标识符，用于在SVG图像中引用该渐变。
- `x1` 和 `y1` 属性定义了渐变的起始点坐标。
- `x2` 和 `y2` 属性定义了渐变的结束点坐标。
- `<stop>` 元素用于指定渐变中的颜色和颜色的位置。

线性渐变可以定义为水平，垂直或角渐变：

- 当 y1 和 y2 相等，而 x1 和 x2 不同时，可创建水平渐变
- 当 x1 和 x2 相等，而 y1 和 y2 不同时，可创建垂直渐变
- 当 x1 和 x2 不同，且 y1 和 y2 不同时，可创建角形渐变

```
<svg xmlns="http://www.w3.org/2000/svg" version="1.1">
  <defs>
    <linearGradient id="grad1" x1="0%" y1="0%" x2="100%" y2="0%">
      <stop offset="0%" style="stop-color:rgb(255,255,0);stop-opacity:1" />
      <stop offset="100%" style="stop-color:rgb(255,0,0);stop-opacity:1" />
    </linearGradient>
  </defs>
  <ellipse cx="200" cy="70" rx="85" ry="55" fill="url(#grad1)" />
  <text fill="#ffffff" font-size="45" font-family="Verdana" x="150" y="86">
  SVG</text>
</svg>
```

<svg xmlns="http://www.w3.org/2000/svg" version="1.1">
  <defs>
    <linearGradient id="grad1" x1="0%" y1="0%" x2="100%" y2="0%">
      <stop offset="0%" style="stop-color:rgb(255,255,0);stop-opacity:1" />
      <stop offset="100%" style="stop-color:rgb(255,0,0);stop-opacity:1" />
    </linearGradient>
  </defs>
  <ellipse cx="200" cy="70" rx="85" ry="55" fill="url(#grad1)" />
  <text fill="#ffffff" font-size="45" font-family="Verdana" x="150" y="86">
  SVG</text>
</svg>

### 2. 径向渐变

​	SVG 中的 `<radialGradient>` 元素用于创建径向渐变，它可以从一个中心点向外扩散形成渐变效果，使图形呈现出环形、放射状等丰富的颜色变化。径向渐变可以应用于填充或描边 SVG 图形元素，为其添加立体感和视觉效果。

```
<radialGradient id="gradient_id" cx="cx" cy="cy" r="r" fx="fx" fy="fy">
  <stop offset="offset1" stop-color="color1" />
  <stop offset="offset2" stop-color="color2" />
  <!-- 更多的 <stop> 元素 -->
</radialGradient>
```

- `id` 属性定义了径向渐变的唯一标识符，用于在SVG图像中引用该渐变。
- `cx` 和 `cy` 属性定义了渐变的中心点坐标。
- `r` 属性定义了渐变的半径。
- `fx` 和 `fy` 属性定义了渐变焦点的坐标（可选），用于控制渐变的形状和方向。
- `<stop>` 元素用于指定渐变中的颜色和颜色的位置。

```
<svg xmlns="https://www.w3.org/2000/svg" version="1.1">
        <defs>
            <radialGradient id="grad1" cx="20%" cy="30%" r="30%" fx="50%" fy="50%">
                <stop offset="0%" style="stop-color:rgb(255,255,255);stop-opacity:0" />
                <stop offset="100%" style="stop-color:rgb(0,0,255);stop-opacity:1" />
            </radialGradient>
        </defs>
        <ellipse cx="200" cy="70" rx="85" ry="55" fill="url(#grad1)" />
    </svg>
```

<svg xmlns="https://www.w3.org/2000/svg" version="1.1">
        <defs>
            <radialGradient id="grad1" cx="20%" cy="30%" r="30%" fx="50%" fy="50%">
                <stop offset="0%" style="stop-color:rgb(255,255,255);stop-opacity:0" />
                <stop offset="100%" style="stop-color:rgb(0,0,255);stop-opacity:1" />
            </radialGradient>
        </defs>
        <ellipse cx="200" cy="70" rx="85" ry="55" fill="url(#grad1)" />
    </svg>