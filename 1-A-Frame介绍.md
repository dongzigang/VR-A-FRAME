<h2>什么是A-frame？</h2>
A-frame是一个开源的WebVR框架，作用是可以用HTML创建一个VR实例

A-frame是一个three.js框架

A-frame比起直接用three.js更简单

<h2>设备与平台支持</h2>

浏览器必须支持WebGL

浏览器必须支持WebVR API

<h2>最佳实战</h2>

1.The common golden rule is to never unexpectedly take control of the camera away from users.

都要遵守的黄金规则就是绝不能出乎意料的控制照片与用户之间的距离<br><br>

2.Units (such as for position) should be considered meters

单位（如位置）应该去考虑<b>米</b>
<h3>性能</h3>
VR中性能是至关重要的，用以下方法提高性能

1.使用推荐的硬件配置

2.使用<b>stats</b>组件监视各种指标

3.利用<b>asset management system</b> ,使浏览器能够缓存和预加载

4.可以利用几何合并限制绘制重复调用共用 material。

5.一般来说，在场景中的entities和lights的数量越少越好。

6.减少代码冗余，用mixins and templating 等方法增加复用性 

7.尽量使用 entity-component-system framework


    













