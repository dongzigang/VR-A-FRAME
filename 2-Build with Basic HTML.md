<h2>用基础的html构建场景</h2>
<h3>添加一个box（长方形）</h3>
```
<a-scene>
  <a-box color="blue" width="0.5" height="3" depth="0.5" opacity="0.8"></a-box>
  <a-sky src="bg.jpg"></a-sky>
</a-scene>
```
A-Feame采用右手坐标系
```
           Y
           ^
           |
           |
           |
           |
          / ——————————————>X
         /
        /
       /
     Z
```
