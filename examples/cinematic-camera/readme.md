# cinematic camera

这个叫电影相机，threejs的文档里并没有说到这种相机，但是在example里却有，可以点击 [CinematicCamera.js](CinematicCamera.js) 下载

原例子见[cinematic camera](https://threejs.org/examples/#webgl_camera_cinematic)

## 使用

可以这样创建

```js
camera = new THREE.CinematicCamera( 60, window.innerWidth / window.innerHeight, 1, 1000 );
				camera.setLens(5);
        		camera.position.set(2, 1, 500);
```
下面的方法可以设置聚焦位置：

```js
					camera.focusAt(targetDistance);
```

## 关键点

#### 这种相机有什么特点

这种相机的特点就是可以调焦，就像真的照相机一样，打开[cinematic camera](https://threejs.org/examples/#webgl_camera_cinematic)，
当鼠标处于某个方块上时，方块就会获得焦点，变清晰

#### sortObjects有什么用

```js
renderer.sortObjects = false;
```

作用如下：
```text
Defines whether the renderer should sort objects. Default is true.

Note: Sorting is used to attempt to properly render objects that have some degree of transparency. By definition, sorting objects may not work in all cases. Depending on the needs of application, it may be neccessary to turn off sorting and use other methods to deal with transparency rendering e.g. manually determining each object's rendering order.
```

#### updateMatrixWorld() 什么时候用

[updateMatrixWorld()](http://threejs.outsidelook.cn/r89/source/docs/index.html?q=obj#Reference/Core/Object3D)函数会更新对象及其子对象的全局变换矩阵

因为，默认情况下`matrixWorldNeedsUpdate`属性是`false`的，所以，每次对象做了变换之后，如果要获取其全局坐标，或者要使用全局变换矩阵，就需要调用这个函数




## 没看懂的代码

```js
var matChanger = function( ) {

					for (var e in effectController) {
						if (e in camera.postprocessing.bokeh_uniforms)
						camera.postprocessing.bokeh_uniforms[ e ].value = effectController[ e ];
					}
					camera.postprocessing.bokeh_uniforms[ 'znear' ].value = camera.near;
					camera.postprocessing.bokeh_uniforms[ 'zfar' ].value = camera.far;
					camera.setLens(effectController.focalLength, camera.frameHeight ,effectController.fstop, camera.coc);
					effectController['focalDepth'] = camera.postprocessing.bokeh_uniforms["focalDepth"].value;
				};

```