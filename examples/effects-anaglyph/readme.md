# 浮雕相机效果

## 关键代码

首先引入：
```js
<script src="examples/js/effects/AnaglyphEffect.js"></script>
```

创建：

```js

var width = window.innerWidth || 2;
				var height = window.innerHeight || 2;

				effect = new THREE.AnaglyphEffect( renderer );
				effect.setSize( width, height );
				
				

```

在渲染函数中执行：

```js
function render() {

				effect.render( scene, camera ); // 代替 renderer.render(scene, camera )

			}
```

## 其它

### 环境贴图的实现方法

环境贴图可以实现反射出周围环境的效果，这种效果如果用光线追踪会很耗性能。

```js
// 创建cube texture
var path = "textures/cube/pisa/";
				var format = '.png';
				var urls = [
					path + 'px' + format, path + 'nx' + format,
					path + 'py' + format, path + 'ny' + format,
					path + 'pz' + format, path + 'nz' + format
				];

				var textureCube = new THREE.CubeTextureLoader().load( urls );


			    // 设置屏幕背景
				scene.background = textureCube;

				// 设置envMap
				var material = new THREE.MeshBasicMaterial( { color: 0xffffff, envMap: textureCube } );

```

### 相机跟随鼠标移动的方法

```js
// 在mousemove中尽量少做工作
function onDocumentMouseMove(event) {

				mouseX = ( event.clientX - windowHalfX ) / 100;
				mouseY = ( event.clientY - windowHalfY ) / 100;

			}
```

在render循环中更新相机位置：

```js
camera.position.x += ( mouseX - camera.position.x ) * .05;
				camera.position.y += ( - mouseY - camera.position.y ) * .05;

				camera.lookAt( scene.position );
```