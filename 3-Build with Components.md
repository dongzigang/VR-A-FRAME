<h3>用组件开发</h3>
让我们用一个entity-component-system 构建一个栗子

这里会介绍3个概念

1.使用标准组件与A-Frame传输

2.使用来自生态系统的第三方组件。

3.编写自定义组件来完成我们想要的。

<h3>引入3d模型</h3>

```html
<!doctype html>
<html lang="en">
<head>
	<meta charset="UTF-8" />
	<title>Document</title>
	<script type="text/javascript" src="js/aframe.min.js" ></script>
	<!--必须引入加载器-->
	<script src="https://rawgit.com/donmccurdy/aframe-extras/v2.1.1/dist/aframe-extras.loaders.min.js"></script>
</head>
<body>
	<a-scene>
		<a-assets>
		  <!--这里要这么写，引入3D模型资源-->
			<a-asset-item id="myPlyModel" src="md/chr_rain.ply"></a-asset-item>
		</a-assets>
		<a-entity ply-model="src: #myPlyModel" position="0 0.5 -2" scale="0.1 0.1 0.1" rotation="270 180 180"></a-entity>
		<a-sky src="imgs/bg.jpg"></a-sky>
	</a-scene>
</body>
</html>
```

