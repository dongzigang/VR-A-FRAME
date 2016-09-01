<h2>a-entity</h2>
实体

我们可以附加组件给它，使之呈现的东西或做一些事情。为了给它形状和外观，我们可以附加的几何形状和材料成分：
```html
<a-eneity geometry="primitive: box" 
          material="color: red"
          light="type: point; intensity: 2.0">
</a-eneity>
```
我们可以使用DOM的API来获取一个实体DOM节点
```
//html
<a-entity id="mario"></a-entity>
//js
var el =document.("#mario")
```
知识点补充<b>querySelector()</b>
querySelector() 方法返回文档中匹配指定 CSS 选择器的一个元素。

注意： querySelector() 方法仅仅返回匹配指定选择器的第一个元素。如果你需要返回所有的元素，请使用 querySelectorAll() 方法替代。
<h4>实例</h4>
```
获取文档中 id="demo" 的第一个元素：

      document.querySelector("#demo");

获取文档中第一个 <p> 元素：

      document.querySelector("p");
      
获取文档中 class="example" 的第一个元素:

      document.querySelector(".example");
      
获取文档中 class="example" 的第一个 <p> 元素:

      document.querySelector("p.example");

获取文档中有 "target" 属性的第一个 <a> 元素：

      document.querySelector("a[target]");
```
<h3>特性Properties</h3>
<h4>组件</h4>
一旦我们有了一个实体，我们可以访问所有的属性和方法，具体介绍如下的。

获取到实体的DOM节点后，还可以进一步获取其节点属性

    var camera = document.querySelector('a-entity[camera]').components.camera.camera;
    var material = document.querySelector('a-entity[material]').components.material.material;
或者，如果一个组件暴露了一个API，我们可以调用它的方法：

      document.querySelector('a-entity[sound]').components.sound.pause();
      
<h4>isPlaying</h4>
不论该实体是激活状态还是播放状态。如果实体被暂停，那么isPlaying值就是false。

<h4>object3D</h4>
object3D是一个THREE.Group对象包含了不同类型的THREE.Object3D，如cameras, meshes, lights, or sounds

不同类型的Object3Ds，可以通过object3DMap被访问。

<h3>object3DMap</h3>
object3DMap是一个js对象用来访问不同类型的THREE.Object3D

一个实体有一个 geometry 和 一个light 附加组件，则他的 object3DMap可能是这样的

    {
      light: <THREE.Light Object>,
      mesh: <THREE.Mesh Object>
    }

<h3>sceneEl</h3>

一个实例引用它自己的场景元素

       //js
      var sceneEl = document.querySelector('a-scene');
      var entity = sceneEl.querySelector('a-entity');
      console.log(entity.sceneEl === sceneEl);  // >> true.
 
 
 
      
<h2>方法</h2>

<h3>addState (stateName)</h3>

addState为实例添加一个状态。

···
//二级DOM
entity.addEventListener('stateadded', function (evt) {
  if (evt.state === 'selected') {
    console.log('Entity now selected!');
  }
});
//为组件添加状态
entity.addState('selected');
//  .is   用来检查
entity.is('selected');  // >> true
···

<h3>emit</h3>

emit(name,detail,bubbles)

emit方法触发实体中自定义的DOM事件

      //html
      <a-entity>
         <a-animation attribute="rotation" begin="rotate" to="0 360 0"></a-animation>
      </a-entity>
      //js
      entity.emit('rotate');//在这里估计作用和start="" 一样
      
我们还可以通过事件详细信息或数据作为第二个参数：

      entity.emit('collide', { target: collidingEntity });
      
最后一个参数决定是否冒泡


entity.emit('sink', null, false);

<h2>flushToDOM (recursive)</h2>

flushToDOM将手动序列化所有实体的组件的数据，并更新DOM。了解更多关于组件到DOM序列化。

<h3>getAttribute (attr)</h3>
getAttribute可用于检索已解析的组件的数据。如果attr参数是注册的组件的名称，getAttribute将只返回在HTML中对应的组件数据。

getAttribute返回的内容是getComputedAttribute的一部分，因为getAttribute返回的组件的数据不包括mixins or default values:

```javascript
// <a-entity geometry="primitive: box; width: 3">
entity.getAttribute('geometry');
// >> { primitive: "box", width: 3 }
entity.getAttribute('geometry').primitive;
// >> "box"
entity.getAttribute('geometry').height;
// >> undefined
```
如果attr不是注册的组件的名称，getAttribute将像通常那样：

          // <a-entity data-position="0 1 1">
          entity.getAttribute('data-position');
          // >> "0 1 1"

