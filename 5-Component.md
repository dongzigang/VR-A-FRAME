<h1>组件Component</h1>

在 实体-组件-系统 模式中，一个组件是一个可复用并且模块化的块，作用是插入实体中，去添加外观，行为，和/或者功能。

在A-frame 中组件修饰的是场景中的3D对象实体，我们把组件混合并组合到一起去构建复杂的组件。组件给我们封装了three.js和js代码在模块中，我们可以在html中声明组件。

打个比方，如果手机是一个已声明的实体，我们可能用组件定义它的外观（颜色，形状），去定义它的行为（来电震动，低电量自动关机），或者添加功能（相机）

组件是大致类似于CSS。像css规则修饰元素外观那样，组件属性修饰实体的外观，行为和功能

<h3>组件看起来像啥</h3>

一个组件像汽车的引擎，气缸啥的

<h3>From HTML</h3>

A_Frame中html属性代表组件名，属性值代表组件数据

<h3>单属性组件</h3>

如果一个组件是一个单属性组件，这意味着它的数据代表一个单个值，在html中，这个组件值就像一个普通的html属性一样

      <!-- `position` is the name of the position component. -->
      <!-- `1 2 3` is the data of the position component. -->
      <a-entity position="1 2 3"></a-entity>

<h3>多属性组件</h3>

多属性组件看起来像行内css样式

        <!-- `light` is the name of the light component. -->
        <!-- The `type` property of the light is set to `point`. -->
        <!-- The `color` property of the light is set to `crimson`. -->
        <a-entity light="type: point; color: crimson"></a-entity>
        
<h3>组件的运行机制</h3>

一个组件实际上是用<b> AFRAME.registerComponent</b>注册的组件，例如position组件：

        //它的底层是这样的
        AFRAME.registerComponent('position', {
          schema: { type: 'vec3' },//三维架构
          update: function () {
            var object3D = this.el.object3D;
            var data = this.data;
            object3D.position.set(data.x, data.y, data.z);
          }
        });

<h3>依赖</h3>

注册组件时先初始化其依赖组件

    // Initializes last.
    AFRAME.registerComponent('a', {
      dependencies: ['b']
    });
    // Initializes second.
    AFRAME.registerComponent('b', {
      dependencies: ['c']
    });
    // Initializes first.
    AFRAME.registerComponent('c', {});
    
<h3>多个实例</h3>

默认的一个组件只能有一个实例，例如，一个实体只能附加一个几何组件，但是有一些组件，像sound component,可以有多个实例附加在单个实体上，

我们用双下划线"__"(有两个下划线)区分同一组件的不同实例

例如：连接sound组件的多个实例

        <a-entity sound="src: url(sound.mp3)"
                  sound__1="src: url(sound1.mp3)"
                  sound__2="src: url(sound2.mp3)"
                  sound__beep="src: url(beep.mp3)"
                  sound__boop="src: url(beep.mp3)">
        </a-entity>
        
为了使组件上能有多个实例，设置multiple: true在组件定义时：

        AFRAME.registerComponent('my-multiple-component', {
          multiple: true,
          init: function () {
            // ...
          }
        });
        
<h3>架构</h3>

一个组件的架构定义和描述了它的属性，组件可以是单属性组件或者是多属性组件

单属性架构看起来像这样：

    schema: {
      type: 'int', default: 5
    }
多属性架构看起来像这样：

      schema: {
        color: { default: '#FFF' },
        target: { type: 'selector' },
        uv: {
          default: '1 1',
          parse: function (value) {
            return value.split(' ').map(parseFloat);
          }
        },
      }








