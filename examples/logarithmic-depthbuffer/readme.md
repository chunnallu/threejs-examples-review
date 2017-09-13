# logarithmic depth buffer

这个直译过来就是——对数深度缓冲,没太明白这个的用法

## 代码要点

#### 加载字体

```js
var loader = new THREE.FontLoader();
				loader.load( 'fonts/helvetiker_regular.typeface.json', function ( font ) {


				} );
```

#### 材质的配置

```js
var materialargs = {
					color: 0xffffff,
					specular: 0x050505,
					shininess: 50,
					shading: THREE.SmoothShading,
					emissive: 0x000000
				};
```

#### 计算包围球

这是Geometry的属性
```js
labelgeo.computeBoundingSphere();
```

#### 使用HSL颜色的方法

```js
materialargs.color = new THREE.Color().setHSL( Math.random(), 0.5, 0.5 );
```