<h3>getComputedAttribute (attr)</h3>

与getAttribute类似，除此之外还可以返回默认值和mixin

```javasceipt
// <a-entity geometry="primitive: box; width: 3">
entity.getComputedAttribute('geometry');
// >> { primitive: "box", depth: 2, height: 2, translate: "0 0 0", width: 3, ... }
entity.getComputedAttribute('geometry').primitive;
// >> "box"
entity.getComputedAttribute('geometry').height;
// >> 2

```
更多的时候，我们将要使用的getComputedAttribute检查组件的数据。

虽然有时我们可能要使用getAttribute辨别哪些被明确定义的属性。

<h3>getObject3D (type)</h3>

查找一个已注册组件中的THREE.Object3D

          AFRAME.registerComponent('example-mesh', {
            init: function () {
              var el = this.el;
              el.getOrCreateObject3D('mesh', THREE.Mesh);
              el.getObject3D('mesh');  // Returns THREE.Mesh that was just created.
            }
          });


<h3>getOrCreateObject3D (type, Constructor)</h3>

如果组件没有一个已经注册过的THREE.Object3D在type下，getOrCreateObject3D将会通过构造函数注册一个实例化的THREE.Object3D，如果有，那他的作用就和getObject3D一样

          AFRAME.registerComponent('example-geometry', {
            update: function () {
              var mesh = this.el.getOrCreateObject3D('mesh', THREE.Mesh);
              mesh.geometry = new THREE.Geometry();
            }
          });

<h3>pause</h3>

pause 将会停止实体内所有的组件和animations定义的动画行为，

当实体暂停时，所有的动画都会停止，并调用Component.pause在他的每一个组件，它是由组件来实现他们如何暂停，但它们通常移除事件侦听器和背景的行为，它将停止它所有的子组件。

          // <a-entity id="spinning-jumping-ball">
          entity.pause();
          
<h3>play()</h3>

播放所有的动态效果

entity.pause（）;
entity.play（）;

<h3>setAttribute (attr, value, componentAttrValue)</h3>

如果attr不是一个注册组件的名字，或者这个组件是一个单属性组件，setAttribute主要表现为它通常那样：

          entity.setAttribute('visible', false);
          
如果attr是一个注册过的组件的名字，它可能会用特殊的解析方式处理attr的值，例如position component是一个单属性组件，但是它的属性值解析时允许它采用一个对象

          entity.setAttribute('position', { x: 1, y: 2, z: 3 });
          
<h4>设置多属性组件数据</h4>
为了设置或替换多属性组件数据，我们可以通过把已注册组件的名字作为attr，并且把对象属性作为属性值

          // All previous properties for the light component will be removed and overwritten.
          entity.setAttribute('light', {
            type: 'spot',
            distance: 30,
            intensity: 2.0
          });
<h4>更新多属性组件数据</h4>

为了更新多属性组件的单个属性，我们可以通过把已注册组件的名字作为attr，属性名作为第二个参数，属性值作为第三个参数

          // All previous properties for the material component (besides the color)  will be unaffected.
          entity.setAttribute('material', 'color', 'crimson');
          
<h3>setObject3D (type, obj)</h3>

没接触过three.js不是很理解

          AFRAME.registerComponent('example-orthogonal-camera', {
            update: function () {
              this.el.setObject3D('camera', new THREE.OrthogonalCamera());
            }
          });

<h3>removeAttribute (attr)</h3>
移除属性

          entity.removeAttribute('sound');  // The entity will no longer play sound.
          
<h3>removeObject3D (type)</h3>

          AFRAME.registerComponent('example-light', {
            update: function () {
              this.el.setObject3D('light', new THREE.Light());
              // Light is now part of the scene.
              // object3DMap.light is now a THREE.Light() object.
            },
            remove: function () {
              this.el.removeObject3D('light');
              // Light is now removed from the scene.
              // object3DMap.light is now null.
            }
          });
          

<h3>removeState (stateName)</h3>
移除状态

          entity.addEventListener('stateremoved', function (evt) {
            if (evt.state === 'selected') {
              console.log('Entity no longer selected.');
            }
          });
          entity.addState('selected');
          entity.is('selected');  // >> true
          entity.removeState('selected');
          entity.is('selected');  // >> false

















