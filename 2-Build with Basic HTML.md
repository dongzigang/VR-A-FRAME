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
```










