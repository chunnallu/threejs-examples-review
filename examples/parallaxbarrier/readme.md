# 视差光栅

人的两只眼睛看到的图像是有细微差别的，这个细微差别在大脑中形成立体感。视差光栅就是利用这个原理，通过技术手段让人的两个眼睛看到有细微差别的图像，从而产生立体感。

## 关键代码

1、引入
```html
<script src="js/effects/ParallaxBarrierEffect.js"></script>
```

2、创建effect

```js
effect = new THREE.ParallaxBarrierEffect( renderer );
				effect.setSize( width, height );
```

3、在渲染循环中用下面的语句来渲染

```js
effect.render( scene, camera );
```


## 其它

### 环境贴图

这里用到了环境贴图，和effect-anaglyph例子类似：

```js
var textureCube = new THREE.CubeTextureLoader()
					.setPath( 'textures/cube/Bridge2/')
					.load( [ 'posx.jpg', 'negx.jpg', 'posy.jpg', 'negy.jpg', 'posz.jpg', 'negz.jpg' ] );
scene.background = textureCube;
```

### 面剔除（culling）

```js
renderer.setFaceCulling( THREE.CullFaceNone );
```
在WebGL渲染过程中的可见性计算中，有一个阶段是把不可见的面。你可以通过`setFaceCulling`改变渲染器的剔除行为，
可以选择剔除前面的面（到相机之间没有其它面遮挡的面）、后面的面（和相机之间有其它面遮挡，也就是不可见面），都删除，都不删除等等

参考：[Face_Culling](https://www.khronos.org/opengl/wiki/Face_Culling)

### 材质用法

这个例子涉及到很多个材质的切换，可以学习材质的各个属性的用法

```js
"Orange": 	new THREE.MeshLambertMaterial( { color: 0xff6600, envMap: textureCube, combine: THREE.MixOperation, reflectivity: 0.3 } ),
```