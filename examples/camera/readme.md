# camera 例子

这个例子用来演示正交相机和透视相机，技术难点是渲染双屏

链接：https://threejs.org/examples/webgl_camera.html

## 代码分析

在键盘事件发生后，切换激活相机：
```js
function onKeyDown ( event ) {

				switch( event.keyCode ) {

					case 79: /*O*/

						activeCamera = cameraOrtho;
						activeHelper = cameraOrthoHelper;

						break;

					case 80: /*P*/

						activeCamera = cameraPerspective;
						activeHelper = cameraPerspectiveHelper;

						break;

				}

			}
```


## 关键点

####  autoClear设为false有什么用？

关闭在渲染前自动清除屏幕

```js
renderer.autoClear = false;
```
参考文档 [WebGL Renderer](https://threejs.org/docs/#api/renderers/WebGLRenderer)

设了这个属性，在调用render函数前，需要手动执行：

```js
renderer.clear();
```

#### 物体随机运动
可以在render函数中使用如下代码让物体随机运动：
```js
                var r = Date.now() * 0.0005;
				mesh.position.x = 700 * Math.cos( r );
				mesh.position.z = 700 * Math.sin( r );
				mesh.position.y = 700 * Math.sin( r );
```

#### 什么时候需要更新投影矩阵

更改了相机的创建参数后，需要执行下面这句：

```js
cameraOrtho.updateProjectionMatrix();
```

#### 隐藏模型

所有继承自Object3D的对象都有visible属性
```js
cameraOrthoHelper.visible = false;
```

#### 渲染多屏

```js
                /** 对屏1 的场景做一些设置 */
                activeHelper.visible = false;

                /** 渲染屏1的场景 ，可以指定屏1 的范围和相机 */
				renderer.setViewport( 0, 0, SCREEN_WIDTH/2, SCREEN_HEIGHT );
				renderer.render( scene, activeCamera );

                /** 对屏2 的场景做一些设置 */
				activeHelper.visible = true;
     
				/** 渲染屏2的场景 ，可以指定屏2 的范围和相机 */
				renderer.setViewport( SCREEN_WIDTH/2, 0, SCREEN_WIDTH/2, SCREEN_HEIGHT );
				renderer.render( scene, camera );
```

暂时不知其和autoClear = false 的关系