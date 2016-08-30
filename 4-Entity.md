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
















