# 设置模型的颜色

一般设置模型的颜色，我们都是通过设置材质的颜色来设置，但是，其实也可以通过点颜色来生成模型的颜色，一般为了实现渐变效果或者模型各部分的颜色动态变化才这么做

## 关键代码

1、拿到模型的几何
```js
geometry  = new THREE.IcosahedronGeometry( radius, 1 ); // 这里是新建一个几何
```

2、拿到几何的每个面的三个点

```js
var faceIndices = [ 'a', 'b', 'c' ]; //每个面中有a,b,c三个属性，保存着面的三个顶点的index
for ( var i = 0; i < geometry.faces.length; i++ ) {

	var face = geometry.faces[ i ];
	for ( var i = 0; i < geometry.faces.length; i++ ) {
		var vertexIndex = face[ faceIndices[ j ] ];
		var p = geometry.vertices[ vertexIndex ];  //
		// 接着做第3点，设置点的颜色
	}

}
```

3、设置顶点的颜色

```js
color = new THREE.Color( 0xffffff );
color.setHSL( ( p.y / radius + 1 ) / 2, 1.0, 0.5 );
face.vertexColors[ j ] = color;
```
如果面的顶点的颜色不同，就会使用线性插值生成渐变颜色。这里`( p.y / radius + 1 ) / 2`会根据顶点的y值生成一个颜色，从而使得面呈现出有规律的渐变色

4、给材质设置`vertexColors`属性

```js
new THREE.MeshPhongMaterial( {  vertexColors: THREE.VertexColors } )
```
设置了这个属性才会使用顶点的颜色来计算面的颜色
