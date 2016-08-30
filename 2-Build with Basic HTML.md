<h2>用基础的html构建场景</h2>
<h3>添加一个box（长方形）</h3>
```
<a-scene>
  <a-box color="blue" width="0.5" height="3" depth="0.5" opacity="0.8"></a-box>
  <a-sky src="bg.jpg"></a-sky>
</a-scene>
```
A-Feame采用右手坐标系,单位为米

旋转的基本单位为'度'，方向判断采用右手定则
```
           Y(m)
           ^
           |
           |
           |
           |
          / ——————————————>X(m)
         /
        /
       /
     Z(m)
```
属性
```
width="x"                 物体x轴长度

height="x"                物体y轴的长度

depth="x"                 物体z轴的长度

position="x y z"          物体的位置

rotation="x y z"          物体旋转角度

scale="x y z"             物体缩放

src="/"                   引入资源，可以引入图片或视频
```
举个栗子
```
<a-scene>
  <a-box width="0.45" depth="0.45" height="0.01" opacity="1" position="0.15 1.4 1" rotation="100 -18 180" src="1.jpg"></a-box>
  <a-sky src="bg.jpg"></a-sky>
</a-scene>
```
<h3>使物体运动起来</h3>
```
<a-scene>
  <a-assets>
    <img id="texture" src="1.jpg">
  </a-assets>
  <a-box width="0.5" height="0.01" depth="0.5"
         position="-1 2 -2" rotation="0 0 45" 
         src="#texture">
    <a-animation attribute="rotation" repeat="indefinite" to="0 360 0"></a-animation>
  </a-box>
  <a-sky src="bg.jpg"></a>
</a-scene>
```
属性
```
要使box运动就要添加<a-animation>子标签

attribute="" 需要运动的属性

repeat="" 动作循环次数

begin="click"   触发某个动作开始运动

to=""   运动结果

```
栗子
```html
  <a-assets>
    <img id="texture" src="1.jpg">
  </a-assets>
  <a-box width="0.5" height="0.01" depth="0.5"
         position="-1 2 -2" rotation="0 0 45" 
         src="#texture" scale-on-click="to: 3 3 3">
         <!--运动为旋转      触发点击事件开始运动  无限次数    y轴旋转360-->
    <a-animation attribute="rotation" begin="click" repeat="indefinite" to="0 360 0"></a-animation>
  </a-box>
  <!--为场景添加一个准心 准心对准目标物体才能互动（如点击等）-->
  <a-camera position="0 1.8 0" src="video/2.jpg">
    <a-cursor color="blue"></a-cursor>
  </a-camera>
  <a-sky src="bg.jpg"></a>
</a-scene>
```
<h2>添加光照效果</h2>

```html
<a-scene>
  <a-assets>
    <img id="texture" src="1.jpg">
  </a-assets>
  <a-box width="0.5" height="0.01" depth="0.5"
         position="-1 2 -2" rotation="0 0 45" 
         src="#texture" scale-on-click="to: 3 3 3">
    <a-animation attribute="rotation" begin="click" repeat="indefinite" to="0 360 0"></a-animation>
  </a-box>
  <!---->
   <a-light type="spot" color="green" position="1.5 0.5 0" look-at="a-box"></a-light>
  <a-light type="point" color="red" position="0 0.5 0.5"></a-light>
  <a-camera position="0 1.8 0" src="video/2.jpg">
    <a-cursor color="blue"></a-cursor>
  </a-camera>
  <a-sky src="bg.jpg"></a>
</a-scene>

```

<h3>组件</h3>

为A-Frame添加组件：

一个实体通过一个HTML元素形式展现（即代表<a-entity>）。

组件是通过HTML属性表示。

组件特性由通过HTML属性定义值表示。

栗子
```html
<!--geometry表示实体的几何属性如宽高，形状等等   
    material表示实体的本身特性，如颜色，透明度等
-->
<a-entity geometry="primitive: sphere; radius: 1.5"
          material="color: tomato; metalness: 0.7"></a-entity>
```














