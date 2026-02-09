### 核心概念
1. **关键帧（Keyframes）**  
   	动画的核心是定义关键帧（`@keyframes`），指定动画在不同时间点的样式状态。关键帧通过百分比或 `from/to` 关键字定义动画的阶段。

2. **动画属性（Animation Properties）**  
           通过一系列属性（如 `animation-name`, `animation-duration` 等）控制动画的行为，包括持续时间、循环次数、播放方向等。

---

### 1. 定义关键帧 `@keyframes`
语法：
```css
@keyframes 动画名称 {
  0% { /* 初始状态 */ }
  50% { /* 中间状态 */ }
  100% { /* 结束状态 */ }
}
```
或使用 `from` 和 `to`：
```css
@keyframes slide {
  from { transform: translateX(0); }
  to { transform: translateX(200px); }
}
```

---

### 2. 动画属性详解
以下是动画的常用子属性，可以简写为 `animation` 属性：

#### 2.1 关键属性
| 属性                         | 作用                          | 示例值                   |
|-----------------------------|------------------------------|-------------------------|
| `animation-name`            | 指定动画名称（对应 `@keyframes`） | `slide`, `fade`         |
| `animation-duration`        | 动画持续时间                   | `2s`, `500ms`           |
| `animation-timing-function` | 动画速度曲线                   | `ease`, `linear`, `cubic-bezier(0.1, 0.7, 1.0, 0.1)` |
| `animation-delay`           | 动画开始前的延迟时间            | `1s`, `0.5s`            |
| `animation-iteration-count` | 动画播放次数                   | `1`, `3`, `infinite`    |
| `animation-direction`       | 动画播放方向                   | `normal`, `reverse`, `alternate`（正反交替） |
| `animation-fill-mode`       | 动画结束时元素的样式状态        | `none`, `forwards`（保留结束状态）, `backwards`（保留初始状态） |
| `animation-play-state`      | 控制动画播放状态               | `running`, `paused`     |

---

#### 2.2 简写语法
```css
animation: [name] [duration] [timing-function] [delay] [iteration-count] [direction] [fill-mode] [play-state];
```

示例：
```css
.box {
  animation: slide 2s ease-in-out 0.5s infinite alternate forwards;
}
```

---

### 3. 实际案例

#### 示例1：基础平移动画
```css
@keyframes slide {
  from { transform: translateX(0); }
  to { transform: translateX(300px); }
}

.box {
  width: 100px;
  height: 100px;
  background: red;
  animation: slide 3s ease-in-out infinite alternate;
}
```
效果：红色方块左右来回移动，每次耗时3秒，无限循环。

---

#### 示例2：多阶段动画
```css
@keyframes color-change {
  0% { background: red; }
  50% { background: yellow; transform: scale(1.2); }
  100% { background: green; }
}

.element {
  animation: color-change 4s linear infinite;
}
```
效果：元素颜色从红→黄→绿变化，中间放大20%，无限循环。

---

#### 示例3：暂停与播放控制
```css
.box {
  animation: rotate 2s linear infinite;
}

.box:hover {
  animation-play-state: paused; /* 悬停时暂停动画 */
}

@keyframes rotate {
  from { transform: rotate(0deg); }
  to { transform: rotate(360deg); }
}
```
效果：元素持续旋转，悬停时暂停动画。

---

### 4. 动画（animation）与过渡（Transition）的区别
| **特性**          | **Transition**              | **Animation**                  |
|-------------------|-----------------------------|--------------------------------|
| 触发方式          | 依赖状态变化（如悬停、点击） | 自动触发或通过 JavaScript 控制 |
| 阶段控制          | 仅定义开始和结束状态        | 可定义多阶段（关键帧）         |
| 循环与方向        | 不支持循环或反向播放        | 支持循环、反向、交替播放       |
| 复杂动画          | 适合简单变化                | 适合多步骤、复杂动画           |

---

### 5. 性能优化
- **优先使用 `transform` 和 `opacity`**：这类属性会触发 GPU 加速，动画更流畅。
- **避免频繁重排（Layout Thrashing）**：如修改 `width`、`height` 会导致布局重新计算。
- **使用 `will-change`**：提前告知浏览器元素会有动画变化：
  ```css
  .box {
    will-change: transform, opacity;
  }
  ```

---

### 6. 浏览器兼容性
- 现代浏览器全面支持 CSS3 动画。
- 部分旧浏览器（如 IE9 及以下）需添加 `-webkit-`、`-moz-` 等前缀：
  ```css
  @-webkit-keyframes slide { /* Safari/Chrome */ }
  @-moz-keyframes slide { /* Firefox */ }
  ```

---

通过 `@keyframes` 和动画属性的组合，你可以创建出复杂的动态效果，如加载动画、页面过渡、交互反馈等，显著提升用户体验！